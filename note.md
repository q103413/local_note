宝塔面板
https://8.212.47.250:8883/5013cd5b
账号:wukaa
密码:btwukaa

Yeaning
用户名: admin
密码:2Q43c325GTX35da7
默认地址:http://8.212.47.250:8000

堡垒机
http://8.212.18.15/ui/#/
maple
2IORUJuU$sK05q6e67

maple
cn-hongkong+dir-7009317511
%x5JpdW7eqDGc67fKe
Tx#CoOrT3gGjY%^Dj5

https://wiki.60889.xyz:8568/confluence/display/OPS
maple
Xnn^VUz3

值班号
0815203744
PV%3e7TK
ywzhiban@gmail.com

18.163.0.139 
root
Cx1B6$J&lHpViqwr6x

服务第一，技术第二
docker ps -a
进入容器
docker attach id 
docker exec -it 243c32535da7 /bin/bash
docker rm id

mysql
运行容器
docker run -it xxx /bin/bash
docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql

docker start <容器 ID>
docker stop <容器 ID>

yum [options] [command] [package ...]
options：可选，选项包括-h（帮助），-y（当安装过程提示选择全部为 "yes"），-q（不显示安装的过程）等等

1）lsof -i:端口号，即可查看某一端口的占用情况，
2)netstat -lntup | grep 端口号 用于查看指定端口号的进程情况，

 ps aux --sort -pmem|head

 find / -name 'tomcat7' -type d 
 find / -name 'server.xml' -print

dpkg --print-architecture
arch
unzip 
tar xvf file

SecretKey xfas6FPQ4sad8s37

参数启动 ./Yearning run --push "IP地址" -port "8000"
nohup command &

初始化成功!
用户名: admin
密码:Yearning_admin
请通过./Yearning run 运行,
默认地址:http://8.212.47.250:8000

systemctl status firewalld
firewall-cmd --state
systemctl start firewalld 
firewall-cmd --zone=public --add-port=8000/tcp --permanent 
firewall-cmd --reload 
netstat -ntlp  
netstat -ntulp |grep 8000   
systemctl stop firewalld 

sudo systemctl restart service

curl 
curl -d



find / -type f -name "*.log" | xargs grep "ERROR"
find . -name "*.log" | xargs grep "error"

find . -name "*GLIBC_2*" 

一、查看 nginx 安装目录
ps -ef | grep nginx

二、查看配置文件 nginx.conf 路径 
nginx -t
这条命令也可以用于检查配置文件是否正确。

# 从 / 根目录下查找文件名为 nginx.conf 的文件
find / -name nginx.conf

sed 's/要被取代的字串/新的字串/g' testfile
sed -n '5,10p' filename 

tail -f/n xxx.file 
route 66
let relex
relexing


1、从服务器上下载文件
scp username@servername:/path/filename /var/www/local_dir（本地目录）

scp root@192.168.0.101:/var/www/test.txt 把192.168.0.101上的/var/www/test.txt的文件下载到/var/www/local_dir（本地目录）

2、上传本地文件到服务器
scp /path/filename username@servername:/path

例如scp /var/www/test.php root@192.168.0.101:/var/www/ 把本机/var/www/目录下的test.php文件上传到192.168.0.101这台服务器上的/var/www/目录中


3、从服务器下载整个目录
scp -r username@servername:/var/www/remote_dir/（远程目录） /var/www/local_dir（本地目录）

例如:scp -r root@192.168.0.101:/var/www/test /var/www/ 

4、上传目录到服务器
scp -r local_dir username@servername:remote_dir
例如：scp -r test root@192.168.0.101:/var/www/ 把当前目录下的test目录上传到服务器的/var/www/ 目录

注：目标服务器要开启写入权限。


scp传文件指定端口
在Linux中, 两台主机传送文件的时候, 经常用到scp命令. 通常情况下, ssh的默认端口都会自定义, 介绍一下指定端口号的方法:
# scp -P port file_name user@ip:/dir_name
-P: 大写的P, 指定端口号
file_name: 指本机的文件路径, 绝对路径相对路径都可
user: 远程主机的一个可用的用户名
ip: 远程主机ip
dir_name: 远程的一个user可以写入文件的目录

实例:
# scp -P 2233 get_info.sh liemer@192.168.76.52:/usr/local/src

