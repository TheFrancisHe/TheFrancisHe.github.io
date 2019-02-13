---
layout:     post
title:      Diving into database（2） —— 路线图
subtitle:   提炼出来的路线图
date:       2019-01-08
author:     HD
catalog: true
tags:
     - database
     - CMU
     - sigmod
     - 数据库基础

---

## 正文

> 目前做数据库的主要是2波人：互联网分布式存储出身和传统数据库出身，二者思考问题可是2个不同的套路，:-).



蛮认同此答主的观点。

此外，该答主还给出了不错的DB学习路线图，见下文“火花”。



对于有价值的观点与建议，我会持续记录在个人博客里，持久化嘛。





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
> - 数据库总论：[http://db.cs.berkeley.edu/papers/fntdb07-architecture.pdf](http://link.zhihu.com/?target=http%3A//db.cs.berkeley.edu/papers/fntdb07-architecture.pdf)
>
> - - 介绍经典思路（这个paper有中文）
>   - 教材书就可以不看了，时效性较差
>
> - CMU数据库课程
>
> - - [CMU 15-445/645 :: Intro to Database Systems (Fall 2017)](http://link.zhihu.com/?target=http%3A//15445.courses.cs.cmu.edu/fall2017/)，非常适合有工程基础但是没有数据库基础的同学入门
>
>   - [Schedule - CMU 15-721 :: Advanced Database Systems (Spring 2017)](http://link.zhihu.com/?target=http%3A//15721.courses.cs.cmu.edu/spring2017/schedule.html)，讨论更高级主题，主要是paper讲解
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
> CMU2017开了一门数据库新课：[CMU 15-445/645 :: Intro to Database Systems (Fall 2017)](http://link.zhihu.com/?target=http%3A//15445.courses.cs.cmu.edu/fall2017/)
>
> 难度介于15-415和15-721之间，更适合有工程基础但是没有数据库基础的同学入门。