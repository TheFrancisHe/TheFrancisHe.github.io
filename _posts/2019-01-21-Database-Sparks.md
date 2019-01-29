---

layout:     post
title:      自己的、同行的关于数据库发展的Sparks
subtitle:   长期更新
date:       2019-01-21
author:     HD
catalog: true
tags:
     - database
     - 他山之石
     - Sparks
     - 行业见解

---

## 正文



2019.1.21 — beginning

https://projects.apache.org/projects.html?category

---

刷 leetcode 需要哪些基础？

https://www.zhihu.com/question/30737325/answer/524120016

---

2019.1.21 

@zhh-4096的微博：

​	`有些同行说数据库里面的SQL引擎是大脑是最难的，对于OLTP场景的数据库，我不这么认为，我觉得事务引擎和存储引擎才是最费神的；对于OLAP的场景，存储引擎的设计以及统计信息的准确度同样对SQL引擎的好坏有巨大影响。CBO还有些通用行，RBO纯粹就是经验的堆积，就算SQL表达式的编译也挺死板的。`





​	`技术人员做数据库这个方向的创业能省一些事，比如产品经理都不太需要了，SQL标准就在那，产品要做什么功能就看对SQL的支持程度了，把精力放在技术实现的创新上即可。最后衡量产品好不好无非是看看三个大的卖点做得如何：性能有多快？方便运维吗？能轻松从一台服务器扩展到3台甚至到上百上千上万台吗。`





`在SQL引擎里引入渐进式优化可能是个好思路。生成plan的时间和执行时间是成反比的，不同应用场景对这两个时间有不同要求。比如OLTP场景通常是在小数据集上做简单查询，要求快速响应，所以对生成plan的时间会限定在微妙级内；`

`而OLAP因为数据集大查询复杂所以更在乎执行时间，多花点时间在生成plan阶段能得到更优的plan从而降低执行时间。但是这其中有一个问题，就是要查询的数据集并不是那么显而易见的，对于一个复杂的查询应用各种过滤条件和索引后可能也只涉及一个很小的数据集，所以如果对这样的查询花了很多时间在生成plan的阶段就不是那么划算了。`

`所以是否可以考虑一种渐进式的优化策略，先用很少的时间得到一个初级plan然后用它去执行，随着遍历的数据越来越多那么这个plan就变成热点了，然后再额外开另一个线程去优化这个plan，优化好了再切到它，也就是说plan的优化程度是受运行时的数据集动态提升的。这里面的难点在于如果前后得到的两个plan走的是不同索引，那么切换到新的plan后如何保证之前处理过的数据不被重复处理呢？`







---

2019.1.28

NO.1

> http://www.yinwang.org/blog-cn/2017/07/06/master-pl  来自王垠的blog-

```
重视语言特性，而不是语言：

变量定义
算术运算
for 循环语句，while 循环语句
函数定义，函数调用
递归
静态类型系统
类型推导
lambda 函数
面向对象
垃圾回收
指针算术
goto 语句
```

```\
掌握关键语言特性，忽略次要特性
意为将重点放在其特色上。
自己动手实现其语言特性。
```



NO.2

> 关于SQL标准：
>
> https://wiki.postgresql.org/wiki/Developer_FAQ#Where_can_I_get_a_copy_of_the_SQL_standards.3F



NO.3

> https://www.zhihu.com/question/47902654

`最简单的办法：关注一下SIGMOD，VLDB，ICDE上每年新发表的paper（尤其是前两个）。把title和abstract看一遍，你基本就都懂了。`



NO.4

> TiDB<==RocksDB<==存储
>
> 来源：http://alimy.me/post/dev_201805021940/
>

`NewSQL: 分布式数据库TiDB、CockroachDB
TiDB
TiDB 开源分布式 NewSQL 关系型数据库 TiDB 是新一代开源分布式 NewSQL 数据库，模型受 Google Spanner / F1 论文的启发，实现了自动的水平伸缩，强一致性的分布式事务，基于 Raft 算法的多副本复制等重要 NewSQL 特性。TiDB 结合了 RDBMS 和 NoSQL 的优点，部署简单，在线弹性扩容和异步表结构变更不影响业务， 真正的异地多活及自动故障恢复保障数据安全，同时兼容 MySQL 协议，使迁移使用成本降到极低。`

`CockroachDB (蟑螂DB/小强DB)
CockroachDB（中文名蟑螂DB，所以又可以称为小强DB），是构建于事务处理及强一致性KV存储上的分布式SQL数据库，支持水平扩展、自动容错处理、强一致性事务，并且提供SQL接口用于数据处理，是Google Spanner/F1的开源实现。 CockroachDB适用于应用对数据要求精确、可靠、完全正确的场景，支持自动复制、均匀分布、基于极小配置的数据恢复，可用于分布式的、可复制的联机事务处理（OLTP），多数据中心的部署，私有云的基础构建，它不适用于读少写多的场景，可以用内存数据库来代替，也不适用于复杂的join查询，重量级的数据分析及联机分析处理（OLAP）。`



NO.5 

> 后Hadoop时代的大数据架构
>
> https://zhuanlan.zhihu.com/p/19962491