注意: 选项-P的位置, 尽量直接放在scp命令之后, 否则可能有错误.


 [root@localhost ~]# unzip [选项] 压缩包名


表 1 unzip 命令常用选项及含义
选项	含义
-d 目录名	将压缩文件解压到指定目录下。
-n	解压时并不覆盖已经存在的文件。
-o	解压时覆盖已经存在的文件，并且无需用户确认。
-v	查看压缩文件的详细信息，包括压缩文件中包含的文件大小、文件名以及压缩比等，但并不做解压操作。
-t	测试压缩文件有无损坏，但并不解压。
-x 文件列表	解压文件，但不包含文件列表中指定的文件。


【例 1】不论是文件压缩包，还是目录压缩包，都可以直接解压缩
unzip dir1.zip
【例 2】使用 -d 选项手动指定解压缩位置，例如：
unzip -d /tmp/ ana.zip


[root@localhost ~]# mv 【选项】 源文件 目标文件
选项：
-f：强制覆盖，如果目标文件已经存在，则不询问，直接强制覆盖；
-i：交互移动，如果目标文件已经存在，则询问用户是否覆盖（默认选项）；
-n：如果目标文件已经存在，则不会覆盖移动，而且不询问用户；
-v：显示文件或目录的移动过程；
-u：若目标文件已经存在，但两者相比，源文件更新，则会对目标文件进行升级；
【例 1】移动文件或目录。

[root@localhost ~]# mv cangls /tmp
#移动之后，源文件会被删除，类似剪切

[root@localhost ~]# mv -f cangls /tmp
#就算 /tmp/ 目录下已经存在同名的文件，由于"-f"选项的作用，所以会强制覆盖

[root@localhost ~]# mv -vn bols cangls lmls /tmp/、
"lmls"->"/tmp/lmls"
#再向 /tmp/ 目录中移动同名文件，如果使用了 "-n" 选项，则可以看到只移动了 lmls，而同名的 bols 和 cangls 并没有移动（"-v" 选项用于显示移动过程）

【例 4】改名。
如果源文件和目标文件在同一目录中，那就是改名。例如：
[root@localhost ~]# mv bols lmls
#把 bols 改名为 lmls

目录也可以按照同样的方法改名。



linux下查看端口是否开启常用命令
发布于 2019-12-18 17:01:17
10.4K0
举报
一、查看哪些端口被打开 netstat -anp

二、关闭端口号:iptables -A INPUT -p tcp --drop 端口号-j DROP

　　iptables -A OUTPUT -p tcp --dport 端口号-j DROP

三、打开端口号：iptables -A INPUT -ptcp --dport 端口号-j ACCEPT

四、以下是linux打开端口命令的使用方法。

　　nc -lp 23 &(打开23端口，即telnet)

　　netstat -an | grep 23 (查看是否打开23端口)

五、linux打开端口命令每一个打开的端口，都需要有相应的监听程序才可以


CDN开启了HTTPS，源站是否必须配置HTTPS？

总之，客户端访问CDN节点和CDN节点访问源站，是两段不同的链路。
CDN开启HTTPS对客户端访问CDN节点有效，源站配置HTTPS对CDN节点访问源站有效。
因此，CDN开启HTTPS，是由阿里云控制台中对源站信息的端口配置决定的，不强制要求源站配置HTTPS。
不过，建议CDN和源站都开启HTTPS，确保全链路的安全。



复制粘贴
进入 normal/正常模式（刚进入 vim 的默认模式），
把光标移动到开始复制的位置。
按下 v 来选择字符。（也可以用 V 来选择整行，Ctrl-v 来选择矩形块）
光标移动 到结束复制的位置。
按下 y 来复制。
光标移动到想要粘贴的位置，按下 p 粘贴。（或者 P 粘贴在当前光标位置之前）。
把 p 换成 gp 可以在粘贴完成时，把光标移动到粘贴内容结束的位置。gP 同样适用。



剪切粘贴
进入 normal 模式（刚进入 vim 的默认模式），
把 光标移动 到开始复制的位置。
按下 v 来选择字符。（也可以用 V 来选择整行，Ctrl-v 来选择矩形块）
光标移动到结束复制的位置。
按下 d 来剪切。
光标移动到想要粘贴的位置，按下 p 粘贴。（或者 P 粘贴在当前光标位置之前）。



less [参数] 文件 
[pagedown]： 向下翻动一页
[pageup]： 向上翻动一页

