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

> 有些同行说数据库里面的SQL引擎是大脑是最难的，对于OLTP场景的数据库，我不这么认为，我觉得事务引擎和存储引擎才是最费神的；对于OLAP的场景，存储引擎的设计以及统计信息的准确度同样对SQL引擎的好坏有巨大影响。CBO还有些通用行，RBO纯粹就是经验的堆积，就算SQL表达式的编译也挺死板的。



> 技术人员做数据库这个方向的创业能省一些事，比如产品经理都不太需要了，SQL标准就在那，产品要做什么功能就看对SQL的支持程度了，把精力放在技术实现的创新上即可。最后衡量产品好不好无非是看看三个大的卖点做得如何：性能有多快？方便运维吗？能轻松从一台服务器扩展到3台甚至到上百上千上万台吗。



> 有些同行说数据库里面的SQL引擎是大脑是最难的，对于OLTP场景的数据库，我不这么认为，我觉得事务引擎和存储引擎才是最费神的；对于OLAP的场景，存储引擎的设计以及统计信息的准确度同样对SQL引擎的好坏有巨大影响。CBO还有些通用行，RBO纯粹就是经验的堆积，就算SQL表达式的编译也挺死板的。 



---

2019.1.28

NO.1

> http://www.yinwang.org/blog-cn/2017/07/06/master-pl  来自王垠的blog-

> - 重视语言特性，而不是语言：

> ​变量定义
> 算术运算
> for 循环语句，while 循环语句
> 函数定义，函数调用
> 递归
> 静态类型系统
> 类型推导
> lambda 函数
> 面向对象
> 垃圾回收
> 指针算术
> goto 语句	

> - 掌握关键语言特性，忽略次要特性
>
> 意为将重点放在其特色上。

> - 自己动手实现其语言特性。

NO.2

> 关于SQL标准：
>
> https://wiki.postgresql.org/wiki/Developer_FAQ#Where_can_I_get_a_copy_of_the_SQL_standards.3F





