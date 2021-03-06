# 配置MongoDB数据源 {#concept_cxg_1s1_p2b .concept}

MongoDB是文档型的NoSQL数据库，目前是全世界最受欢迎的文档型数据库之一，仅次于Oracle、MySQL等，MongoDB数据源提供了读取和写入MongoDB双向通道的能力，可以通过脚本模式配置同步任务。

**说明：** 添加MongoDB数据源，请您在MongoDB管理控制台 中进行白名单设置，IP白名单填写地址如下（地址之间用英文逗号分隔）：

11.192.97.82, 11.192.98.76, 10.152.69.0/24, 10.153.136.0/24, 10.143.32.0/24, 120.27.160.26, 10.46.67.156, 120.27.160.81, 10.46.64.81, 121.43.110.160, 10.117.39.238, 121.43.112.137, 10.117.28.203, 118.178.84.74, 10.27.63.41, 118.178.56.228, 10.27.63.60, 118.178.59.233, 10.27.63.38, 118.178.142.154, 10.27.63.15, 100.64.0.0/8

## 操作步骤 {#section_jy4_q4v_42b .section}

1.  以项目管理员身份进入[DataWorks管理控制台](https://workbench.data.aliyun.com/console)，单击对应项目操作栏中的**进入工作区**。
2.  单击顶部菜单栏中的**数据集成**，导航至**数据源**页面。
3.  单击**新增数据源**，弹出支持的数据源。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16201/15367208887534_zh-CN.png)

4.  在新建数据源弹出框中，选择数据源类型为**MongoDB**。
5.  配置MongoDB数据源的各个信息项。

    MongoDB数据源类型分为**阿里云数据库**和**有公网IP的自建数据库**。

    -   阿里云数据库：一般使用的网络是经典网络类型，同地区的经典网络能连通，跨地区的经典网络连接不保证能通。
    -   有公网IP的自建数据库：一般使用的网络是公网，然而公网可能产生一定的费用。
    以新增**MongDB** \> **阿里云数据库**类型的数据源为例。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16206/15367208887547_zh-CN.png)

    配置项说明如下：

    -   数据源类型：当前选择的数据源类型MongoDB\>阿里云数据库。

        **说明：** 

        如果您尚未授权数据集成系统默认角色，需要主账号前往RAM进行角色授权，然后刷新此页面。

    -   数据源名称： 由英文字母、数字、下划线组成且需以字符或下划线开头，长度不超过60个字符。
    -   数据源描述： 对数据源进行简单描述，不得超过80个字符。
    -   地区：是指在购买MongoDB时所选的区域。
    -   实例ID：您可在MongoDB管控台中查看MongoDB实例ID。
    -   数据库名：您可在MongoDB管控台中新建数据库，设置相应的数据名、用户名和密码。
    -   用户名/密码：数据库对应的用户名和密码。
    以新增**MongDB** \> **有公网IP的自建数据库**类型的数据源为例。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16206/15367208887548_zh-CN.png)

    配置项说明如下：

    -   数据源类型：当前选择的数据源类型MongoDB\>有公网IP的自建数据库。
    -   数据源名称： 由英文字母、数字、下划线组成且需以字符或下划线开头，长度不超过60个字符。
    -   数据源描述： 对数据源进行简单描述，不得超过80个字符。
    -   访问地址：格式为host:port。
    -   添加访问地址：添加访问地址，格式为host:port。
    -   数据库名：该数据源对应的数据库名称。
    -   用户名/密码：数据库对应的用户名和密码。
6.  单击**测试连通性**。
7.  测试连通性通过后，单击**确定**。

    **说明：** 

    -   VPC环境的MongoDB云数据库，添加有公网IP数据源类型并保存。
    -   VPC环境不支持测试连通性。

## 后续步骤 {#section_dqv_5d1_p2b .section}

现在，您已经学习了如何配置MongoDB数据源，您可以继续学习下一个教程。在该教程中您将学习如何通过配置MongoDB Writer插件。详情请参见[配置MongoDB Writer](intl.zh-CN/使用指南/数据集成/作业配置/配置Writer插件/配置MongoDB Writer.md#)和[配置MongoDB Reader](intl.zh-CN/使用指南/数据集成/作业配置/配置Reader插件/配置MongoDB Reader.md#)。

