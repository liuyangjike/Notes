## 定义
>Nginx是一款轻量级的HTTP服务器, 采用事件驱动的异步非阻塞处理方式框架这让其具有极好的IO性能，时常用于服务端的反向代理和负载均衡.

## 配置nginx 

找到nginx.conf文件或者nginx.conf.default文件(一般在/etc/nginx)
```md
user nginx; # 运行时的用户,可以不设置
worker_processes auto; # nginx进程,一般设置为与cpu核数一样多
error_log /var/log/nginx/error.log warn; # 可以不写
pid /run/nginx.pid; # 进程pid存放位置
events {
    worker_connections 768; # 单个后台进程的最大并发量
}
http{
    include /etc/nginx/mime.types; # 文件扩展名与类型映射表
    default_type application/octet-stream; # 默认文件类型
    access_log /var/log/nginx/access.log;  #访问日志
    error_log /var/log/nginx/error.log; # 错误日志
    sendfile on; # 开启高效传输模式
    keepalive_timeout 65; # 超时时间
    gzip on; # 开启gzip压缩
    
    # .. 剩下的server在下面讲解
}

```
## 静态页面服务器
```javascript
server{
    listen  8080; # 监听端口,就是访问的端口
    server_name localhost; #配置域名,没有就localhost(其实就是外部访问的:当外部访问域名时就匹配服务server, 或者外部时ip+port, 就直接匹配到listen监听的端口)
    location / {
        root home/demo; // 静态网页放的文件夹
        index test.html test.htm; #静态网页文件
        allow 45.76.202.231;允许这个IP,禁止其他
        deny all;
    }
    error_page 500 502 503 504 /error.html # 错误状态码显示页面
    location /error.html{
        root /home/common/ # 错误error.html所在的文件夹
    }
}
``` 
上面http://35.221.241.100:8080/ 其实访问服务器/home/demo/test.html
## 虚拟主机
它把一台服务器主机分成一台台“虚拟”的主机，每台虚拟主机都可以具有独立的域名
### 例子
1.基于域名虚拟主机
```javascript 

server {  
       listen       80;  
       server_name  a.com; 
       #charset koi8-r;  
       #access_log  logs/host.access.log  main;  
       location / {  
           root   html-a;  
           index  index.html index.htm;  
       }  
    }   
server {  
       listen       80;  
       server_name  b.com; (有时候要加www.) 
       #charset koi8-r;  
       #access_log  logs/host.access.log  main;  
       location / {  
           root   html-b;  
           index index.html index.htm;  
       }  
    }  
```
访问a.com, 访问b.com 分别到不同的文件
2. 基于IP虚拟主机
```javascript 

server {  
       listen       80;  
       server_name  1.12.323.1;
       #charset koi8-r;  
       #access_log  logs/host.access.log  main;  
       location / {  
           root   html-a;  
           index  index.html index.htm;  
       }  
    }   
server {  
       listen       80;  
       server_name  3.3.41.23; 
       #charset koi8-r;  
       #access_log  logs/host.access.log  main;  
       location / {  
           root   html-b;  
           index index.html index.htm;  
       }  
    }  
```
访问1.12.323.1和3.3.41.23分别显示不同网站
3. 基于端口虚拟主机
```javascript 

server {  
       listen       8002;  
       server_name  35.221.231.100;
       #charset koi8-r;  
       #access_log  logs/host.access.log  main;  
       location / {  
           root   html-a;  
           index  index.html index.htm;  
       }  
    }   
server {  
       listen       8001;  
       server_name  35.221.231.100; 
       #charset koi8-r;  
       #access_log  logs/host.access.log  main;  
       location / {  
           root   html-b;  
           index index.html index.htm;  
       }  
    }  
```
访问35.221.231.100:8081 和35.221.231.100:8081 两个端口，可分别跳转到两个不同的index页面.
## 反向代理
```
server{
        listen 80;
        server_name nginx2.jspang.com;
        location /v1 {
               proxy_pass http://cangdu.org:8001;
        }
}
```
把含有`/v1`请求代理到http://cangdu.org:8001;
还可以配置
```
proxy_set_header :在将客户端请求发送给后端服务器之前，更改来自客户端的请求头信息。

proxy_connect_timeout:配置Nginx与后端代理服务器尝试建立连接的超时时间。

proxy_read_timeout : 配置Nginx向后端服务器组发出read请求后，等待相应的超时时间。
proxy_send_timeout：配置Nginx向后端服务器组发出write请求后，等待相应的超时时间。
proxy_redirect :用于修改后端服务器返回的响应头中的Location和Refresh。
```
## 操作Nginx服务
### 启动
> systemctl start nginx.service

### 查看
> ps aux | grep nginx

### 停止(几种)
> 1. nginx -s stop
> 2. nginx -s quit
> 3. killall nginx

### 重启
> systemctl restart nginx.service

### 重新载入配置文件
> nginx -s reload
