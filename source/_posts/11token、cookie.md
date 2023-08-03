---
title: Cookie、Token
date: 2022-11-18
tag:
- Cookie、Token
categories:
- Js
---

{% note success:: Cookie、Token%}

 

<!-- more -->

- Cookie

  - 作用：http连接是无状态的，客户端与服务器每次都要验证身份，耗费性能。

    cookie是配合session认证机制，客户端在第一次登陆验证通过后服务器会开辟内存创建session保存客户端的信息，然后给客户端发送一个cookie，客户端拿到cookie后保存起来，后面的请求都会自动带上cookie，服务端验证该cookie的有效性。

    cookie不能跨域访问，大小最多是4kb。

- Token

  - 上面所说每次客户端验证通过后，服务器要创建新的session保留客户端的信息，这无疑增加了服务器的压力。当用户量增大的时候，假如服务器要把这些session分摊到其他服务器上减少压力，而cookie的也不能跨域访问。

    token配合jwt认证机制，当客户验证通过后，给客户端发送token，客户拿到token后可以保存在cookie中，也可以保存在localStorage、sessionStorage等，下次的请求客户端带上token，服务器直接验证token有效性。

    token支持跨域访问，需要客户端自己存储，灵活性高。

- 区别：cookie不能跨域访问，大小最多是4kb。token没有内存限制，需要客户端自己存储，可以存储在cookie中，支持跨域访问。

- 相同点：都可以进行身份认证。