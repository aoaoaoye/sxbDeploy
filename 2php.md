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

