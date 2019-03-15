LAMP安装总结
===
1.安装apache
---
安装前可查看端口是否被占用：`netstat -tunlp | grep 80;`<br/>
可查看当前系统版本：`cat /etc/redhat-release;`<br/>
安装时，一般需先安装源，然后下载安装包rpm，然后`rpm -Uvh xxx.rpm;`，很可能需要带上`--force --nodeps`<br/>
安装命令：`yum install httpd -y;`<br/>
如果遇到类似php72u-common conflicts with php-common-5.4.16这样的报错，那就需要执行`yum install php72w;`来解决<br/>
安装完后，使用`systemctl start httpd.service;`，这个过程中可能会因为80端口被占用导致报错，所以需要先查看下该端口`netstat -anp |grep 端口号`,是否状态为LISTEN，如果有，可杀死该进程或通过修改httpd.conf的port。

2.安装php
---
这边以php作为httpd的一个模块进行安装为例。
首先php在此系统中的三大作用：一、配置httpd支持处理PHP请求；二、提供CGI接口和PHP解释器；三、配置支持数据库连接。
安装时同安装apache类似，参考[博客](https://yq.aliyun.com/articles/608093)
重点是安装完后是否lib64php5.so这个拓展文件，如果没有，则httpd无法支持php
有的话，则需修改httpd.conf，加入AddType 以及LoadModule php5_module modules/libphp5.so
重启httpd即可，使用phphinfo()查看是否可用，或`php xxx.php;`

3.安装mysql以及php的mysql拓展
---
首先使用`whereis mysqld`查看mysql-server是否已安装，如果有可通过`systemctl start mysqld.service;`以及查看端口3306是否被监听，来确认安装是否成功。
若没有则可安装源，下载包`yum install mysql-server;`来安装，参考[博客](https://www.cnblogs.com/julyme/p/5969626.html),php一般自带mysql.so所以在mysql安装成功后即可在php上使用。

4.redis的安装
---
需安装redis及php的redis拓展，redis的安装可使用yum，拓展的安装需使用源码安装，涉及到phpize,unzip等工具，参考[博客](https://www.cnblogs.com/eczhou/p/5588375.html)。redis的启动：`redis-server /etc/redis.conf（指定conf）;`,关闭`redis-cli shut down;`。当注释掉redis.conf里的bind 127.0.0.1时，redis将可被任何主机连接，此时需设置配置项requirepass，也可通过iptables限制访问IP。redis的备份方式有两种bgrewrite和appendonly。
