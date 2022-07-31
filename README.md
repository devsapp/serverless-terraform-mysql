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
| 权限/策略 | AliyunFCFullAccess |     


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
本项目为提供 serverless-terraform 一键部署 MySQL 云数据库，并使用该 MySQL 的案例。
通过 Serverless Devs 开发者工具，您只需要几步，就可以体验 Serverless 架构，带来的降本提效的技术红利。
## 应用结构
本应用主要分为三个部分：
![](http://image.editor.devsapp.cn/yxsDtkggiqtE7zdDk2AldGSa8j5CjhsxuDktx1dl8gGdsGqavq/d2jjtDbFFhzCEaCdB1Sh)
1. 资源创建者函数为 serverless-terraform-rds 函数，该函数可以利用内置 terraform 自动创建 MySQL 资源所需的 VPC, VSWITCH, 安全组, rds 实例, db相关配置。
2. 插件是 pre-action 插件，该插件将会在部署消费者函数前，invoke 资源创建者函数，并将结果写入到消费者函数的环境变量中。
3. 消费者函数则会访问创建的 MySQL 数据库，并执行简单的操作。

## 使用方法
使用`s init serverless-terraform-mysql-usage` 并根据提示完成创建
部署完成后，执行 `s invoke --function-name ${vars.service}_consumer`，即可看到结果：
![](http://image.editor.devsapp.cn/yxsDtkggiqtE7zdDk2AldGSa8j5CjhsxuDktx1dl8gGdsGqavq/g51eDltdEiz2zZCktfED)

其中，每执行一次，都会向users表中，插入一条name 为 zhangsanfeng, address 为 central block 的数据。

## 自定义
如需修改自定义能力，首先可以查看 serverless-terraform-rds/data 下的 rds 文件夹以及 data.tf 文件，这两个部分使用了 terraform module 原生能力。 用户可以通过修改 rds下文件 和 data.tf 文件（主要对所需要的 variables 进行设计和更新，再在s.yaml 中 plugin args 部分添加相应 variables 参数即可）。

## 注意
由于由于创建 rds 资源耗时较长及一些配置问题，有小概率会出现超时或创建失败的错误，这需要用户自行去控制台函数日志部分查看执行日志，从而处理已创建的资源。

### 应用执行价格
由于该应用会真实创建出 rds 资源，并且 rds 会根据存在时长而扣费，所以建议用户对 rds 资源扣费情况进行初步了解后再运行该应用。[rds mysql 资源价格](https://help.aliyun.com/document_detail/45020.html)

函数计算计费： 最长：使用内存（1gb） * 使用时长（20 min）= 1 * 20 * 60 * 0.000022120（函数计算单价） = 0.026544元。具体算法请见：[函数计算价格](https://help.aliyun.com/document_detail/54301.html)







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