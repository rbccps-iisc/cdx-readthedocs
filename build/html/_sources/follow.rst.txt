Follow
======

* **Summary**: The follow API is a data exchange enabling API that is used to express interest in another entity's data. It could either be for reading the data, or writing, or b  oth. It is time-bound and the requestor has to explicitly mention the duration for which they would like to the data. Once a follow request is made, it goes to the 
  <device>.follow queue of the owner's device. The owner can then review the request and issue a ``/share``, thereby approving the follow request.

* **Endpoint**: ``https://localhost:8443/api/1.0.0/follow``

* **Method**: ``POST``

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
  |    entityID     | Name of the entity which the requestor is interested in |
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
  |                 | Example: 10D for 10 days, 1Y  for 1 Year and so on      |
  +-----------------+---------------------------------------------------------+
  |  requestorID    | Name of the requesting device                           |
  +-----------------+---------------------------------------------------------+

* **Example Request**::
  
   curl -X POST \
   https://localhost:8443/api/1.0.0/follow \
   -H 'Content-Type: application/json' \
   -H 'apikey: ko6A9npXespXwyK85mtfCfmHSDLFYJZMOxScjk9iUJy' \
   -d 
   '{
        "entityID": "device1",
        "permission":"read", 
        "validity": "10D",
        "requestorID":"device2"
    }'

* **Example Response**:

  .. code-block:: JSON
   
   {"status":"Follow request has been made to device1 with permission read at 2018-09-10T09:42:57.226Z"}

* **Possible error scenarios**:
  
   - ``Invalid authentication credentials`` : Make sure you have provided the right API key
   - ``Possible missing fields``: The fields required in the body, as given above, are not all present according to the format. 
