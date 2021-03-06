# 创建分析型数据库MySQL版2.0结果表

本文为您介绍如何创建实时计算Flink版分析型数据库MySQL版2.0版本的结果表，以及分析型数据库和实时计算Flink版字段类型之间的映射关系。

**说明：** 本文仅适用于Blink 1.4.5及以上版本。

## 什么是分析型数据库MySQL版

分析型数据库MySQL版是阿里巴巴自主研发的海量数据实时高并发在线分析（Realtime OLAP）云计算服务，支持在毫秒级时单位时间内，对千亿级数据进行实时地多维分析透视和业务探索。

## DDL定义

**说明：** 分析型数据库MySQL版 3.0版本（ADS 3.0版本）实时计算Flink版结果表DDL请参见[创建分析型数据库MySQL版3.0结果表](/cn.zh-CN/Blink独享/共享集群（原产品线）/Flink SQL参考/DDL语句/创建数据结果表/创建分析型数据库MySQL版3.0结果表.md)。

实时计算Flink版支持使用分析型数据库MySQL版 2.0作为结果输出。示例代码如下。

```
CREATE TABLE stream_test_hotline_agent (
id INTEGER,
len BIGINT,
content VARCHAR，
PRIMARY KEY(id)
) WITH (
type='ads',
url='yourDatabaseURL',
tableName='<yourDatabaseTableName>',
userName='<yourDatabaseUserName>',
password='<yourDatabasePassword>',
batchSize='20'
);
```

**说明：**

-   建议使用存储注册功能，详情请参见[注册分析型数据库MySQL版](/cn.zh-CN/Blink独享/共享集群（原产品线）/Flink SQL开发指南/数据存储/注册数据存储/注册分析型数据库MySQL版.md)。
-   分析型数据库MySQL版结果表声明中的主键要和分析型数据库MySQL版里的主键保持一致，大小写敏感。如果不一致，则会导致数组索引越界的异常现象。

## WITH参数

|参数|注释说明|备注|
|--|----|--|
|url|JDBC连接地址|分析型数据库MySQL版数据库地址。示例：`url ='jdbc:mysql://databaseName****-cn-shenzhen-a.ads.aliyuncs.com:10014/databaseName'`。其中参数解释如下：-   URI地址查询步骤如下：
    1.  登录[AnalyticDB 控制台](https://ads.console.aliyun.com/?spm=a2c4g.11186623.2.23.2c952b809T8asM)。
    2.  单击对应的集群名称，进入**基本信息**页面。
    3.  在**连接信息**中查看相应的连接地址。
-   分析型数据库MySQL版数据库名称（databaseName）即分析型数据库MySQL版实例名称。 |
|tableName|表名|无|
|username|账号|无|
|password|密码|无|
|maxRetryTimes|写入重试次数|可选，默认值为10。|
|bufferSize|流入多少条数据后开始去重|可选，默认值为5000，表示输入的数据达到5000条就开始输出。|
|batchSize|一次批量写入的条数|可选，默认值为1000。**说明：** 如果错误码是20015，则表示batchSize设置过大。分析型数据库MySQL版batchSize不能超过1 MB。例如，batchSize设置为`1000`，则平均每条记录大小不能超过1 KB。 |
|batchWriteTimeoutMs|写入超时时间|可选，单位为毫秒，默认值为5000。表示如果缓存中的数据在等待5秒后，依然没有达到输出条件，系统会自动输出缓存中的所有数据。|
|connectionMaxActive|单连接池最大连接数|可选，默认值为30。|
|ignoreDelete|是否忽略delete操作|默认值为false。|

## 类型映射

建议使用分析型数据库MySQL版和实时计算Flink版字段类型对应关系进行DDL声明。

|分析型数据库MySQL版字段类型|实时计算Flink版字段类型|
|----------------|--------------|
|BOOLEAN|BOOLEAN|
|TINYINT|INT|
|SAMLLINT|
|INT|
|BIGINT|BIGINT|
|DOUBEL|DOUBLE|
|VARCHAR|VARCHAR|
|DATE|DATE|
|TIME|TIME|
|TIMESTAMP|TIMESTAMP|

