#### Nginx安装

> ```bash
> rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
> yum install nginx
> ```

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

#### Nginx配置

Nginx的默认配置文件可以通过以下命令来获取：



> vim /etc/nginx/conf.d/default.conf

修改index 添加 index.php支持php![](/assets/nginx.png)

继续添加php-fpm配置

![](/assets/php-fpm.png)

location ~ .php$ {

```
                   root           html;



   fastcgi\\_pass   127.0.0.1:9000;



   fastcgi\\_index  index.php;



  fastcgi\\_param SCRIPT\\_FILENAME /usr/share/nginx/html$fastcgi\\_script\\_name;



   include        fastcgi\\_params;



}
```



