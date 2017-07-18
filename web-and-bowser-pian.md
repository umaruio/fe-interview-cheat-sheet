# Web & Browser 篇

##### https 是几次握手？

几次握手和是 https 还是 http 关系不大。因为都是基于 TCP 的所以都是三次握手。

##### https 的原理

##### http 是几次握手？

三次。

##### TSL 的中文名是什么？它处在网络结构的哪一层？

TSL - Transport Layer Security - 传输层安全协议。  
显而易见，属于传输层。

##### 负载均衡的方法

* 使用 DNS 进行负载均衡（将请求解析到不同的 IP 地址上）
* 使用 代理服务器进行请求转发，分担服务器压力。（这种方案用户必须指定代理服务器）
* 使用ATG \(Address Translation Gateway\)，将一个公网 IP 映射到多个内网 IP 。
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

##### Script 脚本阻塞的解决方法

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

###### 理论上



###### 实际上

实际角度考虑，硬件平台通常会对多线程进行优化，所以使用多线程比使用多进程的效率会更高一些。同时，虽然多进程使用 COW（Copy on Write）来提升内存性能，但是无法保证

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



