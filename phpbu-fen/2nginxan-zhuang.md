#### Nginx安装

> ```bash
> rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
> yum install nginx
> ```

#### Nginx配置

Nginx的默认配置文件可以通过以下命令来查找：

> ```
> nginx -t
> ```

该命令会测试当前的配置文件，并输出配置文件目录。如下图![](/assets/nginx-t.png)我返回的配置文件目录在 : `/etc/nginx/nginx.conf`

查看一下这个文件：

> ```
> vim /etc/nginx/nginx.conf
> ```

发现文件末尾引入了其他配置文件，

![](/assets/nginx-conf-view.png)

所以我们只要在这个路径下写 .conf 结尾的文件就可以了：`/etc/nginx/conf.d/`

查看一下这个文件夹，里面就一个default.conf

因为这个文件很多示例注释，影响阅读，所以我们建一个新的配置文件。

新建之前先备份一下这个配置文件：

> ```
> mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.bak
> ```

新建一个配置文件代替原来的默认配置，并打开编辑。

> ```
> touch /etc/nginx/conf.d/default.conf
> vim /etc/nginx/conf.d/default.conf
> ```

在打开的文件中加入以下配置内容\(按 a 或 i 进入插入模式\)：

> ```
> server {
>     listen       80;
>     server_name  localhost;
>     location / {
>         root   /usr/share/nginx/html;
>         # 修改index 添加 index.php支持php
>         index  index.php index.html index.htm;
>     }
>     error_page   500 502 503 504  /50x.html;
>     location = /50x.html {
>         root   /usr/share/nginx/html;
>     }
>
>     # 添加php-fpm配置
>     location ~ \.php$ {
>         root html;
>         fastcgi_pass 127.0.0.1:9000;
>         fastcgi_index index.php;
>         fastcgi_param SCRIPT_FILENAME /usr/share/nginx/html$fastcgi_script_name;
>         include fastcgi_params;
>     }
>
>     # 拦截地址转发到直播项目的tomcat（具体看项目需求）
>     location /zhibo/ {
>         proxy_pass http://127.0.0.1:8080/zhibo/;
>         proxy_set_header Host $host;
>         proxy_set_header X-Real-IP $remote_addr;
>         proxy_set_header REMOTE-HOST $remote_addr;
>         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
>     }
> }
> ```

vim 保存并退出。

> ```
> :wq
> ```



进入nginx网站根路径一般为/usr/share/nginx/html修改目录权限

> ```
> chorm -R nginx ./
> ```

这样我需要的Nginx环境就配好了，接下来启动Nginx就好了。

#### Nginx基本命令

* 启动

> ```
> nginx
> ```

* 停止

> ```
> nginx -s stop
> ```

* Nginx配置修改后重启

> ```
> nginx -s reload
> nginx -s reopen
> ```



