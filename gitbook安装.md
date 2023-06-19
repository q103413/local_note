# gitbook安装教程

# 简介

> Modern book format and toolchain using Git and Markdown

这是 [gitbook](https://github.com/GitbookIO/gitbook) 项目主页上对 gitbook 的定义。

gitbook 首先是一个软件，正如上面定义的那样，它使用 Git 和 Markdown 来编排书本，如果用户没有听过 Git 和 Markdown，那么 gitbook 可能不适合你！

本书也是使用 gitbook 生成，所以在看到这里的时候，你应该对 gitbook 的魔力有了初步印象！

## Node.js安装

Node.js是一个基于Chrome Javascript运行时建立的一个平台，用来方便的搭建快速的，易于扩展的网络应用。

Node.js借助事件驱动，非阻塞I/O模型变得轻量和高效，非常适合run across distributed devices的data-intensivede 的实时应用。

安装完成之后，可以通过下面的命令来验证一下Node.js是否安装成功。



# 在 Linux 下安裝 Node.js

在 Linux 中的安裝方式有好幾種，請自己選擇喜歡的方式。

Node 官网已经把 linux 下载版本更改为已编译好的版本了，我们可以直接下载解压后使用：

[node.js官网下载地址](https://nodejs.org/en/download)

```shell
# cd /usr/local/src/
# wget https://nodejs.org/dist/v14.16.1/node-v14.16.1-linux-x64.tar.xz    // 下载
# tar xf node-v14.16.1-linux-x64.tar.xz         // 解压
# cd node-v14.16.1-linux-x64/                   // 进入解压目录
# ./bin/node -v                                 // 执行node命令 查看版本
v14.16.1
```

解压文件的 bin 目录底下包含了 node、npm 等命令，我们可以使用 ln 命令来设置软连接：

```shell
# ln -s /usr/local/src/node-v14.16.1-linux-x64/bin/node /usr/bin/node
# node -v
v14.16.1

# ln -s /usr/local/src/node-v14.16.1-linux-x64/bin/npm /usr/bin/npm
# npm -v
6.14.12
```

多人协作

由于使用了git工具，所以从根本上说，GitBook的多人协作问题，实际上就是git的多人协作。Git的多人协作流程如下：

- 团队成员使用git pull 命令获得最新内容
- 团队成员各自修改本地内容后，执行推送操作
- 如果遇到冲突，再使用pull合并冲突
- 使用push推送内容
