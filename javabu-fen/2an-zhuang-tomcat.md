#### 安装tomcat

进入tomcat7下载网址

> [https://tomcat.apache.org/download-70.cgi](https://tomcat.apache.org/download-70.cgi)

复制tar.gz包的链接，然后用wget下载到服务器。

> ```
> cd /opt/
> wget http://mirror.bit.edu.cn/apache/tomcat/tomcat-7/v7.0.82/bin/apache-tomcat-7.0.82.tar.gz
> ```

解压，重命名文件夹，改成tomcat7，这样好记一点

> ```
> tar -zxvf apache-tomcat7.0.82.tar.gz
> mv apache-tomcat-7.0.82 tomcat7
> ```

根据项目创建图片服务器文件

> ```
> mkdir -p tomcat7/zhiboImg
> ```

然后还需要配置图片服务器：

```

```



