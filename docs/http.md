# http相关问题

## http缓存

http缓存分为强缓存和协商缓存。

### 强缓存

响应头中cache-control: max-age=xxx 控制缓存时间（单位为秒），在这个时间段内的资源不会重复请求服务器。

cache-control：no-store，表示不进行任何缓存，每次都要向服务器发起请求。

cache-control: public, 表示浏览器和代理服务器都可以缓存。

### 协商缓存

cache-control： no-cache，表示可以缓存，但是必须和服务器校验资源是否变化，如果没发生变化则不下载响应体。

cache-control：private，表示资源只能给当前浏览器缓存，其他代理服务器都不能缓存。

expire响应头表明缓存过期时间，通常和last-modified和etag配合使用。

last-modified响应头是GMT标准时间，表示资源最后过期时间。

etag响应头是一段哈希值，表示资源摘要。

## osi七层模型

1.物理层，比特流

2.数据链路，帧（封装上了mac地址）

3.网络层，包（路由器根据ip地址转发包）

4.传输层，段，利用端口号实现服务进程间数据传输（源端口、目标端口），分为可靠传输和不可靠传输（tcp、udp）

5.会话层

6.表示层，https，解码、编码。

7.应用层，5~7层数据统称为报文。

### tcp/ip模型

1.数据链路层

2.网络层

3.传输层

4.应用层（http协议）