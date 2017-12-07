#### Nginx安装

* rpm -ivh nginx-release-centos-6-0.el6.ngx.noarch.rpm

* yum install nginx

#### 启动Nginx

* systemctl start nginx

#### Nginx配置

* 进入nginx配置文件

> vim /etc/nginx/conf.d/default.conf

修改index 添加 index.php支持php![](/assets/nginx.png)

继续添加php-fpm配置

![](/assets/php-fpm.png)

> location ~ \.php$ {
>
>                            root           html;
>
>            fastcgi\_pass   127.0.0.1:9000;
>
>            fastcgi\_index  index.php;
>
>           fastcgi\_param SCRIPT\_FILENAME /usr/share/nginx/html$fastcgi\_script\_name;
>
>            include        fastcgi\_params;
>
>         }



