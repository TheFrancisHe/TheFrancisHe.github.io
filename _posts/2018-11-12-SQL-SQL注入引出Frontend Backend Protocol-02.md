## 由SQL Injections引出的 Frontend Backend Protocol



***写在前面***

*继上一篇文章后，我了解到 SQL Injections 与 Frontend Backend Protocol（数据库前后端协议）中的 simple query 与Extended Query 密切相关。*



### Frontend Backend Protocol

***以 PostgreSQL的前后端协议为例。***

##### 官方Doc主页面：

​	https://www.postgresql.org/docs/current/protocol.html    



**About Simple Query：*SQL注入可能发生***

​	https://www.postgresql.org/docs/current/protocol-flow.html#id-1.10.5.7.4 



**About  Extended Query：*可彻底避免SQL注入***

​	https://www.postgresql.org/docs/current/protocol-flow.html#PROTOCOL-FLOW-EXT-QUERY



**相关中文总结**

​	https://github.com/Qihoo360/gpstall/wiki/Postgre-Frontend-Backend-Protocol%E7%AE%80%E4%BB%8B

​	***补充理解：*** *不同编程语言，其与前后端通信协议对应的接口库不同。 C : Libpq ； JAVA：JDBC；* 

**案例：SQL 注入的“防”与“治”**

​	https://tapoueh.org/blog/2018/11/preventing-sql-injections/

​	***补充理解：***

​	*文中Server-Side 推测，应该是指协议的数据库服务器端，与协议的应用程序端共同组成整个完整的协议，也就是应用程序和数据库之间的协议层。*

​	*因为文中有一句话： server-side sends message ，刚开始把server-side理解成数据库服务器端，所以纳闷，if so，那数据库服务器是终点了，还要再往哪儿发送message。后来反应过来，应该是指协议里的sever-side部分。*

​	*所以整个顺序是， 应用程序 ==》协议层（含有server-side协议） ==》数据库服务器*

​	*这样，server-side 发送 message 就解释得通了。*





