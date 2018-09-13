Guide
=====

This guide will help you understand the internals and operations of the CDX system.

CDX Configuration 
-----------------

Once we are done with setting up CDX, the configuration file ``ideam.conf`` will updated with the generated passwords for sub-systems ::

   [APIGATEWAY]
   https = 8443

   [BROKER]
   http = 12080
   management = 12081
   amqp = 12082
   mqtt = 12083

   [ELASTICSEARCH]
   elastic = 9200
   kibana = 13081

   [WEBSERVER]
   http = 14080

   [LDAP]
   ldap = 15389

   [CATALOGUE]
   http = 16080

   [KONGA]
   http = 17080

   [VIDEOSERVER]
   rtmp = 18935
   hls = 18080
   http = 18088

   [PASSWORDS]
   ldap = 721UD9ytc1Qc4ORT
   broker = 0Rv7MxG2uLsB2bgq
   cdx.admin = 0BsZmPezYrjbqS2CmYjtiP6ZfJfoKg4k
   database = 9SWhSOyVHHpIBrYDTI613o0YdCclVXc0MlG75y1VGfx

CDX Subsystems
--------------

As explained earlier, CDX consists of multiple subsystems such as APIGateway, Data Broker, Media Broker, IoT Database, Authentication, Authorization and Accounting system etc. 

In this section, we will have detailed usage guide for every subsystem. Let us first understand if all the subsystems are live and operating in the respective ports as per the config file provided. This can be verified by using the docker command ::

    docker ps 

Which gives us the list of live containers running in the system as follows ::

    CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                                                                                    NAMES
    18e3864c3a46        pantsel/konga         "/app/start.sh"          18 minutes ago      Up 17 minutes       127.0.0.1:17080->1337/tcp                                                                                konga
    80a390e62081        ideam/videoserver     "/usr/sbin/sshd -D"      18 minutes ago      Up 18 minutes       22/tcp, 0.0.0.0:18935->1935/tcp, 0.0.0.0:18080->8080/tcp, 0.0.0.0:18088->8088/tcp                        videoserver
    8ed4e4b96ef6        ideam/ldapd           "/usr/sbin/sshd -D"      18 minutes ago      Up 18 minutes       22/tcp, 127.0.0.1:15389->8389/tcp                                                                        ldapd
    67f990e9213c        ideam/webserver       "/bin/sh -c 'tail -f…"   18 minutes ago      Up 18 minutes       127.0.0.1:14080->8080/tcp                                                                                webserver
    47e9730f4184        ideam/elasticsearch   "/usr/sbin/sshd -D"      18 minutes ago      Up 18 minutes       22/tcp, 127.0.0.1:9200->9200/tcp, 127.0.0.1:13081->5601/tcp                                              elasticsearch
    a3099a939d50        ideam/broker          "/bin/sh -c 'tail -f…"   18 minutes ago      Up 18 minutes       0.0.0.0:12083->1883/tcp, 0.0.0.0:12082->5672/tcp, 127.0.0.1:12080->8000/tcp, 127.0.0.1:12081->15672/tcp   broker
    98af3aa5c65f        ideam/catalogue       "/root/run.sh /usr/s…"   19 minutes ago      Up 18 minutes       22/tcp, 27017/tcp, 28017/tcp, 127.0.0.1:16080->8000/tcp                                                  catalogue
    306fd29f57c3        ideam/apigateway      "/docker-entrypoint.…"   19 minutes ago      Up 19 minutes       8000-8001/tcp, 8444/tcp, 0.0.0.0:8443->8443/tcp                                                          apigateway

Each container is mapped to a specific port of the system to expose the APIs and services offered. If you look at the PORTS column, we have ``PORT 8443`` of apigateway container mapped to ``0.0.0.0:8443``. This exposes all the APIs offered by CDX to be accessed from external system. If we look at webserver, ``PORT 8080`` is mapped to ``127.0.0.1:14080``. This exposes the services offered by the webserver to be accessed only from CDX system.   

In order to login to the specific container to view logs or for debugging, CDX provides shell access. The scripts for it is available in ``ideam/shells`` ::

    ls shells/
    apigateway*  broker*  catalogue*  elasticsearch*  ldapd*  videoserver*  webserver*

For example, to login into webserver, you can execute the following ::

    shells/webserver

Now you are in webserver container. To exit the container use ``CTRL + D``

If you have already registered the test device as explained in the Getting Started section you can skip this step. If not, let us now register a device and observe the sequence of events that happen in each subsystem. 

To register a device run the ``create_entity.sh`` script ``tests`` directory with the ID ``testStreetlight``::

    sh tests/create_entity.sh testStreetlight


In the following subsections, we will observe the impact of registering ``testStreetlight`` 


API Gateway
^^^^^^^^^^^

Broker
^^^^^^

Catalog
^^^^^^^

Database
^^^^^^^^

AAA Server
^^^^^^^^^^

Web Server
^^^^^^^^^^
