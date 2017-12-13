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

在打开的文件中加入以下配置内容：

> ```
>
> ```

vim /etc/nginx/conf.d/default.conf

修改index 添加 index.php支持php![](/assets/nginx.png)

继续添加php-fpm配置

![](/assets/php-fpm.png)

```
location ~ \.php$ {
    root           html;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME /usr/share/nginx/html$fastcgi_script_name;
    include        fastcgi_params;
}
```

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



