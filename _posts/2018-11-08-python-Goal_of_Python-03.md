---
layout:     post
title:      Goal of Python
subtitle:   ISO 选择
date:       2018-11-08
author:     HD
catalog: true
tags:
     - Python
---


## 正文

*既有概念的补充*



**1.像纯英语那样容易理解**

有这样一种情况：

开发使用一些语言开发出了某个功能，过段时间后，可能出现连开发者自己都无法读懂自己写的代码。

**2.用一种方法。最好是只有一种方法来做一件事情**

 实现了一个功能，拒绝花俏，拒绝“炫技”代码

**3.人生苦短，我用Python”**

代码量少	==》解决更多问题

**4.OO-面向对象**

Utils直接拿来用，复用性体现了OO。

大概方法型语言复用性较弱。

**5.可扩展性~~**

Python结合C、C++

---


*Python 程序*



**编译型语言错误的演示：**

```python
code：

print("Hello Python");
print("Hello World");
prit("Hello error");
```

**output：**

```python
[dba@bda 认识Python]$ python 01-HelloPython.py 
Hello Python
Hello World   //前两句还是输出结果了，解释型语言，解释一句，执行一句。
Traceback (most recent call last):
  File "01-HelloPython.py", line 3, in <module>
    prit("Hello error");
NameError: name 'prit' is not defined
[dba@bda 认识Python]$ 

```

> 每行代码负责完成一个动作 ： 写python的优秀习惯

> 语法严苛，从而使得写出的代码整齐简洁。








