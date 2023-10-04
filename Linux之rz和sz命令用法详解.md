## Linux之rz和sz命令用法详解

 rz，sz 是Linux/Unix同Windows进行ZModem文件传输的[命令行工具](https://cloud.tencent.com/product/cli?from_column=20065&from=20065)。优点就是不用再开一个sftp工具登录上去上传下载文件。 

- 安装命令：

```javascript
yum install lrzsz 
```

- 从服务端发送文件到客户端：

```javascript
sz filename 
```

- 从客户端上传文件到服务端：

```javascript
rz 
```

在弹出的框中选择文件，上传文件的用户和组是当前登录的用户

- SecureCRT设置默认路径： Options -> Session Options -> Terminal -> Xmodem/Zmodem – ->Directories
- Xshell设置默认路径： 右键会话 -> 属性 -> ZMODEM -> 接收文件夹

# 1. sz 命令

- 用途说明：将选定的文件发送（send）到本地机器。`sz`命令是利用ZModem协议来从Linux[服务器](https://cloud.tencent.com/act/pro/promotion-cvm?from_column=20065&from=20065)传送文件到本地，一次可以传送一个或多个文件。相对应的从本地上传文件到Linux服务器，可以使用`rz`命令。
- 常用参数 `-a`： 以文本方式传输（ascii）。 `-b`： 以二进制方式传输（binary）。 `-e`： 对控制字符转义（escape），这可以保证文件传输正确。
- 如果能够确定所传输的文件是文本格式的，使用： `sz -a files`
- 如果是二进制文件，使用： `sz -be files`

# 2. rz 命令

- 用途说明：运行该命令会弹出一个文件选择窗口，从本地选择文件上传到Linux服务器
- 常用参数 `-b`： 以二进制方式，默认为文本方式。（Binary (tell it like it is) file transfer override.） `-e` ：对所有控制字符转义。
- 如果要保证上传的文件内容在服务器端保存之后与原始文件一致，最好同时设置这两个标志，如下所示方式使用： `rz -be`
- 此命令执行时，会弹出文件选择对话框，选择好需要上传的文件之后，点确定，就可以开始上传的过程了。上传的速度取决于当时网络的状况。
- 如果执行完毕显示“0错误”，文件上传就成功了，其他显示则表示文件上传出现问题了。