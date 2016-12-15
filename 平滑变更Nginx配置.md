平滑变更 Nginx 配置
-------------------
>* 修改Nginx配置文件后的较验命令.( nginx默认路径：/usr/local/nginx/conf/nginx.conf 一般是在这个文件中包含自定义配置的文件路径)
<pre>
   /usr/local/nginx/sbin/nginx -t
</pre>
>* 平滑重启：
<pre>
   对于Nginx 0.8.x 及以上版本,执行命令:  /usr/local/nginx/sbin/nginx -s reload
</pre>
