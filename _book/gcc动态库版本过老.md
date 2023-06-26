## 一，本机查找

## 二，网上下载

将libstdc++.so.6升级到libstdc++.so.6.0.29

1、将libstdc++.so.6.0.29文件拷贝到/usr/lib64/目录下

2、按顺序执行以下命令

```shell
cd  /usr/lib64/
mv ./libstdc++.so.6 ./libstdc++.so.6_bak  
#如果报错就将libstdc++.so.6_bak改为其他任意名字
sudo ln -s libstdc++.so.6.0.29 libstdc++.so.6
ls -l libstdc++.so.6
```

3、最后一条命令执行完，看到类似以下信息表示成功

```shell
lrwxrwxrwx 1 root root 19 Jun  8 21:29 libstdc++.so.6 -> libstdc++.so.6.0.29
```

[下载libstdc++.so.6.0.29](https://files.cnblogs.com/files/xiaoko/libstdc.so.6.0.29.zip)

