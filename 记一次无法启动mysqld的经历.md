**问题**<br/>
欲启动mysqld，执行`systemctl start mysqld`，报错`mysqld:Unit not found。`<br/>
**思路**<br/>
以前碰到这个错时是没有安装`mysql-server`，这次是明显安装了（首先要确定有没有装mysql-server），根据提示使用`systemctl status` 和`journalctl -xe`都看不出错来。<br/>
最后在`/var/log/mysqld.log`中发现错误是因为没有找到`/var/run/mysqld`这个路径，创建mysqld这个文件夹后，然后修改文件夹权限`chmod 777 /var/run/mysqld`就可以成功启动服务。<br/>
**总结**<br/>
1.要解决问题，首先要知道错误是什么。服务器运行一个服务（进程），一般都会有记录的日志文件，在文件中可找到错误记录；<br/> 
2.这个日志文件的存放路径一般是记录在该项服务的配置文件conf里；<br/>
3.一项服务在运行时一般要在run/下建立一个他的套接字文件，比如这次的`/var/run/mysqld/mysqld.sock`，所以检查mysqld等服务是否有在运行时，可查看xx.sock是否存在。
