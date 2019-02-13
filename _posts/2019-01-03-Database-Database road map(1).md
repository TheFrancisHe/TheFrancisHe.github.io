---
layout:     post
title:      Diving into database（1） —— 路线图
subtitle:   提炼出来的路线图
date:       2019-01-03
author:     HD
catalog: true
tags:
     - database
     - CMU
     - sigmod
     - 数据库基础

---

## 正文

那么，以下是我自己的学习路线图：

- 中国大学mooc（人大和哈工大）：获得全面的数据库知识。
- 《数据库系统概念》《数据库系统实现》
- CMU database https://15445.courses.cs.cmu.edu/fall2017/schedule.html

学习过程中，记得进行实践练习。



### 推荐书籍

> https://www.zhihu.com/question/62464757
>
> https://www.zhihu.com/question/52498996



### 火花

> 作者：interma
>
> 链接：https://www.zhihu.com/question/62464757/answer/206887466
>
> 来源：知乎
>
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
>
> 各位大给出的资料和路线（
>
> [@杨志丰](http://www.zhihu.com/people/null)
>
> ， 
>
> [@Ed Huang](http://www.zhihu.com/people/5940b1ec1c21a3538c6cfcf5711a75a6)
>
>  ）都很好，我再补充一个另外的视角，：
>
>
>
> 目前做数据库的主要是2波人：互联网分布式存储出身和传统数据库出身，二者思考问题可是2个不同的套路，:-)
>
> 这个thread中给的大部分资料都是关于前者（如何为一个分布式存储系统加上数据库功能）的，而传统数据库路线，建议看看如下资料（对我自己帮助很大）：
>
> - 数据库总论：[http://db.cs.berkeley.edu/papers/fntdb07-architecture.pdf](https://link.zhihu.com/?target=http%3A//db.cs.berkeley.edu/papers/fntdb07-architecture.pdf)
>
> - - 介绍经典思路（这个paper有中文）
>   - 教材书就可以不看了，时效性较差
>
> - CMU数据库课程
>
> - - [CMU 15-445/645 :: Intro to Database Systems (Fall 2017)](https://link.zhihu.com/?target=http%3A//15445.courses.cs.cmu.edu/fall2017/)，非常适合有工程基础但是没有数据库基础的同学入门
>
>   - [Schedule - CMU 15-721 :: Advanced Database Systems (Spring 2017)](https://link.zhihu.com/?target=http%3A//15721.courses.cs.cmu.edu/spring2017/schedule.html)，讨论更高级主题，主要是paper讲解
>
>   - - 它们2个在youtube上有配上字幕的视频，还可以提升一下英语
>
> - **实现上重点看看Postgres**
>
> - - pg国内用的人很少，但如果深入对它进行了解，会觉得打开了另一扇窗，有很多特别优良的特性
>
>   - 包括但不局限于如下：
>
>   - - 丰富数据类型，更全面的SQL语法支持
>     - Plan+Optimizer
>     - 模块化的Executor 
>     - FDW
>     - MVCC，更强的隔离级别
>     - PL，可编程性
>     - 等等
>
> 最后回到楼主是直博本科学生，可以按照
>
> [@杨志丰](http://www.zhihu.com/people/null)
>
> 给出的路线做一些工程实践，但不推荐投入大量时间（投入了恐怕也写不好）。毕竟今后无论是做研究还是工程，都会站在巨人肩膀之上，数据库也是一个一生之工程（复杂度堪比操作系统），有侧重的了解基本原理之后，最后一定是在某个层次上进行自己的创新了。
>
>
>
> 如上都是自己的一些看法，我自己也是半路出家做数据库，欢迎大家指正。
>
> --2017-12-05更新--
>
> CMU2017开了一门数据库新课：[CMU 15-445/645 :: Intro to Database Systems (Fall 2017)](https://link.zhihu.com/?target=http%3A//15445.courses.cs.cmu.edu/fall2017/)
>
> 难度介于15-415和15-721之间，更适合有工程基础但是没有数据库基础的同学入门。



> 作者：李晨曦
>
> 链接：https://www.zhihu.com/question/62464757/answer/202033688
>
> 来源：知乎
>
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
>
> 分布式的学习不是很了解，数据库有些经验
>
> 可以按照如下步骤学习
>
> \1. 入门：
>
> 接触过数据库的基础知识和应用之后，就可以开始进行内核级的学习了，先学习传统的关系型数据库，因为它是一切数据库的基础，包括现在比较火的内存数据库，分布式数据库等。
>
> 从IV Database System Implementation开始，把这本书吃透了，包括数据的物理存储结构，索引，查询引擎，缓冲池，SQL编译，查询优化，系统恢复，并发控制。然后实现上面这些理论知识，完成一个支持简单DML，DDL的数据库。一定要实现，只是学习理论，不动手实践是不可能深刻理解的，就像空中楼阁。
>
> [《数据库系统实现（英文版）（第2版）》([美\]加西亚·莫利纳，等)【摘要 书评 试读】- 京东图书](https://link.zhihu.com/?target=http%3A//item.jd.com/10059733.html)
>
> [http://dsm.fudan.edu.cn/JSPWiki/attach/Material_db/database%20system%20complete%20book_2nd.pdf](https://link.zhihu.com/?target=http%3A//dsm.fudan.edu.cn/JSPWiki/attach/Material_db/database%2520system%2520complete%2520book_2nd.pdf)
>
>
>
> \2. 深入理解：
>
> 参考这个论文列表，把里面的论文都读一遍，了解关系型数据库历史，了解数据库的发展过程中走过的弯路，理解它为什么会变成现在这个样子
>
> [rxin/db-readings](https://link.zhihu.com/?target=https%3A//github.com/rxin/db-readings)
>
> 同时也要锻炼系统级编程的能力，深刻理解操作系统的工作原理，并行编程，熟悉一些硬件的工作原理，为以后打下良好的基础。可以读一些优秀的开源数据库的源码，如Peloton的[cmu-db/peloton](https://link.zhihu.com/?target=https%3A//github.com/cmu-db/peloton)，只有几万行代码，PostgreSQL的，代码非常多，不过注释非常清晰
>
>
>
> \3. 进阶
>
> 看最近几年数据库相关的论文，各个方向的发展都全面了解一下，可以参考这两个课程提到的论文[Schedule - CMU 15-721 :: Advanced Database Systems (Spring 2017)](https://link.zhihu.com/?target=http%3A//15721.courses.cs.cmu.edu/spring2017/schedule.html)，[Practical Course: Database Implementation](https://link.zhihu.com/?target=https%3A//db.in.tum.de/teaching/ws1617/imlab/%3Flang%3Den)，找一些感觉兴趣的论文复现一下里面提到的方法。很多算法，数据结构都有一定的适用场景和局限性，要通过自己实现与实验来深刻体会。
>
>
>
> \4. 破茧成蝶
>
> 这才是读博最重要的阶段，通过之前的学习，应该对数据库的各个方面都非常了解了，而且也打下了良好的编程能力，可以选1,2个感兴趣的方向，看看有没有什么可以改进，突破的点，想出自己的idea，实现并与现有的方法进行对比，如果可以做的很好，就非常厉害了。



> 作者：grakra
>
> 链接：https://www.zhihu.com/question/62464757/answer/206613596
>
> 来源：知乎
>
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
>
> 多关注数据库的三大顶级会议, 还有OSDI等.
>
> **将motivation和workload作为最根本的方法论。**
>
> **彻底搞明白存储精髓WAL+RSM.**
>
> 好好阅读经典论文, 搞清楚workload和motivation.
>
> 牢记两个基本观点:
>
> **没有抽象的技术, 凡技术都有自己适用的应用场景.**
>
> **没有广谱的系统, 凡系统都有自己典型的workload.**
>
>
>
> 建议看先阅读下面两本书: 
>
> \1. **Stonebraker的Architecture of a database system.** 
>
> \2. **Jim Gray的Transaction.**
>
>
>
> **学习分布式的RoadMap** 
>
> 1. WAL + RSM 
> 2. 研究分布式共识算法, 因为这个是日志复制协议的基石:  TOB协议, Quorum-based协议(mpaxos, raft),  Primary-backup协议.
> 3. partitioning & replication + local storage engine. 
> 4. local storage engine: bdb, innodb, leveldb(可以参考我写的源码阅读). 
> 5. 磁盘和网络优化技术.  
> 6. 分布式一致性(隔离性). 
> 7. 分布式事务: stm, mvcc, 乐观锁.  
> 8. 分布式查询优化.
>
> **工程实现超高的编程技巧**
>
>
> 1.能够像haskell那样impure和pure分离.
> 2.幂等的设计, 让部分有状态的模块成为metal unit, 同时幂等设计和failstop能够将有效地避bf. 
> 3.元编程能力, 降低代码的冗余和耦合, 代码更适合扩展和组合.
> 4.超高的系统编程能力.
> 5.单测, mock测试设计能力.
> 6.漂亮的日志输出. 
> 7.会做性能分析, [参考大牛博客](https://link.zhihu.com/?target=http%3A//www.brendangregg.com/).
> 8.会使用docker加速自己的开发效率. 
>
> **周边涉及**
>
> 1.精通MySQL sharding, 不知道它的痛，就不知道为什么要坚定不移地搞分布式关系数据库.
>
> 2.精通大数据的BI解决方案, 不知道它的痛，就不知道为什么要搞全新的分布式列式数据库.
>
> 3.区块链，分布式计算引擎也了解一点.
>
> **分布式存储的源码分析方法(**[详情可以参考我的分享](https://zhuanlan.zhihu.com/p/28156653)**)**
>
>
>
> ![img](https://pic1.zhimg.com/v2-691da23954622369b75e536a2b70d218_b.png)![img](https://pic1.zhimg.com/80/v2-691da23954622369b75e536a2b70d218_hd.png)