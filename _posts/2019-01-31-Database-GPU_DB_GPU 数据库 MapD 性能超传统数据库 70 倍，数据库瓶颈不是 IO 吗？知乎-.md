---

layout:     post
title:      GPU 数据库 MapD 性能超传统数据库 70 倍，数据库瓶颈不是 IO 吗(1)？
subtitle:   来自知乎。
date:       2019-01-31
author:     HD
catalog: true
tags:
     - database
     - GPU memory
     - CPU memory
     - GPU-based database

---

## 正文

# GPU 数据库 MapD 性能超传统数据库 70 倍，数据库瓶颈不是 IO 吗？

`据[DataInformed报道](https://link.zhihu.com/?target=http%3A//data-informed.com/fast-database-emerges-from-mit-class-gpus-and-students-invention/)，北卡罗来纳大学学生Todd Mostak开发了一款新型并行数据库——MapD，性能超传统CPU数据库70倍！不过该数据库尚需进一步开发，Mostak同时表示将会将其开源。
DataInformed介绍到，2012年Mostak正在哈佛大学中东研究中心攻读硕士学位，出于论文主题需要，他不得不处理阿拉伯之春时期Twitter上的4000万帖子，但往往耗费良久。由于没有任何已有数据库系统能够帮助他快速处理大数据，在接下来的一年里，他基于游戏计算机开发了自己的数据库项目，并取得了优异的成果，学术界和企业都将因此获益。
在MIT的课堂中Mostak将这种新型的并行数据库称之为MapD，能够在几毫秒内处理复杂的空间和GIS数据，相比普通CPU数据库性能提升了70倍。
计算任务是有点重。`

---



> 作者：李晨曦 
>
> 链接：https://www.zhihu.com/question/21003317/answer/111549889
>
> 来源：知乎 
>
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



`数据库瓶颈是IO，说的是Oracle,MySQL,PostgreSQL等传统数据库，磁盘顺序访问最多只有几百M/S（bandwidth是内存的1/100），随机访问就更是惨不忍睹了（latency是内存的100000倍），因此IO成为了瓶颈，需要做很多工作来克服IO的问题，如Buffer Manager，其他的问题就没有那么重要了。`

`但是内存数据库就完全不一样了，尤其是纯内存数据库，也就是所有数据都在内存中，不需要磁盘IO。这时内存bandwidth，CPU性能，L1 cache miss, branch prediction miss, Lock都成了至关重要的东西。举个例子，从L1 cache中读数据的latency是0.5ns, 从内存中读数据的latency是100ns，这样就差了200倍，但是L1 cache只有32KB,所以内存数据库中就需要充分利用L1 cache的数据结构。再比如, 实现并行hash join，lock free版的就会比用mutex.lock()/unlock()快很多。但是传统数据库中，因为大部分时间都用在了IO上，这些问题都不是很重要了。`

`具体到MapD【３】，目前为止我看到了2个使得它性能非常高的原因。`

`１．GPU不管是每秒浮点数运算(FLOPS)，还是从内存（显存）读数据的bandwidth都比CPU强很多，比如NVIDIA Tesla K80的FLOPS为　8.74TFLOPS，bandwidth为500G/S，对应的CPU能有50GFLOPS和30G/s就不错了，参见【１】。数据从内存到显存需要时间，不过如果一直在同一份数据上做分析，可以先把数据全部载入到显存，之后的运算就不用内存参与了。`

`２．查询引擎，传统数据库基本上都用的iterator model，会有很多虚函数调用和interpretation overhead，而MapD的做法是将SQL语句转为LLVM，参见【２】，再编译成机器码，再执行，虽然编译要花一些时间(如20ms)，但是跑OLAP查询的时候可以忽略不计。举个例子，如执行select count(*) from t where c=1;如果是一个大表，查询时间会远高于20ms，因此编译产生的overhead可以忽略不计，有很多expression运算，join的复杂查询优势就更大了。`

`iterator model：`

`每处理一个新的tuple，都会有很多的虚函数调用，极大的影响了性能`

```cpp
class Operator{
public:
    virtual Tuple next() = 0; //获取下一个tuple
    virtual void open() = 0; //初始化
    virtual void close() = 0;
}

class TableScan : public Operator{
public:
    TableScan(string t) : t(t){}
    virtual Tuple next(){
        read something to tuple;
        return tuple;
    }
private:
   string t;
}

bool predicate(int value){
    return value==1;
}

class Select : public Operator{
public:
    Select(Operator *operator) : operator(operator){}
    virtual Tuple next(){
        while(!end){
            Tuple tuple = operator->next();
            if(predicate(tuple))
                return tuple;
        }
    }
private:
    Operator *operator;
}

class Aggregation:public Operator{
public:
    Aggregation(Operator *operator) :operator(operator){}
    virtual Tuple next(){
        operator->next();
        count++;
    }
private:
    Operator *operator:
    int count=0;
}
```

`编译（用Ｃ++示范，实际上是转化为LLVM代码）：`

`把SQL转化为这种代码，运行时编译为机器码，并执行，显然快很多，在复杂一些的查询中，Vectorization, SIMD等能使得速度更快`

```cpp
int count=0;
for(int i = 0; i <tuples.size(); i++){
    count += (tuples[i] == 1);
}
```

`对内存数据库感兴趣的朋友可以关注一下德国慕尼黑工业大学(TUM)数据库组的Hyper（[HyPer: Hybrid OLTP&OLAP High-Performance Database System](https://link.zhihu.com/?target=http%3A//hyper-db.de/index.html%23)），可以说是世界上最先进的内存数据库之一，早在2011年就在查询引擎中使用LLVM了，里面用到的各种技术都在主页的论文列表里。`

【1】 

https://devtalk.nvidia.com/default/topic/451750/gpu-vs-cpu-comparison-over-the-last-years/?offset=6

【２】

http://www.vldb.org/pvldb/vol4/p539-neumann.pdf

【３】

MapD: Massive Throughput Database Queries with LLVM on GPUs