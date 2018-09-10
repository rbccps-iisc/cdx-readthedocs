Unshare
=======

* **Summary**: The unshare API is used to revoke the permissions given to a device. This deletes the ``share`` entry from LDAP and unbinds the queue if bound.
  This API can be used by the owner's device when the data lease time of the requesting device has expired, or the owner for some reason deems that the requestor
  is no longer eligible for their data.
  
* **Endpoint**: ``https://localhost:8443/api/1.0.0/share``

* **Method**: ``DELETE``

* **Required Headers**:

  +-----------------+-------------------------+
  |   Header Name   |      Description        |
  +=================+=========================+
  |     apikey      |  API key of the device  |
  +-----------------+-------------------------+

* **Body**: The body must contain certain specific fields as mentioned below:

  +-----------------+---------------------------------------------------------+
  |      Field      |      Description                                        |
  +=================+=========================================================+
  |    entityID     | Name of the owner's entity                              |
  +-----------------+---------------------------------------------------------+
  |   permission    | Can be any of:                                          |
  |                 |   - ``read``                                            |
  |                 |   - ``write``                                           |
  |                 |   - ``read-write``                                      |
  +-----------------+---------------------------------------------------------+
  |    validity     | Of the form <Integer><Metric>                           |
  |                 |                                                         |
  |                 | Metric can be any of:                                   |
  |                 |   - ``Y``: Year                                         |
  |                 |   - ``M``: Month                                        |
  |                 |   - ``D``: Day                                          |
  |                 |                                                         |
  |                 | Example: 10D for 10 days, 1Y for 1 year and so on       |
  +-----------------+---------------------------------------------------------+
  |  requestorID    | Name of the requesting device                           |
  +-----------------+---------------------------------------------------------+

* **Example Request**::
  
   curl -X DELETE \
   https://localhost:8443/api/1.0.0/share \
   -H 'Content-Type: application/json' \
   -H 'apikey: ko6A9npXespXwyK85mtfCfmHGVLFYJZMOxScjk9iUJy' \
   -d 
   '{
        "entityID": "device1",
        "permission":"read", 
        "validity": "10D",
        "requestorID":"device2"
    }'

* **Example Response**::
 
   Successfully unshared from device2

  
* **Possible error scenarios**:
  
   - ``Invalid authentication credentials`` : Make sure you have provided the right API key
   - ``Possible missing fields``: The fields required in the body, as given above, are not all present according to the format. 
