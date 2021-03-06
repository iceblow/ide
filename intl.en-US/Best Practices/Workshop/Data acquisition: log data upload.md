# Data acquisition: log data upload {#concept_xjn_lps_s2b .concept}

## Related Products {#section_wzl_grs_s2b .section}

The big data products involved in this experiment are [MaxCompute \(big data computing services\)](https://www.alibabacloud.com/product/maxcompute). And [DataWorks \(data factory, original big data development kit\)](https://www.alibabacloud.com/product/ide).

## Prerequisites {#section_scn_5ss_s2b .section}

Before you begin this lab, you need to make sure you have an Alibaba Cloud account and have a real name.

## Activate MaxCompute { .section}

**Note:** If you have already activated MaxCompute, skip this step to create the project space directly.

1.  Log in to the [Alibaba Cloud website](https://www.alibabacloud.com/), click **Log in** in the upper-right corner to fill in your Alibaba Cloud account and password.
2.  Select **Products** \> **Analytics & Big Data** \> **MaxComputute** and go to the MaxCompute product details page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609699063_en-US.png)

3.  Click **Start now**.
4.  Select **Pay-As-You-Go**, click **Buy Now**.

## Create Project {#section_ydr_pxs_s2b .section}

1.  Log on to the [DataWorks console](https://partners-intl.aliyun.com) by using a primary account.
2.  You can create a MaxCompute project in two ways.
    -   On the console overview page, go to **Common Functions****Create Project**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609699071_en-US.jpg)

3.  Fill in the configuration items in the Create Project dialog box. Select a region and a calculation engine service.

    **Note:** If you have not purchase the relevant services in the region, it is directly display that there is no service available in the Region. The data development, O&M center, and data management are selected by default.

4.  Configure the basic information and advanced settings for the new project, and click **Create project**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609699076_en-US.png)

    **Note:** 

    -   The project name needs to begin with a letter or underline, and can only contain letters, underscores, and numbers.
    -   The project name is globally unique, it is recommended that you use your own easy-to-distinguish name as the project space name for this lab.
5.  Once the project has been created successfully, you can select the Project List page to **Data Studio** after viewing the project space.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609699079_en-US.png)


## Create data source {#section_fml_m1t_s2b .section}

**Note:** Based on the scenario simulated by this lab, you need to distribute to create both the FTP data source and the RDS data source.

-   Create a new FTP data source
    1.  Select the **Data Integration** \> **Data Source** Page, and click **Add Data Source**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609699086_en-US.png)

    2.  Select the data source type as FTP, and Protocol selected as SFTP, with other configuration items as follows.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709088_en-US.png)

        Parameters:

        -   Data Source Type type: with public network IP
        -   Data source name: ftp\_workshop\_log
        -   Data source description: ftp log file synchronization
        -   Protocol: sftp
        -   Host：10.80.177.33\(internal network\)//118.31.238.64 \(Public Network\)
        -   Port: 22
        -   Username/Password: workshop/workshop
    3.  Click **Test Connectivity**, and after the connectivity test passes, click **Finish** to save the configuration.

        **Note:** If the test connectivity fails, check your user name/password and the region in which the item is located. It is recommended to create the project in East China 2, and other regions do not guarantee network access.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709100_en-US.png)

-   Add RDS Data Source
    1.  Select the **Data Integration** \> **Data Source**Page, and click **Add Data Source**.
    2.  Select the data source type as MySQL, and fill in the configuration information.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709103_en-US.png)

        Parameters:

        -   Data source type: ApsaraDB for RDS
        -   Data source name: rds\_workshop\_log
        -   Data source description: RDS log data synchronization
        -   RDS instance name: rm-bp1z69dodhh85z9qa
        -   RDS instance buyer ID: 1156529087455811
        -   Database name: workshop
        -   Username/Password: workshop/workshop\#2017
    3.  Click **Test Connectivity**, and after the connectivity test passes, click **Finish** to save the configuration.

## Create a Business Flow {#section_ehz_xdt_s2b .section}

1.  Right-click **Business Flow** under **Data Development**, select **Create Business Flow**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709122_en-US.png)

2.  Fill in the Business Flow name and description.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709124_en-US.png)

3.  Click **Create**to complete the creation of the Business Flow.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709125_en-US.png)

4.  Enter the Business Flow Development Panel and drag a virtual node and two data sync nodes \(ftp\_datasync and rds\_datasync\) into the Panel.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709128_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709131_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709132_en-US.png)

5.  Drag the connection to set the workshop\_start node to the upstream of both data synchronization nodes.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/153706097012038_en-US.png)

## Configure workshop\_start task {#section_xvm_jht_s2b .section}

Since the new version sets the input and output nodes for each node, you need to set an input for the workshop\_start node, the virtual node in the Business Flow can be set to the upstream node as the project root node, the project root node is generally named project name \_ root.

You can configure it by clicking**Schedule**. When the task configuration is complete, click **Save**.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609709137_en-US.png)

## Create Table {#section_oth_h3t_s2b .section}

1.  Right-click **Table** and choose **Create Table**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/153706097011961_en-US.png)

