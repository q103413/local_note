## docker环境维护常用操作-高阶版

## Docker的一些批量脚本（全停，全删，清理，导出）

停止所有docker实例

删除所有docker 实例

删除TAG 为none的镜像（经常被覆盖或打断的无用镜像）

导出指定格式开头的镜像

## 停止所有docker实例（慎用） 

要停止所有的Docker实例，您可以使用以下命令：

```shell
docker stop $(docker ps -aq)
```

这个命令会列出所有正在运行的Docker容器的ID，并将它们传递给`docker stop`命令来停止这些容器。请注意，您需要在具有足够权限的终端或命令行界面中运行这个命令，以确保您可以停止容器。

## 删除所有docker 实例（慎用）

要删除所有Docker实例（容器），您可以使用以下命令：

```shell
docker rm -f $(docker ps -aq)
```

这个命令将停止并删除所有正在运行的Docker容器。 `-f` 选项用于强制删除正在运行的容器。`docker ps -aq` 命令会列出所有容器的ID，然后将它们传递给 `docker rm` 命令来删除它们。

请注意，删除容器将导致其数据和状态的丢失。确保在执行此操作之前，已经备份了重要的数据。同样，您需要在具有足够权限的终端或命令行界面中运行此命令。

## 删除镜像

```shell
## 没有打标签
docker rmi [-f] $(docker images -q | awk '/^<none>/ { print $3 }')

## 镜像名包含关键字
docker rmi --force [-f] $(docker images | grep redis| awk '{print $3}')

## 删除虚悬镜像
docker rmi $(docker images -q -f dangling=true)
```

## docker none镜像说明

有效的 none 镜像
Docker文件系统的组成，docker镜像是由很多 layers组成的，每个 layer之间有父子关系，所有的docker文件系统层默认都存储在/var/lib/docker/graph目录下，docker称之为图层数据库。

最后做一个总结< none>:< none> 镜像是一种中间镜像，我们可以使用docker images -a来看到，他们不会造成硬盘空间占用的问题（因为这是镜像的父层，必须存在的），但是会给我们的判断带来迷

## 删除TAG 为none的镜像（经常被覆盖或打断的无用镜像**无效的 none 镜像**）

要删除所有标签（TAG）为"none"的Docker镜像，您可以使用以下命令：

另一种类型的 < none>:< none> 镜像是dangling images ，这种类型会造成磁盘空间占用问题。
像Java和Golang这种编程语言都有一个内存区，这个内存区不会关联任何的代码。这些语言的垃圾回收系统优先回收这块区域的空间，将他返回给堆内存，所以这块内存区对于之后的内存分配是有用的
docker的悬挂(dangling)文件系统与上面的原理类似，他是没有被使用到的并且不会关联任何镜像，因此我们需要一种机制去清理这些悬空镜像。
我们在上文已经提到了有效的< none>镜像，他们是一种中间层，那无效的< none>镜像又是怎么出现的？这些 dangling镜像主要是我们触发 docker build 和 docker pull命令产生的。

使用下面的命令可以清理

```shell
docker rmi $(docker images -f "dangling=true" -q)
```

这个命令会列出所有"悬挂"（dangling）的镜像，即没有标签的镜像，然后将它们传递给 `docker rmi` 命令来删除它们。

请注意，删除镜像将永久丢失这些镜像和它们的数据。确保在执行此操作之前，已经备份了重要的镜像和数据。同样，您需要在具有足够权限的终端或命令行界面中运行此命令。

## 删除所有的none镜像（慎用）会删除**有效的 none 镜像**

```shell
docker images | grep none | awk '{print $3}' | xargs docker rmi
```



## 导出指定格式开头的镜像

要导出镜像名称以"chenmins/suda"开头的Docker镜像，可以使用以下命令：

```shell
docker save -o chenmins_suda_images.tar $(docker images "chenmins/suda*" -q)
```

这个命令将会保存所有镜像名称以"chenmins/suda"开头的镜像为一个名为 "chenmins_suda_images.tar" 的文件。`docker images "chenmins/suda*" -q` 会列出所有匹配的镜像的ID，然后 `docker save` 命令将这些镜像保存到指定的 tar 文件中。

请确保您在执行此操作之前已经备份了重要的镜像和数据。同样，您需要在具有足够权限的终端或命令行界面中运行此命令。

# 检查Docker镜像-容器的磁盘空间

检查 Docker 磁盘空间使用情况

## 镜像、容器、本地volumes占用了多少空间的基本的Docker方法：

