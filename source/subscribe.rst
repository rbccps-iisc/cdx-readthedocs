Subscribe
=========

* **Summary**: The subscribe API is used to get messages from a queue. This is a destructive action on the message as 
  it will no longer be available in the queue after subscription. This API is not streaming, i.e. as data arrives into the 
  queue it is not pushed to the subscribers. However, it needs to be polled regularly to check for new messages.

* **Endpoint**: ``https://localhost:8443/api/1.0.0/subscribe/<queue_name>/<msg_count>``

  +--------------+-------------------------------------+
  |  Field       | Description                         |
  +==============+=====================================+
  | <queue_name> | The queue from which the messages   |
  |              | need to be subscribed.              |
  +--------------+-------------------------------------+
  | <msg_count>  | The number of messages, in integer, |
  |              | to subscribe from the queue         |
  +--------------+-------------------------------------+

* **Method**: ``GET``

* **Required Headers**:

  +-----------------+-------------------------+
  |   Header Name   |      Description        |
  +=================+=========================+
  |     apikey      |  API key of the device  |
  +-----------------+-------------------------+

* **Example Request**::
  
   curl -X GET \
   https://localhost:8443/api/1.0.0/subscribe/streetlight/1 \
   -H 'apikey: pp1dGjKzsfHwVzK6g0nnVhR6fqnkKO-SVkXvasPXL6E'

* **Example Response**:
  
  .. code-block:: JSON
   
   [
    {
      "data": {
        "ambientLux": 10000,
        "power": "73.26",
        "caseTemp": "34.5"
       },
      "topic": "#",
      "from": "streetlight.protected"
    }
   ]

* **Possible error scenarios**:
  
   - ``Invalid authentication credentials``: Make sure you have provided the right API key
   - If the response is empty: Check if the queue is bound to the right exchange and that 
     the exchange is receiving data from a source.
