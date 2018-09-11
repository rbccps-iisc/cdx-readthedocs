CDX Subsystems
==============

CDX consist of the following systems:

#. **Authenticator and API gateway** : A system which is the entry point for users of the CDX. It authenticates users and if successful connects users to the appropriate microservice inside the CDX.
#. **Data broker** : The main system of CDX which allows users to publish and subscribe data in a secure fashion. This provides the interface to access live data being exchanged with the CDX.
#. **Catalog** : The service which provides the user with a list of devices/apps currently connected to the CDX. It also provides other meta-information such as the data format in which messages are subscribed/published by the device/app.
#. **Database** : The system which stores the historic data.
#. **AAA server** : The system which authenticates and authorizes users.
#. **Video server** : A system which acts as a broker for videos in a smart-city.
#. **Identity manager** : A system which is responsible for providing credentials and maintaining identity of CDX users.
#. **Certificate authority** : A system which provides certificates for CDX users.
#. **Log server** : A system which monitors logs from various system in the CDX. These logs are collected to detect or prevent any intrusions.
#. **IDPS** : The intrusion detection and prevention system, which analyzes the logs produced by the log server and takes appropriate actions to detect/prevent potential intrusions.

More details about the sub-systems can be found in the following sections 

.. toctree::
   :maxdepth: 2

   catalog
   iotdataexchange
   mediadataexchange
