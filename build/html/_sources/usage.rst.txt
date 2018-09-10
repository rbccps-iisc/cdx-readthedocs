Usage
=====

The following workflow will attempt to illustrate the typical usage of the smart city stack.

#. Consider that two devices have registered with the middleware viz. "streetlight" and "app" 
   The API keys obtained are as follows:
   
   For the streetlight

   .. code-block:: JSON

    {
      "Registration": "success",
      "entityID": "streetlight",
      "apiKey": "ReiHIzTA6hQRbv3JO2gRHP9iEh4NzK-bBSl-J0GKJZo",
      "subscriptionEndPoint": "https://smartcity.rbccps.org/api/{version}/follow?id=streetlight",
      "accessEndPoint": "https://smartcity.rbccps.org/api/{version}/db?id=streetlight",
      "publicationEndPoint": "https://smartcity.rbccps.org/api/{version}/publish?id=streetlight",
      "resourceAPIInfo": "https://rbccps-iisc.github.io"
    }

   For the app

   .. code-block:: JSON
 
    {
      "Registration": "success",
      "entityID": "app",
      "apiKey": "7KfqcDOPvz3JECUwwGsQYuTdKtyGTQTpLDaZjIbJpMt",
      "subscriptionEndPoint": "https://smartcity.rbccps.org/api/{version}/follow?id=app",
      "accessEndPoint": "https://smartcity.rbccps.org/api/{version}/db?id=app",
      "publicationEndPoint": "https://smartcity.rbccps.org/api/{version}/publish?id=app",
      "resourceAPIInfo": "https://rbccps-iisc.github.io"
    }

#. Now consider that the device ``app`` is interested in ``streetlight`` s data. 