G - 移动到最后一行
g - 移动到第一行
Q 退出less 命令

vim跳转到指定的行




  admin.156857g.com


葡京 彩票游戏   0607
https://games.mklsijanhy.com
https://www.mklsijanhy.com

games  www
cname
aeb59c84.u.fn01.vip.
18.167.128.128:7811


https://portal.kijsnhuamn.com
https://www.kijsnhuamn.com
https://games.kijsnhuamn.com

18.167.128.128:7815
葡京 彩票游戏   对应7701业务
https://games.mklsijanhy.com/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI
https://www.mklsijanhy.com/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI


葡京 彩票游戏   对应7705业务
https://www.kijsnhuamn.com
https://games.kijsnhuamn.com




永利 彩票游戏
games-lottery   
0531
ga.weanhsgtfklm.com
www.weanhsgtfklm.com
ga  www  @
cname
aeb59c84.u.fn01.vip.
永利游戏彩票备用域名

17701
17705
17702
https://gams.chsunamksj.com/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI
https://app.chsunamksj.com/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI
https://mobile.chsunamksj.com/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI

gams    app  mobile
cname
aeb59c84.u.fn01.vip. 

16.162.73.3   17701   分组  永利游戏彩票
永利游戏彩票 非常用端口，备用地址
https://portal.chsunamksj.com:17701/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI
https://www.chsunamksj.com:17701/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI

Hai (紧急事情发语音), [6/17/2023 14:15]
16.162.73.3   17701   分组  永利游戏彩票
永利游戏彩票 非常用端口，备用地址
https://portal.chsunamksj.com:17701/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI
https://www.chsunamksj.com:17701/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI

portal    www
cname
aeb59c84.u.fn01.vip.

https://gams.bnmcjzxhus.com  
https://app.bnmcjzxhus.com
https://mobile.bnmcjzxhus.com
gams    app  mobile
cname
aeb59c84.u.fn01.vip.  
16.162.73.3:17705     分组  永利游戏彩票 

https://api.bnmcjzxhus.com
https://portal.bnmcjzxhus.com
api  portal
cname
aeb59c84.u.fn01.vip.

https://ga.weanhsgtfklm.com
https://www.weanhsgtfklm.com/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI

api.edcshuankjhs.com
api
cname
aeb59c84.u. fn01.vip.   

/etc/nginx/nginx.conf
nginx -s reload

https://api.edcshuankjhs.com

https://games.fjjfghsd.cn
aeb59c84.u.fn01.vip.

https://games.fjjfghsd.cn/mobile/index/#/betRoom?userToken=Bearer%20eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMDAwMTQiLCJ1c2VySWQiOjEwMDAxNCwidXNlck5hbWUiOiJ4NTAwN1hGQ1Bjd2VBNyIsInN1cFVzZXJJZCI6MTAwMDAwLCJleHAiOjE2ODQ1MzQ0NzF9.T4zJakWbUGITLgLEgRb3uKfNVJLo1BRLqZOW6YPas1FvCZL3TTgwoTK0MhLOQu6rYUL18FEceJUL5ec8G2wd2Mf3kkkaGTTrD_09BjwAHr92RIOII-vdciF-bjIcSkw3bUtFZssSguqyFLR6vIAv4Gd020F_vBG1G05UzTjCVU0&id=101&code=SHI_SHI_CAI






葡京彩票游戏域名信息-- http://doc.xfgjoa.com:18181/docs/game_lottery/game_lottery-1eqbedtmvtag7

永利彩票游戏域名信息-- http://doc.xfgjoa.com:18181/docs/game_lottery/game_lottery-1eqbk5a9e0h0m


https://t.me/tybetter



docker run -it --link red:redis --rm redis redis-cli -h redis -p 26379


$ docker cp redis.crt redis:/usr/local/etc/redis/

$ docker cp redis.key redis:/usr/local/etc/redis/


tls-port 6379
tls-cert-file /usr/local/etc/redis/redis.crt
tls-key-file /usr/local/etc/redis/redis.key


docker run --name redis -p 36379:6379 -v C:\work\redis\redis.conf:/etc/redis/redis.conf -v C:\work\redis:/data -d redis redis-server /etc/redis/redis.conf --appendonly yes


