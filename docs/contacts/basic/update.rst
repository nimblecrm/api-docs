==============
Update contact
==============

Request
-------

Example::
    
    PUT https://api.nimble.com/api/v1/contact/<id>?replace=1
    
Parameters
----------

**replace**
    Optional url parameter that identifies whether to replace all other values for this kind of field or not. Can take 1 or 0 as true or false state, default 0.
    For example if contact has such set of fields:

    .. code-block:: javascript

        {
            "fields": {
                "first name": [
                    {
                        "value": "Jack",
                        "modifier": ""
                    }
                ],
                "email": [
                    {
                        "value": "user@nimble.com",
                        "modifier": "work"
                    }, 
                    {
                        "value": "jack@gmail.com",
                        "modifier": "personal"
                    }
                ]
            }
        }

    then update it with:

    .. code-block:: javascript

        {
            "fields": {
                "email": [
                    {
                        "value": "user@nimble.com",
                        "modifier": "personal"
                    }
                ]
            }
        }

    will update field value with modifier "personal", but leave fields with other modifiers untouched. Result will be: 

    .. code-block:: javascript

        {
            "fields": {
                "first name": [
                    {
                        "value": "Jack",
                        "modifier": ""
                    }
                ],
                "email": [
                    {
                        "value": "user@nimble.com",
                        "modifier": "work"
                    }, 
                    {
                        "value": "user@nimble.com",
                        "modifier": "personal"
                    }
                ]
            }
        }

    With ``replace`` parameter set to 1 if contacts that has:

    .. code-block:: javascript

        {
            "fields": {
                "first name": [
                    {
                        "value": "Jack",
                        "modifier": ""
                    }
                ],
                "email": [
                    {
                        "value": "user@nimble.com",
                        "modifier": "work"
                    }, 
                    {
                        "value": "jack@gmail.com",
                        "modifier": "personal"
                    }
                ]
            }
        }

    and then UPDATE with:

    .. code-block:: javascript

        {
            "fields": {
                "email": [
                    {
                        "value": "user@nimble.com",
                        "modifier": "personal"
                    }
                ]
            }
        }

    will replace ``email`` fields with all modifiers. Result will be: 

    .. code-block:: javascript

        {
            "fields": {
                "first name": [
                    {
                        "value": "Jack",
                        "modifier": ""
                    }
                ],
                "email": [
                    {
                        "value": "user@nimble.com",
                        "modifier": "personal"
                    }
                ]
            }
        }


``fields`` and ``avatar_url`` parameters are passed as JSON in request body. You should pass at least one of the parameters: ``fields`` or ``avatar_url`` (or both).

**fields**
    Describes a dictionary organized in the same structure as a contact listing response. In this structure, each key is field name. 
    Values are lists of dicts, having two fields: value - actual value to store in contact field, modifier - field modifier to use, if field can have one. 
    Values provided in this list will replace actual field's values for contact. 
    If you want to remove all values from field — pass ``null`` as value. 

**avatar_url** — optional, default: None
    String, pointing to avatar, that should be assigned to the contact. 

    .. note:: Nimble uses lazy loading mechanism for avatars, and didn't perform any checks for URL validness during ``avatar_url`` setting. If you'll pass
        invalid parameter here — no avatar will be displayed for contact.    

Example:

.. code-block:: javascript

    {
        "fields": {
            "first name": [
                {
                    "value": "Jack",
                    "modifier": ""
                }
            ],
            "last name": [
                {
                    "value": "Daniels",
                    "modifier": ""
                }
            ],
            "phone": [
                {
                    "value": null,
                    "modifier": "work"
                }
            ]
        }
    }

Response: OK
------------
Updated contact is returned and encoded in the same way that is used in contacts listings. 

.. code-block:: javascript

    {
        "updated": "2012-11-07T16:50:04+0200",
        "created": "2012-11-07T16:50:04+0200",
        "fields": {
            "last name": [
                {
                    "modifier": "",
                    "value": "Daniels",
                    "label": "last name"
                }
            ],
            "source": [
                {
                    "modifier": "",
                    "value": "m",
                    "label": "source"
                }
            ],
            "first name": [
                {
                    "modifier": "",
                    "value": "Jack",
                    "label": "first name"
                }
            ]
        },
        "object_type": "contact",
        "id": "509a751c262b37af05000011",
        "last_contacted": {
            "user_id": "5c459c52ceee1868ee3ab41f",
            "deletion_tstamp": null,
            "type": "LCType<message>",
            "object_id": "ed5afbee-37f5-db6b-7f71-c7d6b8750bbb",
            "tstamp": "2019-01-22T21:57:30+0000"
        },
        "record_type": "person",
        "creator": "Nimble API test",
        "children": [],
        "tags": [],
        "owner_id": "5049f696a694620a0700001c"
    }

For more details see: :ref:`contact-resources-response`.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`quota-error`
* :ref:`notfound-error`
