## Linux常用操作11

## 服务第一，技术第二



## 查看端口和进程

1）lsof -i:端口号，即可查看某一端口的占用情况，
2)netstat -lntup | grep 端口号 用于查看指定端口号的进程情况，

```shell
 ps aux --sort -pmem|head
 find / -name 'tomcat7' -type d 
 find / -name 'server.xml' -print
```

## 后台运行

`nohup command &`

## 防火墙

```shell
systemctl status firewalld
firewall-cmd --state
systemctl start firewalld 
firewall-cmd --zone=public --add-port=8000/tcp --permanent 
firewall-cmd --reload 

netstat -ntlp  

netstat -ntulp |grep 8000  

systemctl stop firewalld 

sudo systemctl restart service
```

## 发送http请求

```shell
# 如果这里的URL指向的是一个文件或者一幅图都可以直接下载到本地
curl “http://www.baidu.com” 
wget “http://www.baidu.com”

curl -d “param1=value1&param2=value2” “http://www.baidu.com”
wget --post-data ‘param1=value1&param2=value2’ http://www.baidu.com
```

curl模拟的访问请求一般直接在控制台显示，而wget则把结果保存为一个文件。

如果结果内容比较少，需要直接看到结果可以考虑使用curl进行模拟请求，如果返回结果比较多，则可考虑wget进行模拟请求。

## 查找

```shell
find / -type f -name "*.log" | xargs grep "ERROR"
find . -name "*.log" | xargs grep "error"
```

一、查看 nginx 安装目录
ps -ef | grep nginx

二、查看配置文件 nginx.conf 路径 
`nginx -t`
这条命令也可以用于检查配置文件是否正确。

`从 / 根目录下查找文件名为 nginx.conf 的文件`

`find / -name nginx.conf`

查找当前目录下名为 file.txt 的文件：

```shell
find . -name file.txt
```

```shell
find / -name "Open-IM*"
```

## SCP文件传输

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

scp -P port file_name user@ip:/dir_name

-P: 大写的P, 指定端口号
file_name: 指本机的文件路径, 绝对路径相对路径都可
user: 远程主机的一个可用的用户名
ip: 远程主机ip
dir_name: 远程的一个user可以写入文件的目录

实例:

scp -P 2233 get_info.sh liemer@192.168.76.52:/usr/local/src

注意: 选项-P的位置, 尽量直接放在scp命令之后, 否则可能有错误.

## 解压

```shell
# unzip [选项] 压缩包名
unzip dir1.zip

# 解压到指定位置
unzip -d /tmp/ ana.zip

# 解压tar包
tar   xvf   filename
```

## 文件操作

[root@localhost ~]# mv 【选项】 源文件 目标文件
选项：
-f：强制覆盖，如果目标文件已经存在，则不询问，直接强制覆盖；
-i：交互移动，如果目标文件已经存在，则询问用户是否覆盖（默认选项）；
-n：如果目标文件已经存在，则不会覆盖移动，而且不询问用户；
-v：显示文件或目录的移动过程；
-u：若目标文件已经存在，但两者相比，源文件更新，则会对目标文件进行升级；

【例 1】移动文件或目录。

```shell
[root@localhost ~]# mv cangls /tmp
#移动之后，源文件会被删除，类似剪切

[root@localhost ~]# mv -f cangls /tmp
#就算 /tmp/ 目录下已经存在同名的文件，由于"-f"选项的作用，所以会强制覆盖

[root@localhost ~]# mv -vn bols cangls lmls /tmp/、
"lmls"->"/tmp/lmls"
#再向 /tmp/ 目录中移动同名文件，如果使用了 "-n" 选项，则可以看到只移动了 lmls，而同名的 bols 和 cangls 并没有移动（"-v" 选项用于显示移动过程）
```

【例 4】改名。
如果源文件和目标文件在同一目录中，那就是改名。例如：

```shell
[root@localhost ~]# mv bols lmls
#把 bols 改名为 lmls
```

目录也可以按照同样的方法改名。

## 重命名

**1、使用“mv”命令进行重命名**

```
mv a.txt b.txt
```

已经存在了重命名的文件了，接着想把某个文件再重命名为该文件，则会提示是否要进行重新命名已存在的文件。

```
mv -i a.txt b.txt
```

此外，“可以通过“mv”命令来对一个文件进行重命名，并把文件的后缀名进行修改。例如把“a.txt”文件重命名为“b.log”文件：

```
mv a.txt b.log
```

