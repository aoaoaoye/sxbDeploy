#### PHP项目

进入nginx项目路径

> ```
> cd /usr/share/nginx/html
> ```

使用git clone 将项目clone到路径下，并指定项目名为zhibo，因为java代码那边调用的路径是zhibo。

> ```
> git clone https://git.coding.net/youchuanneikujun/zhibo-php.git zhibo
> ```

然后会要求你输入账号密码，这是coding上面的项目。输完会检出。

检出完成以后需要改一下这些文件的拥有者为nginx，不然Nginx没有权限访问。

> ```
> chown -R nginx ./
> ```

这样就好了，不需要额外操作，只要Nginx跑着就能用了，因为它不需要编译。

#### 验证是否运行成功

浏览器访问：

> ```
> http://youhost/zhibo/index.php
> ```

这里zhibo是上面php项目检出的时候改过的目录zhibo。

浏览器访问这个项目的index.php会返回如下信息，说明运行成功了。

> ```
> {
>     "errorCode": 10001,
>     "errorInfo": "Invalid request."
> }
> ```

#### 需要注意的地方

这个php项目代码实际对外服务是9000端口，由Nginx进行转发，

而目前连接的数据库是远程的数据库，所以要保证服务器安全组里面开放了9000端口，允许9000端口跟外部通讯。

另外php有连接数据库的配置代码，需要修改一下数据配置，使其连接到自己的后台。



根据部署环境不同，php代码中

model/Account.php 有个创建临时文件的命令会有差异：

centos环境下：

```
$cmd = 'mktemp -t -p ' . DEPS_PATH . '/sig sxb_sig.XXXXXXXXXX';
```

debian环境下：

```
$cmd = 'mktemp -t -p ' . DEPS_PATH . '/sig/sxb_sig.XXXXXXXXXX';
```

空格换成斜杠。

这个代码不对会导致需要创建的sig临时文件生成失败，登录不进去。



上面代码改完，确认nginx有权限访问php项目，然后手机APP端注册一个账户。

注册后在 t\_account 表会生成一个用户，id 是直接用手机号的。



因为这个直播房间发信令的账户是sl805，这个账户一开始是不存在的。所以我们把这个注册的id改成 sl805，手机号名字都改成sl805。然后密码默认是注册时候的密码。这时候通过前端登录一次sl805 这个账户，会自动刷新 user\_sig ，这样sl805的账户就建成了。