docker run --name redis -p 16379:6379 -v C:\work\redis\redis.conf:/etc/redis/redis.conf -v C:\work\redis\redis.crt:/etc/redis/redis.crt -v C:\work\redis\redis.key:/etc/redis/redis.key -v  C:\work\redis:/data -d redis redis-server /etc/redis/redis.conf





# 进入上诉新建的证书存放目录
cd /opt/redis/ssl
# 依次执行以下命令生成证书
openssl genrsa -out ca.key 4096
openssl req -x509 -new -nodes -sha256 -key ca.key -days 3650 -subj '/O=Redis Test/CN=Certificate Authority' -out ca.crt
openssl genrsa -out redis.key 2048
openssl req -new -sha256 -key redis.key -subj '/O=Redis Test/CN=Server' | openssl x509 -req -sha256 -CA ca.crt -CAkey ca.key -CAserial ca.txt -CAcreateserial -days 365 -out redis.crt
openssl dhparam -out redis.dh 2048





redis.conf  rootCA.key  rootCA.pem  rootCA.srl  server.csr  server.key  server.pem


/data/redistls/server.pem
/data/redistls/server.key
/data/redistls/rootCA.pem



docker run --name redistls -p 26379:6379 -v /data/redistls/redis.conf:/etc/redis/redis.conf -v /data/redistls/rootCA.pem:/etc/redis/rootCA.pem \
-v /data/redistls/server.pem:/etc/redis/server.pem -v /data/redistls/server.key:/etc/redis/server.key \
-v  /data/redistls:/data -d redis redis-server /etc/redis/redis.conf




docker run --name redistls -p 26379:6379 -v /data/redistls/redis.conf:/etc/redis/redis.conf -v /data/redistls/rootCA.pem:/etc/redis/rootCA.pem \
-v /data/redistls/server.pem:/etc/redis/server.pem -v /data/redistls/server.key:/etc/redis/server.key \
-v  /data/redistls:/data -d redis  /etc/redis/redis.conf



Either tls-ca-cert-file or tls-ca-cert-dir must be specified w

旧的
47.57.240.128

G%pZQGcsw!DwMwT7qk

C8R77Jp5L3%ru8*Pv5


echo "export LC_ALL=en_US.UTF-8"  >>  /etc/profile
echo "export LC_CTYPE=en_US.UTF-8"  >>  /etc/profile


# 设置语言环境
sudo localedef -i en_US -f UTF-8 en_US.UTF-8
# 重启宝塔面板
bt 1


# 卸载locales和语言包，重新安装，再执行locale-gen
sudo apt-get purge locales
sudo apt-get purge language-pack-en

sudo apt-get install locales
sudo apt-get install language-pack-en

sudo locale-gen en_us.utf-8



scp root@52.69.48.80:/data/redistls/rootCA.pem  ./
 把192.168.0.101上的/var/www/test.txt的文件下载到/var/www/local_dir（本地目录）



redis-cli --tls --cacert /c/work/redis/ssl/rootCA.pem --cert /c/work/redis/ssl/server.pem --key /c/work/redis/ssl/server.key

redis-cli --tls --cacert /data/redistls/rootCA.pem --cert /data/redistls/server.pem --key /data/redistls/server.key

/c/work/redis/ssl



Connection: Disconnect on error: SSL Error: Openssl is missing. Please install Openssl (OpenSSL 1.1.1g  21 Apr 2020)



export PATH=$PATH:/usr/local/jdk-11.0.1/bin:/data/node-v14.21.3-linux-x64/bin:/usr/local/maven-3.8.6/bin




find ./ -name "*.conf" | xargs grep "10881"


jenkins密码
admin
6678c4f808ac49a



npm cache clear --force
rm -rf node_modules
rm -rf  package-lock.json
npm install --force
node -v
npm -v
pwd
cd ./OpenIM-Admin-account
npm install --force
npm run build


cd ./OpenIM-Electron-ToC
npm install --force
npm run build




npm cache clear --force
rm -rf node_modules
rm -rf  package-lock.json
cd ./OpenIM-Electron-ToC
npm install --force
npm run build

npm cache clear --force
rm -rf node_modules
rm -rf  package-lock.json
npm install --force
cd ./OpenIM-Admin-account
npm install --force
npm run build


/var/jenkins_home/workspace/OpenIM-Electron-ToC/OpenIM-Electron-ToC



npm cache clear --force
rm -rf node_modules
rm -rf  package-lock.json
cd ./OpenIM-Admin-account
npm install --force
npm run build


