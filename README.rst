How to install
==============

Preconditions
-------------

* OSX/Linux
* Docker service ready
* Sign up KyAccount

Notice: Docker downloads from here: https://docs.docker.com/install/overview/

Install step
------------

1. Get and start Mysql image::

     ~ $ docker pull mysql:5.7
     ~ $ docker run -itd -e MYSQL_ROOT_PASSWORD=<database password> -e MYSQL_DATABASE=<database name> --name <container name> mysql:5.7

     Example:
     ~ $ docker pull mysql:5.7
     ~ $ docker run -itd -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=superset --name superset-db mysql:5.7

2. Get and start Docker image::

     ~ $ docker pull kyligence/superset-kylin:<version tag>

     Example:
     ~ $ docker pull kyligence/superset-kylin:latest


3. Start Superset by passing some environment variables::

     ~ $ docker run -it -p <host port>:8088 \
     -e KAP_HOST=<hostname> \
     -e SQLALCHEMY_DATABASE_URI=<database DSN> \
     --link <database container name>:superset-db \
     --name <container name> \
     kyligence/superset-kylin:<version tag>

     Example:
     ~ $ docker run -it -p 8088:8088 \
     -e KAP_HOST=sandbox-dong.chinaeast.cloudapp.chinacloudapi.cn \
     -e SQLALCHEMY_DATABASE_URI=mysql://root:root@superset-db/superset \
     --link superset-db:superset-db \
     --name superset-kylin \
     kyligence/superset-kylin:latest

     Welcome to Superset-Kylin! In order to activate your evaluation,
     you need to login with your Kyligence Account. To learn more about
     the activation, please refer to following URL:
     http://kyligence.io/xxxxx

     For any questions, please contact us from http://kyligence.io

     Please enter account: <Enter KyAccount account>
     Please enter password: <Enter KyAccount password>
     starting gunicorn...

     [2018-06-27 05:43:56 +0000] [11] [INFO] Starting gunicorn 19.8.0
     [2018-06-27 05:43:56 +0000] [11] [INFO] Listening at: http://0.0.0.0:8088 (11)
     [2018-06-27 05:43:56 +0000] [11] [INFO] Using worker: sync
     [2018-06-27 05:43:56 +0000] [15] [INFO] Booting worker with pid: 15
     [2018-06-27 05:43:56 +0000] [16] [INFO] Booting worker with pid: 16
     Loaded your LOCAL configuration at [/etc/superset/superset_config.py]
     Loaded your LOCAL configuration at [/etc/superset/superset_config.pyc]
     Registering blueprint: 'one'
     Registering blueprint: 'one'

     Press ctrl+p, ctrl+q(use the escape sequence), detach docker container


Start environments:

============================= ============== ============================================
environment                    default         comments
============================= ============== ============================================
KAP_HOST                        sandbox        Kylin host
----------------------------- -------------- --------------------------------------------
KAP_PORT	                    7070           Kylin port
----------------------------- -------------- --------------------------------------------
KAP_ENDPOINT	                /kyiln/api     Kylin API prefix
----------------------------- -------------- --------------------------------------------
KAP_API_VERSION                 v1             Kylin API version <v1|v2>
----------------------------- -------------- --------------------------------------------
MAPBOX_API_KEY                  NULL           Mapbox API token
----------------------------- -------------- --------------------------------------------
SQLALCHEMY_DATABASE_URI         NULL           Superset metadata DSN
============================= ============== ============================================

Notice:

* SQLALCHEMY_DATABASE_URI: <driver>://<username>:<password>@<hostname>/<database>
* Get Mapbox Token from here: https://www.mapbox.com/help/how-access-tokens-work/

4. Open http://localhost:8088,  login Superset,  the login username/password are the corresponding username/password of sandbox-dong.

5. Sync Cube, Source → Refresh Kylin

.. image:: https://github.com/Kyligence/Insight-for-Superset/raw/master/images/sync-cubes.png

6. Query Cube, Source → Kylin Cubes

.. image:: https://github.com/Kyligence/Insight-for-Superset/raw/master/images/list-cubes.png

