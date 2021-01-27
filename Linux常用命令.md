# Linux常用命令
----
##### 查看所有进程
```
ps aux 
```

查看公网ip
```
curl ifconfig.me 
```
##### 在 Linux上 安装 Docker
	Docker 的 安装资源文件 存放在Amazon S3，会间歇性连接失败。所以安装Docker的时候，会比较慢。你可以通过执行下面的命令，高速安装Docker。

```
curl -sSL https://get.daocloud.io/docker | sh
```

##### 卸载Docker
```
sudo apt-get remove docker docker-engine
```

`	卸载Docker后,/var/lib/docker/目录下会保留原Docker的镜像,网络,存储卷等文件. 如果需要全新安装Docker,需要删除/var/lib/docker/目录`

rm -fr /var/lib/docker/

##### 查看Linux系统版本信息
```
cat /proc/version
lsb_release -a 
cat /etc/issue
```

##### Google cloud shell启动命令
```
gcloud alpha  cloud-shell ssh
```

##### docker快速搭建可道云（kodexplorer）私有云网盘
```
docker run -d -p 8080:80 --name kodexplorer -v /home/brokenstone2012/html:/var/www/html xaljer/kodexplorer
```

##### docker快速搭建SSR
###### SSR镜像①
```
docker run -d --name ssr -p 22:21618 -e PASSWORD=a588188 oldiy/ssr-docker

# 配置参数

ENV SERVER_ADDR 0.0.0.0
ENV SERVER_PORT 21618
ENV PASSWORD oldiy
ENV METHOD rc4-md5
ENV PROTOCOL auth_sha1_v4
ENV OBFS tls1.2_ticket_auth
ENV TIMEOUT 300
EXPOSE $SERVER_PORT/tcp
EXPOSE $SERVER_PORT/udp
```
###### SSR镜像②
```
docker ponycool/shadowsocksr-3.1.2:1.0

# 启动容器

docker run -d \
--name ssr \
-p 30000:528 \
-e PASSWORD=pwd \
-e METHOD=aes-256-cfb \
-e PROTOCOL=origin \
-e OBFS=plain \
ponycool/shadowsocksr-3.1.2:1.0 
```
###### SSR镜像③
```
docker run -p 2333:2333 -v /path/to/your/configuration/file.json:/etc/shadowsocks/configuration.json -d thnuiwelr/ssr-docker -v -c /etc/shadowsocks/configuration.json 
```
##### 解决raw.githubusercontent.com 无法访问的问题
	在 www.ipaddress.com 查询 raw.githubusercontent.com 的真实IP。
	修改/etc/hosts文件快速生效   
```
vim /etc/hosts
199.232.96.133 raw.githubusercontent.com
/etc/init.d/networking restart
```

##### 通过docker ps 查看当前启动的容器
```
docker kill <容器ID或容器名> :直接关闭容器
docker rm <容器ID或容器名>   :销毁容器
```

##### 利用docker快速部署v2ray一键脚本
	（基于官方docker版）适合centos、ubuntu、debian等
```
bash <(curl -L -s https://raw.githubusercontent.com/Baiyuetribe/ss-panel-v3-mod_Uim/docker/v2ray.sh)
```

	手动安装：(适合熟悉docker的人)
	使用docker命令（不熟悉docker的，请使用一键脚本）：
```
docker run -d --name v2ray --restart always --network host jrohy/v2ray    #安装程序
docker exec v2ray bash -c "v2ray info"  #查看配置信息
```

	默认创建mkcp + 随机一种伪装头配置文件(如果使用xray则换成镜像jrohy/xray)：
```
docker run -d --name v2ray --privileged --restart always --network host jrohy/v2ray
```
	自定义v2ray配置文件:
```
docker run -d --name v2ray --privileged -v /home/ubuntu/config.json:/etc/v2ray/config.json --restart always --network host jrohy/v2ray
```