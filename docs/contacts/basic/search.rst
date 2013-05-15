.. _contacts-search-ref:

===============
Search contacts
===============

.. _advanced-search-ref:

Advanced search query syntax
----------------------------

Query language for Advanced search is JSON encoded structure.

Short example of querying all persons with skype “john.doe”:

.. code-block:: javascript

    {
       "and": [
           {
               "skype id": {
                   "is": "john.doe",
                }
           },
           {
               "record type": {
                   "is": "person"
               }
           }
       ]
    }

For more examples, see :ref:`examples <advanced-search-examples>`.

Terminology
~~~~~~~~~~~

Based on example above, let’s define basic terminology:

**and**     
    is join operator for occurrences
    
**skype id** (``john.doe``)
    is a term to search by

**is** 
    is occurrence of term in search index

**record_type** (``person``)
    is a value for occurrence

Joins
~~~~~
Possible variants for join operators are ``and`` and ``or``. They could be combined in different ways and priorities. Some examples with explanations will be listed below.

Let’s define several occurrences:

.. code-block:: javascript

    o1 = {
        "skype id": {
            "is": "john.doe"
        }
    };

    o2 = {
            "record type": {
                "is": "person"
            }
    },

    o3 = {
        "first name": {
            "contain": "John"
        }
    },

    o4 = {
        "created": {
            "range": {
                "start_date": "2012-02-13",
                "end_date": "2012-02-23",
            }
        }
    }

Join like o1 and o2 and o3 and o4::

    {
       "and": [o1, o2, o3, o4]
    }

Join like (o1 and o2) or o3 and o4::

    {
       "and": [o4, {"or": [o3, {"and": [ o1, o2 ] } ] } ]
    }

Join like (o1 and o2) or (o3 and o4)::

    {
       "or": [{"and": [ o1, o2 ] }, {"and": [ o3, o4 ] }]
    }

.. note::
    Maximum limit of occurrences in one request query is 11; If request could be done without join operators — then it should contain only single occurrence.

Search operators
----------------
.. list-table:: Full list of available search operators
   :widths: 5 15 15
   :header-rows: 1

   * - Operator
     - Description
     - Example
.. _advanced_search_contain_occurrence:
   * - contain
     - performs left match on ANY word in the text string
     - Some of words in provided search request(one or more) for specified field is equal to some word(one or more)
       in field of contact(contacts).
       This contacts will be returned as result of search request.
       .. note::
           As more equal words in request are in contact field as higher contact is in returned list if
           :ref:`sorting is by relevance in descending order`.
   * - contain(old)
     - Provided value matches field value from left or right side. For example ``*document_value`` or
       ``document_value*``. But not both.
       Note: ``old`` means only another approach to ger right results, API parameters is still same.
     - ``{"first name": {"contain": "aaa"}}``
   * - is
     - Provided value is equal to field value
     - ``{"record type": {"is": "all"}}``
   * - is_empty
     - Feild value with specified name is absent or empty
     - ``{"last name": {"is_empty": True}}``
   * - in_the_last
     - Date field value of matched documents is within last X days/weeks/monthes
     - ``{"created": {"in_the_last": {"unit": "day", "quantity": 2}}}``
   * - range
     - Date field value of matched documents is within specified period
     - ``{"company last contacted": {"range": {"start_date": "2013-03-19", "end_date": "2013-03-19"}}}``
   * - gt
     - Field value with specified name have lower value than provided in the search criteria
     - ``{"rating": {"gt": "3"}}``
   * - lt
     - Field value with specified name have greater value than provided in the search criteria
     - ``{"rating": {"gt": "3"}}``
   * - gte
     - Field value with specified name have lower or equal value than provided in the search criteria
     - ``{"rating": {"gte": "3"}}``
   * - lte
     - Field value with specified name have greater or equal value than provided in the search criteria
     - ``{"rating": {"lte": "3"}}``

.. _search-fields-list:

