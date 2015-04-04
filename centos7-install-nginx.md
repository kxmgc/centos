#安装Nginx 在 CentOS 7
##关于Nginx
Nginx的是一款高性能的Web服务器软件。
##先决条件
###步骤 1—添加 Nginx源[资源库]
要添加的CentOS7 Nginx的yum软件库，打开SSH终端，并使用下面的命令：
`sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm`
###步骤 2—安装 Nginx
现在，Nginx的资源库已安装在服务器上，使用以下yum command安装Nginx的：
`sudo yum install nginx`
当你回答Y，Nginx的将完成安装虚拟专用服务器（VPS）上。
###步骤 3—开启 Nginx
Nginx的不会自动启动。为了让Nginx的运行，键入：
`sudo systemctl start nginx.service`
你可以访问你的服务器的公网IP地址，在网络浏览器（请参阅下标题下的说明）：
`http://server_domain_name_or_IP/`
您将看到默认的CentOS7 Nginx的网页，其中有用于提供信息和测试目的。它应该是这个样子：

CentOS 7 Nginx Default

如果您看到这个页面，那么你的Web服务器现在可以正确安装。 

在继续之前，你可能会想要启用Nginx的系统引导时启动。要做到这一点，请输入以下命令：

sudo systemctl enable nginx.service
恭喜您！Nginx的现在已经安装并正在运行！

如何找到你的服务器的公网IP地址



您可以运行下面的命令来显示服务器的公网IP地址：

ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
服务器的根目录和配置
如果你想开始担任自己的网页或应用程序是如何通过Nginx的，你会想知道Nginx的配置文件和默认的服务器根目录的位置在哪里吧，请随着Cantgis看如下操作。

默认的服务器根目录


 默认的服务器根目录是/usr/share/nginx/html.

这个位置是默认的服务器模块配置文件中指定附带的Nginx，它位于

/etc/nginx/conf.d/default.conf.

服务器模块配置


任何额外的服务器模块（称为Apache中的虚拟主机）通过创建新的配置文件在这里：

 /etc/nginx/conf.d. 

当Nginx的启动与.conf 文件在该目录最终文件将被加载。

Nginx的全局配置


主要Nginx的配置文件位于

 /etc/nginx/nginx.conf. 

也可以改变进程数，在扩大机器负载.