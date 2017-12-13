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

所以我们只要在这个路径下写 .conf 文件就可以了：`/etc/nginx/conf.d/`

查看一下这个文件

因为这个文件很多示例注释，影响阅读，所以我们建一个新的配置文件。

新建之前先备份一下这个配置文件：

> ```
> mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
> ```

新建一个配置文件代替原来的默认配置。

> ```
> touch /etc/nginx/nginx.conf
> ```

vim /etc/nginx/conf.d/default.conf

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



