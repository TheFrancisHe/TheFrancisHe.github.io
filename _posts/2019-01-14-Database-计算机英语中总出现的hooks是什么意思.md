---

layout:     post
title:      计算机中的hooks如何理解？
subtitle:   从知乎提炼出的观点
date:       2019-01-1４
author:     HD
catalog: true
tags:
     - database
     - callback
     - hooks
     - Postgres

---

## 正文

https://www.zhihu.com/question/20610442

Postgres内核里，有很多hooks，所以有必要全面了解下hooks。

搜了wiki，对运行机制大致有了解。

搜了知乎，从中选取了不错的答案，摘录在下面。



pg_stat_statments 源码里的hooks用法，有两个想法切入到我的脑海：


- **Servlet** 接口定义的init方法，通常让user自行实现。
- AOP思想。

下个blog会谈谈Postgres的hooks。



**计算机英语中总出现的"hooks" 是什么意思? "钩子" ? 这个钩子应该怎么理解? 是回调的意思?**



### 火花

答案1：



> > In computer programming, the term hooking covers a range of techniques used to alter or augment the behavior of an operating system, of applications, or of other software components by intercepting function calls or messages or events passed between software components. Code that handles such intercepted function calls, events or messages is called a "hook".

> 作者：安江泽
>
> 链接：https://www.zhihu.com/question/20610442/answer/128122399
>
> 来源：知乎
>
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



---

答案2：



> 一个定义不明的术语而已Hook：在已经可以正常运作的程序中额外添加流程控制可以实现，但不限于获取所hook流程中特定时刻的各种数据，修改数据，修改程序流程比如，在一家公司，所有采购事宜只需财务和专员协调沟通即可完成。现在公司决定下个hook, 采购事宜需总经理签字批准才可继续执行。至于总经理怎么hook操作：是随便签字，还是搞潜规则，或者有自己的想法和安排来进行新的采购事项，这就属于hook的具体实现实际上不理解hook，也无所谓。毕竟不一定用得到，用到的时候自然有自己的理解
>
>
>
> 作者：Saterblues
> 链接：https://www.zhihu.com/question/20610442/answer/128149486
> 来源：知乎
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



---

答案3：

> 一个初学者的理解：Hooks就像一些外来的钩子，在源代码之间钩取（窃听）一些信息，当它捕捉到自己感兴趣的事发生，就拦截下来，让自己的代码执行一下，处理一下这个信息，然后再放出去继续之前的进程。这样就可以在不用改变源代码的情况下，做一些别的事情，比方说监控、分析和一些恶意的事。
> 如有不对请指正。
>
> 作者：凌霜
>
> 链接：https://www.zhihu.com/question/20610442/answer/128226574
>
> 来源：知乎
>
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。