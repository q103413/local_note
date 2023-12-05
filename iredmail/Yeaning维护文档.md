安装步骤

**1、创建 Yearning 库,字符集应为 UTF8mb4【宝塔本地MySQL】**

  create database Yearning DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;

**【安装目录在/data】**
**2、下载zip或者二进制安装包**
  下载地址  https://github.com/cookieY/Yearning/releases

**3、解压unzip 或者tar** 

**4、进入Yearning 目录（/data/Yearning）**

**5、修改配置文件 conf.toml**

```shell
cat conf.toml
[Mysql]
Db = "Yearning"
Host = "127.0.0.1"
Port = "3306"
Password = "xxxx"
User = "root"

[General]   #数据库加解密key，只可更改一次。
SecretKey = "dbcjqheupqjsuwsm"
```

**6、初始化及安装**
  ./Yearning install
 
**7、开8000端口**

  1、云服务器后台管理修改【推荐】
  2、本地修改【如果有必要】

​    firewall-cmd --zone=public --add-port=8000/tcp --permanent 
​    firewall-cmd --reload 

### 运行

 **运行 ./Yearning run**
 **参数启动 ./Yearning run --push "IP地址" -port "8000"**
 **后台运行 nohup ./Yearning run &**

### 升级

  **无需手动更新表结构。停止原服务并替换安装包后重新启动**
  1.备份原Yearning数据库

  2.执行Yearning目录下migrate 二进制文件。
    ./Yearning migrate

  3.正常启动Yearning

### **官方文档**

https://guide.yearning.io/
