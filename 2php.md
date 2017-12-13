#### PHP项目

进入nginx项目路径

> ```
> cd /usr/share/nginx/html
> ```

使用git clone 将项目clone到路径下：

> ```
> git clone https://git.coding.net/youchuanneikujun/zhibo-php.git
> ```

然后会要求你输入账号密码，这是coding上面的项目。输完会检出。

把检出的php项目名字改成zhibo，因为java代码那边调用的路径是zhibo。

> ```
> mv zhibo-php zhibo
> ```

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



