该引导给您介绍如何在离线环境下快速启动 Kyligence Insight for Superset

目前支持的Linux发行版
===================
* SUSE Linux Enterprise Server 11 SP4 x86_64 (64-bit)
* CentOS release 7 (64-bit)
* CentOS release 6 (64-bit)

注：
需要用户获得安装机器的Linux发行版信息，用于后续安装过程。
如果您使用离线方式部署,MapBox相关可视化将无法使用,因为其运行需要访问外网。

安装Kyligence Insight for Superset
==================================
1.首先在 `Kyligence下载页`_ 下载 Supserset 安装包

2.解压安装包::

           $ tar -xf [安装包文件名]

             如:

           $ tar -xf Insight-Linux-x86_64-0.10.2.tar.gz

3.进入解压后的目录，并设置当前所在目录为环境变量 SUPERSET_HOME::

           $ export SUPERSET_HOME=`pwd`

4.开始安装Superset的依赖项::

           $ bin/bootstrap.sh install [Linux发行版]

             如:

           $ bin/bootstrap.sh install centos7

5.修改./conf文件夹下的Superset的配置文件::

           $ vi conf/insight.default.yaml 

找到下载的insight.default.yaml文件, 根据自己环境进行配置 ::

  superset:
    sqlalchemy_database_uri: <SQLAlchemy DSN, 如果留空会用文件数据库作为元数据库>
    sqllab_timeout: <SQLLab超时时间(秒)>
    mapbox_api_key: <mapbox token>
    kap_host: <填入Kylin主机名或者IP>
    kap_port: <Kylin 端口>
    kap_endpoint: /kylin/api
    kap_api_version: v1


6.(可选项) Superset启动时默认占用8099端口，如果需要修改，请修改./conf文件夹下的gunicorn_config.py 文件中的端口配置 :: 
            
          $ vi conf/gunicorn_config.py
 
7.启动Superset ::

          $ bin/bootstrap.sh start
 
升级 Kyligence Insight for Superset
===================================
1.备份元数据及配置文件 ::

          $ cp [Superset安装目录]/superset.db [备份目标文件夹]/superset.db

          $ cp [Superset安装目录]/conf/insight.default.yaml  [备份目标文件夹]/insight.default.yaml 

2.停止应用 ::

          $ [Superset安装目录]/bin/bootstrap.sh stop


3.卸载应用 ::

          $ [Superset安装目录]/bin/bootstrap.sh uninstall

4.删除整个Insight目录 ::

          $ rm -rf [Superset安装目录]

5.下载新的安装包并解压,进入解压后的目录，并设置当前所在目录为环境变量 SUPERSET_HOME::

           $ export SUPERSET_HOME=`pwd`

6.开始安装Superset的依赖项 ::

          $ bin/bootstrap.sh install [Linux发行版]

             如:

          $ bin/bootstrap.sh install centos7

7.将元数据及配置文件放回到新的安装目录下 ::

          $ cp -f [备份目标文件夹]/superset.db ./superset.db

          $ cp -f [备份目标文件夹]/insight.default.yaml ./conf/insight.default.yaml 


8.启动应用 ::

          $ bin/bootstrap.sh start


Kyligence Insight for Superset使用
==================================

如果您按照向导部署Kyligence Insight for Superset, 那么现在已经可以通过浏览器访问 http://127.0.0.1:8088 打开Kyligence Insight for Superset

1. 请直接使用Kylin账户和密码登录Kyligence Insight for Superset

   .. image:: images/Insight_login_cn.png

2. 点击 Refresh Kylin Cubes，同步Kylin的cube

   .. image:: images/Insight_refresh_cn.png

3. 点击 Kylin Cubes，列出可供查询的cube

   .. image:: images/Insight_list_cubes_cn.png

4. 点击 需要查询的Cube的名称，即可直接查询 Cube

   .. image:: images/Insight_explore_cn.png

5. 在SQL实验室 中使用SQL自由查询

   .. image:: images/Insight_SQLLab_cn.png


用如果您在使用时遇到任何问题，可在如下链接 **创建一个issue** 将问题反馈给我们：https://github.com/Kyligence/Insight-for-Superset/issues



.. _`Kyligence Insight for Superset配置文件`: https://raw.githubusercontent.com/Kyligence/Insight-for-Superset/master/insight.default.yaml
.. _`Kyligence下载页`: http://download.kyligence.io/#/products


