# 前 言

## 【简介】

OpenIM服务端包括**Open-IM-Server（开源核心）和Open-IM-Enterprise（业务核心）**两部分，本文档是以单机docker-compose方式部署。

##  【注意事项】

1、请仔细按文档流程操作，跳一步可能就会失败。

2、修改.yaml配置文件要遵循文件格式（如: 后有空格）。 

## 【准备工作】

1、运行环境：linux系统即可，Ubuntu 7.5.0-3ubuntu1~18.04最优，root用户

2、机器资源：如果用户量小于10万，可用单机部署，建议最低8C 16G （使用minio需要优秀的网络带宽和至少IT普通磁盘）

3、开放9090端口（minio）、10001至10010端口，具体可参考下文【端口开放及访问路由】

4、安装go/git/docker/docker-compose

可参考https://doc.rentsoft.cn/#/component/docker

# 部署Open-IM-Server开源核心

## 一、安装依赖组件（仅首次部署时需要）

### 1、进入Open-IM-Server目录，编辑.env 

```shell
USER=root #不用修改

PASSWORD=AFn1a6nfid7lup7kS1  # 密码不能包括任何特殊符号（如@#等）且至少8位，仅对redis mysql mongo三个组件密码生效

ENDPOINT=http://127.0.0.1:10005 # 用minio存储需要填写外网ip:10005或https://域名

DATA_DIR=./ # 指定大磁盘目录
```

### 2、修改IM离线推送配置 config/usualConfig.yaml，以下是个推配置示例（组件密码会根据.env自动生成）

```shell
getui:

  pushUrl: "https://restapi.getui.com/v2/$appId"

  masterSecret: "g00Z1P65VO9InOnp2" #需添加

  appKey: "4UwKSLHtOCAu9DC5" #需添加

  enable: true #true启动个推推送
```

### 3、修改业务配置 config/config.yaml（包括离线配置、生成IM管理员账号、云存储配置、单群最大人数等）

#### （1）27行 mongo离线消息配置（按需设置）

```shell
dbRetainChatRecords: 5      # mongo保存离线消息时间（天）

chatRecordsClearTime: "0 3 * * *"  # 每天凌晨3点清除消息
```

#### （2）116行credential 云存储配置（以下是腾讯云示例）

```shell
tencent:

appID: 1312026995

region: ap-hongkong

bucket: opim-mantianxing-qwe-1312026995

secretID: AKIDa1B6kMiodBRQAeqlPmshFXYJn0wby5vU

secretKey: JM8dqmSrzqRkmX2GCsHQIsBE0yg7HAl7
```

#### （3）258行生成IM管理员，建议用以下配置：

```shell
manager:

#app管理员userID和对应的secret

appManagerUid: [ "xfIM123456","xfIM654321", "xfIM333", "xfIMAdmin"]

secrets: [ "xfIM111111","xfIM222222", "xfIM333333", "xfIMAdmin"]

appSysNotificationName: "系统通知"
```

#### （4）371-768行notification中所有switch设为false（关闭不必要的通知）

```shell
switch: false 
```

### 4、修改业务配置docker-compose_cfg/config.yaml

#### （1）12行生成后台管理员，建议用以下配置：

```shell
# 默认管理员账号
admin:

defaultAccount:

account: [ "admin1", "admin2" ]

defaultPassword: [ "XF123456", "XF123456" ]

openIMUserID: [ "xfIM123456", "xfIMAdmin" ]

faceURL: [ "", "" ]

nickname: [ "admin1", "admin2" ]

level: [ 1, 100 ]
```

#### （2）50行oss云存储配置（以下是腾讯云示例，use表示使用的云存储类型）

```shell
tencent:

BucketURL: ""

serviceURL: https://opim-man-qwe.cos.accelerate.myqcloud.com

secretID: "AKIDa1B6kMiodBRXYJn0wby5vU"

secretKey: "JM8dqmSrzqRkmXsBE0yg7HAl7"

sessionToken: ""

bucket: "opim-mantianxing-qwe-131995"

use: "tencent"
```