pwd
npm cache clear --force
rm -rf node_modules
rm -rf  package-lock.json
cd ./OpenIM-Electron-ToC
pwd
npm install --force
npm run build:main


/var/jenkins_home/workspace/OpenIM-Electron-ToC/OpenIM-Admin-account/dist

npm cache clear --force
rm -rf node_modules


npm cache clear --force
rm -rf node_modules
rm -rf  package-lock.json
cd ./OpenIM-Admin-account
npm install --force
npm run build


cd /data/jenkins_home/workspace/testtoc/OpenIM-Electron-ToC




ssh -t -t root@52.69.48.80 "cp -rf /data/testadmin/dist /data/testadmin/backfile/testadmin_`date +%F_%H:%M:%S`"
rsync -avz --delete --exclude 'public/*' --exclude 'runtime/*' --exclude '.env' ./. root@13.215.58.44:/data/testadmin
ssh -t -t root@52.69.48.80 "chown -R nginx:nginx /data/testadmin/dist"



ssh -t -t root@47.57.13.206 "cp -rf /data/front/testadmin /data/front/backfile/admin_`date +%F_%H:%M:%S`"

ssh -t -t root@47.57.13.206 "cp -rf /data/front/testadmin /data/front/backfile/admin_`date +%F_%H:%M:%S`"
scp -r dist  root@47.57.13.206:/data/front/testadmin

rsync -avz --delete  ./dist/. root@47.57.13.206:/data/front/testadmin

ssh -t -t root@47.57.13.206 "chown -R nginx:nginx /data/front/testadmin"



cd ./OpenIM-Admin-account
npm run build

47.57.13.206


ssh-copy-id root@目标节点IP（需要输入对应服务器密码）
ssh-copy-id root@47.57.13.206 


docker exec -it xxx /bin/bash


ssh-copy-id -i ~/.ssh/id_rsa.pub remote-host

ssh-copy-id root@47.57.13.206 


ssh-keygen
 ssh-copy-id root@47.57.13.206 

gTXUdvrj5Q$DUVrPTx

ssh 47.57.13.206 


scp ./1.log  root@47.57.13.206:/data/front/testadmin



ssh -t -t root@47.57.13.206 "mv /data/front/testadmin /data/front/backfile/admin_`date +%F_%H:%M:%S`"
scp -r dist root@47.57.13.206:/data/front/testadmin
ssh -t -t root@47.57.13.206 "chown -R nginx:nginx /data/front/testadmin"
ssh -t -t root@47.57.13.206 "cd /data/front & ls"





cd ./OpenIM-Admin-account
npm run build
ssh -t -t root@47.57.13.206 "mv /data/front/admin /data/front/backfile/admin_`date +%F_%H:%M:%S`"
scp -r dist root@47.57.13.206:/data/front/admin


cd ./OpenIM-Electron-ToC
npm run build:renderer
ssh -t -t root@47.57.13.206 "mv /data/front/pc /data/front/backfile/pc_`date +%F_%H:%M:%S`"
scp -r build root@47.57.13.206:/data/front/pc





mysql -h127.0.0.1 -P3306 -usuvdata -p0buGzN5fq8VUibFtl0

find . -name "*.conf" | xargs grep "9901"
find / -type f -name "*.conf" | xargs grep "54.65.207.85"




cd ./OpenIM-Admin-account
npm run build
ssh -t -t root@47.57.13.206 "mv /data/front/admin /data/front/backfile/admin_`date +%F_%H:%M:%S`"
scp -r dist root@47.57.13.206:/data/front/admin



pujing-cluster-server-1-1


47.57.137.252

fG1Vgp6UZ5lIOMjvTbU5zcelHM

i-j6cbg2ptljvb1y1z5q6a


1gwe7eh2fDsN9X1

172.16.0.246

https://admin.wanshmjikl.com




http://8.212.0.111:11008  


https://api.dhsujkainbl.com/complete_admin/admin/init/get_client_config
https://api.dhsujkainbl.com/complete_admin/admin/init/set_client_config




pujing-open-im-c-front-1-1

8.212.10.119
ucF3jkMTgoMR7HNyDDUqTMSWSe

https://portal.fgzxkk.com
亚洲云海05

portal.fgzxkk.com
portal
cname
f42a34db.u.fn01.vip.


yunwei 123456


wy@5090442127606325.onaliyun.com
NQC#W^PUGnJVc!IiiW3V&ERKTN