Available search fields
-----------------------
.. list-table:: Full list of available field types for searching on them
   :widths: 7 15
   :header-rows: 1

   * - Field name
     - Possible operators
   * - email
     - ``is``, ``is_not``, ``contain(old)``, ``not_contain(old)``, ``is_empty``
   * - skype id
     - ``is``, ``is_not``, ``contain(old)``, ``not_contain(old)``, ``is_empty``
   * - twitter
     - ``is``, ``is_not``, ``contain(old)``, ``not_contain(old)``, ``is_empty``
   * - linkedin
     - ``is``, ``is_not``, ``contain(old)``, ``not_contain(old)``, ``is_empty``
   * - facebook
     - ``is``, ``is_not``, ``contain(old)``, ``not_contain(old)``, ``is_empty``
   * - phone
     - ``is``, ``is_not``, ``contain(old)``, ``not_contain(old)``, ``is_empty``
   * - last name
     - ``is``, ``is_not``, ``contain(old)``, ``not_contain(old)``, ``is_empty``
   * - street
     - ``is``, ``is_not``, ``contain``, ``not_contain``, ``is_empty``
   * - city
     - ``is``, ``is_not``, ``contain``, ``not_contain``, ``is_empty``
   * - state
     - ``is``, ``is_not``, ``contain``, ``not_contain``, ``is_empty``
   * - zip
     - ``is``, ``is_not``, ``contain``, ``not_contain``, ``is_empty``
   * - country
     - ``is``, ``is_not``, ``contain``, ``not_contain``, ``is_empty``
   * - company name
     - ``is``, ``is_not``, ``contain``, ``not_contain``, ``is_empty``
   * - title
     - ``is``, ``is_not``, ``contain``, ``not_contain``, ``is_empty``
   * - name
     - ``is``, ``is_not``, ``contain(old)``, ``not_contain``
   * - first name
     - ``is``, ``is_not``, ``contain(old)``, ``not_contain``
   * - lead source
     - ``is``, ``is_not``, ``is_empty``
   * - lead type
     - ``is``, ``is_not``, ``is_empty``
   * - lead status
     - ``is``, ``is_not``, ``is_empty``
   * - rating
     - ``is``, ``is_not``, ``is_empty``, ``gt``, ``lt``, ``lte``, ``gte``
   * - created
     - ``in_the_last``, ``range``
   * - updated
     - ``in_the_last``, ``range``
   * - company last contacted
     - ``in_the_last``, ``range``
   * - address
     - ``contain``, ``not_contain``, ``is_empty``
   * - tag
     - ``is``
   * - custom_fields
     - ``is``, ``is_not``, ``contain``, ``not_contain``, ``is_empty``
   * - record type
     - ``is``
   * - description
     - ``contain``, ``not_contain``, ``is_empty``
   * - saved_search
     - ``is``

Saved Advanced Searches
~~~~~~~~~~~~~~~~~~~~~~~
Query language allows to specify as occurrence other (previously saved) search query. You can combine saved search occurrences in a way as regular occurrences are used. Explanation example is provided bellow.

Let’s assume we have saved search query like:

.. code-block:: javascript

    {
        "or": [{
            "description": {
                "is_empty": true
            }
        }, {
            "twitter": {
                "contain": "jondoe"
            }
        }]
    }

This saved search has id 4fc886dc682c4a64dd060062 in database (detailed information about saved searches :ref:`API endpoints<saved_search_api>` section).

To use previously saved search we need to construct next query:

.. code-block:: javascript

    {
        "and": [{
            "skype id": {
                "is": "john.doe"
            }
        }, {
            "saved_search": {
                "is": "4fc886dc682c4a64dd060062"
            }
        }]
    }


And it will be expanded (on server) to:

.. code-block:: javascript

    {
        "and": [{
            "skype id": {
                "is": "john.doe"
            }
        }, {
            "or": [{
                "description": {
                    "is_empty": true
                }
            }, {
                "twitter": {
                    "contain": "jondoe"
                }
            }]
        }]
    }


.. note::
    Number of occurrences is still under the rule of maximum limit of occurrences in one request query is 11.
    Occurrences will be counted through expanded query. Query can also contain only reference to saved search without joins and additional occurrences.
    

.. _advanced-search-examples:    

More search examples
~~~~~~~~~~~~~~~~~~~~
Search all contacts with specified type::

    {"record type": {"is": "person"}}
    
Search contacts with name, containing "Gal" and tagged with specific tag:

