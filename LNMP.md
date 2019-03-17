LNMP的安装，
===
  1.CGI(Common Gateway Interface)。
  ---
  
  CGI是外部应用程序（CGI程序）与Web服务器之间的接口标准，是在CGI程序和Web服务器之间传递信息的规程。CGI规范允许Web服务器执行外部程序，并将它们的输出发送给Web浏览器，CGI将Web的一组简单的静态超媒体文档变成一个完整的新的交互式媒体。
  cgi就是专门用来和web 服务器打交道的。web服务器收到用户请求，就会把请求提交给cgi程序（php的fastcgi），cgi程序根据请求提交的参数作应处理（解析php），然后输出标准的html语句返回给web服服务器，再返回给客户端，这就是普通cgi的工作原理。cgi的好处就是完全独立于任何服务器，仅仅是做为中间分子。提供接口给apache和php。他们通过cgi搭线来完成搞基动作。这样做的好处了尽量减少2个的关联，使他们2个变得更独立。
  
  2.关于php-fpm
  ---
  -PHP-FPM是一个PHP FastCGI管理器，是只用于PHP的,可以在 http://php-fpm.org/download 下载得到。  
  -PHP-FPM其实是PHP源代码的一个补丁，旨在将FastCGI进程管理整合进PHP包中。必须将它patch到你的PHP源代码中，在编译安装PHP后才可以使用。    
  -由上可知，如果服务器上已安装的php没有支持php-fpm，则需手动给php打上php-fpm的补丁（没找到解决办法），或者先将旧版php卸载然后php和php-fpm一起安装。 
  -然而百度文库里有篇介绍说：如果要使用php-fpm，则必须在安装php前打上这个补丁。
