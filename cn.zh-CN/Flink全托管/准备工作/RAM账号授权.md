---
keyword: [Flink全托管, RAM账号授权, 授权, 子账号授权]
---

# RAM账号授权

本文为您介绍，如何在Flink全托管开发控制台上，为阿里云RAM账号授权。

如果您的RAM账号没有被主账号授权，当您进入到Flink全托管开发控制台后，会看到**403**信息。

![403报错](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8833449951/p133353.png)

1.  使用主账号登录[实时计算控制台](https://realtime-compute.console.aliyun.com/console/cell?spm=a2c4g.11186623.2.16.1a8023a9J8TiPV)。

2.  在**Flink全托管**页签，单击对应工作空间**操作**列下的**开发控制台**。

3.  在左侧导航栏上，单击**系统管理** \> **成员管理**。

4.  单击**添加成员**。

5.  选择**角色**，填写**Member**信息。

    ![添加成员](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3415903061/p133336.png)

    -   角色

        不同角色功能差异如下。

        |功能|owner|editor|viewer|
        |--|-----|------|------|
        |查看作业列表|Y|Y|Y|
        |启停作业|Y|Y|N|
        |更改作业配置|Y|Y|N|
        |上传JAR|Y|Y|N|
        |编写SQL|Y|Y|N|
        |注册UDF|Y|Y|N|
        |注册元数据|Y|Y|N|
        |查看作业模板|Y|Y|Y|
        |增删改作业模板|Y|Y|N|
        |管理成员|Y|N|N|

    -   **Member**：阿里云RAM账号对应的UID。其中阿里云RAM账号的UID获取方式如下：
        1.  使用主账号登录[RAM控制台](https://ram.console.aliyun.com/)。
        2.  在左侧导航栏，单击**人员管理** \> **用户**。
        3.  单击目标RAM账号名称。
        4.  在**用户基本信息**区域，查看**UID**信息。
6.  单击**确定**。


