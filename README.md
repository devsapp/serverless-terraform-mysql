# serverless-terraform-mysql-usage 帮助文档

<p align="center" class="flex justify-center">
    <a href="https://www.serverless-devs.com" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=serverless-terraform-mysql-usage&type=packageType">
  </a>
  <a href="http://www.devsapp.cn/details.html?name=serverless-terraform-mysql-usage" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=serverless-terraform-mysql-usage&type=packageVersion">
  </a>
  <a href="http://www.devsapp.cn/details.html?name=serverless-terraform-mysql-usage" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=serverless-terraform-mysql-usage&type=packageDownload">
  </a>
</p>

<description>

> ***一键创建MySQL资源并简单使用***

</description>

<table>

## 前期准备
使用该项目，推荐您拥有以下的产品权限 / 策略：

| 服务/业务 | 函数计算 |     
| --- |  --- |   
| 权限/策略 | AliyunFCFullAccess</br>AliyunOSSFullAccess</br>AliyunRDSFullAccess</br>AliyunContainerRegistryFullAccess</br>AliyunECSFullAccess |     


</table>

<codepre id="codepre">



</codepre>

<deploy>

## 部署 & 体验

<appcenter>

- :fire: 通过 [Serverless 应用中心](https://fcnext.console.aliyun.com/applications/create?template=serverless-terraform-mysql-usage) ，
[![Deploy with Severless Devs](https://img.alicdn.com/imgextra/i1/O1CN01w5RFbX1v45s8TIXPz_!!6000000006118-55-tps-95-28.svg)](https://fcnext.console.aliyun.com/applications/create?template=serverless-terraform-mysql-usage)  该应用。 

</appcenter>

- 通过 [Serverless Devs Cli](https://www.serverless-devs.com/serverless-devs/install) 进行部署：
    - [安装 Serverless Devs Cli 开发者工具](https://www.serverless-devs.com/serverless-devs/install) ，并进行[授权信息配置](https://www.serverless-devs.com/fc/config) ；
    - 初始化项目：`s init serverless-terraform-mysql-usage -d serverless-terraform-mysql-usage`   
    - 进入项目，并进行项目部署：`cd serverless-terraform-mysql-usage && s deploy -y`

</deploy>

<appdetail id="flushContent">

# 应用详情

## 应用功能
本项目为演示应用中心可以通过使用 Serverless Terraform 函数一键部署 MySQL 云数据库，并使用该 MySQL 的案例。

## 目的

用户在应用中心创建访问云资源应用时，不用手动创建资源，而是可以使用该应用演示的方式在创建应用之前创建资源，之后再创建应用，这节省了应用中心用户手动创建资源的时间。
## 架构详解
![](https://img.alicdn.com/imgextra/i3/O1CN018bA3Wz1iU7OqeXFO5_!!6000000004415-2-tps-1500-1564.png)  


函数 1：部署资源函数：Serverless Terraform
- Serverless Terraform 将 Terraform 集成在 FC Custom Container 函数中。  
- 用户向函数输入 TF 资源文件以及资源配置参数即可创建出对应资源，（创建过程由内置 Terraform 执行）  
- Serverless Terraform 将会把资源创建后的配置信息返回  
- 对于 端到端 MySQL 应用，我们内置了 RDS TF资源文件，用户只需要输入 RDS 配置参数即可创建出对应 RDS 资源  

函数2：部署消费函数
-   创建资源：

    1. Serverless Devs 工具具备 pre-action 能力，即在部署函数前完成某项工作。

    2. 利用 pre-action 能力在部署应用消费函数前调用资源函数，创建出资源，并将资源配置返回，传入到应用消费函数的环境变量里。
- 消费函数是用户的业务逻辑代码。

  1. 对于端到端 MySQL 创建与应用演示来说，消费函数通过从环境变量中获取 MySQL 资源配置，创建链接，之后使用链接创建一个Users表，执行插入数据，之后查询数据返回结果。

通过 Serverless Devs 开发者工具，您只需要几步，就可以体验 Serverless 架构，带来的降本提效的技术红利。

## 使用方法
### 参数
| 参数                 | 类型   | 默认值                          | 名称       | 备注                                                                                                                                                   |
| ------------------- | ----- | ------------------------------ |----------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| region              | string | cn-hangzhou                    | 地域       | 创建应用所在的地区，资源也会创在该地域                                                                                                                                  |
| serviceName         | string | serverless-terraform-mysql     | 服务名      | 应用所属的函数计算服务                                                                                                                                          |
| roleArn             | string | 无默认，必填                    | RAM角色ARN | 应用所属的函数计算服务配置的 role, 请提前创建好对应的 role, 授信函数计算服务, 并配置好 AliyunOSSFullAccess, AliyunFCDefaultRolePolicy, AliyunRDSFullAccess policy 和 AliyunECSFullAccess |
| ossBucket           | string | 必填                            | OSS存储桶名  | OSS存储桶名(注意和函数同地域)                                                                                                                                    |
| ossObjectName           | string | backend-test     | oss 对象名  | oss 对象名                                                                                                                                              |
| databaseName        | string | db-test                        | 数据库名     | 数据库名                                                                                                                                                 |
| databaseCharacterSet | string | utf8                           | 数据库字符集   | 数据库字符集                                                                                                                                               |
| instanceName        | string | serverless-terraform-mysql-test | RDS 实例名  | rds 实例                                                                                                                                               |
| instanceType        | string | mysql.n1.micro.1               | 实例规格     | rds 实例规格，参考https://help.aliyun.com/document_detail/276975.html?spm=5176.rdsbuy.0.tip.detail.40a5752fwc2ZQu                                           |
| accountName         | string | user                           | RDS 用户名  | RDS 账户                                                                                                                                               |
| password            | string | 123456                         | RDS 密码   | RDS 密码                                                                                                                                               |


### 验证
1. 部署应用成功后，转到 [RDS 实例列表](https://rdsnext.console.aliyun.com/rdsList/cn-huhehaote/basic)，注意选择地域，查看创建出来的资源
   ![](https://img.alicdn.com/imgextra/i1/O1CN01udRR8j1x10ShUfISS_!!6000000006382-2-tps-3570-1032.png)
2. invoke 以 consumer 结尾的函数，可以看到结果
   ![](https://img.alicdn.com/imgextra/i1/O1CN01PN1Hbe1s7oGbbjdKX_!!6000000005720-2-tps-3574-1386.png)

## 注意
由于创建 RDS 资源耗时较长及一些配置问题，小概率会出现超时或创建失败的错误，这需要用户自行去控制台函数日志部分查看执行日志(详见[此处](#日志))，并查看 RDS 创建情况，从而处理已创建的资源。
- 在函数日志中查看相对应资源创建函数的函数日志，通过日志中的appy_start字段判断哪些资源已经开始创建，已经创建的日志需要到对应资源处去管理。日志中的 apply_complete 字段判断哪些资源已经创建完成。
- [用户 RDS 实例列表](https://rdsnext.console.aliyun.com/rdsList/cn-huhehaote/basic), 查看是否已经创建实例，可以手动删除

### 应用执行价格
由于该应用会真实创建出 RDS 资源，并且 RDS 会根据存在时长而扣费，所以建议用户对 RDS 资源扣费情况进行初步了解后再运行该应用。[RDS MySQL 资源价格](https://help.aliyun.com/document_detail/45020.html)

函数计算计费： 创建资源最大消费：使用内存（1 GB） * 使用时长（20 min）= 1 * 20 * 60 * 0.000022120（函数计算单价 元 / s） = 0.026544元（如果处于免费额度时则为免费）具体算法请见：[函数计算价格](https://help.aliyun.com/document_detail/54301.html)

## 删除资源
1. 手动删除  
   a. 删除 RDS 资源  
   打开 [Rds 资源管理网站](https://rdsnext.console.aliyun.com/rdsList/cn-huhehaote/basic), 选择创建资源的地域，比如呼和浩特。  
   ![](https://img.alicdn.com/imgextra/i2/O1CN0173X11z202KSFc556o_!!6000000006791-2-tps-3550-830.png)    
   点击更多  
   ![](https://img.alicdn.com/imgextra/i4/O1CN01GvWZ3B1cNoFgkOOM1_!!6000000003589-2-tps-3146-612.png)  
   选择释放实例，弹出提示窗口:  
   ![](https://img.alicdn.com/imgextra/i2/O1CN01xNHWiD1JKAOqW6eOi_!!6000000001009-2-tps-1088-372.png)  
   选择确定，即可释放 RDS 实例。    
   VPC 资源由于和函数计算服务绑定，所以在删除函数时会自动删除 VPC  
   b. 删除函数   
   注意：删除函数前，请确保已经删除了 RDS 实例，否则将不能自动删除 VPC。
   应用中心删除应用，将会自动删除函数以及 VPC。
2. 一键删除，即将上线，敬请期待   
## 详细步骤 
### 通过应用中心创建   
1. 浏览器搜索框输入 https://fcnext.console.aliyun.com/applications/create?template=serverless-terraform-mysql-usage 并跳转，进入应用创建页面。
![](https://img.alicdn.com/imgextra/i1/O1CN01IW8p6O1D8otdMlyjP_!!6000000000172-2-tps-3300-1572.png)  
 根据提示填写应用参数  
2. 填写参数完毕后，点击最下方的创建，即可开始部署应用
3. 待应用部署成功后，即可转到 [FC 服务列表](https://fcnext.console.aliyun.com/cn-huhehaote/services)查看刚刚部署的服务
![](https://img.alicdn.com/imgextra/i3/O1CN01R7Jk7N29nLekuqAxn_!!6000000008112-2-tps-3528-1446.png)
4. 点击服务名进入函数列表
![](https://img.alicdn.com/imgextra/i2/O1CN01uDDLp625bf5IKvscB_!!6000000007545-2-tps-3566-826.png)  
可以看到有两个函数，以 creator 结尾的是资源创建函数，以 consumer 结尾的是消费函数。
5.  <span id="日志"></span> 点击进入以 creator 结尾的函数，选择调用日志->函数日志，即可看到资源创建的情况。
![](https://img.alicdn.com/imgextra/i1/O1CN01y08u6729NhTgp4NKy_!!6000000008056-2-tps-3472-1642.png)  
6. 退出到服务列表，选择以 consumer 结尾的函数，点击函数配置。
![](https://img.alicdn.com/imgextra/i2/O1CN017sbYpV1Mr5iqKTjAE_!!6000000001487-2-tps-3584-514.png)
7. 下拉即可看资源函数创建的资源配置写到了消费函数的环境变量内，所以消费者函数可以通过使用环境变量消费资源。
![](https://img.alicdn.com/imgextra/i4/O1CN014fhcpa1IeUMODqyEV_!!6000000000918-2-tps-3498-640.png)
8. 接下来选择测试函数，并点击测试函数
 ![](https://img.alicdn.com/imgextra/i2/O1CN01WztMgq1DDOr6MyNw2_!!6000000000182-2-tps-3584-1082.png)
9. 等待片刻即可得到结果
![](https://img.alicdn.com/imgextra/i1/O1CN01PN1Hbe1s7oGbbjdKX_!!6000000005720-2-tps-3574-1386.png)

### 通过 Serverless Devs 创建
使用`s init serverless-terraform-mysql-usage` 并根据提示完成创建
部署完成后，执行 `s invoke --function-name ${vars.service}_consumer`，即可看到结果：
![](https://img.alicdn.com/imgextra/i3/O1CN01vcNITp1C0HtoDLW0i_!!6000000000018-2-tps-3442-520.png)

其中，每执行一次，都会向users表中，插入一条name 为 zhangsanfeng, address 为 central block 的数据。

## 自定义
如需修改自定义能力，首先可以查看 serverless-terraform-rds/data 下的 rds 文件夹以及 data.tf 文件，这两个部分使用了 terraform module 能力。 用户可以通过修改 rds 下文件 和 data.tf 文件（主要对所需要的 variables 进行设计和更新，再在s.yaml 中 plugin args 部分添加相应 variables 参数即可）。


</appdetail>

<devgroup>

## 开发者社区

您如果有关于错误的反馈或者未来的期待，您可以在 [Serverless Devs repo Issues](https://github.com/serverless-devs/serverless-devs/issues) 中进行反馈和交流。如果您想要加入我们的讨论组或者了解 FC 组件的最新动态，您可以通过以下渠道进行：

<p align="center">

| <img src="https://serverless-article-picture.oss-cn-hangzhou.aliyuncs.com/1635407298906_20211028074819117230.png" width="130px" > | <img src="https://serverless-article-picture.oss-cn-hangzhou.aliyuncs.com/1635407044136_20211028074404326599.png" width="130px" > | <img src="https://serverless-article-picture.oss-cn-hangzhou.aliyuncs.com/1635407252200_20211028074732517533.png" width="130px" > |
|--- | --- | --- |
| <center>微信公众号：`serverless`</center> | <center>微信小助手：`xiaojiangwh`</center> | <center>钉钉交流群：`33947367`</center> | 

</p>

</devgroup>
