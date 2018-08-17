---
layout:     post
title:      MVCC-进阶(2)-
subtitle:   PostgresDoc对Transaction Isolation的认识
date:       2018-08-13
author:     HD
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - MVCC - Isolation - 事务隔离级别 - 并发控制
---


## 前言

事务隔离级别的理解，也是并发控制的关键组成部分。


## 正文

>The SQL standard defines four levels of transaction isolation. The most strict is Serializable, which is defined by the standard in a paragraph which says that any concurrent execution of a set of Serializable transactions is guaranteed to produce the same effect as running them one at a time in some order. The other three levels are defined in terms of phenomena, resulting from interaction between concurrent transactions, which must not occur at each level. The standard notes that due to the definition of Serializable, none of these phenomena are possible at that level. (This is hardly surprising -- if the effect of the transactions must be consistent with having been run one at a time, how could you see any phenomena caused by interactions?)

***keywords: Serializable,phenomena***

大意：

SQL 标准定义了4种隔离级别，Serializable是最严格的一种，可以保证并发事务可以按照someorder（某种顺序）一个个串行执行。在该隔离级别下，不会出现任何“脏读、幻读”等现象。

其余三种隔离级别的定义，是根据phenomena（现象）的不同而定义的（这部分一会儿会着重说明）。

>The phenomena which are prohibited at various levels are:

>dirty read（脏读）

>A transaction reads data written by a concurrent uncommitted transaction.(某个事务读取到了另一个并发事务未提交的data)

在SQL标注的，Read uncommitted隔离级别里 ，无法避免脏读，但是Postgres的Read uncommitted 则可以避免脏读 WHY ?

演示：

用mysql的例子演示下脏读（PG里没有脏读的现象）：

```

a窗口
set transaction isolation level read uncommitted;
start transaction;
select * from account; // 第一步
-------------发现a帐户是1000元，转到b窗口

select * from account; //第三步
-------------发现a帐户是1100元，发生了脏读（这个事务读取到了别的事务未提交的数据）



b窗口
start transaction;
update account set money=money+100 where name='aaa'; //第二步
-------------事务在不提交的情况下，转到a窗口进行查询

```

>nonrepeatable read（不可重复读）
A transaction re-reads data it has previously read and finds that data has been modified by another transaction (that committed since the initial read).
（事务A读取到它先前读取过的行，却发现前后读取的行的内容不一致，因为该行内容在再次读取之前，被另一个已提交的事务修改了）这句话有点绕，完后会有例子验证。

简要理解： 读取到对方提交的数据。

Read uncommitted ， Read committed  会出现这种情况。


![table](https://github.com/TheFrancisHe/TheFrancisHe.github.io/blob/master/img/post-pg-rr.png)


>phantom read（幻读）
A transaction re-executes a query returning a set of rows that satisfy a search condition and finds that the set of rows satisfying the condition has changed due to another recently-committed transaction.
（一个事务再次执行query，查询condition不变，却发现前后返回的行数不同，原因是由于另一个最新提交的事务（新插入或删除了一行或多行））

Read uncommitted ， Read committed  ，Repeatable read.

![table2](https://github.com/TheFrancisHe/TheFrancisHe.github.io/blob/master/img/post-pg-hd.png)


并不是说幻读就是错的，适用于转账，但不适用与做报表。


>serialization anomaly（序列化异常现象）
The result of successfully committing a group of transactions is inconsistent with all possible orderings of running those transactions one at a time. （提交一组事务返回的结果和把这些事务按照既定顺序返回的结果不一致，有点难理解，完后会有解释）






![table3](https://raw.githubusercontent.com/TheFrancisHe/TheFrancisHe.github.io/master/img/post-pg-transaction.png)

>In PostgreSQL, you can request any of the four standard transaction isolation levels, but internally only three distinct isolation levels are implemented, i.e. PostgreSQL's Read Uncommitted mode behaves like Read Committed. This is because it is the only sensible way to map the standard isolation levels to PostgreSQL's multiversion concurrency control architecture.

在PostgreSQL中，您可以设置四个标准事务隔离级别中的任何一个，但在内部只有三种隔离级别。其中，在pg里， Read Uncommitted 从功能上看，基本能相当于Read Committed，所以PG里就吧RU给省略了，这是一种比较明智的策略，以便将Postgres自身的MVCC架构，与SQL标注定义隔离级别的标准的对应起来。WHY ？需要看看postgres的隔离的内部原理。


>The table also shows that PostgreSQL's Repeatable Read implementation does not allow phantom reads. Stricter behavior is permitted by the SQL standard: the four isolation levels only define which phenomena must not happen, not which phenomena must happen. The behavior of the available isolation levels is detailed in the following subsections.

从表里看出，postgres不允许phantom phantom （幻读）。这也是符合SQL标准的，因为SQL关于隔离级别的定义，该表还显示PostgreSQL的Repeatable Read实现不允许幻读。SQL标准允许更严格的行为：四个隔离级别仅定义哪些现象不得发生，而不是必须发生哪种现象 。可用隔离级别的行为将在以下小节中详细说明。


>To set the transaction isolation level of a transaction, use the command SET TRANSACTION.

通过命令 SET TRANSACTION 设置隔离级别。

Important: Some PostgreSQL data types and functions have special rules regarding transactional behavior. In particular, changes made to a sequence (and therefore the counter of a column declared using serial) are immediately visible to all other transactions and are not rolled back if the transaction that made the changes aborts. See Section 9.16 and Section 8.1.4.

（这部分暂时不表）





### 参考：



