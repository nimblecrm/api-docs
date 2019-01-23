==============
Create contact
==============

Request 
-------
Example::

    POST https://api.nimble.com/api/v1/contact
    
Parameters
----------

All parameters are passed as JSON in request body. 

**record_type** — required
    Specifies the type of contact to create - the record type. This parameter could be one of two values: ``company`` or ``person``.

**fields** — required
    Describes a dictionary organized in the same structure as a contact listing response. In this structure, each key is field name. 
    Values are lists of dictionaries, having two fields: value - actual value to store in contact field, modifier - field modifier to use, 
    if field can have one. At a minimum, contacts require a name (first or last for a person, company name for a company).
    
**tags** — optional, default: None
    Comma separated list of tags to assign to contacts. If you need to create tags, containing comma sign — escape it with backslash. E.g.
    ``our customers,best\,premium`` will create tags ``our customers`` and ``best,premium``.

    .. note:: Maximum 5 tags are allowed in this list during contact creation.
    
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
                    "modifier": "work",
                    "value": "123123123"
                },
                {
                    "modifier": "work",
                    "value": "2222"
                }
            ]
        },
        "record_type": "person",
        "tags": "our customers,best"
    }
    
Response: OK
------------
On success, server returns response with HTTP code 201 and newly created contact resource. 

.. code-block:: javascript

     {
        "avatar_url": null,
        "children": [],
        "company_last_contacted": {
            "in": null,
            "out": null
        },
        "created": "2013-10-22T12:26:31+0300",
        "creator": "NimbleAPItest",
        "fields": {
            "first name": [
                {
                    "modifier": "",
                    "value": "Jack",
                    "label": "first name"
                }
            ],
            "last name": [
                {
                    "modifier": "",
                    "value": "Daniels",
                    "label": "last name"
                }
            ],
            "phone": [
                {
                    "modifier": "work",
                    "value": "123123123",
                    "label": "phone"
                },
                {
                    "modifier": "work",
                    "value": "2222",
                    "label": "phone"
                }
            ],
            "source": [
                {
                    "modifier": "",
                    "value": "m",
                    "label": "source"
                }
            ]
        },
        "id": "526644c7837d4e249372f091",
        "is_important": null,
        "last_contacted": {
            "user_id": null,
            "deletion_tstamp": null,
            "type": null,
            "object_id": null,
            "tstamp": null
        },
        "object_type": "contact",
        "owner_id": "4decc6b662100441e200000b",
        "record_type": "person",
        "reminder": null,
        "tags": [
            {
                "id": "52664434837d4e249372f081",
                "tag": "our customers"
            },
            {
                "id": "52664434837d4e249372f083",
                "tag": "best"
            }
        ],
        "updated": "2013-10-22T12:26:31+0300",
        "updater": null
     }

For more details see: :ref:`contact-resources-response`.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`quota-error`