```shell
docker system df
# 运行此命令获得按 Docker 组件分组的所有磁盘使用信息。

```

![image-20231101180845950](./docker实战维护-进阶版.assets/image-20231101180845950.png)


```
docker system df -v
```

## 查看 Docker 镜像及其大小：

```
docker image ls
```

它列出了系统上的所有 Docker 镜像，展示了一些详细信息，包括大小：

```shell
docker image ls

Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
REPOSITORY TAG IMAGE ID CREATED SIZE
docker.io/library/nginx latest 2b7d6430f78d 7 days ago 146 MB
```



## 检查正在运行的容器大小

想知道正在运行的 Docker 容器的大小，可以使用 docker ps 命令：

```
docker ps --size
```



## 查看 SIZE 列：

```shell
docker ps --size

Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES SIZE
8900fc2086b3 docker.io/library/nginx:latest nginx -g daemon o... 14 seconds ago Up 14 seconds ago 0
```



## docker镜像的获取-查看-删除-docker镜像管理-docker容器管理

docker镜像的获取、查看、删除、docker镜像管理、docker容器管理



## 一、docker镜像的获取、查看、删除

## 获取镜像

\# 查看docker镜像存储位置

```shell
[root@localhost ~]# docker info|grep Root
Docker Root Dir: /var/lib/docker
[root@localhost ~]# ls /var/lib/docker/image/overlay2/imagedb/content/sha256/ -l
```

总用量 32
-rw-------. 1 root root 2142 1月 3 13:28 5d0da3dc976460b72c77d94c8a1ad043720b0416bfc16c52c45d4847e53fadb6
-rw-------. 1 root root 7656 12月 29 22:36 605c77e624ddb75e6110f997c58876baa13f8754486b461117934b24a9dc3a85
-rw-------. 1 root root 7700 1月 3 11:16 7614ae9453d1d87e740a2056257a6de7135c84037c367e1fffa92ae922784631
-rw-------. 1 root root 2794 1月 3 13:24 afb6fca791e071c66276202f8efca5ce3d3dc4fb218bcddff1bc565d981ddd1e
-rw-------. 1 root root 1462 1月 3 13:22 ba6acccedd2923aee4c2acc6a23780b14ed4b8a5fa4e14e252a23b846df9b6c1
-rw-------. 1 root root 1866 1月 4 14:45 d9e50bf288963ff3a78d1decfcd1deda5acd15a0e3094c9e4b317cf8299bd465
\# 打开任意文件，里面记录的是镜像和容器之间的配置关系，以json的形式存储

```shell
[root@localhost ~]# cat /var/lib/docker/image/overlay2/imagedb/content/sha256/5d0da3dc976460b72c77d94c8a1ad043720b0416bfc16c52c45d4847e53fadb6
```



## # 查找镜像，选择点赞数最多的pull

```
docker search centos
```



## # 获取镜像

```
docker pull centos
```



## # 使用不同镜像生成容器

```
\# -t 开启一个交互终端，--rm 容器退出时删除该容器，容器名后面不指定版本默认运行最新的
docker run -it --rm centos bash
\# 在运行一个7.8版本的
docker run -it --rm centos:7.8.2003 bash
```



## 查看镜像

```shell
# 查看全部镜像
docker images
# 查看具体镜像
docker images nginx

# 格式化显示镜像 -- format是docker的模板语言，{{}}中首字母大写其余字母小写
[root@localhost ~]# docker images --format "{{.ID}}---{{.Repository}}"
605c77e624dd---nginx
7614ae9453d1---redis
\# 表格形式显示信息
[root@localhost ~]# docker images --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"
```



## 删除镜像

```
docker rmi 镜像名/镜像id
```



## 删除容器

```
docker rm 容器id
docker rm 指定id的前三位也行
```



## 二、镜像管理

批量删除镜像慎用

```
docker rmi `docker images -aq`
```

批量删除容器慎用

```
docker rm `docker ps -aq`
```

导出镜像命令

```
docker image save centos:7.8.2003 > /opt/centos7.8.2003.tgz
```

导入命令

```
docker image load -i /opt/centos7.8.2003.tgz
```

查看docker服务的详细信息

```
docker info
```

查看docker镜像的详细信息

```
docker image inspacet 镜像id
```



## 三、容器管理

docker run 镜像名，如果镜像不存在本地，则会在线去下载该镜像

注意：容器内进程必须处于前台运行状态，否则容器就会直接退出

自己部署一个容器运行，命令不得后台运行，前台运行即可。
如果容器内什么事都没做，容器也会挂掉，容器内必须有一个进程在前台运行。