### 5、单群最大人数配置pkg/common/constant/constant.go

```shell
   # 362行
   MaxNotificationNum = 5000 #（设为5000，官方建议不超过1万）
```

### 6、安装组件并启动（ETCD、MySQL、MongoDB、Redis、Kafka、Minio）

```shell
chmod +x install_im_server.sh;

./install_im_server.sh;
```

如果安装失败时，只能停止docker-compose并删除组件文件夹components，然后从第一步重新开始；生产环境禁止删除（组件中包含数据库）

### 7、检查组件

```shell
cd script;

./docker_check_service.sh
```

出现 all services launch success 表示所有组件启动成功。

## 二、编译Open-IM-Server

### 1、确保Go版本至少为1.15。

### 2、下载SDK-Core源码到服务器

```shell
cd Open-IM-Server/cmd/

git clone https://github.com/OpenIMSDK/openim-sdk-core.git --recursive

mv openim-sdk-core/ Open-IM-SDK-Core/
```

### 3、设置脚本权限

```shell
cd ../script/

chmod +x *.sh
```

### 4、编译源码

```shell
./batch_build_all_service.sh

#出现all services launch success表示服务启动成功
```

## 三、启动Open-IM-Server

1、启动服务

```shell
cd script

./start_all.sh 
```

2、检查服务

```shell
./check_all.sh 

# 出现all services launch success表示服务启动成功
```

【nginx配置参考】官方文档：         https://doc.rentsoft.cn/#/v2/server_deploy/easy_deploy_new?id=%e4%ba%94%e3%80%81nginx%e9%85%8d%e7%bd%ae%e5%8f%82%e8%80%83

【端口开放及访问路由】官方文档：    https://doc.rentsoft.cn/#/v2/server_deploy/easy_deploy_new?id=%e5%85%ad%e3%80%81%e7%ab%af%e5%8f%a3%e5%bc%80%e6%94%be%e5%8f%8a%e8%ae%bf%e9%97%ae%e8%b7%af%e7%94%b1

# 部署Open-IM-Enterprise业务核心

## 1、修改配置项

```shell
cd Open-IM-Enterprise/

vi config/config.yaml

# 将etcd中的secret改成组件密码（Open-IM-Server目录.env中的密码）
```

## 2、设置脚本权限、停止服务

```shell
cd script


If 首次部署 {

chmod +x *.sh      # 设置脚本权限

else {

./stop_all.sh       # 停止服务

}
```

## 3、编译服务

```shell
./batch_build_all_service.sh
```

出现all services build success 表示编译完成

## 4、启动服务

```shell
./start_rpc_service.sh
```

## 5、检测服务

```shell
./check_all.sh
```

#  配置线路和服务地址

## 1、配置线路

在第三方云平台配置线路json，参考格式如下：

```
{
    "data":{
        "lines":[
            {
                "base_url":"https://域名",
                "remark":"app线路一"
            },
            {
                "base_url":"https://域名",
                "remark":"app线路二"
            }
        ]
    },
    "errCode":true
}
```

注意：如果首次配置json，需要将json的url地址发给客户端。

## 2、配置服务地址

登录管理后台-应用管理-登录全局配置（参下图：配置服务地址），填写：

```shell
图片存储引擎：cos、minio（按需选择）

wsURL地址配置：wss://域名/msg_gateway

apiURL地址配置：https://域名/api

registerURL地址配置：https://域名/chat

configURL地址配置：https://域名/complete_admin
```

备注：后台账号参见上文 docker-compose_cfg/config.yaml中的配置，如果没改就是：admin1 / XF123456

## 3、验证

参见下文： 验证方法

 

