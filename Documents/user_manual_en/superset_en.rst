Kyligence Insight for Superset User Manual
==========================================

Kyligence Insight for Superset is a deeply customized visualization tool
for Kyligence/Kylin users . It integrates seamlessly with
Kyligence/Kylin, one-click sync cube and automatically adapts Kyligence
query syntax. This article will introduce the use of Kyligence Insight
for Superset step by step.

log in
------

Open the sueprset interface and enter the default username and password admin/admin to log in. |image0|

Import/Refresh cube
-------------------

Firstly,need to add a connection string for the Kyligence project at the **Sources-Database** |image33|

The format of the database URL is **kylin://username:password@host:port/project**. If you need to use the table in the project in the SQL Lab, you need to check ’Expose in SQL Lab‘.  |image34|

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
|image25|

Then click **Run Query** in the upper left corner or the middle of the
blank space to run the query and get the result set chart. |image3|

Click **Visualization Type** to change the visualization chart type.
|image4|

Such as ‘Pie Chart’ |image5|


EXPORT CSV
--------

Export CSV by clicking the CSV button on the explore page  |image27|

Export CSV by clicking the CSV button on the SQL Lab page |image28|

Note: The method of opening a standard UTF-8 encoded CSV file using EXCEL is:

Click **Data** - **From text** |image29|

Import using the **Delimited**, select the original format of the file as **UTF-8** |image30|

Select **Comma** as delimiters |image31|

As a result ,Characters of all languages are displayed normally |image32|


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


Rights Management - Data Source Permissions
-------------------------------------------

Besides the initial administrator user, you can create new users. In Superset, you manage user permissions by creating, modifying roless and giving users roles.

The roles can be edited in **Security - List Roles** |image19|

Users can be edited in **Security - List Users** |image21|

Super built-in several roles, mainly:

**Admin (Super Administrator)** , with all administrative privileges, having the ability to create new roles and users, grant or revoke permissions for other users.Admin can create, modify and have access to all data sources. Admin can access, and modify all dashboards.

**Alpha (Admin)** , with partial administrative privileges, cannot grant or revoke permissions from other users. Alpha can create, modify, and access all data sources. All dashboards can be accessed by Alpha.Alpha only can modify the dashboards that they have access to.

** Gamma (analyst)** , with partial access privileges. They have no permissions to create, modify users and create , modify data sources. By default, they have no access to all data sources and need to be granted by the Admin user. Gamma can only access and modify the dashboards that you have access to.

For example, if you need to create an analyst user -Ming, you need to create another role, then create a new user and give him a role:

1.Create a role
Copy a Gamma role in **Security - List Roles** and rename to Ming.

2.Give data source permissions to the role
  Then click edit to add the permission item:

  **database access on [project_name]**,

  **datasource access on [project_name]**,

  **datasource access on [project_name].[cube_name]**  (Note, every cube that needs to be queried need be added)

  Then click save |image33|

3.Create new users and assign roles
  Create a new user in **Security - List Users**, named Ming |image34|

  Fill in the relevant information and give the role of Ming, then save the user, the user can only access the authorized data source |image35|


Rights Management - Analysis Permissions
----------------------------------------

You can change the user's related permissions by modifying the role's analysis permissions. For example, if you need to disable the user's ability to export CSV, you need to create another role and then give him the role:

1.Copy the Alpha role and name Alpha_no_csv

2.Removed **can download on SliceModelView** permission in the Alpha_no_csv role (export CSV permissions)
|image22|

3.Assign ANALYST user Alpha_no_csv role in **Security - List Users**

After the change, ANALYST users do not have permission to download CSV |image24|



.. |image0| image:: ../images/user_manual_en/01.png
.. |image1| image:: ../images/user_manual_en/02.png
.. |image2| image:: ../images/user_manual_en/03.png
.. |image3| image:: ../images/user_manual_en/05.png
.. |image4| image:: ../images/user_manual_en/06.png
.. |image5| image:: ../images/user_manual_en/07.png
.. |image6| image:: ../images/user_manual_en/22.png
.. |image7| image:: ../images/user_manual_en/23.png
.. |image8| image:: ../images/user_manual_en/24.png
.. |image9| image:: ../images/user_manual_en/25.png
.. |image10| image:: ../images/user_manual_en/26.png
.. |image11| image:: ../images/user_manual_en/08.png
.. |image12| image:: ../images/user_manual_en/09.png
.. |image13| image:: ../images/user_manual_en/10.png
.. |image14| image:: ../images/user_manual_en/11.png
.. |image15| image:: ../images/user_manual_en/12.png
.. |image16| image:: ../images/user_manual_en/13.png
.. |image17| image:: ../images/user_manual_en/14.png
.. |image18| image:: ../images/user_manual_en/15.png
.. |image19| image:: ../images/user_manual_en/16.png
.. |image20| image:: ../images/user_manual_en/17.png
.. |image21| image:: ../images/user_manual_en/18.png
.. |image22| image:: ../images/user_manual_en/19.png
.. |image23| image:: ../images/user_manual_en/20.png
.. |image24| image:: ../images/user_manual_en/21.png
.. |image25| image:: ../images/user_manual_en/04.png
.. |image27| image:: ../images/user_manual_en/27.png
.. |image28| image:: ../images/user_manual_en/28.png
.. |image29| image:: ../images/user_manual_en/29.png
.. |image30| image:: ../images/user_manual_en/30.png
.. |image31| image:: ../images/user_manual_en/31.png
.. |image32| image:: ../images/user_manual_en/32.png
.. |image33| image:: ../images/user_manual_en/33.png
.. |image34| image:: ../images/user_manual_en/34.png