.. code-block:: javascript

    {
        "and": [{
            "first name": {
                "contain": "Gal"
            }
        }, {
            "tag": {
                "is": "csv import2"
            }
        }]
    }

Search for contacts without values in `city` field::

    {"city": {"is_empty": False}}


Search for contacts, created in given date range:

.. code-block:: javascript

    {
        "created": {
            "range": {
                "start_date": "2012-10-16",
                "end_date": "2012-10-18"
            }
        }
    }

Search for specific value in custom field::

    {"custom_fields": {"custom field1": {"is": "value"}}}

.. note:: 
    If your custom field is ``select-box``, in search you should specify not it's value, but id of this value. For example, if you have field with following values:
    
    .. code-block:: javascript
    
        "values": [
            {
                "id": "1",
                "value": "Open"
            },
            {
                "id": "2",
                "value": "Closed"
            }
        ]
    
    You should use ``2`` as value, if you want to find contacts with field equal to ``closed``. For example::

        {"custom_fields": {"comminication state": {"is": "2"}}}

Validation
~~~~~~~~~~
To validate join operators, occurrences and values we’re using `"Json Schema" <http://json-schema.org/>`_ standard. Current implementation of rules is built with json-schema `Draft 3 <http://tools.ietf.org/html/draft-zyp-json-schema-03>`_. Please, use this draft for better understanding of query language rules.

In Nimble we’re using `json-schema <https://github.com/Julian/jsonschema>`_ python library to validate user search queries.

Also, on github you can find the library from one of the json-schema authors `json-schema-validator <https://github.com/fge/json-schema-validator>`_. It's fully implementing draft 3 spec, and can be used as reference library.

Top level validation schema

.. code-block:: javascript

    {
    	"additionalProperties": false,
    	"patternProperties": {
    		"^(email|skype id|twitter|linkedin|facebook|phone|last name|title|description|street|city|state|zip|country|lead type|company name|custom_fields|name|first name|lead source|created|address|tag|or|and|record type|saved_search)$": {
    			"required": true,
    			"type": "object"
    		}
    	},
    	"type": "object",
    	"description": "top level (all fields) validation rule"
    }

Joins validation schema

.. code-block:: javascript

    {
    	"additionalProperties": false,
    	"patternProperties": {
    		"^(or|and)$": {
    			"minItems": 2,
    			"type": "array"
    		}
    	},
    	"type": "object"
    }
    
Schema for validation of default fields occurrences

.. code-block:: javascript

    {
    	"patternProperties": {
    		"^(email|skype id|twitter|linkedin|facebook|phone|last name|street|city|state|zip|country|company name|title)$": {
    			"additionalProperties": false,
    			"patternProperties": {
    				"^(is|is_not|contain|not_contain|is_empty)$": {
    					"minLength": 2,
    					"required": true,
    					"type": ["string", "boolean"]
    				}
    			},
    			"type": "object"
    		}
    	},
    	"type": "object",
    	"description": "/twitter/linkedin/facebook/phone/last name/street/city/state/zip/country/company name/title validation rule"
    }

Schema for validation of full name/first name fields

.. code-block:: javascript

    {
    	"patternProperties": {
    		"^(name|first name)$": {
    			"additionalProperties": false,
    			"patternProperties": {
    				"^(is|is_not|contain|not_contain)$": {
    					"minLength": 2,
    					"required": true,
    					"type": "string"
    				}
    			},
    			"type": "object"
    		}
    	},
    	"type": "object",
    	"description": "name/first name validation rules. name == first name + last name"
    }

Schema for validation of lead source/lead type field

.. code-block:: javascript

    {
    	"type": "object",
    	"description": "lead source/lead type validation rules",
    	"patternProperties": {
    		"^(lead source|lead type)$": {
    			"additionalProperties": false,
    			"patternProperties": {
    				"^(is|is_not|is_empty)$": {
    					"required": true,
                        "type": ["string", "boolean"]
    				}
    			},
    			"type": "object"
    		}
    	}
    }

Schema for validation of created occurrences

