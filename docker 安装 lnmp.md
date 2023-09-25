docker 安装 lnmp

## 拉取镜像

```
search php

docker pull php:latest

docker images
```



## 构建容器

```
$ docker run --name  myphp-fpm -v ~/nginx/www:/www  -d  php:5.6-fpm
```

命令说明：

--name myphp-fpm : 将容器命名为 myphp-fpm。

-v ~/nginx/www:/www : 将主机中项目的目录 www 挂载到容器的 /www

```
docker run --name  myphp-fpm -v C:\work\www:/www  -d php

 docker run --name centos-bt -v C:\work\www:/www -d centos
```



## 启动容器

docker start <容器 ID>
docker stop <容器 ID>

## 进入容器

docker ps -a
进入容器
docker attach id 
docker exec -it 5bf6ae8373e6 /bin/bash
docker rm id

## 修改容器端口

1.提交一个运行中的容器为镜像

```shell
docker commit [containerid] [new_imagename]
```

2.运行新建的镜像并添加端口映射

```shell
docker run -d -p 8000:80  [imagename] /bin/sh
docker run -d -p 8000:80  centosbt /bin/sh
docker run --name centos-bt2 -v C:\work\www:/www -d centosbt
```



Congratulations! Installed successfully!
========================面板账户登录信息==========================

 外网面板地址: https://47.242.38.67:21991/10f321f2
 内网面板地址: https://172.17.0.2:21991/10f321f2
 username: s9q5sumw
 password: e63d8b48

=========================打开面板前请看===========================

 【云服务器】请在安全组放行 21991 端口
 因默认启用自签证书https加密访问，浏览器将提示不安全
 点击【高级】-【继续访问】或【接受风险并继续】访问
 教程：https://www.bt.cn/bbs/thread-117246-1-1.html



外网面板地址:  https://47.242.38.67:21991/10f321f2
内网面板地址:  https://172.17.0.2:21991/10f321f2
username: s9q5sumw
password: e63d8b48
If you cannot access the panel,
release the following panel port [21991] in the security group
若无法访问面板，请检查防火墙/安全组是否有放行面板[21991]端口
注意：初始密码仅在首次登录面板前能正确获取，其它时间请通过 bt 5 命令修改密码



| 项目名称 |     服务器名称     |                     ip                     |                       pc 18080                        |                  admin 18081                   |                       api 18082                        |                           h5 18083                           |
| :------: | :----------------: | :----------------------------------------: | :---------------------------------------------------: | :--------------------------------------------: | :----------------------------------------------------: | :----------------------------------------------------------: |
| 色站测试 |  sz-dj-java-test   |                52.69.48.80                 |        pc.vwebsdke.com web.terzdmweq.com 自建         |   admin.vwebsdke.com admin.terzdmweq.com自建   |       api.vwebsdke.com portal.terzdmweq.com 自建       |           h5.vwebsdke.com phone.terzdmweq.com自建            |
| ELK服务  | sz-test-aws-bg-elk | 18.182.255.29(弹性IP)172.31.46.130(内网IP) | 基本配置：4cpu 16GiB 云盘：200GiB 系统：Amazon Linux2 | 安全组开放端口： 22、9200、9600、5601、 4560。 | 主要服务：Logstash、 Elasticsearch、Kibana 版本：7.8.0 | 配置文件主目录： /data/elk/ 服务器用户名：root 密码：2UkUHIuTzu?N+EH&4BSFTlgrIu |