2.  Type in **Table Name**\(ods\_raw\_log\_d and ods\_user\_info\_d\) for FTP logs and RDS respectively.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/153706097011969_en-US.png)

3.  Type in your **Table Alias** and choose **Partitioned Table**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/153706097111978_en-US.png)

4.  Type in the field and partition information,click **Submit to Development Environment** and **Submit to Production Environment**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/153706097111992_en-US.png)

    You can also click **DDL Mode**, use the following SQL statements to create tables.

    ```
    //Creates a target table for FTP logs
    CREATE TABLE IF NOT EXISTS  ods_raw_log_d (
      Col_string
    )
    PARTITIONED BY (
      dt STRING
    );
    
    //Creates a target table for RDS
    CREATE TABLE IF NOT  EXISTS ods_user_info_d (
      uid STRING COMMENT 'User ID',
      gender STRING COMMENT 'Gender',
      age_range STRING COMMENT 'Age range',
      zodiac STRING COMMENT 'Zodiac'
    )
    PARTITIONED BY (
      dt STRING
    );
    ```

5.  Click **Submit to Development Environment** and **Submit to Production Environment**. You can configure both of the tables in this way.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/153706097112023_en-US.png)


## Configure the data synchronization task {#section_vfl_dkt_s2b .section}

-   Configure the ftp\_datasync node
    1.  Double-click the ftp\_datasync node node to go to the node configuration page.
    2.  Select a data source.

        Select the data source as the maid in the FTP data source.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719142_en-US.png)

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719143_en-US.png)

        Parameters:

        -   Data source: ftp\_workshop\_ftp
        -   File path: /home/workshop/user\_log.txt
        -   Column Separator: |
    3.  Select data destination

        Select the data destination is ods\_raw\_log\_d in the odps\_first data source. Both partition information and cleanup rules take the system default, the default configuration of the partition is $\{bizdate\}.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719144_en-US.png)

    4.  Configure the field mapping, connect the fields that you want to synchronize.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719145_en-US.png)

    5.  Configure **Transmission Rate** with a maximum operating rate of 10 Mb/s.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719146_en-US.png)

    6.  Verify that the current task is configured and can be modified. After the confirmation is correct, click **Save** in the upper left corner.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719153_en-US.png)

    7.  Closes the current task and returns to the Business Flow configuration panel.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719147_en-US.png)

-   Configure the rds\_datasync node Node
    1.  Double-click the rds\_datasync node node to go to the node configuration page.
    2.  Select a data source.

        Select the data source that is located in the MySQL data source rds\_workshop\_log, and the table is named as ods\_user\_info\_d, the split key uses the default to generate columns.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719148_en-US.png)

    3.  Select data destination

        Select the data destination ods\_user\_info\_d in the data source named odps\_first. Both partition information and cleanup rules take the system default, the default configuration of the partition is $\{bizdate\}.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719149_en-US.png)

    4.  Configure the field mapping, default in association with the name mapping.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609729151_en-US.png)

    5.  Configure **Transmission Rate** with a maximum operating rate of 10 Mb/s.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609719146_en-US.png)

    6.  Verify that the current task is configured and can be modified. After the confirmation is correct, click **Save** in the upper left corner.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609729157_en-US.png)

    7.  Closes the current task and returns to the Business Flow configuration panel.

## Submit Business Flow tasks {#section_uyy_p4t_s2b .section}

1.  Click **Submit** to submit the current Business Flow.
2.  Select the nodes in the submit dialog box, and check the **Ignore Warning on I/O Inconsistency**, click **Submit**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609729160_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609729162_en-US.png)


## Run workflow task {#section_inw_mpt_s2b .section}

1.  Click **Run**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609729163_en-US.png)

    During a task run, you can view the run status.

2.  Right-click the SQL task and select **view log**.
3.  Right-click the FTP \_ Data Synchronization task and select **view log**.
4.  Right-click the RDS \_ Data Synchronization task and select **view log**.

## Check if the data is successfully imported into MaxCompute {#section_mdg_sqt_s2b .section}

1.  Click **temporary query** in the left-hand navigation bar.
2.  Select **New** \> **ODPS SQL**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609729169_en-US.png)

3.  Write and execute SQL statement to check the entries imported into ods\_raw\_log\_d.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15370609729170_en-US.png)

4.  Also write and execute SQL statements to view the number of imported ods\_user\_info\_d records.

    **Note:** The SQL statement is as follows, where the partition columns need to be updated to the business date, if the task runs on a date of 20180717, the business date is 20180716.

    ```
    Check that data was written to MaxCompute
    select count(*) from ods_raw_log_d where dt=business date;
    select count(*) from ods_user_info_d where dt=business date;
    ```


## Next step {#section_agb_rrt_s2b .section}

Now that you've learned how to synchronize the log data, complete the data acquisition, you can continue with the next tutorial. In this tutorial, you will learn how to calculate and analyze the collected data. For more information, see [Data processing: user portraits](intl.en-US/Best Practices/Workshop/Data processing: user portraits.md#).