.. code-block:: javascript

    {
        "type": "object",
        "description": "created validation rule",
        "properties": {
            "created": {
                "type": [
                    {
                        "type": "object",
                        "description": "sub-schema for validation range type occurrence",
                        "properties": {
                            "range": {
                                "additionalProperties": false,
                                "required": true,
                                "type": "object",
                                "properties": {
                                    "start_date": {
                                        "required": true,
                                        "type": "string",
                                        "description": "start date in format YYYY-MM-DD",
                                        "format": "date"
                                    },
                                    "end_date": {
                                        "required": true,
                                        "type": "string",
                                        "description": "end date in format YYYY-MM-DD",
                                        "format": "date"
                                    }
                                }
                            }
                        }
                    },
                    {
                        "type": "object",
                        "description": "sub-schema for validation in the last type occurrence",
                        "properties": {
                            "in_the_last": {
                                "additionalProperties": false,
                                "required": true,
                                "type": "object",
                                "properties": {
                                    "quantity": {
                                        "required": true,
                                        "type": "integer",
                                        "description": "quantity of units, like 10 days, 2 months etc"
                                    },
                                    "unit": {
                                        "required": true,
                                        "type": "string",
                                        "description": "possible types of period",
                                        "enum": ["day", "month", "week"]
                                    }
                                }
                            }
                        }
                    }
                ]
            }
        }
    }

Schema for validation of address occurrences

.. code-block:: javascript

    {
    	"type": "object",
    	"description": "address validation rule",
    	"properties": {
    		"address": {
    			"additionalProperties": false,
    			"patternProperties": {
    				"^(contain|not_contain|is_empty| )$": {
    					"minLength": 2,
    					"required": true,
    					"type": ["string", "boolean"]
    				}
    			},
    			"type": "object"
    		}
    	}
    }

Schema for validation of tag occurrences

.. code-block:: javascript

    {
    	"type": "object",
    	"description": "tag validation rule",
    	"properties": {
    		"tag": {
    			"additionalProperties": false,
    			"type": "object",
    			"properties": {
    				"is": {
    					"minLength": 2,
    					"required": true,
    					"type": "string"
    				}
    			}
    		}
    	}
    }

Schema for validation of custom fields

.. code-block:: javascript

    {
    	"type": "object",
    	"description": "custom field validation rule",
    	"properties": {
    		"custom_fields": {
                "type": "object",
                "patternProperties": {
                    "^.{1,150}$": {
                        "additionalProperties": false,
                        "required": true,
                        "type": "object",
                        "patternProperties": {
                            "^(is|is_not|contain|not_contain|is_empty)$": {
                                "required": true,
                                "type": ["string", "boolean"]
                            }
                        }
                    }
                }
            }
        }
    }

Schema for validation of record type

.. code-block:: javascript

    {
        "type": "object",
        "description": "record type validation rule",
        "properties": {
            "record type": {
                "additionalProperties": false,
                "type": "object",
                "properties": {
                    "is": {
                        "minLength": 2,
                        "required": true,
                        "type": "string",
                        "enum": ["all", "person", "company"]
                    }
                }
            }
        }
    }

Schema for validation of description

.. code-block:: javascript

    {
        "type": "object",
        "description": "description validation rule",
        "properties": {
            "description": {
                "additionalProperties": false,
                "patternProperties": {
                    "^is_empty|contain|not_contain$": {
                        "minLength": 2,
                        "required": true,
                        "type": ["string", "boolean"]
                    }
                }
            }
        }
    }

Schema for validation of saved searches

.. code-block:: javascript

    {
        "type": "object",
        "description": "saved search validation rule",
        "properties": {
            "saved_search": {
                "additionalProperties": false,
                "type": "object",
                "properties": {
                    "is": {
                        "required": true,
                        "type": "string",
                        "pattern": "^[A-Fa-f0-9]{24}$"
                    }
                }
            }
        }
    }

.. note::
    Most field names in query language are the same as field name in Nimble database, except some special cases (search by not a fields) 
    like: ``record type``, ``saved_search``, ``custom_fields``.
    For more information about default fields and their names in Nimble, see: :ref:`contact-fields`.

API endpoints
---------------------

Advanced search requests should be done through statard contacts listing entry point::

    GET /api/v1/contacts

Parameters are the same as for regular listing, except new one:

**query**
    Should contain url-encoded JSON. Syntax of queries is :ref:`described above <advanced-search-ref>`.

 .. note::
    Parameter ``record_type`` will be ignored, if ``query`` parameter was specified. To filter persons/companies, please use corresponding sub query in query.

 .. note::
    Parameter ``keyword`` will be ignored, if ``query`` parameter was specified.