**2、使用“cp”命令进行重命名**

例如我们想把“a.txt”文件重命名为“b.txt”文件，

我们先使用“cp”命令将“a.txt”文件拷贝到“b.txt”文件中，具体代码如下：

```
cp a.txt b.txt
```

接着使用“rm”命令删除“a.txt”文件即可完成文件的重命名，具体代码如下：

```shell
rm a.txt
```

## CDN


CDN开启了HTTPS，源站是否必须配置HTTPS？

总之，客户端访问CDN节点和CDN节点访问源站，是两段不同的链路。
CDN开启HTTPS对客户端访问CDN节点有效，源站配置HTTPS对CDN节点访问源站有效。
因此，CDN开启HTTPS，是对源站信息的端口配置决定的，不强制要求源站配置HTTPS。
不过，建议CDN和源站都开启HTTPS，确保全链路的安全。

## Linux文本三剑客

### grep

### awk

### sed

sed 's/要被取代的字串/新的字串/g' testfile
sed -n '5,10p' filename 

## 日志

### tail

tail -f /n xxx.file 

### less

less [参数] 文件 
[pagedown]： 向下翻动一页
[pageup]： 向上翻动一页

G - 移动到最后一行
g - 移动到第一行
Q 退出less 命令

### more

### head

### cat

## vim

| 快捷键   | 功能               |
| -------- | ------------------ |
| `u`      | 撤销最后的操作     |
| `Ctrl+r` | 重做最后撤销的操作 |

| `/search_text` | 检索文档，在文档后面的部分搜索 search_text |
| -------------- | ------------------------------------------ |
| `?search_text` | 检索文档，在文档前面的部分搜索 search_text |

| `dd` | 删除该行/剪切当前行    |
| ---- | ---------------------- |
| `yy` | 复制当前行至存储缓冲区 |

复制粘贴
按下 v 来选择字符。（也可以用 V 来选择整行，Ctrl-v 来选择矩形块）
按下 y 来复制。
按下 p 粘贴。（或者 P 粘贴在当前光标位置之前）。

剪切粘贴，
按下 v 来选择字符。（也可以用 V 来选择整行，Ctrl-v 来选择矩形块）
按下 d 来剪切。
按下 p 粘贴。（或者 P 粘贴在当前光标位置之前）。

vim跳转到指定的行

 :n （跳转到文件第n行，需要回车）

如果只是临时显示vim的行号，只须按ESC键退出编辑内容模式，输入“：set number”后按回车键，就可以显示行号了。行号显示只是暂时的，退出vim后再次打开vim就不显示行号了

**:set nu**





清理磁盘

Linux 查看磁盘空间

```
df -h
```

```
# du -sh *
```

**du** 的英文原义为 **disk usage**，含义为显示磁盘空间的使用情况，用于查看当前目录的总大小。

例如查看当前目录的大小：



## 软连接

查看

```shell
ls -al
```



#### 创建

ln 命令的基本格式如下：

[root@localhost ~]# ln [选项] 【源文件】 【目标文件】

源文件是指软连接指向的目录，就比如C盘下的某个文件的路径。

目标文件是指“快捷键”文件名称 该文件是指令创建的。

以上两个文件都必须使用绝对地址 

例如：

当前路劲创建 test 引向 /var/www/test 文件夹

```
ln -s /var/www/test test
```

创建 /var/test 引向 /var/www/test 文件夹

```
ln -s /var/www/test /var/test
```

#### 删除

没有rm删不掉的，如果有,那就sudo

我们可以使用 ln 命令来创建软连接，那么怎样删除呢？

```
rm symbolic_link_name
```

使用 unlink 命令删除软链接
当然也可以使用 unlink 命令，但是不要直接使用软链接的名称，因为它不仅仅用于删除链接，还会删除文件。

删除软链接的另一种方法是使用 unlink 命令。这个命令乍听起来好像只用于删除链接，但其实它也可以删除文件。使用方式如下：

```
unlink name_or_path_of_link
```

这么说unlink岂不是一点用都没得，就像rmdir一样

  export NODE_HOME=/data/gitbook/node
  export PATH=$NODE_HOME/bin:$PATH

#### 修改

修改软连接

ln -snf [新的原文件或目录] [目标文件或目录]

这将会修改原有的链接地址为新的地址

例如:

创建一个软链接

```
ln -s /var/www/test /var/test
```

修改软链接

```
ln -snf /var/www/test1 /var/test
```
