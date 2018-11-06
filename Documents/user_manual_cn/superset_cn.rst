Kyligence Insight for Superset 使用手册
=======================================

Kyligence Insight for Superset 是 Kyligence工程师深度定制的可视化工具，
与Kyligence/Kylin无缝集成，一键同步cube并自动适配Kyligence/Kylin查询语法，本文将分步介绍
Kyligence Insight for Superset的使用方法

登录
----

首次登录，打开sueprset界面，输入默认管理员的用户名和密码 admin/admin 即可登录 |image0|

导入/刷新cube
-------------
首先需要在 **数据源- 数据库** 处增加Kyligence的项目的连接串 |image31|

其中，数据库URL的格式为 **kylin://username:password@host:port/project** ，如果您需要在SQL实验中使用该项目中的表，则需要勾选 在SQL实验室中显示  |image32|

在Superset界面内点击 **数据源- Kylin 数据源刷新**，即可导入/刷新所有已经增加的项目下的cube |image1|

刷新成功后会自动进入 **数据源- Kylin Cubes** 界面，显示全部cube |image2|

查询Cube
--------

在 **数据源-Kylin Cubes** 点击cube名称，即可进入分析界面
在各栏选择相应的值，如时间筛选值，维度和度量值，以及行数限制等，然后点击左上角的
**运行查询** ，即可运行查询，得到结果集图表 |image3|

点击 **图表类型** 可以更改可视化图表类型 |image4|

比如选择饼图 |image5|

导出CSV文件
--------

在数据探索页面点击CSV按钮即可导出CSV  |image29|

在SQL实验室页面点击CSV按钮即可导出CSV  |image30|

注：使用EXCEL打开标准UTF-8编码的CSV文件的方法为：

点击 **数据** - **从文本** |image25|

使用 **分割符号** 的方式导入，选择文件原始格式为 **从UTF-8** |image26|

选择分隔符为 **逗号** |image27|

即可正常显示中文 |image28|

保存与分享
----------

在数据探索界面，点击左上角的保存 填入对应的信息，然后点击保存 |image6|

在仪表版界面，点击 **Edit Dashboard**, 然后点击 **Actions** 中的
**邮件** 即可使用邮件分享仪表板 |image7|

在自动生成的邮件中填入收件人，然后点击发送 |image8|

收件人点击邮件中的链接，即可在浏览器中进入到相应的仪表板页面 |image9|

在SQL 实验室 进行自定义SQL查询
------------------------------

点击 **SQL 实验室- SQL编辑器** 即可进入自定义SQL查询 |image10|

选择对应的数据库和表，输入SQL，点击 **运行查询** 即可得到查询结果
|image11|

在查询结果处选择 **可视化** ，可对查询结果集进行可视化 |image12|

自定义维度/度量
---------------

在 **数据源- Kylin Cubes** 界面，点击编辑记录，对某个cube进行编辑
|image13|

在 **列名列表** 处点击加号，增加自定义维度, 编辑相应信息，点击保存
|image14|

然后在列名列表处将新增维度勾选为 **可分组** ，**可筛选** 即可，同理可以增加自定义度量 

权限管理-数据源权限
------------------

除初始管理员用户外，您可以创建新的用户。在Superset中，通过创建、修改角色，并给用户赋予角色的方式管理用户的权限。

在 **安全 - 角色列表** 中可以编辑角色 |image19|

在 **安全 - 用户列表** 中可以编辑用户 |image21|

Superset内置了几个角色，主要是：

**Admin(超级管理员)**，拥有所有管理权限，能够新建角色及用户，授予或撤销其他用户的权限。可以创建、修改、访问所有数据源,可以访问、修改所有仪表板。

**Alpha(管理员)**，拥有部分管理权限，无法授予或撤销其他用户的权限。可以创建、修改、访问所有数据源。可以访问所有仪表板，只能修改自己有权访问的仪表板。

**Gamma(分析师)**，拥有部分访问权限。 没有创建、修改用户及创建、修改数据源的权限。默认对所有数据源都没有访问权限，需要由Admin用户来授予。只能访问、修改自己有权访问的仪表板。

比如，如果需要创建一个分析师用户Ming，则需要再建立一个角色，然后新建一个用户，给他赋予角色：

1.新建角色
  在 **安全 - 角色列表** 中复制一个Gamma角色，重命名为Ming 

2.给角色赋予数据源权限
  然后点击编辑，增加权限项 : 

  **database access on [project_name]**,

  **datasource access on [project_name]**,

  **datasource access on [project_name].[cube_name]** （注，每个需要查询的cube都要添加进去）

  然后点击保存 |image33|

3.新建用户及赋予角色
  在 **安全 - 用户列表** 中新建一个用户，命名为Ming |image34|

  填写相关信息，并赋予其角色为Ming，然后保存用户即可，该用户就只能访问被赋权的数据源 |image35|



权限管理-分析权限
----------------

您可以通过修改角色的分析权限的方式更改用户的相关权限，比如，需要禁用用户导出CSV的权限，则需要再建立一个角色，然后给他赋予角色：

1.复制了 Alpha 角色，命名为 Alpha_no_csv 角色

2.在 Alpha_no_csv 角色中删除了 **can download on SliceModelView** 权限（导出CSV权限）
|image20|

3.在 **安全 - 用户列表** 中赋予 ANALYST 用户 Alpha_no_csv 角色

更改后，ANALYST用户没有下载CSV的权限 |image23|

.. |image0| image:: ../images/user_manual_cn/01.png
.. |image1| image:: ../images/user_manual_cn/02.png
.. |image2| image:: ../images/user_manual_cn/03.png
.. |image3| image:: ../images/user_manual_cn/04.png
.. |image4| image:: ../images/user_manual_cn/05.png
.. |image5| image:: ../images/user_manual_cn/06.png
.. |image6| image:: ../images/user_manual_cn/07.png
.. |image7| image:: ../images/user_manual_cn/08.png
.. |image8| image:: ../images/user_manual_cn/09.png
.. |image9| image:: ../images/user_manual_cn/10.png
.. |image10| image:: ../images/user_manual_cn/11.png
.. |image11| image:: ../images/user_manual_cn/12.png
.. |image12| image:: ../images/user_manual_cn/13.png
.. |image13| image:: ../images/user_manual_cn/14.png
.. |image14| image:: ../images/user_manual_cn/15.png
.. |image17| image:: ../images/user_manual_cn/18.png
.. |image18| image:: ../images/user_manual_cn/19.png
.. |image19| image:: ../images/user_manual_cn/20.png
.. |image20| image:: ../images/user_manual_cn/21.png
.. |image21| image:: ../images/user_manual_cn/22.png
.. |image22| image:: ../images/user_manual_cn/23.png
.. |image23| image:: ../images/user_manual_cn/24.png
.. |image25| image:: ../images/user_manual_cn/25.png
.. |image26| image:: ../images/user_manual_cn/26.png
.. |image27| image:: ../images/user_manual_cn/27.png
.. |image28| image:: ../images/user_manual_cn/28.png
.. |image29| image:: ../images/user_manual_cn/29.png
.. |image30| image:: ../images/user_manual_cn/30.png
.. |image31| image:: ../images/user_manual_cn/31.png
.. |image32| image:: ../images/user_manual_cn/32.png
.. |image33| image:: ../images/user_manual_cn/33.png
.. |image34| image:: ../images/user_manual_cn/34.png
.. |image35| image:: ../images/user_manual_cn/35.png
