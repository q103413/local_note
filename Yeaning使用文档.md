[Skip to end of metadata](https://wiki.60889.xyz:8568/confluence/pages/viewpage.action?pageId=36143373#page-metadata-end)

- 由 [Maple](https://wiki.60889.xyz:8568/confluence/display/~maple)创建, 最后修改于[五月 22, 2023](https://wiki.60889.xyz:8568/confluence/pages/diffpagesbyversion.action?pageId=36143373&selectedPageVersions=8&selectedPageVersions=9)

[Go to start of metadata](https://wiki.60889.xyz:8568/confluence/pages/viewpage.action?pageId=36143373#page-metadata-start)

# 一、配置

## 1、数据源

### 1-1、创建数据源

![image-20230619212438660](C:\Users\Admins\AppData\Roaming\Typora\typora-user-images\image-20230619212438660.png)

重点名词释义:

- 流程 赋予该新建数据源已有的审核流程(非查询)
- 负责人 该用户为数据源实际负责人，且当查询审核开启后由该负责人负责该数据源的查询审批
- 类型 当前类型共分三种:1.读写(既可以被查询也可以被执行),2.写(仅执行),3.读(仅查询)

### 1-2、编辑数据源

<img src="https://next.yearning.io/images/flowtarget.png" alt="img" style="zoom: 33%;" />

重点名词释义:

- 排除数据库 选择需要排除的数据库并保存后，该数据库将不会出现在提交工单/查询页面的数据库选择下拉框中。
- 脱敏字段 输入脱敏字段后该数据源下匹配的该字段数据(大小写敏感)将不会显示在查询结果中。

## 2、用户

### 2-1、创建用户

![image-20230619212517047](C:\Users\Admins\AppData\Roaming\Typora\typora-user-images\image-20230619212517047.png)

### 2-2、编辑用户

点击编辑按钮可编辑改用户行数据,如下所示:

 ![img](https://next.yearning.io/images/user02.png)

重点名词释义:

1.审计人 当用户为审计人角色时，将可查看审计页面下相关信息。

### 2-3、用户赋权

![image-20230619212555534](C:\Users\Admins\AppData\Roaming\Typora\typora-user-images\image-20230619212555534.png)

点击权限按钮即可对该用户进行赋权。可以同时将多个权限组赋予用户，用户的权限将根据所赋予的1个或多个权限组权限计算并去重后获得。

## 3、权限组

权限组内权限共分为DDL权限(表结构修改)，DML权限（表数据变更），Query权限（查询）共三大类。

![image-20230619212620253](C:\Users\Admins\AppData\Roaming\Typora\typora-user-images\image-20230619212620253.png)

TIP

当某一个数据源类型为读写时，该数据源将会出现在所有三大类权限列表中

读时仅会出现在Query权限表中

写时仅会出现在DDL/DML权限表中

## 4、工单流程

### 4-1、创建流程

进入 **管理->流程** 页面，点击新建流程按钮

**Yearning 最多支持7层的审核流程，但必须注意的是流程的开头必然是提交人阶段，流程的结束必然是执行阶段。否则将会导致流程错乱！**

![image-20230619212643820](C:\Users\Admins\AppData\Roaming\Typora\typora-user-images\image-20230619212643820.png)

名词释义:

- 流程名称 (顾名思义)
- 阶段名称 (当前设置的流程阶段的名称)
- 阶段类型 (当前阶段的类型,共分两种:1.审核,2.执行)
- 审核人员 (指定当前阶段审核人员范围,可多选)
- 添加 (点击后将该阶段添加至流程中)

步骤添加后并不代表该流程已创建成功，点击**保存按钮**后即可保存

**更改流程时请确保该环境下的工单都已处理完毕，否则可能会引起流程错乱！**

**如没有将对应环境配置流程则用户无法对这个环境进行任何DDL/DML工单提交操作**

### 4-2、数据源应用该流程

创建完流程后，在 管理->数据源 处找到需要赋予流程的数据源，将流程添加到该数据源中并点击保存。

<img src="https://next.yearning.io/images/flowtarget.png" alt="img" style="zoom:33%;" />

TIP

只有当数据源被赋予了流程之后,该数据源才被允许提交审批工单。

# 二、使用

## 1、工单

### 1-1、工单提交

点击工单申请页面，根据实际提单需求选择DML/DDL/Query中的某一类进行工单提交。

![img](https://wiki.60889.xyz:8568/confluence/download/attachments/36143373/image2023-5-22_13-11-0.png?version=1&modificationDate=1684736413105&api=v2)

点击对应数据源卡片进入工单提交页面

![img](https://wiki.60889.xyz:8568/confluence/download/attachments/36143373/image2023-5-22_13-16-4.png?version=1&modificationDate=1684736413054&api=v2)

布局介绍

- 页面左侧
  - 当选择对应数据表之后点击**获取表结构**按钮将会展示该数据表字段及索引信息
  - 定时执行 该功能依赖Yearning所部署服务器上本地时间，请将服务器时间与本地使用时间保持一致，否则将会出现错误。同时，由于Yearning并未依赖其他第三方定时服务，如在定时执行时间之前Yearning崩溃/重启将会丢失定时信息导致工单无法执行。
  - 当**是否回滚**选项选择为 **是** 时，该工单提交的SQL语句执行时如果该数据库开启binlog则会自动生成对应的回滚语句并保存。
- 页面右侧
  - 右上SQL编辑框 请将需要提交的SQL语句填写入该编辑框内，鼠标右键菜单中选择 **SQL检测** 按钮进行SQL语句检测或通过 **SQL美化** 按钮进行SQL语句美化
  - 右下审核结果区域 当点击 SQL检测 按钮后该区域将会展示该SQL语句的检测结果。

TIP

- 当焦点处于编辑器中时，可以采用Ctrl/Cmd + E 快捷键触发SQL检测
- 当焦点处于编辑器中时，可以采用Ctrl/Cmd + B 快捷键触发SQL美化
- 同时该编辑器支持常用文本快捷键
- **提交**按钮只有在检测语句 **错误等级** 均为0时才会激活

### 1-2、工单审批/执行

进入 审核->工单 页面选择需要审批的工单点击详情按钮进入该工单审核详情页

![img](https://wiki.60889.xyz:8568/confluence/download/attachments/36143373/image2023-5-22_13-45-45.png?version=1&modificationDate=1684737944862&api=v2)

![img](https://wiki.60889.xyz:8568/confluence/download/attachments/36143373/image2023-5-22_13-55-23.png?version=1&modificationDate=1684738522607&api=v2)

布局介绍

- 页面上侧
  - 工单基本信息展示
  - 审核按钮
- 页面下侧
  - 工单流程及进度
  - SQL语句展示 鼠标右键菜单中选择 **SQL检测** 按钮进行SQL语句检测或通过 **SQL美化** 按钮进行SQL语句美化
  - SQL语句审核结果

TIP

- 当焦点处于编辑器中时，可以采用Ctrl/Cmd + E 快捷键触发SQL检测
- 当焦点处于编辑器中时，可以采用Ctrl/Cmd + B 快捷键触发SQL美化
- 同时该编辑器支持常用文本快捷键
- **同意**按钮只有在检测语句 **错误等级** 均为0时才会激活
- 当流程最后节点人员通过后Yearning将会自动执行该工单

### 1-3、回滚工单生成

![img](https://wiki.60889.xyz:8568/confluence/download/attachments/36143373/image2023-5-22_13-44-30.png?version=1&modificationDate=1684737869483&api=v2)

工单执行成功且开启生成回滚语句时，如需对执行的SQL进行回滚操作

请点击该工单详情页 **结果栏** 点击 **提交回滚语句**之后将会生成一个新的工单(包含此回滚语句)重新走完流程后即可执行自动化任务

### 1-4、自动化任务

自动执行任务:

用户可通过该功能设置自动执行任务。当提交的dml语句符合相应任务条件。将会自动执行，无需审核人审核。

该功能仅限dml语句使用。请慎重使用！

## 2、查询

### 2-1、提交

点击工单申请页面，选择Query类进行查询。

![img](https://wiki.60889.xyz:8568/confluence/download/attachments/36143373/image2023-5-22_14-12-47.png?version=1&modificationDate=1684739566429&api=v2)

如开启查询审核功能将进入如下界面：

![img](https://wiki.60889.xyz:8568/confluence/download/attachments/36143373/image2023-5-22_14-38-32.png?version=1&modificationDate=1684741111248&api=v2)

TIP

- 查询审核开启后需要在查询前提交查询申请经由数据源负责人审批通过后方可查询，且同一时间只能申请一个数据源进行查询操作(可申请的数据源为用户其所拥有的query权限数据源)。
- 如开启查询审核需要在申请时注明是否导出(且系统已开启查询导出功能)。
- 如查询审核功能未开启则系统开启查询导出功能后所有人员均可导出数据
- 未开启查询审核功能，用户仅可对其拥有query权限的数据源进行查询
- 由于查询采用websocket连接，如使用反向代理(nginx)请确保对websocket代理的正确配置

##### **查询界面**

![img](https://wiki.60889.xyz:8568/confluence/download/attachments/36143373/image2023-5-22_14-17-24.png?version=1&modificationDate=1684739843922&api=v2)

### 2-2、审核

##### 查询审核

数据源负责人通过 审核 -> 查询 页面查看需要审核的查询工单(未开启查询审核时工单将自动批准)

<img src="https://next.yearning.io/images/query07.png" alt="img" style="zoom:50%;" />

##### 查询详情

点击对应查询工单详情按钮后进入，可查看该工单的基本信息以及执行的SQL语句。

![img](https://next.yearning.io/images/query08.png)



# 3、审计

审计功能为具有**审计人**角色的用户提供平台工单/查询数据的审计支持。

#### 如何使用审计功能

1. 赋予审计用户审计人角色(用户页面)
2. 审计用户重新登录后即可在导航栏处看到审计栏

![img](https://wiki.60889.xyz:8568/confluence/download/attachments/36143373/image2023-5-22_14-11-19.png?version=1&modificationDate=1684739478486&api=v2)