永利iom搭建

j6cbg2ptljvb1y1z5q6a


https://qsjielkdinsjkl.com/videoGame/VerifySession



测试iom-Jenkins修改项目名


mlsjuanhgybf.com
miskiajnhyg.com


将DNS服务器修改为：ns1.dns.com  ns2.dns.com  


location /chatjs/ {
    alias  /data/front/chatjs/;
}


api.usjamnhgbn.com
api.ksnhajhgs.com

cname

8c303f3a.u.fn01.vip.



2023-07-07  晚班检测报告1：

1、鑫博、葡京直播检测
  鑫博4个直播账号检测，每个账号 推流和拉流域名正常，站内信暂无异常提醒
  葡京3个直播账号检测，每个账号检测 腾讯云国内jiaozi811@126.com账号 播放域名   portal.senessbz.com 昨晚被封，已加新域名。其他账号正常。
  没有欠费。

2、OPEN-IM检测
  OPEN-IM鑫博 使用pc登陆 发消息和图片验证，正常使用。
  OPEN-IM葡京 使用pc登陆 发消息和图片验证，正常使用。

3、鑫博、葡京站点访问检测：
  鑫博站点使用H5域名登陆检测，登陆正常，api域名正常。
  葡京站点使用H5域名登陆检测，登陆正常，api域名正常。





2023-07-07  晚班检测报告2：

1、鑫博、葡京直播检测
  鑫博4个直播账号检测，域名正常，无异常提醒
  葡京3个直播账号检测，域名正常，无异常提醒
  没有欠费。

2、OPEN-IM检测
  OPEN-IM鑫博 使用pc登陆 发消息和图片验证，正常使用。
  OPEN-IM葡京 使用pc登陆 发消息和图片验证，正常使用。

3、鑫博、葡京站点访问检测：
  鑫博站点使用H5域名登陆检测，登陆正常，api域名正常。
  葡京站点使用H5域名登陆检测，登陆正常，api域名正常。


http://124.71.182.151:8000/admin/#/admin/domain/domainsiteinfo/


good.brrencdnaomsecan.com

47.243.241.27





2023-07-09  晚班检测报告2：

1、鑫博、葡京直播检测
  鑫博4个直播账号检测，域名正常，无异常提醒
  葡京3个直播账号检测，域名正常，无异常提醒
  没有欠费。

2、OPEN-IM检测
  OPEN-IM鑫博 使用pc登陆 发消息和图片验证，正常使用。
  OPEN-IM葡京 使用pc登陆 发消息和图片验证，正常使用。

3、鑫博、葡京站点访问检测：
  鑫博站点使用H5域名登陆检测，登陆正常，api域名正常。
  葡京站点使用H5域名登陆检测，登陆正常，api域名正常。


另一些事情
一切都搭建好以后，你会发现你给gmail，qq，163发邮件都能收到，唯独outlook被退信，这是因为你的IP不在outlook邮件服务的白名单中，你需要向他们提供你的IP及相关信息，我这里没有提供，故不作演示




账号 yzm@bbtx888.xyz
密码 85lw@7H5nv

SMTP  
mail.bbtx888.xyz 


端口&加密端口
25,587


yzm@bbtx888.xyz

ywzhiban@gmail.com


admin.bskiejnsmlaj.com

smtp://yzm@bbtx888.xyz:85lw@7H5nv@mail.bbtx888.xyz:25/备注22222

13.213.234.171


ehlo mail.bbtx888.xyz 
mail from: yzm@bbtx888.xyz
rcpt to: ywzhiban@gmail.com
Data
subject: testsmtp
testsmtptestsmtptestsmtp
.


find ./ -name "*.conf" | xargs grep "13008"



512387616




2023-07-10  晚班检测报告：

1、鑫博、葡京直播检测
  鑫博4个直播账号检测，域名正常，无异常提醒
  葡京3个直播账号检测，域名正常，无异常提醒
  没有欠费。

2、OPEN-IM检测
  OPEN-IM鑫博 使用pc登陆 发消息和图片验证，正常使用。
  OPEN-IM葡京 使用pc登陆 发消息和图片验证，正常使用。

3、鑫博、葡京站点访问检测：
  鑫博站点使用H5域名登陆检测，登陆正常，api域名正常。
  葡京站点使用H5域名登陆检测，登陆正常，api域名正常。
