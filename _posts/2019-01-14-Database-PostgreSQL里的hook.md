---

layout:     post
title:      Hooks in PostgreSQL
subtitle:   读过的文章，与hooks,postgreSQL相关
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

*1.维基百科上的hooking*

> **钩子编程**（hooking），也称作“挂钩”，是[计算机程序设计](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1)术语，指通过拦截[软件模块](https://zh.wikipedia.org/w/index.php?title=%E6%A8%A1%E5%9D%97%E5%8C%96%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1&action=edit&redlink=1)间的函数调用、[消息传递](https://zh.wikipedia.org/wiki/%E8%A8%8A%E6%81%AF%E5%82%B3%E9%81%9E_(%E8%BB%9F%E9%AB%94))、事件传递来修改或扩展操作系统、应用程序或其他软件组件的行为的各种技术。处理被拦截的函数调用、事件、消息的代码，被称为**钩子**（hook）。
>
> 钩子编程有多种用途，如[调试](https://zh.wikipedia.org/wiki/%E8%B0%83%E8%AF%95)、扩展功能。例如在键盘或鼠标事件到达应用程序之前拦截这些事件；拦截应用程序或其他模块的操作系统调用以监督行为、修改功能。也广泛用于benchmarking程序，如度量3D游戏的[帧率](https://zh.wikipedia.org/wiki/%E5%B8%A7%E7%8E%87)。
>
> 钩子编程也被用于恶意代码，如[rootkit](https://zh.wikipedia.org/wiki/Rootkit)是各种通过假扮系统API调用输出来隐藏自身进程的可见性的工具与技术；[游戏外挂](https://zh.wikipedia.org/wiki/%E6%B8%B8%E6%88%8F%E5%A4%96%E6%8C%82)是另一类例子。



链接：https://zh.wikipedia.org/wiki/%E9%92%A9%E5%AD%90%E7%BC%96%E7%A8%8B



---

*2.postgres 里 hooks的示例1 ：*

使用了什么HOOK： ClientAuthentication_hook_type

功效：认证失败时，SLEEP一段时间后再返回客户端，用于加大暴力破解的难度。

```c

//中文部分来自德哥的blog https://yq.aliyun.com/articles/603965/

src/backend/libpq/auth.c

/*
 * This hook allows plugins to get control following client authentication,
 * but before the user has been informed about the results.  It could be used
 * to record login events, insert a delay after failed authentication, etc.
 */
ClientAuthentication_hook_type ClientAuthentication_hook = NULL;

...............
/*
 * Client authentication starts here.  If there is an error, this
 * function does not return and the backend process is terminated.
 */
void
ClientAuthentication(Port *port)
{
................
// 走到这里，如果定义了HOOK，那么就执行HOOK定义的函数。
// 即延迟响应客户端。
// 从而实现提高暴力破解的两次重试之间的等待，提高暴力破解时间。

        if (ClientAuthentication_hook)
                (*ClientAuthentication_hook) (port, status);

        if (status == STATUS_OK)
                sendAuthRequest(port, AUTH_REQ_OK, NULL, 0);
        else
                auth_failed(port, status, logdetail);
}
```





---

3.再提供一个自定义hook的示例，该示例来自“健哥的数据花园”

链接：https://www.cnblogs.com/gaojian/p/3259147.html

该示例的逻辑如下：

> 此处使用的是 ProcessUtility_hook，作为了例子，当我们从psql等发起 drop database xxx命令的时候。
>
> 本hook被激活，然后进行检查，如果被删除的数据库名为 fooddb，那么只有用户foo才有机会删除它。

作者将hook用于控制数据库中特定活动的执行

---

4.这篇blog详细讲解了hook的内部机制：

https://www.cnblogs.com/flying-tiger/p/7801258.html













