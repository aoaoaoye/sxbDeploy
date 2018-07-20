#### java项目

注意：Java项目需要在PHP之前部署运行，因为里面有数据库建表的操作，需要Java项目去做。

本地IDEA打包，点击Build-&gt;Build Artifacts![](/assets/build.png)

在项目路径classes-&gt;artifacts下可以找到这个war包

然后使用SCP将项目上传到tomcat/webapp下：

> ```
> scp /Users/im/Projects/zhibohoutai/classes/artifacts/bikex_war/bikex_war.war root@47.52.46.100:/opt/tomcat7/webapps/zhibo.war
> ```

这里服务器IP改成你要上传的服务器IP，然后输入密码即可上传。

上传成功以后启动tomcat，war包会自动打开。

启动tomcat：

> ```
> sh /opt/tomcat7/bin/startup.sh
> ```



# 经过测试，使用zip包部署也可以。war部署我莫名报错，zip包再解压部署就可以正常运行。



