# Step 3: Create a synchronization task {#concept_ofg_4zl_s2b .concept}

This article will take MySQL Data sources as an example, showing how to export data from MaxCompute to a MySQL data source through the data integration feature.

In DataWorks, data integration is typically used to periodically import the business data generated in your system into the workspace, after the calculation of the SQL task, the calculation results are periodically exported to the data source that you specify, for further presentation or running usage.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748989_en-US.png)

Currently, data from the following data sources can be imported to or exported from the workspace through the data integration function: RDS, MySQL, SQL Server, PostgreSQL, MaxCompute, ApsaraDB for Memcache, DRDS, OSS, Oracle, FTP, DM, Hdfs, MongoDB, and so on. For more information, see [Supported data sources](../../../../intl.en-US/User Guide/Data Integration/Data source configuration/Supported data sources.md#).

## Prerequisites {#section_bz3_bvr_s2b .section}

-   If you are using a self-built database on ECS, you need to [add security groups](../../../../intl.en-US/User Guide/Data Integration/Common configuration/Add security group.md#) to your ECS.
-   If you are using data sources such as RDS/MongoDB, you need to [add a white list](../../../../intl.en-US/User Guide/Data Integration/Common configuration/Add whitelist.md#) to a console such as RDS/MongoDB.

    **Note:** If you use a custom resource group to schedule the RDS data synchronization task, you must add the IP address of the computer hosting the custom resource group to the RDS whitelist.


## Procedure { .section}

**Add a data source**

**Note:** Only the Project Administrator role can create new data sources, and members of other roles can view data sources only.

1.  Log on to the [DataWorks management console](https://workbench.data.aliyun.com/console) as the Project Administrator.
2.  Select **enter workspace** in the corresponding item actions column under the **list of items**.
3.  Click **data integration** in the top menu bar.
4.  Click **data sources**in the left-hand navigation bar.
5.  Click **Add data source** in the upper-right corner.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748990_en-US.png)

6.  Fill in each configuration item in the Add Data Source dialog box.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748991_en-US.jpg)

    -   Data Source Type: With a public IP address.
    -   Data source name: The name must contain letters, numbers, and underlines, but cannot begin with a number or underline, For example, abc\_1123.
    -   Data source description: The description cannot exceed 80 characters.
    -   JDBC URL: `jdbc:mysql://host:port/database`.
    -   User name/Password: The user name and password used to connect to the database.
    For configuration instructions for different data source types, see [Data source configuration](../../../../intl.en-US/User Guide/Data Integration/Data source configuration/Configure MySQL database.md#).

7.  \(Optional\).Click **Test Connectivity** after entering all the required information in the relevant fields.
8.  If the test connectivity is successful, click **Finish**.

**Note:** Make sure that the target MySQL database contains tables.

Create the table odps\_result in the MySQL database. The statements used for table creation are as follows:

```
CREATE TABLE `ODPS_RESULT` (
`education`  varchar(255) NULL ,
`num`  int(10) NULL 
)
```

After the table has been built, you can execute the `desc odps_result;` to view the table details.

**Creating and configuring synchronization node**

This section shows how to create and configure the synchronization node **write\_result**, and write data from result\_table to the MySQL database. The specific steps are as follows.

1.  Create the node write\_result, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748992_en-US.png)

2.  Sets the dependencies between nodes so that the write\_result node is dependent on the insert\_data node.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748993_en-US.png)

3.  Select the source.

    Select the MaxCompute data source and the source table result\_table and click **Next**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748994_en-US.png)

4.  Select a Target.

    Select the MySQL data source and target table ODPS \_result, and click **Next**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748995_en-US.png)

5.  Map the fields.

    Select the mapping between fields. You need to configure the field mapping relationships. The "Source Table Fields" on the left correspond one to one with the "Target Table Fields" on the right.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748996_en-US.png)

6.  Control the channel.

    Click **Next** to configure the maximum job rate and dirty data check rules.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748997_en-US.png)

7.  Preview and store.

    After completing the above configuration, scroll the mouse up and down to view the task configuration, and if it is not, click **Save**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748998_en-US.png)


**Submit a data synchronization task**

Once you save a synchronization task click **Submit**, and the synchronization task is submitted to the scheduling system. The scheduling system automatically and periodically runs the task from the second day according to the configuration attributes.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15371509748999_en-US.png)

## Subsequent steps {#section_bp2_lzr_s2b .section}

Now, you know how to create a synchronization task and export data to data sources of different types. Continue to the next tutorial for further study. This tutorial shows you how to set the scheduling attribute and dependency for a synchronization task. For more information, see[setting schedule properties and dependencies](intl.en-US/Quick Start/Step 4: Scheduling and dependence settings.md#) for tasks.

