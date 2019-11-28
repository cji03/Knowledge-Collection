### What is Nginx

`Nginx`是一款轻量级，高性能的`http`服务器。

- 处理静态文件，索引文件以及自动索引；打开文件描述符缓冲
- 无缓存的反向代理加速，简单的负载均衡和容错
- FastCGI，简单的负载均衡和容错
- 模块化的结构，包括gzip, byte ranges, chunked responses，以及SSI-filter等filter。
- 支持SSL和TLSSNI.

简单介绍介绍前端可能会接触到的一些相关知识。

#### 正向代理

为Client端提供代理服务，使得Client可以依靠正向代理访问一些自身无法访问到的资源（梯子其实就是一种正向代理，通过它请求到资源后再返回给我们）。这种情况下对于Server端来说，它并不知道这个请求来自Client/Proxy。

#### 反向代理

相反是为Server端提供代理服务，在接收到Internet上的请求后转发给内部网络服务器，并将返回的结果返给Internet上的Client。（请求分发，负载均衡等功能）。这种情况下，Client端是不知道自己具体访问了Proxy/Server。

#### 一些小应用

##### 1. 解决跨域问题

通过Proxy访问同源之外的资源

##### 2. 请求过滤 - 访问限制

a. 根据状态码过滤请求。
b. 根据Url，精准匹配Url/ip，来判断是否允许继续访问，否则重定向或者拒绝。
c. 根据request类型来过滤。

##### 3. gzip - http压缩

使用比较广泛的功能之一。对于文本文件的压缩效果显著（CSS，JS，HTML）。
nginx自带的模块功能，可以通过相关配置打开。

```
gzip on;
gzip_vary on;
gzip_proxied any;
gzip_comp_level 4;
gzip_types text/plain text/css text/xml application/json application/javascript application/xml+rss application/atom+xml image/svg+xml;
```

开启后在api的`response headers`中可以发现`content-encoding: gzip`，表明已经开启了服务。

###### 4. 负载均衡

将requests分配到多台服务器上。相关策略：轮询，最小连接数，最快响应时间，Client Ip绑定等。

##### 5. 静态资源服务器

##### 6. 静态资源请求合并

`nginx-http-concat`淘宝写的轮子，可以将多个资源请求合并，并返回合并拼接后的资源。

##### 7. 适配PC与移动端环境

依据Client端的`userAgent`来返回不同的入口或者重定向。
