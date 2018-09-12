Catalog
-------

The information resource catalog is one of the key components of the CDX stack. It contains a list of data resources and their descriptions in a machine readable format. The resource descriptions may include API endpoints, and other meta-data like access hints, ownership, providers, structure of data, e.g., list of parameters and their descriptions etc. A useful analogy is the online shopping catalog, where a consumer can browse through available products, their features, reviews etc. and then decide to purchase a subscription or a copy of them. The resource catalog plays a similar role for the clients wishing to use the smart city resources and, as additional benefit, it can help nucleate the development of a new data/digital economy.


Key services offered by resource catalog are: 

#. Secure, authenticated, open API based 

   - Discovery of information sources
   - Addition/Modification of meta-data for new/existing resources
   - Semantic search over resource meta-data

#. API framework supporting

   - Filtering of query results (For example, sorting, access modifier based filtering, specific field based filtering etc.)
   - Grouping



As an example, Hypercat is a recent alliance which has developed a standard for a catalogue under the British Standards Institution (PAS212).  It is a lightweight, JSON based hypermedia catalogue format for exposing a collection of Uniform Resource Identifiers (URI) for IoT assets. The interactions with the catalogue use REST APIs over HTTP and the catalogue items are stored as RDF-like triples. RDF triples are essentially of the form “Subject, Predicate, Object” and can be used to encode relationships and hence provide a way to link the data/device parameters to external concepts. This will enable creating appropriate metadata for the devices that can then provide the right context and semantics for analysing the data from the IoT device. The framework allows a lot of flexibility in defining new annotations for new devices or information sources. In addition, Hypercat also advocates a few different search APIs, with a key one based on geographic indices. Another important feature in Hypercat is the possibility of having links to other catalogues. This is to enable federated/distributed growth of IoT resources which will be a very desirable property.


Data Schemas
^^^^^^^^^^^^
From the above, it is clear that the resource meta-data is the key element that enables data interoperability. However, this is possible only if the meta-data is described with a common vocabulary which is unambiguous and free from semantic conflicts.

Open data schemas from all data sources (and actuators) needs to be developed to enable data interoperability. Key desirable features of data schemas are:

#. Flexibility to accommodate diverse nature of underlying data sources
#. Describable in both human and machine-readable formats
#. Should be accompanied by a rich set of tools to create, modify and validate schema data
#. Should be extensible, allowing for easy enhancement

There are many online repositories for schemas like json-schema.org  (for schema templates in JSON), www.oneiota.org for some data schemas for some IoT devices. In addition, projects like FiWare have also proposed schemas. We need to adapt and extend existing schemas (and develop new ones if they do not exist), to meet the needs for the IoT devices (and other data resources) for the Indian Smart Cities. As an example, we have discussed (and made publicly available) examples of schemas for  street light and power meter.

Recently, Open Connectivity Foundation, which is an international consortium of companies and some academic institutions, has developed data schemas for many IoT devices.  The schemas are based on “JSON Schemas”. We find JSON-Schemas to be a better way to describe the metadata than that proposed in Hypercat as there are open-source tools readily available that allow schema creation, integrity checking of the schemas etc. (Essentially, JSON-schema allows a simple grammar to be defined and hence it is easy to check schemas against that). This will be particularly  important when one wants “user-contributed” schema development and deployment. 

We recommend combining the best features of Hypercat (API based access to catalogue, with powerful search capabilities), and OCF (JSON-Schema based information description to enable integrity checking). We believe that the structures proposed in OCF can be further extended as described next. 

As in OCF, we recommend to use JSON schemas to define the structure of each entry in the resource catalog. The schemas define specific fields to be included in the metadata for a given class of devices. Apart from mandating the inclusion of certain fields, there exist provisions to include (optional) device/vendor specific fields, e.g., links to reference ontologies, additional device information, usage hints etc., which enhances the usability of data by third party applications. The schemas are further used to validate the catalog entries at the time of on-boarding the device using the easily available json-schema validation tools.

Towards defining the structure of catalog items, we propose to organize the metadata into following categories: 
        - Static information: General information about the device/information resource, e.g., geo-location, type of device, ID, tags etc.
        - Message sub-schemas: Meta-information for the various types of messages that the device/resource cand send or receive. Access to these messages can be provisioned based on individual message types. Examples include, but are not limited to, the following message types:

                - Observation messages:  Sensed parameters etc. 
                - Control messages: Actuation parameters accepted by the device, e.g., control inputs etc. 
                - Configuration messages: Configuration parameters of the device, e.g., sampling rates, sleep times etc.
                - Management messages: Messages related to Device management.
                - JSON-RPC messages and responses.			

Of course the above message types could be further extended in the future. 

