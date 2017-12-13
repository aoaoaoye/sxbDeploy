#### PHP安装

逐行执行以下命令，碰见需要安装的都是按 y（yes）安装。

> ```
> yum install epel-release
> rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
> yum install --enablerepo=remi --enablerepo=remi-php56 php php-opcache php-devel php-mbstring php-mcrypt php-mysqlnd php-phpunit-PHPUnit php-pecl-xdebug php-pecl-xhprof
> yum install  --enablerepo=remi --enablerepo=remi-php56 php-fpm
> ```

#### 修改php-fpm的用户和用户组

> ```
> vim /etc/php-fpm.d/www.conf
> ```

找到下面两行，用户和组都改成 nginx：

#### 启动php-fpm

> ```
> systemctl start php-fpm
> ```



