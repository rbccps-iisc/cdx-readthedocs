Publish
=======

* **Summary**: The publish API is used to publish data from devices to the middleware. To access this API, the device API key obtained after device registration must be used.
  Published messages go into the specified exchange of the device. There are 6 exchanges and 4 queues assigned to a device. They are as follows:

  +-------------------------+-------------------------+
  |        Exchanges        | Queues                  |
  +=========================+=========================+
  | <device_name>.configure | <device_name>           |
  +-------------------------+-------------------------+
  | <device_name>.follow    | <device_name>.configure |
  +-------------------------+-------------------------+
  | <device_name>.notify    | <device_name>.follow    |
  +-------------------------+-------------------------+       
  | <device_name>.public    | <device_name>.notify    |
  +-------------------------+-------------------------+
  | <device_name>.protected | <device_name>.priority  |
  +-------------------------+-------------------------+
  | <device_name>.private   |                         |
  +-------------------------+-------------------------+

  Some of the exchanges are pre-bound to queues for convenience. They are as follows:

  +-------------------------+-------------------------+
  |       Exchange          |      Bound Queue        |
  +=========================+=========================+
  | <device_name>.configure | <device_name>.configure |
  +-------------------------+-------------------------+
  | <device_name>.follow    | <device_name>.follow    |
  +-------------------------+-------------------------+
  | <device_name>.notify    | <device_name>.notify    |
  +-------------------------+-------------------------+

  This is just a default setting and can be changed anytime by the device administrator.

* **Endpoint**: ``https://localhost:8443/api/1.0.0/publish/<exchange_name>`` Here <exchange_name> specifies the exchange to which the message must be published to.

* **Method**: ``POST``

* **Required Headers**:

  +-----------------+-------------------------+
  |   Header Name   |      Description        |
  +=================+=========================+
  |     apikey      |  API key of the device  |
  +-----------------+-------------------------+

* **Optional Headers**:

  +------------------+-------------------------------------------------+
  |   Header Name    |                Description                      |
  +==================+=================================================+
  |   routingKey     |   Topic to which the published message belongs  |
  +------------------+-------------------------------------------------+

* **Body**: The message from the device that conforms to the schema specified during registration

* **Example Request**::
  
   curl -X POST \
   https://localhost:8443/api/1.0.0/publish/streetlight.protected \
   -H 'Content-Type: application/json' \
   -H 'apikey: yJv7sxFginCYPHq4v4ji-XTLP-Ya0stwAaGGkYuwgrw' \
   -H 'routingKey: #' \
   -d '{
         "ambientLux": "10000",
         "power": "73.26",
         "caseTemp": 34.5
       }'

* **Response**: ``200 OK``
  
  Unless the API key is wrong, this endpoint will not throw any errors. For the sake of security and speed, any publish message will give back a ``200 OK`` but it may or 
  may not have reached its intended destination.
