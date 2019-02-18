---

layout:     post
title:      Java RoadMap By zhh-4096 aka codefollower
subtitle:   面向数据库行业的Java RoadMap
date:       2019-02-13
author:     HD
catalog: true
tags:
     - database
     - Java
     - Roadmap
     - codefollower

---



#### 写在前面：



> 作者：codefollower
>
> 链接：https://www.zhihu.com/question/305924723/answer/558177879
>
> 来源：知乎
>
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



## 正文

如果我是一个新人，想学后端的Java开发，我会这么学:



**初级阶段**

`拿本core java，把java的语言特性熟练掌握，学会io/nio/net/jdbc这些基础知识，熟练使用util包中的map/set/list/queue，掌握多线程编程并熟练应用concurrent包中的工具。`

**中级阶段**

`有了初级阶段的知识储备后，找本讲HTTP协议的书来看，然后把Netty框架的代码下下来，看看它如何用初级阶段提到的知识去实现一个HTTP Server/Client。`

`理解了Netty的实现后，就能很容易学会使用Vert.x、Node.js这类异步事件驱动的平台框架。`

**高级阶段**

`取决于想往哪个方向走，有数据库、大数据/NoSQL、各类中间件。`

`想做数据库，得把基本的数据库理论基础补上，阅读H2数据库的代码是Java程序员从事数据库开发的最好起点。`

`大数据/NoSQL方向更加庞大，通常阅读Google的老三篇是起点，然后学习hadoop/spark/flink，hadoop权威指南那本书可以快速了解大数据方向的概况。`

`中间件稍微容易点，有服务框架、消息中间件、分库分表这类传统中间件，不太需要多高深的理论。`

**JVM**

`找本专门讲JVM原理的书来读读即可，除非工作需要，HotSpot VM的代码能不碰就不要碰，不要担心面试时碰到面试官问HotSpot VM的实现细节怎么办，真懂HotSpot VM实现细节的人在国内屈指可数。`

**补充**

`有网友看了觉得这样学就废了，意思是觉得容易或没用吧？2010年我就会netty的代码了，三年前我重新做web项目，不想用spring全家桶，找到了vert.x，读了一个下午官方的文档我就拿来开发应用了，vert.x的核心还是基于netty的，vert.x web也只不过在netty的http协议实现之上做了一层包装。`

`达到中级阶段足够开发java web应用了，谁要是觉得简单，有机会被我面试时最好做好心理准备，一个netty就能把你问出汗。`

**再补充**

`看了几个其他高赞的回答，你们若是到了我这把年纪还想用spring撸点刚毕业的新人就能做的java web应用，请忽视我说的。`

`知乎的受众群就这点技术追求？！jdbc都不学，你连给某个数据库实现个jdbc driver的能力都没有，你连MyBatis的代码都看不懂，真的就是个只会调api的低端CRUD码农了，还想个毛线的架构师，来我这应聘连个初级程序员我都不想给。`