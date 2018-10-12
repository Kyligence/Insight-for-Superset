Quick start of Kyligence Insight for Supersetin in an offline environment.

Supported Linux distributions
=============================
* SUSE Linux Enterprise Server 11 SP4 x86_64 (64-bit)
* CentOS release 7 (64-bit)
* CentOS release 6 (64-bit)

Note:
The user is required to obtain the Linux distribution information of the installed machine for subsequent installation.
If you deploy offline, MapBox related visualizations will not be available because they need to access the external network.

Install Kyligence Insight for Superset
======================================
1. Download installation package of Supserset in `Kyligence Download Page`_ .

2. Unzip the installation package ::

     $ tar -xf [Package Name]

     e.g. :

     $ tar -xf Insight-Linux-x86_64-0.12.0.tar.gz

3. Enter the decompressed directory and set the current directory as the environment variable SUPERSET_HOME ::

     $ cd Insight-Linux-x86_64-0.12.0

     $ export SUPERSET_HOME=`pwd`

4. Install the dependencies of the Superset ::

     $ bin/bootstrap.sh install [Linux distribution]

     e.g. :

     $ bin/bootstrap.sh install centos7

5. Modify the configuration file of the superset under the ./conf folder ::

     $ vi conf/insight.default.yaml

   Find the insight.default.yaml file and configure it according to your environment ::

     superset:
       sqlalchemy_database_uri: <SQLAlchemy DSN, if empty, superset will use SQLlite instead>
       sqllab_timeout: <SQLLab timeout>
       mapbox_api_key: <mapbox token>

6. (Optional) Superset starts up to port 8099 by default. If you need to modify it, please modify the port configuration in the gunicorn_config.py file under the ./conf folder. ::

     $ vi conf/gunicorn_config.py

7. Start Superset, The first start Supuerset will update the metadata and takes a few minutes. ::

     $ bin/bootstrap.sh start

8. Stop Superset ::

     $ bin/bootstrap.sh stop


Upgrade Kyligence Insight for Superset
======================================
1. Backup metadata and configuration files ::

     $ cp [Superset installation directory]/superset.db [Backup destination folder]/superset.db

     $ cp [Superset installation directory]/conf/insight.default.yaml  [Backup destination folder]/insight.default.yaml 

2. Stop Application ::

     $ [Superset installation directory]/bin/bootstrap.sh stop


3. Uninstall Application ::

     $ [Superset installation directory]/bin/bootstrap.sh uninstall

4. Delete the entire Insight directory ::

     $ rm -rf [Superset installation directory]

5. Download the new installation package and extract it , Enter the decompressed directory and set the current directory as the environment variable SUPERSET_HOME ::

     $ tar -xf [Package name]

     $ cd [Superset installation directory]

     $ export SUPERSET_HOME=`pwd`

6. Install the dependencies of the Superset ::

     $ bin/bootstrap.sh install [Linux distribution]

     e.g. :

     $ bin/bootstrap.sh install centos7

7. Put the metadata and configuration files back into the new installation directory ::

     $ cp -f [Backup destination folder]/superset.db  ./superset.db

     $ cp -f [Backup destination folder]/insight.default.yaml ./conf/insight.default.yaml


8. Start Application ::

     $ bin/bootstrap.sh start

9. Stop Superset ::

     $ bin/bootstrap.sh stop


If you encounter any problems while using, you can click on the link below **Create an issue** Send us your questions: https://github.com/Kyligence/Insight-for-Superset/issues

.. _`Kyligence Insight for Superset config file`: https://raw.githubusercontent.com/Kyligence/Insight-for-Superset/master/default.yaml
.. _`Kyligence Download Page`: http://download.kyligence.io/#/products


