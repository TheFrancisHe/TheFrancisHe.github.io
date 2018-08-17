---
layout:     post
title:      MVCC-进阶(1)
subtitle:   PostgresDoc对MVCC的概述
date:       2018-08-08
author:     HD
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Database
    - MVCC
    - concurrency
    - Postgres
---
# 前言

从Postgres的doc里，一窥Postgres开发者们，是如何理解MVCC的。

# 正文

## postgres开发者们对于mvcc的认识

链接 : https://www.postgresql.org/docs/9.5/static/mvcc-intro.html


> PostgreSQL provides a rich set of tools for developers to manage concurrent access to data. Internally, data consistency is maintained by using a multiversion model (Multiversion Concurrency Control, MVCC). 


***关键词：concurrent access to data 、data consistency ***

大意：从外部表现来看，Postgres 通过MVCC 用以处理数据并发访问；从内部原理来看，用以维护数据一致性（data consistency）

	  两个角度的理解，前者侧重行为，后者侧重可能引起的结果。意思是，往往在高并发的数据访问下，
	  数据库会出现脏读等代表的数据不一致的情况。　如何解决？
	  这里的解决方案是：MVCC


> This means that each SQL statement sees a snapshot of data (a database version) as it was some time ago, regardless of the current state of the underlying data. 


***关键词：each SQL statement ，snapshot，current state ***

大意：采用MVCC机制后，意味着每次的sql访问的数据为快照数据（或者是一个　database version（另外一种情况）），即某段时间之前的数据或者database version，无需考虑底层数据的真实状态。


> This prevents statements from viewing inconsistent data produced by concurrent transactions performing updates on the same data rows, providing transaction isolation for each database session.

***关键词：inconsistent data,concurrent transactions,same data rows ，transaction isolation ***

大意：MVCC 防止readers读取到不一致的数据，后者是由并发事务对相同rows进行并发更新产生的，从而为每个事务提供隔离。


> MVCC, by eschewing the locking methodologies of traditional database systems, minimizes lock contention in order to allow for reasonable performance in multiuser environments. 

***关键词：locking methodologies,minimizes lock contention ***

大意：MVCC ，可以避开常见的锁机制，从而最小化锁争用开销，通过这种方式，在多用户即并发环境下，是一种合理地性能提升机制。



The main advantage of using the MVCC model of concurrency control rather than locking is that in MVCC locks acquired for querying (reading) data do not conflict with locks acquired for writing data, and so reading never blocks writing and writing never blocks reading. PostgreSQL maintains this guarantee even when providing the strictest level of transaction isolation through the use of an innovative Serializable Snapshot Isolation (SSI) level.

***关键词：reading never blocks writing and writing never blocks reading，SSI ***

大意：MVCC相较于锁机制，主要优势在于在查询（读取）数据时获取的MVCC锁与写入数据时获取的锁不冲突，即便在最严格的Serializable隔离级别即SSI下，
	 Postgres也能做到读写互不阻塞的特点。


Table- and row-level locking facilities are also available in PostgreSQL for applications which don't generally need full transaction isolation and prefer to explicitly manage particular points of conflict. However, proper use of MVCC will generally provide better performance than locks. In addition, application-defined advisory locks provide a mechanism for acquiring locks that are not tied to a single transaction.


***关键词：Table-level locking ,  row-level locking***

大意：当然了，Postgres也提供了传统的表级锁和行锁工具，以便适用于那些需要人为明确锁管理的应用程序。但是，合理使用MVCC通常会提供比锁更好地性能。另外，postgr	   es也提供了Advisory Locks，详情查看：https://www.postgresql.org/docs/current/static/explicit-locking.html 。




