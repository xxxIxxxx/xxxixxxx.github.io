---
title: Cookie 和 Session 的关系和区别是什么？
date: 2021-02-18 11:55
categories: [网络协议]
tags: [Cookie,Session]
sticky:  #9999
---

# Cookie 和 Session 的关系和区别
1. Cookie 在客户端（浏览器），Session 在服务器端。 
2. Cookie 的安全性一般，他人可通过分析存放在本地的 Cookie 并进行 Cookie 欺骗。在安全性第一的前提下，选择 Session 更优。重要交互信息比如权限等就要放在 Session 中，一般的信息记录放 Cookie 就好了。 
3. 单个 Cookie 保存的数据不能超过 4K，很多浏览器都限制一个站点最多保存 20 个 Cookie。 
4. Session 可以放在文件、数据库或内存中，比如在使用 Node 时将 Session 保存在 redis 中。由于一定时间内它是保存在服务器上的，当访问增多时，会较大地占用服务器的性能。考虑到减轻服务器性能方面，应当适时使用 Cookie。 
5. Session 的运行依赖 Session ID，而 Session ID 是存在 Cookie 中的，也就是说，如果浏览器禁用了 Cookie，Session 也会失效（但是可以通过其它方式实现，比如在 url 中传递 Session ID）。 
6. 用户验证这种场合一般会用 Session。因此，维持一个会话的核心就是客户端的唯一标识，即 Session ID。

题外话，那么话说 Session Cookie 能被篡改么？ 理论上可以，只要改变了连接时的 Session ID 就可以了~



# Cookie 
Cookie 是客户端保存用户信息的一种机制，用来记录用户的一些信息。如何识别特定的客户呢？cookie 就可以做到。每次 HTTP 请求时，客户端都会发送相应的 Cookie 信息到服务端。它的过期时间可以任意设置，如果你不主动清除它，在很长一段时间里面都可以保留着，即便这之间你把电脑关机了。
既然它是存储在客户端的，换句话说通过某些手法我就可以篡改本地存储的信息来欺骗服务端的某些策略。

# Session
Session 是在无状态的 HTTP 协议下，服务端记录用户状态时用于标识具体用户的机制。它是在服务端保存的用来跟踪用户的状态的数据结构，可以保存在文件、数据库或者集群中。在浏览器关闭后这次的 Session 就消失了，下次打开就不再拥有这个 Session。其实并不是 Session 消失了，而是 Session ID 变了，服务器端可能还是存着你上次的 Session ID 及其 Session 信息，只是他们是无主状态，也许一段时间后会被删除。

---
实际上 Cookie 与 Session 都是会话的一种方式。它们的典型使用场景比如 “购物车”，当你点击下单按钮时，服务端并不清楚具体用户的具体操作，为了标识并跟踪该用户，了解购物车中有几样物品，服务端通过为该用户创建 Cookie/Session 来获取这些信息。

如果你的站点是多节点部署，使用 Nginx 做负载均衡，那么有可能会出现 Session 丢失的情况（比如，忽然就处于未登录状态）。这时可以使用 IP 负载均衡（IP 绑定 ip_hash，每个请求按访问 ip 的 hash 结果分配，这样每个访客固定访问一个后端服务器，可以解决 Session 的问题），或者将 Session 信息存储在集群中。在大型的网站中，一般会有专门的 Session 服务器集群，用来保存用户会话，这时可以使用缓存服务比如 Memcached 或者 Redis 之类的来存放 Session。

目前大多数的应用都是用 Cookie 实现 Session 跟踪的。第一次创建 Session 时，服务端会通过在 HTTP 协议中反馈到客户端，需要在 Cookie 中记录一个 Session ID，以便今后每次请求时都可分辨你是谁。有人问，如果客户端的浏览器禁用了 Cookie 怎么办？建议使用 URL 重写技术进行会话跟踪，即每次 HTTP 交互，URL 后面都被附加上诸如 sid=xxxxx 的参数，以便服务端依此识别用户。


> 摘录于 https://ruby-china.org/topics/33313