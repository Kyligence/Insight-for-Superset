先决条件
========

该引导给您介绍如何快速启动Kyligence Insight for Superset. 其假设您已经安装了Docker服务. 如果还没有安装可以去参考

* `Install Docker for Windows`_
* `Install Docker for Mac`_
* `Install Docker for CentOS`_

需要注册一下 `Kyligence Account`_ 账户, 以便您免费激活Kyligence Insight for Superset.

最后需要下载一下 `Kyligence Insight for Superset配置文件`_ (或者新建一个insight.default.yaml文件，拷贝链接内的内容到新文件), 以便配置Superset各种启动参数.

如果您想使用MapBox交互式地图服务, 还需要准备一个 `Mapbox Token`_ (可选项)

当然您还需要知道Kylin主机名和端口, 这个可以询问Kylin集群管理员.


修改配置文件
============

找到下载的insight.default.yaml文件, 根据自己环境进行配置 ::

  superset:
    sqlalchemy_database_uri: <SQLAlchemy DSN, 如果留空会用文件数据库作为元数据库>
    sqllab_timeout: <SQLLab超时时间>
    mapbox_api_key: <mapbox token>

快速上手
========

**特别注意** , 如果您用 **快速上手** 章节启动的Kyligence Insight for Superset, 您是无法升级的. 因为您的元数据没有做外部存储.

到default.yaml所在目录执行如下命令, 启动Kyligence Insight for Superset! ::

  $ docker run -it -p <本地端口>:8099 -v /<绝对路径>/insight.default.yaml:/usr/local/superset/conf/insight.default.yaml --name <容器名称> kyligence/superset-kylin:latest

  例如:
  $ docker run -it -p 8099:8099 -v `pwd`/insight.default.yaml:/usr/local/superset/conf/insight.default.yaml --name superset-kylin kyligence/superset-kylin:latest

启动成功后请连续使用组合键ctrl+p, ctrl+q, 以便docker做为后台进程运行.

我们还需要创建一个superset默认的admin账户 ::

   $ docker exec -it superset-kylin bin/create-admin.sh

现在打开浏览器访问http://127.0.0.1:8099 , 使用admin/admin即可登录Kyligence Insight for Superset.


使用MySQL作为元数据启动Kyligence Insight for Superset
=====================================================

在前面的快速上手部分, 我们没有使用外部数据库作为Kyligence Insight for Superset的元数据库, 如果您为了版本升级或运维方便, 请您使用外部数据库作为Kyligence Insight for Superset的元数据库, 现在以MySQL为例示范如何使用MySQL作为Kyligence Insight for Superset的元数据库.

1. (可选项)如果您没有MySQL服务, 可以使用docker启动一个MySQL服务, 如果您已经有了MySQL服务那么这步可以跳过 ::

     $ docker pull mysql:5.7
     $ docker run -itd -p <local port>:3306 -e MYSQL_ROOT_PASSWORD=<database password> -e MYSQL_DATABASE=<database name> --name <container name> mysql:5.7 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci

     例如:
     $ docker pull mysql:5.7
     $ docker run -itd -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=superset --name superset-db mysql:5.7 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci

2. 获取Kyligence Insight for Superset镜像最新版 ::

     $ docker pull kyligence/superset-kylin:latest

3. 准备一个MySQL的连接字符串, 以便Kyligence Insight for Superset使用MySQL元数据, 并且把这个字符串填入default.yaml中 ::

     mysql://<db username>:<db password>@<db container name>:<db port>/<database>

     ### 如果您是使用先前Docker启动的MySQL, 那么这个字符串就为

     mysql://root:root@superset-db:3306/superset

4. 到default.yaml所在目录执行如下命令, 启动Kyligence Insight for Superset! ::

     $ docker run -it -p <本机端口>:8099 \
     --link <db container name>:<db container name> \
     -v /<绝对路径>/insight.default.yaml:/usr/local/superset/conf/insight.default.yaml \
     --name <容器名称> \
     kyligence/superset-kylin:latest

     ### 如果您是使用先前Docker启动的MySQL, 那么启动容器命令为:

     $ docker run -it -p 8099:8099 \
     --link superset-db:superset-db \
     -v `pwd`/insight.default.yaml:/usr/local/superset/conf/insight.default.yaml \
     --name superset-kylin \
     kyligence/superset-kylin:latest

5. 按照提示输入您的Kyligence Account账户和密码, 以便免费使用Kyligence Insight for Superset ::

     Welcome to Kyligence Insight for Superset!
     In order to activate your evaluation, you need to login with your Kyligence Account.

     If you do not have a Kyligence Account, please register at:
     https://account.kyligence.io/#/extra-signup?lang=en&source=superset

     To learn more about the activation, please refer to following URL:
     http://kyligence.io/zh/2018/07/11/kyligence-insight-for-superset-big-data-visualization/

     Please enter account: 输入KyAccount账户
     Please enter password: 输入KyAccount密码


6. 现在本地8099端口已经开启了一个Kyligence Insight for Superset服务了, 可以通过docker ps -a 来验证Kyligence Insight for Superset容器是否正常启动 ::

     $ docker ps -a
     ONTAINER ID        IMAGE                             COMMAND                  CREATED             STATUS                            PORTS                    NAMES
     3b059d2723cb        kyligence/superset-kylin:latest   "bootstrap.sh"           2 days ago          Up 3 seconds (health: starting)   0.0.0.0:8099->8099/tcp   superset-kylin

启动成功后请连续使用组合键ctrl+p, ctrl+q, 以便docker做为后台进程运行.

7. 我们还需要创建一个superset默认的admin账户 ::

   $ docker exec -it superset-kylin bin/create-admin.sh


insight.default.yaml 配置
==========================

============================= ============================================
key                              comments
============================= ============================================
mapbox_api_key                  Mapbox API token
sqlalchemy_database_uri         Superset metadata DSN
sqllab_timeout                  SQLLab timeout(second)
============================= ============================================


Kyligence Insight for Superset使用
==================================

如果您按照向导部署Kyligence Insight for Superset, 那么现在已经可以通过浏览器访问 http://127.0.0.1:8099 打开Kyligence Insight for Superset

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
  docker pull kyligence/superset-kylin

然后再按照 **使用MySQL作为元数据启动Kyligence Insight for Superset** 中第4步, 开启Docker服务即可.

**特别注意**: 如果您用 **快速上手** 章节启动的Kyligence Insight for Superset, 您是无法升级的. 因为您的元数据没有做外部存储.

用如果您在使用时遇到任何问题，可在如下链接 **创建一个issue** 将问题反馈给我们：https://github.com/Kyligence/Insight-for-Superset/issues


.. _`Kyligence Account`: https://account.kyligence.io/#/extra-signup?lang=en&source=superset
.. _`Install Docker for Windows`: https://docs.docker.com/docker-for-windows/install/
.. _`Install Docker for Mac`: https://docs.docker.com/docker-for-mac/install/
.. _`Install Docker for CentOS`: https://docs.docker.com/install/linux/docker-ce/centos/
.. _`Mapbox Token`: https://www.mapbox.com/help/how-access-tokens-work/
.. _`Kyligence Insight for Superset配置文件`: https://raw.githubusercontent.com/Kyligence/Insight-for-Superset/master/insight.default.yaml


