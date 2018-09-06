Prerequisites
========

This guide shows you how to get a quick start with Kyligence Insight for Superset. 

1.It assumes that you have already installed the Docker service. If you haven't installed it yet, you can refer the following links to download the installation package and install:

* `Install Docker for Windows`_
* `Install Docker for Mac`_
* `Install Docker for Linux`_

2.Need to download Supserset image in `Kyligence Download Page`_ .

3.And then you need to download this file `Kyligence Insight for Superset config file`_ (or you can just create a file called 'default.yaml' locally,  then copy the content in the config file mentioned above), so that we can make some config to bootstrap Superset.

4.(Optional)If you want to use interactive map(base on MapBox), you also need to prepare a `Mapbox Token`_ which is optional if you don't use interactive map.

5.ou will also need to know the hostname and port of Kylin instance. The administrator of Kylin cluster should be able to provide you this information.


Modify default.yaml
===================
Go to the config file you have download(or created) above, and modify it due to your environment. ::

  superset:
    sqlalchemy_database_uri: <SQLAlchemy DSN, if empty, superset will use SQLlite instead>
    sqllab_timeout: <SQLLab timeout>
    mapbox_api_key: <mapbox token>
    kap_host: <Kylin hostname or IP>
    kap_port: <Kylin port>
    kap_endpoint: /kylin/api
    kap_api_version: v1

Quick Start
===========

**Note:** you would not be able to upgrade `Kyligence Insight for Superset` with quick start launch, because you don't have external metadata store configured.

As you've done all the preparations above, let us start Kyligence Insight for Superset with the following command ::
  

  $ tar -zvxf  superset-kylin.tar.gz

  $ docker load --input superset-kylin.tar

  $ docker run -it -p <local port>:8088 -e -v /<absloute path>/default.yaml:/usr/local/superset/data/default.yaml --name <container name> kyligence/superset-kylin:premises


  e.g. go the directory where default.yaml locate, then run :

  $ docker run -it -p 8088:8088 -v `pwd`/default.yaml:/usr/local/superset/data/default.yaml --name superset-kylin kyligence/superset-kylin:premises


After executing the command successfully, you can type Ctrl+P and Ctrl+Q continuously, so that docker can run as a daemon process.

Now open a browser window and go to http://127.0.0.1:8088. You can log in to Kyligence Insight for Superset with the same username and password you use to access Kylin.


Use MySQL as metadata store to start Kyligence Insight for Superset
=====================================================

In the quick start section above, we did not use an external database as the meta store of Kyligence Insight for Superset. If you want to operate it long run or upgrade it in the future, please setup an external database as the metadata store. In the following, we will use MySQL as an example to show you how to setup an external metadata store. 


1. Prepare the MySQL connection string, so that Kyligence Insight for Superset can connect to the MySQL instance and store metadata there: ::

     mysql://<db username>:<db password>@<db host>:<db port>/<database>

2. Run the following command in the directory where default.yaml is located to start Kyligence Insight for Superset! ::
    
     $ tar -zvxf  superset-kylin.tar.gz

     $ docker load --input superset-kylin.tar

     $ docker run -it -p <local port>:8088 \
     --link <database>:<database> \
     -v /<absloute path>/default.yaml:/usr/local/superset/data/default.yaml \
     --name superset-kylin \
     kyligence/superset-kylin:premises

     e.g. go the directory where default.yaml locate, then run :

     $ docker run -it -p 8088:8088 \
     --link superset-db:superset-db \
     -v `pwd`/default.yaml:/usr/local/superset/data/default.yaml \
     --name superset-kylin \
     kyligence/superset-kylin:premises

5. The local port 8088 should be open for Kyligence Insight for Superset service, you can verify it with the docker ps command. ::

     $ docker ps -a
     ONTAINER ID        IMAGE                             COMMAND                  CREATED             STATUS                            PORTS                    NAMES
     3b059d2723cb        kyligence/superset-kylin:premises   "bootstrap.sh"           2 days ago          Up 3 seconds (health: starting)   0.0.0.0:8088->8088/tcp   superset-kylin

You can type Ctrl+P and Ctrl+Q continuously to make docker run as a daemon process.


default.yaml Paramaters
=======================

============================= ============================================
key                              comments
============================= ============================================
kap_host                        Kylin host
----------------------------- --------------------------------------------
kap_port                        Kylin port
----------------------------- --------------------------------------------
kap_endpoint                    Kylin API prefix
----------------------------- --------------------------------------------
kap_api_version                 Kylin API version <v1|v2>
----------------------------- --------------------------------------------
mapbox_api_key                  Mapbox API token
----------------------------- --------------------------------------------
sqlalchemy_database_uri         Superset metadata DSN
----------------------------- --------------------------------------------
sqllab_timeout                  SQLLab timeout(second)
============================= ============================================


How to use Kyligence Insight for Superset
=========================================

Once you start Kyligence Insight for Superset, you can start a browser window to access its user interface.

1. Login with Kylin username and password

   .. image:: images/Insight_login_en.png

2. Click Kylin Refresh to synchronize cubes in Kylin

   .. image:: images/Insight_refresh_en.png

3. Click Kylin Cubes to list all available cubes

   .. image:: images/Insight_list_cubes_en.png

4. Click the name of a cube, you can start query the cube

   .. image:: images/Insight_explore_en.png

5. Edit and run your query in SQL Lab

   .. image:: images/Insight_SQLLab_en.png


Upgrade
========

If you use Docker to run Kyligence Insight for Superset, the upgrade is super simple, just stop and remove the original container and open new one. ::

  docker rm -f superset-kylin

Then Download new superset package follow step #2 in the section **Use MySQL as metadata store to start Kyligence Insight for Superset** to start container again.

**Note**: you would not be able to upgrade `Kyligence Insight for Superset` with quick start launch, because you don't have external metadata store configured.

If you encounter any problems , you can **create a issue** at the following link. Give us feedback: https://github.com/Kyligence/Insight-for-Superset/issues



.. _`Install Docker for Windows`: https://store.docker.com/editions/community/docker-ce-desktop-windows
.. _`Install Docker for Mac`: https://store.docker.com/editions/community/docker-ce-desktop-mac
.. _`Install Docker for Linux`: https://download.docker.com/linux/
.. _`Mapbox Token`: https://www.mapbox.com/help/how-access-tokens-work/
.. _`Kyligence Insight for Superset config file`: https://raw.githubusercontent.com/Kyligence/Insight-for-Superset/master/default.yaml
.. _`Kyligence Download Page`: http://download.kyligence.io/#/products


