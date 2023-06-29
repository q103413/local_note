

# 1.jenkins信息

jenkins访问：http://8.212.47.250:19898/

账号：admin

密码：6678c4f808ac49a

## 2.jenkins服务

### 启动jenkins服务

```shell
docker start jenkins
```

#### 启动docker容器

 设置端口为19898并映射`jenkins_home`到宿主机`/home/jenkins_home`。

```shell
[root@baota-1 jenkins_home]# docker run -d --name jenkins -p 19898:8080 -v /data/jenkins_home:/var/jenkins_home jenkins
```

# 3.jekins目录

挂载目录 /data/jenkins_home/

容器目录  /var/jenkins_home/

# 4.服务器

 jenkins                8.212.47.250 
