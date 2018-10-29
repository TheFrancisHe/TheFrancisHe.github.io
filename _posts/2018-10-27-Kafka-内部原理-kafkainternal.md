---
layout:     post
title:      Kafka 内部原理总结
subtitle:   生产者、消费者、zookeeper
date:       2018-10-27
author:     HD
catalog: true
tags:
     - 消息队列
     - kafka
     - kafka internal
     - 生产者、消费者、zookeeper
---


## 正文

**异构系统之间的通信**


比如，淘宝电商系统，很庞大，有很多个系统，如果没有中间件，这些系统间的通信是很麻烦的。

同时，这些系统**解耦**后也容易维护和扩展。


![kafka内部原理图](https://raw.githubusercontent.com/TheFrancisHe/TheFrancisHe.github.io/master/img/Kafkainternal.png)



### kafka原理

####kafka的核心组成部分：

**生产者生产消息**  ： 生态系统的输入部分

**Kafka集群管理消息**  

**消费者消费消息**  ： 生态系统的输出部分

**Zookeeper注册消息** ：整个集群的管理、配置信息的注册。


##### 生产者（producer）：
 
这里有两个生产者，产生数据的地方，或者说是pipeline（pipeline概念的理解自行搜索）的入口。

生产者把消息分别发送到两个分区的leader上。

##### Kafka Cluster（集群管理）：

这里有三个broker（kafka实例或者节点），管理很多个topic，topic里还有很多个分区（类似于磁盘的各个区域，分区内部存储有序

这里面涉及到**分区和备份的概念**

1. 多分区： Topic A里，一份数据，多个分区，多个副本；一个leader，多个follower

2. 单分区： Topic B里，一个broker，一个分区，一个副本。


######分区内部存储有序的示例。

1. 多分区：生产者按顺序生产出消息，消费者取出来的消息无序（pub/sub）。
2. 单分区：生产者按顺序生产出消息，消费者取出来的消息有序（p2p，pulling）。

##### 消费者（consumer）：

单分区消费消息时，分两种：

1. 低级API ： 自己控制从哪个角标开始读，读多少，还剩多少。

2. 高级API ： 读多少，还剩多少，都统一管理好，不需要自己维护。


**Consumer Group**

1. CG里面成员消费的时候，不关心follower，只去leader消费。
   当leader挂掉，follower升级为leader，才可以被消费。


2. CG里，Consumer A 和 Consumer B 不能同时消费同一个分区。

##### zookeeper（注册信息）：

1. 注册了 kafka cluster 的信息。

2. 消费者的信息。

3. **不注册生产者的信息。**

