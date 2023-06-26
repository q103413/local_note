

1.jenkins部署信息

jenkins访问：http://8.212.47.250:19898/

账号：admin

密码：6678c4f808ac49a

2.docker

#### 启动jenkins

 设置端口为9090并映射`jenkins_home`到宿主机`/home/jenkins_home`。

```shell
[root@baota-1 jenkins_home]# docker run -d --name jenkins -p 19898:8080 -v /data/jenkins_home:/var/jenkins_home jenkins
```

 可以通过`docker ps`查看运行的容器。

3.jekins目录

挂载目录 /data/jenkins_home/

容器目录  /var/jenkins_home/