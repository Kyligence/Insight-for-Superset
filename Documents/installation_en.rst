Prerequisites
=============

This guide shows you how to get a quick start with Kyligence Insight for Superset. It assumes that you have already installed the Docker service. If you haven't installed it yet, you can refer the following links to install it.


* `Install Docker for Windows`_
* `Install Docker for Mac`_
* `Install Docker for CentOS`_

It also requires sign up for a `Kyligence Account`_, then you can activate Kyligence Insight for Superset for free.

If you want to use interactive map(base on MapBox), you also need to prepare a `Mapbox Token`_ which is optional if you don't use interactive map.


Quick Start
===========

**Note:** you would not be able to upgrade `Kyligence Insight for Superset` with quick start launch, because you don't have external metadata store configured.

1. As you've done all the preparations above, let us start Kyligence Insight for Superset with the following command ::

  $ docker run -it -p <local port>:8099 --name <container name> kyligence/superset-kylin:latest

  e.g. :

  $ docker run -it -p 8099:8099 --name superset-kylin kyligence/superset-kylin:latest

After executing the command successfully, you can type Ctrl+P and Ctrl+Q continuously, so that docker can run as a daemon process.

2. We need to create a superset default admin account ::

  $ docker exec -it superset-kylin bin/create-admin.sh

3. Now open a browser window and go to http://127.0.0.1:8099 You can login to Kyligence Insight for Superset by admin/admin.


Use MySQL as metadata store to start Kyligence Insight for Superset
===================================================================

In the quick start section above, we did not use an external database as the meta store of Kyligence Insight for Superset. If you want to operate it long run or upgrade it in the future, please setup an external database as the metadata store. In the following, we will use MySQL as an example to show you how to setup an external metadata store. 

1. Create a new file called 'insight.default.yaml', then copy the content in the config file mentioned above, so that we can make some config to bootstrap Superset. ::

  superset:
    sqlalchemy_database_uri: <SQLAlchemy DSN, if empty, superset will use SQLlite instead>
    sqllab_timeout: <SQLLab timeout>
    mapbox_api_key: <mapbox token>


2. (Optional) If you don't have a MySQL instance, you can use docker to start one. If you already have a MySQL service, you can skip this step. ::

     $ docker pull mysql:5.7
     $ docker run -itd -p <local port>:3306 -e MYSQL_ROOT_PASSWORD=<database password> -e MYSQL_DATABASE=<database name> --name <database container name> mysql:5.7

     e.g.:
     $ docker pull mysql:5.7
     $ docker run -itd -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=superset --name superset-db mysql:5.7

3. Get the latest version of Kyligence Insight for Superset image: ::

     $ docker pull kyligence/superset-kylin:latest

4. Prepare the MySQL connection string, so that Kyligence Insight for Superset can connect to the MySQL instance and store metadata there: ::

     mysql://<db username>:<db password>@<database host name>:<db port>/<database>

     ### If you are using MySQL started with Docker, then it is

     mysql://root:root@superset-db:3306/superset

5. Then we can launch the container of Kyligence Insight for Superset with the following: ::

     $ docker run -it -p <local port>:8099 \
     --link <database container name>:<database host name> \
     -v /<absloute path>/insight.default.yaml:/usr/local/superset/conf/insight.default.yaml \
     --name <container name> \
     kyligence/superset-kylin:latest

     ### If you are using MySQL started with Docker, then it is:

     $ docker run -it -p 8099:8099 \
     --link superset-db:superset-db \
     -v `pwd`/insight.default.yaml:/usr/local/superset/conf/insight.default.yaml \
     --name superset-kylin \
     kyligence/superset-kylin:latest

6. Follow the prompts to enter your Kyligence account credential, then you can start using Kyligence Insight for Superset. ::

     Welcome to Kyligence Insight for Superset!
     In order to activate your evaluation, you need to login with your Kyligence Account.

     If you do not have a Kyligence Account, please register at:
     https://account.kyligence.io/#/extra-signup?lang=en&source=superset

     To learn more about the activation, please refer to following URL:
     http://kyligence.io/zh/2018/07/11/kyligence-insight-for-superset-big-data-visualization/

     Please enter account: username

     Please enter password: password

7. The local port 8099 should be open for Kyligence Insight for Superset service, you can verify it with the docker ps command. ::

     $ docker ps -a
     ONTAINER ID        IMAGE                             COMMAND                  CREATED             STATUS                            PORTS                    NAMES
     3b059d2723cb        kyligence/superset-kylin:latest   "bootstrap.sh"           2 days ago          Up 3 seconds (health: starting)   0.0.0.0:8099->8099/tcp   superset-kylin

You can type Ctrl+P and Ctrl+Q continuously to make docker run as a daemon process.

8. We need to create a superset default admin account ::

  $ docker exec -it superset-kylin bin/create-admin.sh


default.yaml Paramaters
=========================

============================= ============================================
key                              comments
============================= ============================================
mapbox_api_key                  Mapbox API token
sqlalchemy_database_uri         Superset metadata DSN
sqllab_timeout                  SQLLab timeout(second)
============================= ============================================


Upgrade
========

If you use Docker to run Kyligence Insight for Superset, the upgrade is super simple, just stop and remove the original container and open new one. ::

  docker rm -f superset-kylin
  docker pull kyligence/superset-kylin:latest

Then follow step #4 in the section **Use MySQL as metadata store to start Kyligence Insight for Superset** to start container again.

**Note**: you would not be able to upgrade `Kyligence Insight for Superset` with quick start launch, because you don't have external metadata store configured.

If you encounter any problems , you can **create a issue** at the following link. Give us feedback: https://github.com/Kyligence/Insight-for-Superset/issues


.. _`Kyligence Account`: https://account.kyligence.io/#/extra-signup?lang=en&source=superset
.. _`Install Docker for Windows`: https://docs.docker.com/docker-for-windows/install/
.. _`Install Docker for Mac`: https://docs.docker.com/docker-for-mac/install/
.. _`Install Docker for CentOS`: https://docs.docker.com/install/linux/docker-ce/centos/
.. _`Mapbox Token`: https://www.mapbox.com/help/how-access-tokens-work/
.. _`Kyligence Insight for Superset config file`: https://raw.githubusercontent.com/Kyligence/Insight-for-Superset/master/insight.default.yaml
