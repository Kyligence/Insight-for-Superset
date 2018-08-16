Kyligence Insight for Superset User Manual
==========================================

Kyligence Insight for Superset is a deeply customized visualization tool
for Kyligence/Kylin users . It integrates seamlessly with
Kyligence/Kylin, one-click sync cube and automatically adapts Kyligence
query syntax. This article will introduce the use of Kyligence Insight
for Superset step by step.

log in
------

Open the sueprset interface and enter the username and password in
Kyligence to log in. |image0|

Import/Refresh cube
-------------------

Click **Sources-Kylin Refresh** in the Superset interface to
import/refresh all cubes. |image1|

After the refresh is successful, it will automatically enter the
**Sources-Kylin Cubes** interface, showing all cubes. |image2|

Query Cube
----------

Click on the cube name in **Sources-Kylin Cubes** to analyze. Select the
appropriate values in each column, such as the time filter value in the
red box, the dimensions and metrics in the blue box, and the number of
rows in the yellow box.

.. figure:: ./04.png
   :alt: 

Then click **Run Query** in the upper left corner or the middle of the
blank space to run the query and get the result set chart. |image3|

Click **Visualization Type** to change the visualization chart type.
|image4|

Such as ‘Pie Chart’ |image5|

Save and share
--------------

In the Explore interface, click **Save** in the top left corner.
|image6|

Fill in the corresponding information and click Save. |image7|

Go to the Dashboard interface, click **Edit Dashboard**, then click
**Email** in **Actions** to share dashboard with email. |image8|

Fill in the recipient in the automatically generated email and click
Send. |image9|

The recipient clicks on the link in the email to earn the corresponding
dashboard page. |image10|

Custom SQL Query in SQL Lab
---------------------------

Click **SQL Lab-SQL Editor** to use the custom SQL query |image11|

Select the database and table, enter SQL to get the query result
|image12|

Visualize the query result set by selecting **Visualize** at the query
result |image13| |image14|

Custom Dimensions / Metrics
---------------------------

In the **Sources-Kylin Cubes** interface, click edit to edit a cube.
|image15|

Click the plus sign at List Columns to add a custom dimension. |image16|

Edit the information and click Save. |image17|

Then set the new dimension to **groupable** at List Columns, which can
be filtered. |image18|

Similarly, you can add custom metrics. |image19|

Query using new custom dimensions and metrics. |image20|

Modify permissions
------------------

Kyligence's administrator user defaults to the superset administrator
(Admin), with full administrative privileges, other users as analyst
permissions (Alpha), with permissions of creating report and querying
dashboard. |image21|

Roles can be created/edited in the **Security-List Roles**, such as
editing the permissions of Alpha , deleting the permissions that can be
downloaded in the SliceModelView (exporting CSV permissions) |image22|

Granted the new role to ANALYST users in **Security-List Users**
|image23|

As a result , ANALYST users do not have permission to download CSV
|image24|

.. |image0| image:: ./01.png
.. |image1| image:: ./02.png
.. |image2| image:: ./03.png
.. |image3| image:: ./05.png
.. |image4| image:: ./06.png
.. |image5| image:: ./07.png
.. |image6| image:: ./22.png
.. |image7| image:: ./23.png
.. |image8| image:: ./24.png
.. |image9| image:: ./25.png
.. |image10| image:: ./26.png
.. |image11| image:: ./08.png
.. |image12| image:: ./09.png
.. |image13| image:: ./10.png
.. |image14| image:: ./11.png
.. |image15| image:: ./12.png
.. |image16| image:: ./13.png
.. |image17| image:: ./14.png
.. |image18| image:: ./15.png
.. |image19| image:: ./16.png
.. |image20| image:: ./17.png
.. |image21| image:: ./18.png
.. |image22| image:: ./19.png
.. |image23| image:: ./20.png
.. |image24| image:: ./21.png