我们运行基础镜像，没有运行任何程序，因此容器挂掉了

\# 显示所有状态的容器

```
docker ps -a
```

\# 1、运行一个挂掉的容器（从错误演示开始）,这个写法会产生多个独立的容器记录，且容器内没有程序在跑所以挂了。

```shell
docker run centos:7.8.2003
```

\# 2、运行容器，且进入容器内，且在容器内执行某个命令

```tex
[root@localhost ~]# docker run -it centos:7.8.2003 sh
sh-4.2#
sh-4.2# cat /etc/redhat-release
CentOS Linux release 7.8.2003 (Core)
```

\# 3、开启一个容器，让他帮你运行某个程序，属于前台运行，会卡住一个终端

```
[root@localhost ~]# docker run centos:7.8.2003 ping baidu.com
PING baidu.com (110.242.68.66) 56(84) bytes of data.
64 bytes from 110.242.68.66 (110.242.68.66): icmp_seq=1 ttl=127 time=30.4 ms
```

\# 4、运行一个活着的容器，docker ps可以看到的容器
\# -d 参数，让容器在后台运行（针对宿主机而言）
\# 会返回一个容器id
\# 后面是你需要执行的操作，保证当前容器不会挂掉

```
[root@localhost ~]#docker run -d centos:7.8.2003 ping www.baidu.com
487a71fc0d91245b93525ed45f6a5f8e8bf72c14150a2c35ad1e98bb0e905b9c
```

\# 5、丰富docker运行参数
\# -d 后台运行
\# --rm 容器挂掉后自动会删除，也就是停止容器后即使通过`docker ps -a`也无法查到该容器是否运行过
\# --name 给容器起个名字

```
[root@localhost ~]# docker run -d --rm --name baidu centos:7.8.2003 ping www.baidu.com
8adc4e96dc7e374c1d8bd337719d3e9aa374d7baa155593e9164bba2c360251c
```

\# 6、查看容器日志，刷新日志

```
docker logs -f 容器id
```

\# 查看最新的五条日志

```
docker logs 容器id | tail -5
```

\# 7、进入正在运行的容器内部，并进行交互操作（bash）

```
docker exec -it 容器id bash
```

\# 查看容器内进程

```
ps -ef
```

\# 8、查看容器的详细信息，用于高级调试

```
docker container inspect 容器id
```

\# 9、容器的端口映射
\# -p 宿主机端口：容器内运行的端口
\# -d 后台运行
\# --name 容器名称

```
docker run -d --name nginx_80 -p 80:80 nginx
```

\# 9.1、查看端口的映射情况

```
[root@localhost ~]# docker port 容器id
80/tcp -> 0.0.0.0:80
80/tcp -> :::80
```

\# 9.2、随机端都映射，一般不用
\# -P 会随机应以一个宿主机的空闲端口

```
docker run -d --name nginx_random -P nginx
```

\# 10、容器的提交
\# 运行基础的centos:7.8.2003,在容器内安装vim，然后提交新的镜像
\# 新的镜像再运行出的容器，默认就携带vim
[root@localhost ~]# docker run -it --name cenost centos:7.8.2003 bash
[root@c2cd263e5a38 /]# vim
bash: vim: command not found
[root@c2cd263e5a38 /]# yum install vim
\# 安装完成以后退出容器，查看容器id进行打包
docker ps -a
\# docker commit 容器id 新的镜像名称

```
[root@localhost ~]# docker commit b50aa98a6cc7 cemtos-vim-7.8.2003
sha256:33380b6e852a9fd41eef03a2e43ab63755aab50b849413a72e85e374c7403be8
```

\# 查看生成的新镜像

```
[root@localhost ~]# docker images
REPOSITORY TAG IMAGE ID CREATED SIZE
cemtos-vim-7.8.2003 latest 33380b6e852a 4 minutes ago 452MB
```

\# 运行新镜像，查看vim的情况，可以运行ok

```
[root@localhost ~]# docker run -it cemtos-vim-7.8.2003 bash
[root@4d41883b08ff /]# vim hahah.txt
[root@4d41883b08ff /]# cat hahah.txt
dao ci jieshu xiexie!!!
[root@4d41883b08ff /]#
```

\# 11、本地镜像导出、导入
\# 导出镜像命令

```
docker image save centos:7.8.2003 > /opt/centos7.8.2003.tgz
```

\# 导入命令

```
docker image load -i /opt/centos7.8.2003.tgz
```


