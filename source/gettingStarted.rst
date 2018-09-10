Getting Started
===============

This guide will help you to quickly get started with a single node instance of CDX and start publishing data from a device.

Installation
------------
* Clone the project using::

      git clone https://github.com/rbccps-iisc/ideam && cd ideam
* Make sure you have docker installed (`Link <https://docs.docker.com/v17.12/install/>`_)
* Run::
      
      ./install

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