A key idea is to store  dynamic meta-information within a catalog entry as a JSON-schema itself. Thus, the metadata becomes an actionable specification that can be used to dynamically validate various messages  being sent from/to the device (see Figure 1).

.. image:: catalog_validation.png
    :width: 800px
    :align: center
    :height: 500px
    :alt: alternate text

Figure 1: A device schema in the catalog is validated against a global-meta-schema. Each data item coming from/to the device is further validated by the embedded schemas in the device schema. /cat is the API endpoint for the Information Resource Catalog in the CDX  stack.


We give an example of a schema entry in the catalog for a smart streetlight ::

    {
      "refCatalogueSchema": "generic_iotdevice_schema.json",
      "id": "70b3d58ff0031de5",
      "tags": [
        "Onstreet",
        "streetlight",
        "Energy",
        "still under development!"
      ],
      "refCatalogueSchemaRelease": "0.1.0",
      "latitude": {
        "value": 13.0143335,
        "ontologyRef": "http://www.w3.org/2003/01/geo/wgs84_pos#"
      },
      "longitude": {
        "value": 77.5678424,
        "ontologyRef": "http://www.w3.org/2003/01/geo/wgs84_pos#"
      },
      "owner": {
        "name": "Indian Institute of Science",
        "Id": "IISC", 
        "website": "http://www.iisc.ac.in"
      },
      "provider": {
        "name": "Robert Bosch Centre for Cyber Physical Systems, IISc",
        "Id": "RBCCPS",
        "website": "http://rbccps.org"
      },
      "geoLocation": {
        "address": "80 ft Road, Bangalore, 560012"
      },
     "data_schema": {
    "type": "object",
    "properties": {
        "observation_msg": {
            "type": "object",
            "direction": "from-device",
            "accessModifier": "public",
            "tags": [
              "on street",
               "energy"
            ],
            "properties": {
               "dataSamplingInstant": {
                 "type": "string",
                 "description": "Sampling Time in UTC format",
                 "units": "seconds"
               },
               "caseTemperature": {
                 "type": "number",
                 "description": "Temperature of the device casing",
                 "units": "degreeCelsius"
               },
               "powerConsumption": {
                 "type": "number",
                 "description": "Power consumption of the device",
                 "units": "watts"
               },
               "luxOutput": {
                 "type": "number",
                 "description": "lux output of LED measured at LED",
                 "units": "lux"
               },
               "ambientLux": {
                 "type": "number",
                 "description": "lux value of ambient",
                 "units": "lux"
               }
            },
            "additionalProperties": false
        },
        "setpoints_msg": {
            "type": "object",
            "direction": "from-device",
            "accessModifier": "protected",
            "tags": [
               "on street",
               "energy",
               "control"
            ],
            "properties": {
                "targetPowerState": {
                  "type": "string",
                  "enum": [
                    "ON",
                    "OFF"
                  ]
                },
                "targetBrightnessLevel": {
                  "type": "number",
                  "description": "Number between 0 to 100 to indicate the percentage brightness level.”,
                  "units": "percent"
                },
                "targetControlPolicy": {
                  "enum": [
                    "AUTO_TIMER",
                    "AUTO_LUX",
                    "MANUAL"
                  ],
                  "description": "Indicates which of the behaviours the device is currently set to. AUTO_TIMER is timer based, AUTO_LUX uses ambient light and MANUAL is controlled by app. Writeable only allowed for authorized apps"
                },
                "targetAutoTimerParams": {
                  "type": "object",
                  "properties": {
                    "targetOnTime": {
                      "type": "number",
                      "description": "Indicates time of day in seconds from 12 midnight when device turns ON in AUTO_TIMER.”,
                      "units": "seconds"
                    },
                    "targetOffTime": {
                      "type": "number",
                      "description": "Indicates time of day in seconds from 12 midnight when device turns OFF in AUTO_TIMER.”,
                      "units": "seconds"
                    }
                  }
                },
                "targetAutoLuxParams": {
                  "type": "object",
                  "properties": {
                    "targetOnLux": {
                      "type": "number",
                      "description": "Indicates ambient lux when device turns ON in AUTO_LUX.”,
                      "units": "lux"
                    },
                    "targetOffLux": {
                      "type": "number",
                      "description": "Indicates ambient lux when device turns OFF in AUTO_LUX.”,
                      "units": "lux"
                    }
                  }
                }
            },
            "additionalProperties": false
        }
      },
        "control_msg": {
            "type": "object",
            "direction": "to-device",
            "accessModifier": "protected",
            "tags": [
               "on street",
               "energy",
               "control"
            ],
            "properties": {
                "targetPowerState": {
                  "type": "string",
                  "enum": [
                    "ON",
                    "OFF"
                  ],
                  "description": "If set to ON, turns ON the device. If OFF turns OFF the device. Writeable parameter. Writeable only allowed for authorized apps"
                },
                "targetBrightnessLevel": {
                  "type": "number",
                  "description": "Number between 0 to 100 to indicate the percentage brightness level. Writeable only allowed for authorized apps",
                  "units": "percent"
                },
                "targetControlPolicy": {
                  "enum": [
                    "AUTO_TIMER",
                    "AUTO_LUX",
                    "MANUAL"
                  ],
                  "description": "Indicates which of the behaviours the device should implement. AUTO_TIMER is timer based, AUTO_LUX uses ambient light and MANUAL is controlled by app. Writeable only allowed for authorized apps"
                },
                "targetAutoTimerParams": {
                  "type": "object",
                  "properties": {
                    "targetOnTime": {
                      "type": "number",
                      "description": "Indicates time of day in seconds from 12 midnight when device turns ON in AUTO_TIMER. Writeable only allowed for authorized apps",
                      "units": "seconds"
                    },
                    "targetOffTime": {
                      "type": "number",
                      "description": "Indicates time of day in seconds from 12 midnight when device turns OFF in AUTO_TIMER. Writeable only allowed for authorized apps",
                      "units": "seconds"
                    }
                  }
                },
                "targetAutoLuxParams": {
                  "type": "object",
                  "properties": {
                    "targetOnLux": {
                      "type": "number",
                      "description": "Indicates ambient lux when device turns ON in AUTO_LUX. Writeable only allowed for authorized apps",
                      "units": "lux"
                    },
                    "targetOffLux": {
                      "type": "number",
                      "description": "Indicates ambient lux when device turns OFF in AUTO_LUX. Writeable only allowed for authorized apps",
                      "units": "lux"
                    }
                  }
                }
            },
            "additionalProperties": false
        }
      },
      "oneOf": [
        {"required": [ "observation_msg" ] },{"required": [ "control_msg" ]},{"required": [ "setPoint_msg" ] }
      ]
    }
    }


