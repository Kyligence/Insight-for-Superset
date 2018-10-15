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
1. 首先在 `Kyligence下载页`_ 下载 Supserset 安装包

2. 解压安装包::

     $ tar -xf [安装包文件名]

     如:

     $ tar -xf Insight-Linux-x86_64-0.12.0.tar.gz

3. 进入解压后的目录，并设置当前所在目录为环境变量 SUPERSET_HOME::

     $ cd [解压后的目录名]

     $ export SUPERSET_HOME=`pwd`
     
     如:
     
     $ cd Insight-Linux-x86_64-0.12.0

     $ export SUPERSET_HOME=`pwd`

4. 安装Superset, 安装时会创建默认用户admin, 密码admin的superset账户::

     $ bin/bootstrap.sh install [Linux发行版]

     如:

     $ bin/bootstrap.sh install centos7

5. 修改./conf文件夹下的Superset的配置文件::

     $ vi conf/insight.default.yaml

   根据自己环境进行配置insight.default.yaml文件 ::

     superset:
       sqlalchemy_database_uri: <SQLAlchemy DSN, 如果留空会用文件数据库作为元数据库>
       sqllab_timeout: <SQLLab超时时间(秒)>
       mapbox_api_key: <mapbox token>
  
6. (可选项) Superset启动时默认占用8099端口，如果需要修改，请修改./conf文件夹下的gunicorn_config.py 文件中的端口配置 ::

   $ vi conf/gunicorn_config.py

7. 启动Superset, 首次启动会需要几分钟的时间来更新元数据  ::

     $ bin/bootstrap.sh start

8. 停止Superset ::

     $ bin/bootstrap.sh stop

升级 Kyligence Insight for Superset
===================================
1. 备份元数据及配置文件 ::

     $ cp [Superset安装目录]/superset.db [备份目标文件夹]/superset.db

     $ cp [Superset安装目录]/conf/insight.default.yaml  [备份目标文件夹]/insight.default.yaml 

2. 停止应用 ::

     $ [Superset安装目录]/bin/bootstrap.sh stop


3. 卸载应用 ::

     $ [Superset安装目录]/bin/bootstrap.sh uninstall

4. 删除整个Insight目录 ::

     $ rm -rf [Superset安装目录]

5. 下载新的安装包并解压,进入解压后的目录，并设置当前所在目录为环境变量 SUPERSET_HOME::

     $ tar -xf [安装包文件名]

     $ cd [解压后的目录名]

     $ export SUPERSET_HOME=`pwd`

6. 开始安装Superset的依赖项 ::

     $ bin/bootstrap.sh install [Linux发行版]

     如:

     $ bin/bootstrap.sh install centos7

7. 将元数据及配置文件放回到新的安装目录下 ::

     $ cp -f [备份目标文件夹]/superset.db ./superset.db

     $ cp -f [备份目标文件夹]/insight.default.yaml ./conf/insight.default.yaml 


8. 启动Superset ::

     $ bin/bootstrap.sh start

9. 停止Superset ::

     $ bin/bootstrap.sh stop


用如果您在使用时遇到任何问题，可在如下链接 **创建一个issue** 将问题反馈给我们：https://github.com/Kyligence/Insight-for-Superset/issues



.. _`Kyligence Insight for Superset配置文件`: https://raw.githubusercontent.com/Kyligence/Insight-for-Superset/master/insight.default.yaml
.. _`Kyligence下载页`: http://download.kyligence.io/#/products


