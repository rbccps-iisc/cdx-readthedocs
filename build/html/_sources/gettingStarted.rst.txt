Getting Started
===============

This guide will help you to quickly get started with a single node instance of CDX and start publishing data from a device.

Prerequisite
------------

#. Install Docker ::

    sudo apt-get install docker

#. Add permission to user ::

    sudo usermod -a -G docker $USER

#. Add DNS to the file /etc/docker/daemon.json. If it does not exist, create one ::

    {"dns": ["8.8.8.8", "8.8.4.4"]}

#. Add DNS in /etc/default/docker file ::

    DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4"

#. Restart Docker ::

    service docker restart

#. Install python ::

    sudo apt-get install python

#. Install git ::

    sudo apt-get install git


CDX Installation
----------------

#. Clone CDX git repo ::

    git clone https://github.com/rbccps-iisc/ideam.git

CDX installation has a configuration file (ideam.conf), which details about the ports used by different services and also allows the user to configure the passwords that needs to be used for certain services during installation. By default, the password field in the config file is set to ?, which indicates the system to generate password during run-time ::

    cd ideam/
    vim ideam.conf
    make necessary changes

#. Install CDX ::

    cd ideam/
    ./instal


Registering your first device
-----------------------------
* Once CDX has installed you can now start registering devices with it. Let's create a simple test device for the sake of illustration::
      
      sh tests/create_entity.sh testStreetlight

* This will give you the details of the registration

  .. code-block:: JSON

   {
     "Registration": "success",
     "entityID": "teststreetlight",
     "apiKey": "EHQilai5cF_tNmWOwg-oiPdncmRPdfGCIhFHM85zDDW",
     "subscriptionEndPoint": "https://smartcity.rbccps.org/api/{version}/followid=teststreetlight",
     "accessEndPoint": "https://smartcity.rbccps.org/api/{version}/db?id=teststreetlight",
     "publicationEndPoint": "https://smartcity.rbccps.org/api/{version}/publish?id=teststreetlight",
     "resourceAPIInfo": "https://rbccps-iisc.github.io"
   }     

* You can now publish data from this device using::

     sh tests/publish.sh teststreetlight EHQilai5cF_tNmWOwg-oiPdncmRPdfGCIhFHM85zDDW
  
  This will publish ``{"body": "testdata"}`` to the exchange ``teststreetlight.protected``

* That's it! You can similarly register more devices and apps with the middleware.
