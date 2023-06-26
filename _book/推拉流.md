# 一、准备工作

- 登陆国内腾讯云
https://console.cloud.tencent.com/live/domainmanage
使用直播账号登陆

-  在对应群内找客服获取国内备案域名
比如:永利的直播需要两个直播备用域名，做推/播流用，要国内备案和证书。
拿到域名后检查是否备案成功。

# 二、操作步骤
## 1.添加播流域名

### 1.1 添加域名
云直播-域名管理-添加域名
![](/uploads/mk/images/m_6b6bc0560db7196794d7d6e417a13a06_r.png)

### 1.2 填写域名相关配置
类型：播放域名
加速区域：全球加速
域名：填写备案好的域名
域名归属验证：找客服协助添加ns解析
![](/uploads/mk/images/m_e1938b1dc4fe9072339a106ddac92065_r.png)

## 1.3 让客服协助ns解析
点击下一步，获取域名cname，继续找客服协助添加ns解析。
参考格式：
域名				
portal.kuug.cn 	
主机记录  
portal   
记录类型	
 CNAME     
 记录值
 portal.kuug.cn.txlivecdn.com 

## 1.4 证书配置
点击证书管理-配置配置，填写证书内容和密钥。
![](/uploads/mk/images/m_1ad0f83837edc5e9ce2eaea92291f281_r.png)

## 1.5 播流域名配置
- 自适应码率配置
点击配置好的播流域名-模版配置-自适应码率配置-编辑-功能模版（首次需创建）
![](/uploads/mk/images/m_b22a88f401ebbc8db72535de8fa15583_r.png)
![](/uploads/mk/images/m_d5906e56d13108838339d0661e94f2c5_r.png)

点击功能模版-创建模版：
模版名称 p
子流信息：
如图所示，配置三个子流。
子流名称分别为1080p,720p,480p
![](/uploads/mk/images/m_b066d2d929a38b5d694eda921cb447b1_r.png)
![](/uploads/mk/images/m_a170c752bf3b8a6356e6eeb2995329f6_r.png)

- 绑定域名：
创建模版完成后，点击绑定域名。
将创建的模版绑定到对应的域名下。
![](/uploads/mk/images/m_69b3fee93c4c9d491f355fe70eb9da0f_r.png)

- 开启鉴权：
点击配置好的播流域名-访问控制-Key鉴权
![](/uploads/mk/images/m_55d4254b8a75fa157ace97cad8af4493_r.png)

- HTTP响应头配置
点击配置好的播流域名-访问控制-高级配置-HTTP响应头配置
添加所有可选参数 取值*
![](/uploads/mk/images/m_3ebfd8d4a5a626b79b993dea1e443aa5_r.png)

- 播放配置
点击配置好的播流域名-访问控制-播放配置-播放地址生成器
填写StreamName，点击生成地址，查看生成结果，是否为https。
![](/uploads/mk/images/m_5a85bd6d60305c8ecff7eb4381e567cd_r.png)

## 2.添加推流域名
### 2.1 添加域名
云直播-域名管理-添加域名

### 2.2 填写域名相关配置
**类型：推流域名**
域名：填写备案好的域名
![](/uploads/mk/images/m_fc6dbf4d2e7120c808fdeb75b38898e7_r.png)
其他和1.添加播流域名一样，让客服协助加ns解析。

### 2.3 推流域名配置
点击配置好的推流域名-高级配置-延播配置-开启配置状态
![](/uploads/mk/images/m_7d69657acd4f89c72ccfba1ea1a32823_r.png)

点击配置好的推流域名-推流配置-鉴权配置
查看鉴权配置是否开启
![](/uploads/mk/images/m_2b588e089807882330d080d3a232e4ac_r.png)


## 三.配置回调（先不用管）
地址配置：http(s)://域名或者IP：端口号/live/auth/tencentCallback
说明：由于国内服务器不给非备案域名发送回调。建议优先配置IP+端口，其次配置备案域名
![](/uploads/mk/images/m_ac4438ab07d6fc5532210bb5a0c85ba8_r.png)
![](/uploads/mk/images/m_884fabbcb6bbe0b6659c9bd3dade561f_r.png)

## 四.通知老板等相关人
在上一步的鉴权配置中，找到域名对应的主KEY
参考格式：
腾讯云-鑫博永利-直播-备用域名

播放域名
portal.kuug.cn
主KEY 
rKbTSb6Z3tjx5Pz87b7x

推流域名
185669.push.tlivecloud.com 
主KEY 
dc08ce309c4a897bb187050b55c225ae