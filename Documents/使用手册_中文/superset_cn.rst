Kyligence Insight for Superset 使用手册
=======================================

Kyligence Insight for Superset 是 Kyligence工程师深度定制的可视化工具，
与Kyligence/Kylin无缝集成，一键同步cube并自动适配Kyligence/Kylin查询语法，本文将分步介绍
Kyligence Insight for Superset的使用方法。

登录
----

打开sueprset界面，输入Kyligence中的用户名和密码即可登录 |image0|

导入/刷新cube
-------------

在Superset界面内点击 **数据源- Kylin 数据源刷新**
，即可导入/刷新全部cube |image1|

刷新成功后会自动进入 **数据源- Kylin Cubes** 界面，显示全部cube |image2|

查询Cube
--------

在 **数据源-Kylin Cubes** 点击cube名称，即可进入分析界面
在各栏选择相应的值，如时间筛选值，维度和度量值，以及行数限制等，然后点击左上角的
**运行查询** ，即可运行查询，得到结果集图表 |image3|

点击 **图表类型** 可以更改可视化图表类型 |image4|

比如选择饼图 |image5|

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

在查询结果处选择 **可视化**\ ，可对查询结果集进行可视化 |image12|

自定义维度/度量
---------------

在 **数据源- Kylin Cubes** 界面，点击编辑记录，对某个cube进行编辑
|image13|

在 **列名列表** 处点击加号，增加自定义维度, 编辑相应信息，点击保存
|image14|

然后在列名列表处将新增维度勾选为 **可分组** ，**可筛选** 即可，同理可以增加自定义度量 

修改权限
--------

Kyligence的管理员用户默认为Superset的管理员(Admin)，拥有全部管理权限，其他用户为分析师权限(Alpha)，有创建报表和查询仪表板权限
|image18|

在 **安全 - 角色列表** 中可以创建/编辑用户角色 |image19|

如复制了Alpha 角色，命名为Alpha\_no\_csv 角色，在Alpha\_no\_csv
角色中删除了 **can download on SliceModelView** 权限（导出CSV权限）
|image20|

在 **安全 - 用户列表** 中赋予ANALYST用户Alpha\_no\_csv 角色 |image21|
|image22|

更改后，ANALYST用户没有下载CSV的权限 |image23|

.. |image0| image:: ./01.png
.. |image1| image:: ./02.png
.. |image2| image:: ./03.png
.. |image3| image:: ./04.png
.. |image4| image:: ./05.png
.. |image5| image:: ./06.png
.. |image6| image:: ./07.png
.. |image7| image:: ./08.png
.. |image8| image:: ./09.png
.. |image9| image:: ./10.png
.. |image10| image:: ./11.png
.. |image11| image:: ./12.png
.. |image12| image:: ./13.png
.. |image13| image:: ./14.png
.. |image14| image:: ./15.png
.. |image17| image:: ./18.png
.. |image18| image:: ./19.png
.. |image19| image:: ./20.png
.. |image20| image:: ./21.png
.. |image21| image:: ./22.png
.. |image22| image:: ./23.png
.. |image23| image:: ./24.png
