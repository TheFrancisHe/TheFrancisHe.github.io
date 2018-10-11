---
layout:     post
title:      Kafka-Connect-数据同步
subtitle:   Kafka Connect+CDC，实现mysql到PG的数据同步
date:       2018-10-11
author:     HD
catalog: true
tags:
    - Kafka 
    - Kafka Connect
    - CDC工具
    - debezium
---


## 正文

#### Kafka Connect 介绍

1. 官网
2. 这篇博文：http://benx.io/2018/05/20/kafka-connect/


#### CDC工具介绍
1. https://yq.aliyun.com/articles/228292
2. 官网
3. Debezium：https://blog.csdn.net/lzufeng/article/details/81197821


#### mysql到pg的同步案例：
1. 将变更捕获到Kafka：https://juejin.im/post/5b7c036bf265da43506e8cfd
2. 将变更捕获到Kafka，同时同步到目标数据库，即实现mysql到pg的数据同步：
   http://blog.51cto.com/11257187/2153817?source=dra




### 参考：

图文来自：

https://www.journaldev.com/9743/jms-messaging-models

部分资料来自网络

