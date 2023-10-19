## 如何将docker 镜像上传到docker hub仓库

Docker 将容器制作成镜像并上传



# 前言

#### 之前通过[docker](https://cloud.tencent.com/product/tke?from_column=20065&from=20065)搭建过各种环境，如果想要在不同的机器上搭建一样的环境，就可以将之前搭建的镜像上传到[镜像仓库](https://cloud.tencent.com/product/tcr?from_column=20065&from=20065)，这样方便在不同的机器上快速搭建同一套环境。 如果公开的话，别人也可以用你的镜像快速搭建环境，类似于 GitHub 本地代码上传到代码仓库，再从仓库拉取代码到本地。

在使用docker时候常常需要把自己配置好环境的容器制作成镜像并上传到dockerhub以便之后拉取。本篇文章就是介绍如何将docker容器制作成镜像并上传到dockerhub。

## 背景

很多docker hub上拉下来的镜像，通过修改配置文件等操作，定制成了适合自己的镜像，以后用自己的镜像就可以，因此需要上传到docker hub，以后可以像代码一样管理维护自己的docker镜像。

## 1.注册docker hub账号

访问Docker Hub官网
https://hub.docker.com/

## 2.docker hub上创建仓库

![img](./docker上传镜像.assets/1606616-20220322184846620-385055832.png)
创建成功如下图：
![img](./docker上传镜像.assets/1606616-20220322184901964-1467112222.png)

## 查看容器列表

首先是查看容器：在**命令台**中键入 `docker ps -a` 命令，得到如下界面。

![image-20231020014448189](./docker上传镜像.assets/image-20231020014448189.png)

## 从容器创建一个新镜像

接着，**dockers commit 容器名 要保存成的镜像名：版本名**（若没有 **：版本名** 则直接默认为latest）

**注：**`docker commit` 命令主要是实现从容器创建一个新镜像。

例如 `docker commit vser vs:v1`

![image-20231020014651956](./docker上传镜像.assets/image-20231020014651956.png)

## 4.将容器commit 成镜像

```xml
docker tag <existing-image> <hub-user>/<repo-name>[:<tag>]
docker commit 277e80820516 jerrymouseli/wvp_lirj:0322
```

这里的tag不指定就是latest。

![img](./docker上传镜像.assets/image-20231020022927684.png)

![image-20231020022744064](./docker上传镜像.assets/image-20231020022744064.png)

sha256是镜像文件的校验码。

## 打本地标签tag

在上传之前，先给本地镜像打个tag标签，相当于

重新复制镜像并重命名为docker账户名/仓库名称

`docker tag <existing-image> <hub-user>/<repo-name>[:<tag>]`

```javascript
docker tag 本地镜像:tag docker账号/docker仓库:tag
```

```javascript
docker tag jenkins/jenkins:lts user/Repositories:v1
docker images                                           
```

## ![image-20231020015248079](./docker上传镜像.assets/image-20231020015248079.png)

## 3.docker hub 帐号在本地验证登陆

docker 本地登录

```shell
docker login
```

![image-20231020021704074](./docker上传镜像.assets/image-20231020021704074.png)

## 5.docker push 镜像到docker hub 的仓库

上传本地镜像标签到镜像仓库，使用docker指令

```shell
docker push docker账号/仓库名称:tagname
```

```xml
docker push<hub-user>/<repo-name>:<tag>
docker push jerrymouseli/wvp_lirj:0322
```

![img](./docker上传镜像.assets/1606616-20220322184941845-1720317000.png)

## 6.验证

### 6.1 命令验证

```mipsasm
docker inspect jerrymouseli/wvp_lirj:0322
```

![image-20231020021900078](./docker上传镜像.assets/image-20231020021900078.png)

### 6.2 线上仓库验证

 上传完成后打开自己的docker hub账号，查看镜像仓库 

![img](./docker上传镜像.assets/1606616-20220322185007416-681271531.png)

# pull 拉取镜像

拉取镜像使用docker pull 你自己的镜像名称

```javascript
docker login

docker pull user/Repositories:tag
```

![image-20231020022420535](./docker上传镜像.assets/image-20231020022420535.png)

