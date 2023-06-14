
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
