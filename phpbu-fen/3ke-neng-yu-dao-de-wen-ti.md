#### 可能遇到的问题



访问php的时候可能出现404的错误，如果保证ng和php配置都是对的，那很可能是php-fpm没有权限读取文件

请先查看php-fpm和nginx的用户

> ps aux \|grep nginx
>
> ps aux \|grep php-fpm



![](/assets/userNg.png)



![](/assets/fpmUser.png)



这个是我已经修改好的，都为nginx，修改方式如下

#### Nginx

> vim /etc/nginx/nginx.conf

修改第一行user 为nginx



#### php-fpm

> vim /etc/php-fpm.d/[www.conf](https://link.jianshu.com/?t=http://www.conf)

修改user 和 group 为nginx

然后进入nginx网站根路径一般为/usr/share/nginx/html修改目录权限

> chorm -R nginx ./



然后重启nginx和php-fpm即可



