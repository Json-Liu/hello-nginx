Nginx限流配置
-------------
###配置范例
```
http {
    limit_req_zone $binary_remote_addr zone=perip:10m rate=1r/s;
    limit_req_zone $server_name zone=perserver:10m rate=10r/s;
    limit_req_log_level notice ;
    ...

    server {

        ...

        location /search/ {
            limit_req zone=perip burst=5 nodelay;
            limit_req zone=perserver burst=10;
        }
```
###范例详解
>* limit_req_zone [key] zone = [name]:[size] rate=[rate]
<pre>
    limit_req_zone  这个变量只能在HTTP中使用，limit_req_zone，用来限制请求的频率。
    limit_req_zone $binary_remote_addr zone=perip:10m rate=1r/s;
    每个IP的请求频率每秒不能超过1次且最大容量为10M.
    limit_req_zone $server_name zone=perserver:10m rate=10r/s;
    每个虚拟服务的请求频率每秒不能超过10次且最大容量为10M。
    key 表示限制的关键词 可以是 IP 或 虚拟服务
    zone的名称可以自定义，但不能重复，它代表一个存储 session 状态的容器，size 表示 容器的大小。以范例中的 perip 限制区域为例，大小为10M，按照 64-byte / session，约能存储 1.6W 个 session。
    rate 表示请求的频率，另外还有 r/m 表示每分钟的请求频率限制。
</pre>
>* limit_req zone=[name] burst=[count] nodelay
<pre>
    limit_req 这个变量可以放在 server 中 或者 location 中，放在 server 中时表示对整个服务做限流，放在 location 中表示对特定请求做限流。
    参数说明：
    zone  选择的限流容器 name 限流容器名称
    burst 缓存的数量  count 最大请求缓存数
    nodelay 表示不延迟，即如果请求缓存超过 count 的值时马上返回 503 错误。
</pre>

>* limit_req_log_level info | notice | warn | error;
<pre>
    限流日志级别 ，默认为 error。
</pre>
###备注
一般用 IP 限流就好，虚拟服务（域名）限流要慎用。
