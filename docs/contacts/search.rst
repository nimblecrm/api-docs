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
               "skype_id": {
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

Terminology
~~~~~~~~~~~

Based on example above, let’s define basic terminology:

**and**     
    is join operator for occurrences
    
**skype_id** (record_type) 
    is a term to search by

**is** 
    is occurrence of term in search index

**person** (john.doe) 
    is a value for occurrence

Joins
~~~~~
Possible variants for join operators are ``and`` and ``or``. They could be combined in different ways and priorities. Some examples with explanations will be listed below.

Let’s define several occurrences:

.. code-block:: javascript

    o1 = {
        "skype_id": {
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
        "creation date": {
            "is_within": {
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

Saved Advanced Searches
~~~~~~~~~~~~~~~~~~~~~~~
Query language allow to specify as occurrence of other (previously saved) search query. You can combine saved search occurrences in a way as regular occurrences are used. Explanation example is provided bellow.

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

This saved search has id 4fc886dc682c4a64dd060062 in database (detailed information about saved searches API see in public API endpoints section).

To use previously saved search we need to construct next query:

.. code-block:: javascript

    {
        "and": [{
            "skype_id": {
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
            "skype_id": {
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
    		"^(skype_id|twitter|linkedin|facebook|phone|last name|title|description|street|city|state|zip|country|lead type|company name|any|custom_fields|name|first name|lead source|creation date|address|tag|or|and|record type|saved_search)$": {
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
    		"^(skype_id|twitter|linkedin|facebook|phone|last name|street|city|state|zip|country|company name|title)$": {
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
    	"description": "skype_id/twitter/linkedin/facebook/phone/last name/street/city/state/zip/country/company name/title validation rule"
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

Schema for validation of creation date occurrences

.. code-block:: javascript

    {
    	"type": "object",
    	"description": "creation date validation rule",
    	"properties": {
    		"creation date": {
    			"additionalProperties": false,
    			"type": "object",
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
    			"additionalProperties": false,
    			"patternProperties": {
    				"^[A-Fa-f0-9]{24}$": {
    					"additionalProperties": false,
    					"patternProperties": {
    						"^(is|is_not|contain|not_contain|is_empty)$": {
    							"required": true,
    							"type": ["string", "boolean"]
    						}
    					},
    					"required": true,
    					"type": "object"
    				}
    			},
    			"type": "object"
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
                        "enum": ["person", "company"]
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

..note::
    Most field names in query language are the same as field name in Nimble database, except some special cases (search by not a fields) 
    like: ``record type``, ``saved_search``, ``custom_fields``.
    For more information about default fields and their names in Nimble, see: :ref:`contact-fields`.

Public API
----------
As any contacts public API - Advanced Search has its own entry point.

Next URL is handling all requests to advanced search::

    GET /api/v1/contacts/list

This entry point can have following parameters:

**query** — required
    Should contain url-encoded JSON. Syntax of queries :ref:`described above <advanced-search-ref>`.
    
**fields** — optional, default: all fields in contact

  Specifies a comma separated list of fields to return. If this parameter is excluded, all fields will be returned. 
  For example: ``fields=first%20name,my%20custom%20field``. For more detailed info on Nimble's fields see :ref:`contact-fields`.

  .. note:: 
    If field name contains "," (comma) it should be shielded with "\\". For example: we have some custom field with name 
    "hello, Jon Doe" it should be HTML-encoded in ``hello%5C%2C%20John%20Doe`` (``hello\, John Doe``).

**tags** — optional, default: 1

  Specifies whether tags should be included in the results. 

**per_page** — optional, default: 30

  Specifies the number of items to return per page of results.

**page** — optional, default: 1

  Specifies which page to display. Numeration starts from 1. 

**sort** — optional, default: ``name:asc``

  Identifies the sort field and sort order. Sort order is required when this parameter is used. 
  An single sort field can be specified. Any field can be sorted in either ``asc`` or ``desc`` order.

.. note::
    Parameter ``record_type`` will be ignored, if query parameter was specified. To filter persons/companies, please use corresponding sub query in query.

Response: OK
------------

On success, results are returned in format, similar to contacts :ref:`listing response <contact-resources-response>`.

Response: Errors
----------------
Possible errors:

* :ref:`validation-error`

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
    
    GET https://app.devnimble.com/api/v1/contacts/saved_search/

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
    
    POST https://app.devnimble.com/api/v1/contacts/saved_search/

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
    
    PUT https://app.devnimble.com/api/v1/contacts/saved_search/50885f43837d4e0df1000000

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

    DELETE https://app.devnimble.com/api/v1/contacts/saved_search/50885f43837d4e0df1000001

Response OK::

    {
        "status": "ok",
        "data": {}
    }

Response if this search is referenced by other::

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
