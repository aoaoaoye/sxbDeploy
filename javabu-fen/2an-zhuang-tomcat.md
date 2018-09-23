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
1、找到 tomcat 发布目录，默认是 IDE 帮你配置的，如 eclipse 中默认发布目录是一个 w...的一个临时目录，把发布目录改成 tomcat 安装目录下的 webapps。注意，eclipse 中发布目录的信息会被 Servers 里的配置冲掉，所以配置需要在 eclipse 中的 Servers 进行。

2、找到 tomcat 安装目录，在 webapps 的兄弟节点创建一个文件夹，命名为 boweiImg

3、在文件路径：  tomcat 安装目录 / conf / server.xml 下，找到并修改 server.xml
在 <Server></Server> 标签下 添加一个新的<Service></Service> 标签，内容如下：

<Service name="imgService">
                <!--分配8081端口 -->
                <Connector URIEncoding="UTF-8" connectionTimeout="20000" port="8081" protocol="HTTP/1.1" redirectPort="8443"/>
                <Engine defaultHost="localhost" name="imgService">
                        <!--name为项目访问地址 此配置的访问为http://localhost:8081 appBase配置tomcat下wabapps下的路径-->
                        <Host appBase="/home/im/Project/mofangweb/tomcat/webapps" autoDeploy="true" name="localhost" unpackWARs="true" xmlNamespaceAware="false" xmlValidation="false">
                                <!--资源地址-->
                                <Context debug="0" docBase="/home/im/Project/mofangweb/tomcat/boweiImg" path="" reloadable="false"/>
                        </Host>
                </Engine>
        </Service>

注：
红色字体 ：是你的 tomcat 发布目录
绿色字体 ：是你的图片服务器根地址，也就是刚刚 步骤2 建的 boweiImg

```



