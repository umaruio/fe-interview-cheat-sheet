# Web & Browser 篇

##### https 是几次握手？

几次握手和是 https 还是 http 关系不大。因为都是基于 TCP 的所以都是三次握手。

##### https 的原理

https，顾名思义，是使用了 SSL 的 HTTP 连接，它的目的是为了保证传输过程中的数据安全。  
这里有一篇非常好的文章：[http://www.jianshu.com/p/650ad90bf563](http://www.jianshu.com/p/650ad90bf563)  
简单来说，https 首先使用非对称加密，由服务器提供公钥，由客户端提供随机算子，确认双方互信。如果达成互信，再使用客户端生成的随机算子进行对称加密传输。（非对称加密的开销太大）

##### http 是几次握手？

基于 TCP ，都是三次握手。

##### TSL 的中文名是什么？它处在网络结构的哪一层？

TSL - Transport Layer Security - 传输层安全协议。  
显而易见，属于传输层。

##### SSL 与 TSL 的关系是什么？

SSL（Secure Sockets Layer）是 TSL 的前身，是一种安全协议，目的是为互联网通信，提供安全及数据完整性保障。

##### SSL/TLS 的原理是什么？

[https://segmentfault.com/a/1190000002554673](https://segmentfault.com/a/1190000002554673)

##### SSL 3.0 和 TSL 1.0 的关系

从技术上讲，TLS 1.0与SSL 3.0的差异非常微小。但TLS 还是在安全性上进行了一些改进。  
另外，TLS 从 1.2 开始删除了对 SSL 的兼容，以避免安全问题。

##### 负载均衡的方法

* 使用 DNS 进行负载均衡（将请求解析到不同的 IP 地址上）
* 使用代理服务器进行请求转发，分担服务器压力。（这种方案用户必须指定代理服务器）
* 使用 ATG \(Address Translation Gateway\)，将一个公网 IP 映射到多个内网 IP 。
* 使用 HTTP 的重定向进行负载均衡。
* 使用 NAT（Network Address Translation）进行地址转换。
* 使用反向代理（比如 Nginx）。

##### DNS 负载均衡的原理

请求不同的 DNS Server 会获得不同的 IP 地址，借此访问不同的服务器资源。

##### DNS 是基于 TCP 的还是 UDP 的？

DNS 同时占用 TCP 和 UDP 的 53 端口。几乎所有的 DNS 请求都会使用 UDP，但是如果 Response 过长（超过 512 字节），DNS 会先通过 UDP 发送一个 Response 并将 TC 删节标志位置为 1 ，以请求使用 TCP 重新发送 Response 。

##### Nginx 负载均衡的原理

* 访问不同 URL 的负载均衡：使用 `proxy_pass` 将不同的 URL 代理到不同的 Server 上。
* 访问同一 URL 的负载均衡：定义 `upstream` 和权重，将请求**均衡的**代理到不同的 Server 上。

##### 正向代理和反向代理的区别

正向代理是指用户通过 VPN 等手段连接到代理服务器，再通过代理服务器访问网络。此时，用户能清晰的感知到自己在使用代理。  
反向代理是用户直接访问代理服务器（对于用户来说就是一个普通的网络请求），代理服务器自动作为中间节点请求目标资源，并转发给用户。此时，用户并不知道自己在使用代理。

正向代理通常用于让防火墙内的局域网用户访问墙外资源，反向代理通常用于将防火墙内的服务提供给墙外用户。同时，反向代理还经常被用于负载均衡，或提供缓存服务。

##### 浏览器是怎么加载页面的

首先加载 HTML 文档，然后**严格按照 HTML 文档的顺序**进行资源加载 / DOM 渲染，除非遇到 `defer` ，`async` 这样的延迟标签。

##### Script 脚本阻塞的解决方法

使用 `defer` 和 `async` 异步加载不重要的脚本。

##### defer 和 async 的区别

参考这个回答：[https://segmentfault.com/q/1010000000640869](https://segmentfault.com/q/1010000000640869)

* `<script src="script.js"></script>`：没有 `defer` 或 `async`，浏览器会立即加载并执行指定的脚本，“立即”指的是在渲染该 `script` 标签之下的文档元素之前，也就是说不等待后续载入的文档元素，读到就加载并执行。
* `<script async src="script.js"></script>`：有 `async`，加载和渲染后续文档元素的过程将和 script.js 的加载与执行**并行进行**（异步）。
* `<script defer src="script.js"></script>`：有 `defer`，加载后续文档元素的过程将和 script.js 的加载并行进行（异步），但是 **script.js 的执行**要在所有元素解析完成之后，`DOMContentLoaded` 事件触发之前完成。
  区别显而易见：都是异步加载，但是 `defer` 的执行要等到 DOM 渲染完成之后。

##### Socket.io 解决了什么问题，什么情况下用得到？

说实话没用过 Socket.io 但是用过 WebSocket，可以强答一发：  
Socket.io 对 ws ，轮询等实时通信的方式进行了封装，提供了一套稳定可靠的前端即时通信方案。

##### 计算机网络的五层结构与七层结构

###### 五层结构

物理层  
数据链路层  
网络层：IP  
运输层：TCP、UDP  
应用层：HTTP、FTP

###### 七层结构（OSI：Open System Interconnect 开放系统互连参考模型）

物理层  
数据链路层  
网络层：IP  
传输层：TCP、UDP  
会话层：SQL、RPC  
表示层：GIF、JPEG、MPEG  
应用层：WWW、FTP、HTTP

##### 多线程和多进程的区别

先聊聊线程与进程的区别：  
**进程**：进程代表着 CPU 所处理的单个任务。任一时刻，单个 CPU 核心只运行一个进程，进程有独立的内存空间。  
**线程**：一个进程可以包含多个线程，执行任务的不同或相同模块，线程可以共享进程的内存。  
从通信角度来讲，由于线程可以共享相同的内存空间，所以可以使用内存进行直接通信。而 RPC 要依赖于 Socket 进行通信。  
为了避免线程同时访问相同的内存地址空间，Linux 引入了 Mutex Lock 和 Semaphore 机制协调多线程。（这是个坑，最好查查资料）  
多进程就是允许多个进程“同时”执行，多线程就是允许多个线程同时执行。从实际角度考虑，硬件平台通常会对多线程进行优化，所以使用多线程比使用多进程的效率会更高一些。  
（欢迎补充！）

##### HTTP 的状态与状态码有哪些

列举一些常用的：

###### 1XX 消息

* ###### 2XX 成功
* 200 OK

###### 3XX 重定向

* 301 Moved Permanently
* 302 Move Temporarily
* 304 Not Modified
* 305 Use Proxy
* 307 Temporary Redirect

###### 4XX 请求错误

* 400 Bad Request
* 401 Unauthorized
* 402 Payment Required
* 403 Forbidden
* 404 Not Found
* 405 Method Not Allowed
* 406 Not Acceptable - 请求的资源的内容特性无法满足请求头中的条件，因而无法生成响应实体。
* 407 Proxy Authentication Required - 与401响应类似，只不过客户端必须在代理服务器上进行身份验证。
* 408 Request Timeout

###### 5XX/6XX 服务器错误

* 500 Internal Server Error
* 502 Bad Gateway - 作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到无效的响应。
* 503 Service Unavailable - 由于临时的服务器维护或者过载，服务器当前无法处理请求。
* 600 Unparseable Response Headers - 源站没有返回响应头部，只返回实体内容。

##### CDN 的用法

这个题，没办法回答。自己配置 CDN 服务器的话，不太现实，最好的办法就是直接购买现成的 CDN 服务。

##### XSS 与 CSRF 的防范

要想回答这个问题，首先要搞明白什么是 XSS ，什么是 CSRF。  
**XSS**：Cross Site Scripting 跨站脚本攻击 - 通常是利用浏览器的 `<input>` 等接收用户输入的标签，将自己的 JS 脚本注入到网站当中。在脚本设定的条件触发时，注入的脚本便会运行。运行的脚本可以执行将用户输入发送到指定服务器等行为，以达到窃取用户信息，或者其他目的。  
**CSRF**：Cross Site Request Forgery 跨站请求伪造 - 这种攻击并不常见，它的原理大概是这样：有一个受信任的网站 A 和一个不受信任的网站 B，用户通过登陆的方式访问了网站 A 并且将授权凭据存入了 Cookie ，同时用户访问网站 B，B 会隐藏地请求网站 A。根据 Cookie 的机制，浏览器请求 A 时会自动带上 A 的 Cookie ，这样 B 就可以伪装成用户私下进行一些危险操作，比如利用用户在 A 的网银进行转账。  
了解了这两个概念之后，谈谈如何防范：

###### 防范 XSS

* 限制用户输入
* 对富文本中包含的 HTML Tag 进行转义。
* 对 URL 进行编码：`encodeURIComponent`

###### 防范 CSRF

* 使用 POST 方法发送表单，并在表单中加入 hash ，保证表单来源可靠。服务器验证 hash 是否正确。
* 使用一次性令牌机制（One-Time Tokens）。

##### 输入一个 URL 后发生了什么？

[http://www.zyy1217.com/2017/03/01/从点击到呈现 — 详解一次HTTP请求/](http://www.zyy1217.com/2017/03/01/从点击到呈现 — 详解一次HTTP请求/)

##### 如何实现 Web 缓存机制？

当浏览器向服务器请求资源时，HTTP Response Header 中会包含一些有关缓存的信息。

* Cache-Control：通过向 `Cache-Control` 指定一个生命周期（`max-age`），可以通知浏览器在有效生命周期内不重复请求该资源。\(例如：`Cache-Control: max-age=604800`\) 还可以通过 `private` 和 `public` 控制是否允许代理服务器缓存资源。
* Expires：使用 `Expires` 指定缓存具体的过期日期。如果它与 `Cache-Control` 冲突，`Cache-Control` 会覆盖 `Expires` 。
* Last-Modified 和 ETag（Entity Tag）：`Last-Modified` 表示被请求资源在服务器端的上次修改时间；`ETag` 是一个唯一的文件标识符，每次文件修改都会生成新的 `ETag` ，服务器通过这两个字段通知浏览器其获取的资源版本。不过这种缓存更新机制通常要等用户主动执行刷新时，客户端请求 `If-Modified-Since` 或 `If-None-Match` 字段才有效。当客户端发送的字段内容与服务器相符时，会返回 `304 Not Modified` 。
  配置好这些信息，就能实现有效的缓存管理了。

##### 服务器端更新脚本，如何保证客户端不受缓存机制影响，实时更新脚本？

1. 使用 Webpack 为生成的脚本文件名添加 Hash 强制浏览器刷新。
2. 利用好 Web 缓存机制，使用诸如 `last-modified` 等字段控制缓存刷新。

##### HTTP 有几种请求方法，option 请求方法的作用是什么？

HTTP 总共用 16 种请求方法，常用的有以下几种：

* GET
* POST
* PUT
* DELETE
* OPTIONS

###### GET/POST 和 PUT/DELETE 的区别

PUT/DELETE 使用 URI 明确制定了请求资源的位置，GET/POST 只是访问特定接口，实际操作的资源是由服务器指定的。举个例子：PUT [http://example.com/resources/test.txt](http://example.com/resources/test.txt) 即是把 text.txt 放置在 example 这个网站的 resources 文件夹下。

###### OPTIONS 的作用

OPTIONS 方法是用于请求获得由Request-URI 标识的资源在请求/响应的通信过程中可以使用的功能选项。通过这个方法，客户端可以在采取具体资源请求之前，决定对该资源采取何种必要措施，或者了解服务器的性能。  
对 OPTIONS 最常见的是在跨域情况下，通过 OPTIONS 提交预检请求（preflight）以确定请求的资源是否允许跨域访问。

##### HTTP 有哪些与缓存有关的状态码？

* 200\(from cache\) 直接从本地缓存获取资源
* 304 Not Modified 先请求服务器，确定资源是否更新，如果没有则直接使用本地资源。

##### GET 和 POST 的区别

从语义上来说，GET 是用来获取信息的，POST 是用来发送信息的。  
从形式上来说，GET 请求的数据会附在 URL 之后，所以其长度受 URL 长度限制。POST 则是把提交的数据包裹在 HTTP Request Body 中，理论上没有限制。同时，由于 POST 不直接展示请求数据，安全性高于 GET 。

##### WebSocket 的实现机制和工作原理

Websocket 基于 Socket 实现（这是废话）。WS 利用 HTTP 协议与服务器建立连接（仅限于建立连接），通知服务器要建立的连接为 WS 类型，此后使用 WebSocket 协议与服务器建立**长连接**。WS 使用推送机制，由事件驱动实现双向通信，避免了轮询造成的巨大开销。

##### 跨域是什么？前端如何解决跨域？

这个问题几乎是前端必考题。跨域源于浏览器的同源策略限制：浏览器不允许在 `a.example.com` 下动态请求 `b.example.com` 或者 `a.example.com:8080` 或者 `exampleB.com` 的资源。即：一级域名、二级域名、端口有一个不同，都属于跨域行为。同时，跨域状态下，浏览器默认会限制 HTTP Request 发送 Cookie 中的凭据信息。

前端解决跨域的方法不多，早期的 Chrome 允许在启动时添加启动参数关闭浏览器的同源策略，新的 Chrome 可以借助 CORS 插件代理同域请求到跨域接口。  
除了这些开发层面上的解决方案，实际编码中，常用的解决方案有以下两个：CORS（Cross-Origin Resource Sharin） 和 JSONP 。  
CORS 不做过多解读，JSONP 的原理是利用 `<script>` 标签允许跨域资源请求的漏洞实现的，它使用 `<script>` 发送跨域请求，并使用一个 callback 参数将请求信息传递给服务器，服务器返回一个 JS 脚本包含我们指定的 callback 函数，然后我们执行 callback 即可获得服务器返回的内容。由于局限于 `<script>` ，所以 JSONP 只能发送 GET 请求。

除了这些，还有一些曾经常见的解决方案：利用`document.domain` 或 `window.name` 实现跨域。

关于跨域的详细内容，可以参阅这篇文章：[https://github.com/wengjq/Blog/issues/2](https://github.com/wengjq/Blog/issues/2)

