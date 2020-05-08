 1.  Linux系统安装OpenVPN Access Server

我们将演示两种常用的Linux系统发行版体系，即  CentOS/RHEL  和  Ubuntu  的安装。当然OpenVPN还支持其他类型的Linux发行版，需要的话可以查看其官方手册。

在安装OpenVPN AS之前，需要在系统安装一些工具：

# yum install net-tools wget             //CentOS/RHEL
# sudo apt-get install net-tools wget    //Ubuntu
由于OpenVPN要求服务端和客户端要严格同步，否则会出现认证失败的问题，所以我们还需要在服务器上安装Ntp软件包：

# yum install ntp             //CentOS/RHEL
$ sudo apt-get install ntp    //Ubuntu
安装完成后，就可以从OpenVPN的官方网站下载服务器软件包了：

# wget https://openvpn.net/downloads/openvpn-as-latest-CentOS7.x86_64.rpm     //CentOS/RHEL
$ wget https://openvpn.net/downloads/openvpn-as-latest-ubuntu18.amd_64.deb    //Ubuntu
如果使用了其他版本的系统，可自行下载对应的软件包。下载成功后，就可以使用如下命令安装OpenVPN AS：

# rpm -Uvh openvpn-as-latest-CentOS7.x86_64.rpm         //CentOS/RHEL
# sudo dpkg -i openvpn-as-latest-ubuntu18.amd_64.deb    //Ubuntu
