#CentOS7编译安装Nginx
##一、安装准备
>首先由于nginx的一些模块依赖一些lib库，所以在安装nginx之前，必须先安装这些lib库，这些依赖库主要有g++、gcc、openssl-devel、pcre-devel和zlib-devel 所以执行如下命令安装

```js
    $yum install gcc-c++  
    $yum install pcre pcre-devel  
    $yum install zlib zlib-devel  
    $yum install openssl openssl--devel
    //yum install gcc-c++ pcre-devel zlib-devel make openssl-devel
```
#二、安装Nginx
>检查是否已经有，如果有的话就删掉。下载，解压，编译，安装

```js
    $find -name nginx
    $yum remove nginx
    $cd /usr/local
    $wget http://nginx.org/download/nginx-1.7.8.tar.gz
    $tar -zxvf nginx-1.7.8.tar.gz
    $cd nginx-1.7.8
    ./configure --prefix=/httx/nginx --with-http\_ssl\_module
    $make
    $make install
    //make && make install
```
#三、启动
>启动服务，检测是否成功

```js
    /httx/nginx/sbin/nginx                      //启动
    ps -ef | grep nginx
    curl -s http://localhost | grep nginx.com
    /httx/nginx/sbin/nginx -s reload            //重置
    /httx/nginx/sbin/nginx -s stop              //关闭
```

#四、设置系统开机服务
>在 /etc/init.d/  目录下创建 nginx 文件

```
 scp ramhost71:/etc/init.d/nginx ~/nginx.txt
```

chkconfig --add nginx
chkconfig --level 345 nginx on
chkconfig --list nginx
启动
service nginx start
停止
service nginx stop


1. 首先配置服务脚本，建立文件 /etc/rc.d/init.d/nginx2 ， 其内容如下：
#!/bin/sh
#chkconfig: 2345 10 90
#name: nginx
#description: Nginx Service Script
#
case $1 in
    start)
                echo  "Starting Nginx..."
        /usr/local/nginx2/sbin/nginx  -c /usr/local/nginx2/conf/nginx.conf
        ;;
    stop)
        echo  "Stopping Nginx..."
        /usr/bin/killall  -s  QUIT  nginx
        ;;
    restart)
                echo  "Reloading Nginx..."
        $0  stop
        $0  start
         ;;
    *)
                echo  "Usage: $0 {start|stop|restart}"
esac
exit  0

2. 配置自启动
chkconfig --add nginx2    //加入到自启服务中
chkconfig --level 2345 nginx2 off   //调节不同系统级别启动

chkconfig --level 2345 nginx2 on    //调节不同系统级别启动

chkconfig | grep nginx2   //查看状态