


docker run -i -t -d --name bt -p 2000:20 -p 2100:21 -p 8000:80 -p 4430:443 -p 8880:888 -p 8888:8888 --privileged=true -v /data/baota:/www/wwwroot ubuntu

docker run -i -t -d --name newbt -p 2000:20 -p 2100:21 -p 8000:80 -p 4430:443 -p 8880:888 -p 8888:8888 -p 20182:20182 --privileged=true -v /data/baota:/www/wwwroot bt1


Congratulations! Installed successfully!
========================面板账户登录信息==========================

 外网面板地址: http://120.78.137.40:20182/04229fe4
 内网面板地址: http://:20182/04229fe4
 username: xagbas2a
 password: eeec55b5
 
=========================打开面板前请看===========================

 【云服务器】请在安全组放行 20182 端口
 因默认启用自签证书https加密访问，浏览器将提示不安全
 点击【高级】-【继续访问】或【接受风险并继续】访问
 教程：https://www.bt.cn/bbs/thread-117246-1-1.html

==================================================================
Time consumed: 4 Minute!


shopxo
数据库账号资料

数据库名：ds_ai5200_com

用户：ds_ai5200_com

密码：JSZYrBWYYw

访问站点：http://ds.ai5200.com/index.php


