
docker 安装 lnmp

docker search php

docker pull php:latest

docker images

$ docker run --name  myphp-fpm -v ~/nginx/www:/www  -d php:5.6-fpm
命令说明：

--name myphp-fpm : 将容器命名为 myphp-fpm。

-v ~/nginx/www:/www : 将主机中项目的目录 www 挂载到容器的 /www
docker run --name  myphp-fpm -v C:\work\www:/www  -d php