Figure 2: Example catalogue schema for a smart streetlight

There are two portions to the above schema, highlighted by the two shades. The first (in green shading) pertains to static information. The second part (light blue shaded) provides meta-information about various message types the device receives/sends. In the above example, the streetlight device has three messages:
observation_msg: Observations made by the streetlight (caseTemperature, ambientLux etc.). This message flows “from-device” as is indicated by the keyword “direction”. For example, the streetlight measures “caseTemperature” which is a number and it describes the temperature of the light casing and its units are “degreeCelcius”. 


Control parameters for this device (targetPowerState, targetBrightnessLevel etc.). This message flows “to-device” as is indicated by the keyword “direction”. For example, the parameter “targetPowerState” can be used to switch ON (and OFF) the streetlight. This parameter is a dimensionless quantity.
setPoint parameters for this device (targetPowerState, targetBrightnessLevel etc.). This message flows “from-device” as is indicated by the keyword “direction”. It indicates the values of writeable parameters which may have been set to certain values using control messages.

The structure for streetlight catalog item is defined by the base schema ”generic_iotdevice_schema.json”.  This information is contained within the static information part of the item using the json fields, namely  “refCatalogueSchema” and “refCatalogueSchemaRelease”. To enable format validation of an uploaded catalog item, it should mandatorily mention the name of reference schema files and the schema release numbers.


.. image:: catalog_message_validation.png
    :width: 800px
    :align: center
    :height: 500px
    :alt: alternate text

Figure 3: Streetlight observation and control data


To highlight the validation features of the catalog,  we present an example of the observation, setPoint (up-arrow) and control (down arrow) data packets for the streetlight device in Figure 3. A key point is that, the observation schema which is stored in catalog (e.g., see the example streetlight item above), can be directly used to validate the incoming observation packets. The same applies to the control packets in the reverse direction.


Another important field in the above example is the “ontologyRef” field included within “latitude” and “longitude” fields. This field provides a reference to a site where further explanation as to the meaning/semantics of the “key” can be found. For example, a website explicitly created to hold the ontology (dictionary) for that IoT device parameters in a standard ontology language (for example RDF).


We recommend that an Indian City specific dictionary/ontology be created and which contains semantic descriptions of things which are unique to Indian cities and hence not available in other existing ontologies. The dictionary as well as the catalogue should be ideally made available in all Indian languages.
The catalogue can be accessed and searched via HTTP(S) commands and hence will be accessible from anywhere in the web.
We advocate a resource catalogue be a part of every smart city middleware instance and it adheres to a standard schema as well as an API format for querying.