Request example 1::

    https://api.nimble.com/api/v1/contacts?query=%7B%22first%20name%22%3A%20%7B%22is%22%3A%20%22Anton%22%7D%7D&tags=0&per_page=5&fields=first%20name

Advanced search query in this request is:

    .. code-block:: javascript

         {
             "first name": {
                "is": "Anton"
             }
         }

Request example 2::

    https://api.nimble.com/api/v1/contacts?query=%7B%22and%22%3A%20%5B%7B%22last%20name%22%3A%20%7B%22is%22%3A%20%22Ferrara%22%7D%7D%2C%20%7B%22first%20name%22%3A%20%7B%22is%22%3A%20%22Jon%22%7D%7D%5D%7D&tags=0&per_page=5&fields=last%20name,first%20name

Advanced search query in this request is:

  .. code-block:: javascript

         {
              "and": [
                  {
                      "last name": {
                          "is": "Ferrara"
                      }
                  },
                  {
                      "first name": {
                          "is": "Jon"
                      }
                  }
              ]
         }

Response: OK
------------

On success, results are returned in format, similar to contacts :ref:`listing response <contact-resources-response>`.

Response: Errors
----------------
Possible errors:

* :ref:`validation-error`


.. _saved_search_api:

Saved search API
~~~~~~~~~~~~~~~~
We provide REST API for saved searches API.

List all saved searches for current user::

    GET /api/v1/contacts/saved_search/ 

Creates new saved search for current user::
    
    POST /api/v1/contacts/saved_search/ 

Parameters:

**query_name** 
    Desired name for saved search.
**query**
    JSON-encoded valid query.

Update saved search with provided id with new values for name and|or query::
    
    PUT /api/v1/contacts/saved_search/<id> 

Parameters:

**query_name**
    New desired name for saved search.
**query**
    New JSON-encoded valid query.
    
Remove saved search with provided id::
    
    DELETE /api/v1/contacts/saved_search/<id> 

.. note::
    In case of attempt to remove saved search, referenced within another saved search query - validation error response will be returned.

**Listing example**:: 
    
    GET https://api.nimble.com/api/v1/contacts/saved_search/

Response:

.. code-block:: javascript

    {
        "resources": [
            {
                "query": "{\"name\": {\"is\": \"John Doe\"}}",
                "id": "50885f44837d4e0df1000002",
                "name": "q1"
            },
            {
                "query": "{\"name\": {\"is\": \"John Doe\"}}",
                "id": "50885f44837d4e0df0000001",
                "name": "q2"
            },
            {
                "query": "{\"name\": {\"is\": \"John Doe\"}}",
                "id": "50885f44837d4e0df1000003",
                "name": "q3"
            }
        ]
    }

**Creating example**:: 
    
    POST https://api.nimble.com/api/v1/contacts/saved_search/

Request data is::

    {
        'query': '{"name": {"is": "John Doe"}}',
        'query_name': 'q1'
    }

Response::

    {
        "query": "{\"name\": {\"is\": \"John Doe\"}}",
        "id": "50885f43837d4e0df1000000",
        "name": "q1"
    }
    
**Updating example**::
    
    PUT https://api.nimble.com/api/v1/contacts/saved_search/50885f43837d4e0df1000000

Request data is::

    {
        'query': '{"name": {"is": "John Doe"}}',
        'query_name': 'q1'
    }

Response::

    {
        "query": "{\"name\": {\"is\": \"John Doe\"}}",
        "id": "50885f43837d4e0df1000000",
        "name": "q1"
    }
    
**Deleting example**::

    DELETE https://api.nimble.com/api/v1/contacts/saved_search/50885f43837d4e0df1000001

Response OK::

    {
        "status": "ok",
        "data": {}
    }

Response if this saved search is referenced by other saved search::

    {
        "message": "something wrong while deleting advanced search instance",
        "code": 107,
        "errors": {
            "DeleteError": [
                "The search that is used as the parameter of search criteria in other saved searches can not be deleted.\n" +
                "Please, remove it from each of saved searches where it's used and then try to delete it again."
            ]
        }
    }
