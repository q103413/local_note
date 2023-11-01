## 一张脑图整理Docker常用命令

先上图：

![Docker](./docker实战维护-基础版.assets/6lldlbgfhn.png)

## Dcoker基本概念

[Docker](https://cloud.tencent.com/product/tke?from_column=20065&from=20065) 包括三个基本概念：

-  镜像（`Image`）：Docker 镜像是一个特殊的文件系统，除了提供[容器](https://cloud.tencent.com/product/tke?from_column=20065&from=20065)运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。镜像不包含任何动态数据，其内容在构建之后也不会被改变。 
-  容器（`Container`）：镜像（`Image`）和容器（`Container`）的关系，就像是面向对象程序设计中的 `类` 和 `实例` 一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。 
-  仓库（`Repository`）：仓库（`Repository`）类似Git的远程仓库，集中存放镜像文件。 

三者关系可以用下图表示：

![Docker](./docker实战维护-基础版.assets/joa65awgh4.png)

Docker

接下来看一看Docker的常用命令。

## 服务

- 查看Docker版本信息

```javascript
docker version
```

复制

- 查看docker简要信息

```javascript
docker -v
```

复制

- 启动Docker

```javascript
systemctl start docker
```

复制

- 关闭docker

```javascript
systemctl stop docker
```

复制

- 设置开机启动

```javascript
systemctl enable docker
```

复制

- 重启docker服务

```javascript
service docker restart
```

复制

- 关闭docker服务

```javascript
service docker stop
```

复制

## 镜像

## 镜像仓库

[Docker Hub](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fhub.docker.com%2Fsearch%3Fq%3D%26type%3Dimage) 等[镜像仓库](https://cloud.tencent.com/product/tcr?from_column=20065&from=20065)上有大量的高质量的镜像可以用，可以从仓库获取镜像。

- 检索镜像

```javascript
docker search 关键字
```

复制

- 拉取镜像

```javascript
docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]
```

复制

## 镜像管理

- 列出镜像

```javascript
docker image ls
docker images
```

复制

- 删除镜像

```javascript
# 删除指定镜像
docker rmi <镜像Id>
```

复制

- 导出镜像

```javascript
# 将镜像保存为归档文件
docker save
```

复制

- 导入镜像

```javascript
docker load
```

复制

## Dockerfile构建镜像

Dockerfile 是一个文本格式的配 文件，用户可以使用 Dockerfile 来快速创建自定义的镜像。

Dockerfile 由一行行行命令语句组成，并且支持以＃开头的注释行.

### Dockerfile常见指令

下面是Dockerfile中一些常见的指令：

-  FROM：指定基础镜像 
-  RUN：执行命令 
-  COPY：复制文件 
-  ADD：更高级的复制文件 
-  CMD：容器启动命令 
-  ENV：设置环境变量 
-  EXPOSE：暴露端口 

其它的指令还有ENTRYPOINT、ARG、VOLUME、WORKDIR、USER、HEALTHCHECK、ONBUILD、LABEL等等。

以下是一个Dockerfile实例：

```javascript
FROM java:8
MAINTAINER "jinshw"<jinshw@qq.com>
ADD mapcharts-0.0.1-SNAPSHOT.jar mapcharts.jar
EXPOSE 8080
CMD java -jar mapcharts.jar
```

复制

### 镜像构建

```javascript
docker build
```

复制

### 镜像运行

镜像运行，就是新建并运行一个容器。

```javascript
docker run [镜像ID]
```

## 容器

## 容器生命周期

- 启动：启动容器有两种方式，一种是基于镜像新建一个容器并启动，另外一个是将在终止状态（stopped）的容器重新启动。

```javascript
# 新建并启动
docker run [镜像名/镜像ID]
# 启动已终止容器
docker start [容器ID]
```

复制

- 查看容器

```javascript
# 列出本机运行的容器
$ docker ps 
# 列出本机所有的容器（包括停止和运行）
$ docker ps -a
```

复制

- 停止容器

```javascript
# 停止运行的容器
docker stop [容器ID]
# 杀死容器进程
docker  kill [容器ID] 
```

复制

- 重启容器

```javascript
docker restart [容器ID] 
```

复制

- 删除容器

```javascript
docker  rm [容器ID]
```

复制

## 进入容器

进入容器有两种方式：

```javascript
# 如果从这个 stdin 中 exit，会导致容器的停止
docker attach [容器ID]
# 交互式进入容器
docker exec [容器ID]
```

复制

进入容器通常使用第二种方式，`docker exec`后面跟的常见参数如下：

－ d, --detach 在容器中后台执行命令； － i, --interactive=true I false ：打开标准输入接受用户输入命令

## 导出和导入

- 导出容器

```javascript
#导出一个已经创建的容器到一个文件
docker export [容器ID]
```

复制

- 导入容器

```javascript
# 导出的容器快照文件可以再导入为镜像
docker import [路径]
```

复制

## 其它

- 查看日志

```javascript
# 导出的容器快照文件可以再导入为镜像
docker logs [容器ID]
```

复制

这个命令有以下常用参数 -f : 跟踪日志输出

```javascript
--since :显示某个开始时间的所有日志

-t : 显示时间戳

--tail :仅列出最新N条容器日志
```

复制

- 复制文件

```javascript
# 从主机复制到容器
sudo docker cp host_path containerID:container_path 
# 从容器复制到主机
sudo docker cp containerID:container_path host_path
```



## docker

```
docker ps -a
进入容器
docker attach id 
docker exec -it 243c32535da7 /bin/bash
docker rm id
```

mysql
运行容器

```shell
docker run -it xxx /bin/bash
docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
```

docker start <容器 ID>
docker stop <容器 ID>

yum [options] [command] [package ...]
options：可选，选项包括-h（帮助），-y（当安装过程提示选择全部为 "yes"），-q（不显示安装的过程）等等

```shell
docker logs -f -t --since="2017-05-31" --tail=10 edu_web_1
```

--since : 此参数指定了输出日志开始日期，即只输出指定日期之后的日志。

-f : 查看实时日志

-t : 查看日志产生的日期

-tail=10 : 查看最后的10条日志。

edu_web_1 : 容器名称

​	

##### docker 重启所有的容器

```
docker restart $(docker ps -a -q)
```



## 日志

通过docker logs命令可以查看容器的日志。

**命令格式：**

```shell
$ docker logs [OPTIONS] CONTAINER
  Options:
        --details        显示更多的信息
    -f, --follow         跟踪实时日志
        --since string   显示自某个timestamp之后的日志，或相对时间，如42m（即42分钟）
        --tail string    从日志末尾显示多少行日志， 默认是all
    -t, --timestamps     显示时间戳
        --until string   显示自某个timestamp之前的日志，或相对时间，如42m（即42分钟）
```

**例子：**

查看指定时间后的日志，只显示最后100行：

```shell
$ docker logs -f -t --since="2018-02-08" --tail=100 CONTAINER_ID
```

查看最近30分钟的日志:

```shell
$ docker logs --since 30m CONTAINER_ID
```

查看某时间之后的日志：

```shell
$ docker logs -t --since="2018-02-08T13:23:37" CONTAINER_ID
```

查看某时间段日志：

```shell
$ docker logs -t --since="2018-02-08T13:23:37" --until "2018-02-09T12:23:37" CONTAINER_ID
```
