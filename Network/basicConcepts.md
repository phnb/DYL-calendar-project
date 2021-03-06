# Cookie, Session & Token
[参考文章](https://www.cnblogs.com/moyand/p/9047978.html)

### Cookie

cookie 是一个非常具体的东西，指的就是浏览器里面能永久存储的一种数据，仅仅是浏览器实现的一种数据存储的一种数据。

cookie是由服务器生成发送给浏览器，浏览器吧cookie以kv的形式保存到某个目录下的文本文件内，下一次请求同一网站会把该cookie发送给服务器。由于cookie是存在客户端上的,所以浏览器加入了一些限制确保cookie不会被恶意使用，同时不会占据太多的磁盘空间，所以每个域的cookie数量是有限的。

### Session
session从字面上讲，就是会话。服务器需要指导当前发送请求给自己的是谁。为了做这种区分，服务器就要给每个客户端分配不同的“身份标识”，可以有很多种方式，对于浏览器客户端，大家都采用cookie的方式。

服务器使用session把用户临时信息保存在了服务器上，用户离开网站后session会被销毁，这种用户信息储存方式相对cookie来说更安全，可是session有一个缺陷，如果web服务器做了负载均衡，那么下一个操作请求到了另一台服务器的时候session会丢失。

### Token
在web领域基于token的身份验证随处可见。在大多数使用Web API的互联网公司中，tokens是多用户下处理认证的最佳方式。
一下几点特性会让你在程序中使用基于Token的身份验证


+ 1. 无状态
+ 2. 支持移动设备
+ 3. 跨程序调用
+ 4. 安全

##### 1.1 Token的起源
在Token之前，认证都是基于服务器的验证，我们都知道HTTP协议是无状态的，这种无状态意味着程序需要验证每一次请求，从而辨别客户端的身份。在Token之前,程序都是通过服务端存储的登录信息来辨别请求的。这种方式一般都是痛殴存储Session来完成。

随着Web, 应用程序，以及移动端的星期，这种验证烦事逐渐暴露了问题，尤其是在可拓展性方面。

基于服务器验证方式暴露的一些问题：
+ Session: 每次认证用户发起请求时，服务器需要区创建一个记录来存储信息，当越来越多的用户发起请求时，内存的开销也会不断增加。
+ 可拓展性：在服务端的内存中使用session存储登录信息，伴随而来的是可拓展性问题。
+ CORS(跨域资源共享)：当我们需要让数据跨多台移动设备上使用时，跨域资源的共享会是一个让人头疼的问题。在使用Ajax抓取另一个域的资源时，就可能会出现禁止请求的情况。
+ CSRF(跨域请求伪造)：用户在访问银行网站时，他们很容易收到跨站请求伪造的攻击，并且能够被利用其访问其他的网站。
<br>

基于Token的验证原理
1. 用户通过用户名和密码发送请求
2. 程序验证
3. 程序返回一个签名的Token给客户端
4. 客户端存储Token, 并且每次用于发送请求
5. 服务端验证Token 并返回数据

每一次请求都需要Token。Token应该在HTTP的头部发送从而保证了HTTP请求的无状态。我们同时可以通过设置服务器属性Access-Control-Allow-Origin:* , 从而让服务器能接受来自所有域的请求。需要注意的是，在ACAO头部标明（designating）*时，不得带有像HTTP认证，客户端SSL证书和cookies证书。

Token的优势
+ 安全性
+ 无状态，可拓展性
+ 多平台跨域（）