![img](file:///C:/Users/Admins/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

图：配置服务地址

# 验证方法

## 【检查服务】

```shell
cd script

./check_all.sh
```

出现 all services launch success 代表服务正常

## 【验证minio存储】

1、管理后台验证：设置-个人设置-头像-点击上传（参见下图），图片显示说明正常（如果异常可通过浏览器调试工具查看图片域名是否正确）。

![img](file:///C:/Users/Admins/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)

2、客户端验证：登录web版（或移动端）更改自己头像或发送图片消息验证。

## 【验证三方云存储】

由于web版暂未接入三方云存储，只能登录安卓/苹果版，修改个人头像或发送图片消息验证（账号可以在客户端注册或管理后台用户管理中添加）。

#  更换mino域名

## 1、修改配置文件 

#### （1）config/config.yaml 123行minio配置项：

```shell
endpoint:          #minio外网地址，给客户端访问的

endpointInner:        #minio官网建议内网（外网也行）
```

（备注：如果换了存储桶，还需要修改相关配置项）

#### （2）config/usualConfig.yaml 23行minio配置项：

```shell
endpoint:          # 同上 
```

（备注：如果换了accessKeyID，还需要修改相关配置项）

## 2、停止服务

```shell
cd Open-IM-Server/script/

./stop_all.sh
```

## 3、编译服务

```shell
./batch_build_all_service.sh
```

## 4、启动服务

```shell
./start_all.sh
```

## 5、验证

参见上文：验证方法

# 更换云存储

1、修改配置文件

（1）config/config.yaml 116行credential配置项（以下是腾讯云示例）

```shell
tencent:

appID: 1312026995

region: ap-hongkong

bucket: opim-mantianxing-qwe-1312026995

secretID: AKIDa1B6kMiodBRQAeqlPmshFXYJn0wby5vU

secretKey: JM8dqmSrzqRkmX2GCsHQIsBE0yg7HAl7
```

（2）docker-compose_cfg/config.yaml 50行oss配置项（以下是腾讯云示例，use表示使用哪个云存储）

```shell
tencent:

BucketURL: ""

serviceURL: https://opim-man-qwe.cos.accelerate.myqcloud.com

secretID: "AKIDa1B6kMiodBRXYJn0wby5vU"

secretKey: "JM8dqmSrzqRkmXsBE0yg7HAl7"

sessionToken: ""

bucket: "opim-mantianxing-qwe-131995"

use: "tencent"
```

2、停止服务

```shell
cd Open-IM-Server/script/

./stop_all.sh
```

3、编译服务

```shell
./batch_build_all_service.sh
```

4、启动服务

```shell
./start_all.sh
```

5、验证

参见上文：验证方法

# 修改离线推送配置

1、修改配置文件

如需【更换离线推送配置】修改config/usualConfig.yaml，以下是个推配置示例：

```shell
getui:

  pushUrl: "https://restapi.getui.com/v2/$appId"

  masterSecret: "g00Z1P65VO9InOnp2" #需添加

  appKey: "4UwKSLHtOCAu9DC5" #需添加

  enable: true #true启动个推推送
```

如需【关闭APP不必要的通知】修改config/config.yaml 371-768行，将notification中所有switch设为false

2、停止服务

```shell
cd Open-IM-Server/script/

./stop_all.sh
```

3、编译服务

```shell
./batch_build_all_service.sh
```

4、启动服务

```shell
./start_all.sh
```

5、检查服务

```shell
./check_all.shshell
```

出现 all services launch success 代表服务正常

6、验证功能

只能通过移动端验证。



# 清理离线消息

说明：通过此配置，可以定期清理用户的离线消息。

1、修改配置文件 config/config.yaml 27行mongo离线消息配置（按需填写）

```shell
dbRetainChatRecords: 5      # mongo保存离线消息时间（天）

chatRecordsClearTime: "0 3 * * *"  # 每天凌晨3点清除消息
```

 

2、停止服务

```shell
cd Open-IM-Server/script/

./stop_all.sh
```

 

3、编译服务

```shell
./batch_build_all_service.sh
```

 

4、启动服务

```shell
./start_all.sh
```

 

5、检查服务

```shell
./check_all.sh
```

出现 all services launch success 代表服务正常



6、检验功能

只能通过用户端验证。
