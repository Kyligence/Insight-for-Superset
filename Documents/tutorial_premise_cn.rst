先决条件
========

该引导给您介绍如何快速启动Kyligence Insight for Superset. 

1.其假设您已经安装了Docker服务. 如果还没有安装可以下载Docker安装包并安装：

* `Install Docker for Windows`_
* `Install Docker for Mac`_
* `Install Docker for Linux`_

2.需要在 `Kyligence下载页`_ 下载 Supserset 镜像

3.需要下载一下 `Kyligence Insight for Superset配置文件`_ (或者新建一个default.yaml文件，拷贝链接内的内容到新文件), 以便配置Superset各种启动参数.

4.(可选项)如果您想使用MapBox交互式地图服务, 还需要准备一个 `Mapbox Token`_ 

5.当然您还需要知道Kyligence/Kylin主机名和端口, 这个可以询问Kyligence/Kylin集群管理员.


修改配置文件
============

找到下载的default.yaml文件, 根据自己环境进行配置 ::

  superset:
    sqlalchemy_database_uri: <SQLAlchemy DSN, 如果留空会用文件数据库作为元数据库>
    sqllab_timeout: <SQLLab超时时间>
    mapbox_api_key: <mapbox token>
    kap_host: <填入Kylin主机名或者IP>
    kap_port: <Kylin 端口>
    kap_endpoint: /kylin/api
    kap_api_version: v1

快速上手
========

**特别注意** , 如果您用 **快速上手** 章节启动的Kyligence Insight for Superset, 您是无法升级的. 因为您的元数据没有做外部存储.

到default.yaml 所在目录执行如下命令, 启动Kyligence Insight for Superset! ::
  
  $ tar -zvxf  superset-kylin.tar.gz

  $ docker load --input superset-kylin.tar

  $ docker run -it -p <本地端口>:8088 -v /<绝对路径>/default.yaml:/usr/local/superset/data/default.yaml --name <容器名称> kyligence/superset-kylin:premises

  例如:
  $ docker run -it -p 8088:8088 -v `pwd`/default.yaml:/usr/local/superset/data/default.yaml --name superset-kylin kyligence/superset-kylin:premises

启动成功后请连续使用组合键ctrl+p, ctrl+q, 以便docker做为后台进程运行.

现在打开浏览器访问http://127.0.0.1:8088 , 使用Kylin的用户名和密码即可登录Kyligence Insight for Superset.


使用MySQL作为元数据启动Kyligence Insight for Superset
=====================================================

在前面的快速上手部分, 我们没有使用外部数据库作为Kyligence Insight for Superset的元数据库, 如果您为了版本升级或运维方便, 请您使用外部数据库作为Kyligence Insight for Superset的元数据库, 现在以MySQL为例示范如何使用MySQL作为Kyligence Insight for Superset的元数据库.


1. 准备一个MySQL的连接字符串, 以便Kyligence Insight for Superset使用MySQL元数据, 并且把这个字符串填入default.yaml中 ::

     mysql://<db username>:<db password>@<db host>:<db port>/<database>

2. 到default.yaml所在目录执行如下命令, 启动Kyligence Insight for Superset! ::
    
     $ tar -zvxf  superset-kylin.tar.gz

     $ docker load --input superset-kylin.tar

     $ docker run -it -p <本机端口>:8088 \
     --link <db container name>:<db container name> \
     -v /<绝对路径>/default.yaml:/usr/local/superset/data/default.yaml \
     --name <容器名称> \
     kyligence/superset-kylin:premises

     ### 如果您是使用先前Docker启动的MySQL, 那么启动容器命令为:
     $ tar -zvxf  superset-kylin.tar.gz

     $ docker load --input superset-kylin.tar

     $ docker run -it -p 8088:8088 \
     --link superset-db:superset-db \
     -v `pwd`/default.yaml:/usr/local/superset/data/default.yaml \
     --name superset-kylin \
     kyligence/superset-kylin:premises

5. 现在本地8088端口已经开启了一个Kyligence Insight for Superset服务了, 可以通过docker ps -a 来验证Kyligence Insight for Superset容器是否正常启动 ::

     $ docker ps -a
     ONTAINER ID        IMAGE                             COMMAND                  CREATED             STATUS                            PORTS                    NAMES
     3b059d2723cb        kyligence/superset-kylin:premises   "bootstrap.sh"           2 days ago          Up 3 seconds (health: starting)   0.0.0.0:8088->8088/tcp   superset-kylin

启动成功后请连续使用组合键ctrl+p, ctrl+q, 以便docker做为后台进程运行.


default.yaml 配置
==================

============================= ============================================
key                              comments
============================= ============================================
kap_host                        Kylin host
----------------------------- --------------------------------------------
kap_port	                      Kylin port
----------------------------- --------------------------------------------
kap_endpoint	                  Kylin API prefix
----------------------------- --------------------------------------------
kap_api_version                 Kylin API version <v1|v2>
----------------------------- --------------------------------------------
mapbox_api_key                  Mapbox API token
----------------------------- --------------------------------------------
sqlalchemy_database_uri         Superset metadata DSN
----------------------------- --------------------------------------------
sqllab_timeout                  SQLLab timeout(second)
============================= ============================================


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


升级方式
========

如果您使用Docker部署的Kyligence Insight for Superset, 升级操作很简单, 只需要停止原容器, 再开启新容器即可 ::

  docker rm -f superset-kylin

然后下载新的Superset安装包，再按照 **使用MySQL作为元数据启动Kyligence Insight for Superset** 中第2步, 开启Docker服务即可.

**特别注意**: 如果您用 **快速上手** 章节启动的Kyligence Insight for Superset, 您是无法升级的. 因为您的元数据没有做外部存储.

用如果您在使用时遇到任何问题，可在如下链接 **创建一个issue** 将问题反馈给我们：https://github.com/Kyligence/Insight-for-Superset/issues


.. _`Install Docker for Windows`: https://store.docker.com/editions/community/docker-ce-desktop-windows
.. _`Install Docker for Mac`: https://store.docker.com/editions/community/docker-ce-desktop-mac
.. _`Install Docker for Linux`: https://download.docker.com/linux/
.. _`Mapbox Token`: https://www.mapbox.com/help/how-access-tokens-work/
.. _`Kyligence Insight for Superset配置文件`: https://raw.githubusercontent.com/Kyligence/Insight-for-Superset/master/default.yaml
.. _`Kyligence下载页`: http://download.kyligence.io/#/products


