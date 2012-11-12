====================
Nimble API Responses
====================

.. contents::

.. _contact-details-response:

Contacts details
----------------

Typical response to this request is a dictionary with 2 keys (unless otherwise specified by the specific API): meta and resources. 

.. _contact-resources-response:

Contact resources
~~~~~~~~~~~~~~~~~

This field usually contains all data for the contacts you've requested. Here is an example of a Nimble contact

.. code-block:: javascript

    'resources': [{
        'updated': '2012-09-07T16:49:56+0300',
        'created': '2012-09-07T16:49:56+0300',
        'fields': {
            'parent company': [{
                'group': 'Basic Info',
                'field_id': '5049f697a694620a0700004d',
                'value': 'Nimble',
                'label': 'parent company',
                'extra_value': '5049fb7d9b85f669e4000063',
                'modifier': ''
            }],
            'description': [{
                'field_id': '5049f697a694620a0700007f',
                'modifier': 'other',
                'group': 'Extra Info',
                'value': 'Nimble Developers team member',
                'label': 'description'
            }, {
                'field_id': '5049f697a694620a07000082',
                'modifier': 'linkedin',
                'group': 'Extra Info',
                'value': 'Highly professional Python developer',
                'label': 'description'
            }],
            'last name': [{
                'field_id': '5049f697a694620a07000045',
                'modifier': '',
                'group': 'Basic Info',
                'value': 'Akopyan',
                'label': 'last name'
            }],
            'phone': [{
                'field_id': '5049f697a694620a07000058',
                'modifier': 'mobile',
                'group': 'Contact Info',
                'value': '+7 (917) 202-456-1111',
                'label': 'phone'
            }, {
                'field_id': '5049f697a694620a07000056',
                'modifier': 'home',
                'group': 'Contact Info',
                'value': '+7 244 231 84 22',
                'label': 'phone'
            }],
            'URL': [{
                'field_id': '5049f697a694620a0700007d',
                'modifier': 'other',
                'group': 'Extra Info',
                'value': 'https://nimble.com',
                'label': 'URL'
            }, {
                'field_id': '5049f697a694620a0700007d',
                'modifier': 'other',
                'group': 'Extra Info',
                'value': 'https://app.nimble.com',
                'label': 'URL'
            }],
            'source': [{
                'field_id': '5049f697a694620a0700004f',
                'modifier': '',
                'group': 'Basic Info',
                'value': 'csv',
                'label': 'source'
            }],
            'address': [{
                'field_id': '5049f697a694620a07000075',
                'modifier': 'other',
                'group': 'Contact Info',
                'value': '{"city": "Dushanbe", "street": "First str. 15", "zip": "54055", "country": "Farganistan"}',
                'label': 'address'
            }],
            'email': [{
                'field_id': '5049f697a694620a07000065',
                'modifier': 'other',
                'group': 'Contact Info',
                'value': 'fake_person@nimble.com',
                'label': 'email'
            }],
            'first name': [{
                'field_id': '5049f697a694620a07000043',
                'modifier': '',
                'group': 'Basic Info',
                'value': 'Amayak',
                'label': 'first name'
            }]
        },
        'object_type': 'contact',
        'id': '5049fb849b85f669e40000dc',
        'last_contacted': {
            'last_contacted': '2012-09-17T11:43:51+0300',,
            'thread_id': 5049f697a694620a07000062,
            'message_id': 5049f697a694620a17000075
        },
        'record_type': 'person',
        'creator': 'Emil Kio',
        'children': [],
        'tags': [{
            'tag': 'csv import',
            'id': '5049fa0c9b85f62cb4000639'
        }],
        'owner_id': '5049f696a694620a0700001c'
    }]
    
Here is a description of the response in detail:

**updated**
    Timestamp of contact's last update time
    
**created**
    Timestamp of contact's creation time
    
**fields**
    Dictionary containing contact's fields data. Keys are field names and values are lists of field values. All default contact fields 
    are :ref:`described here <contact-fields>`.

**object_type**
    String specifying document type. For contacts it's ``contact``.

**id**
    Unique contact id in BSON format.
    
**last_contacted**
    Information about last outbound message to this contact (if any). Contains following fields.
        * *last_contacted* — timestamp of last outbound message
        * *thread_id* — unique id of message thread in BSON format
        * *message_id* — unique id of message in BSON format
                    
**record_type**
    Type of contact.  This can have one of two values: ``person`` and ``company``.
    
**creator**
    Name of the person who created the contact
    
**children**
    For ``company`` contacts this field contains list of ``person`` contacts associated with the company.
    
**tags**
    List of tags associated with the contact. Each tag is represented as a dictionary having following keys.
        * *tag* — tag's text
        * *id* — unique id of tag in BSON format
    
**owner_id**
    Id of the person owning the contact in BSON format
        
.. _contacts-meta-response:

Contacts metadata
~~~~~~~~~~~~~~~~~

Contact's metadata contains information about all basic and custom fields created in Nimble for a user. Below is it's typical structure. Please note that this listing doesn't contain all metadata as the full list is very big.  The typical records are shown here. All default contact fields are :ref:`described here <contact-fields>`.

.. code-block:: javascript

    'meta': {
        'fields': {
            'first name': [{
                'field_type': None,
                'group': 'Basic Info',
                'label': 'first name',
                'values': None,
                'modifier': '',
                'id': '5049f697a694620a07000043'
            }],        
            'email': [{
                'field_type': None,
                'group': 'Contact Info',
                'label': 'email',
                'values': None,
                'modifier': 'other',
                'id': '5049f697a694620a07000065'
            }, {
                'field_type': None,
                'group': 'Contact Info',
                'label': 'email',
                'values': None,
                'modifier': 'personal',
                'id': '5049f697a694620a07000064'
            }],
            'lead status': [{
                'field_type': 'select-box',
                'group': 'Lead Details',
                'label': 'lead status',
                'values': [{
                    'id': '1',
                    'value': 'Open'
                }, {
                    'id': '2',
                    'value': 'Contacted'
                }, {
                    'id': '3',
                    'value': 'Qualified'
                }, {
                    'id': '4',
                    'value': 'Unqualified'
                }],
                'modifier': '',
                'id': '5049f697a694620a0700008d'
            }]
        },
        'groups': {
            'Basic Info': {
                'id': '5049f696a694620a07000031',
                'order': ['first name', 'last name', 'middle name', 'company name', 'title', 'parent company', 'source', 'last contacted'],
                'name': 'Basic Info',
                'label': 'Basic Info'
            }
        }
        'meta_last_modified': 0
    }
    
Here is a description of the response in detail:
    
**fields**
    Information about the fields in Nimble. Represented by dictionary where keys are fields names, and values are lists containing details about 
    all possible modifications of this field. If field have no modifiers (like ``first name`` on example above), this list contains only one element.
    
    Information stored in dictionaries with following keys:
        * *field_type* — type of the field if this is specially treated field, ``None`` otherwise. ``lead status`` is typically a specially treated field.  Field types are :ref:`described here <field-types>`.
        * *group* — unique name of the group containing this field.
        * *label* — unique name representing the field in human-readable form.
        * *values* — possible values for specially treated fields. More details are :ref:`described here <field-types>`.
        * *modifier* — name of the field's modifier
        * *id* — unique id of the field in BSON format
    
**groups**
    Information about field groups. Represented by dictionary where keys are unique group names and values are dictionaries with more info. ``Basic Info`` represents typical group, and all default groups :ref:`described here <field-groups>`. Groups info dictionary contains following fields:
        * *id* — unique id of the group in BSON format.
        * *order* — list containing names of the fields as they appeared in group.
        * *name* — unique name of the group. (Outdated: as we have field name as the key of ``groups`` dictionary.)
        * *label* — unique name representing the field in human-readable form.

**meta_last_modified**
    Outdated field, used to contain last metadata modification timestamp. Now for this purposes used E-Tag mechanism.
    

.. _contact-list-response:

Contact list
------------
Contact list request is similar to :ref:`contact-details-response`. It has the same key with resources, :ref:`described here <contact-resources-response>`. Difference is in ``meta`` key value. For contact listing it returns pagination details. 

.. code-block:: javascript

    'meta': {
        'per_page': 30,
        'total': 45,
        'pages': 2,
        'page': 1
    }

Keys meaning:

**per_page**
    Number of contacts returned per page
**total**
    Total number of contacts
**pages**
    Total pages count
**page**
    Current page number

.. _api-errors:

API Errors
----------

Errors in Nimble are returned as a JSON dictionary with appropriate HTTP error codes and following keys:

**message**
    Message about the error
**code**
    Extended error code

.. _validation-error:

Validation Error
~~~~~~~~~~~~~~~~
Sent on invalid parameters. Returns with HTTP code 409 and code field equal to 245.

This response looks like common error dictionary:

.. code-block:: javascript

    {
        "message": "You can specify either `keyword` or `query` parameter, not both!", 
        "code": 245
    }
    
    
On contact creation and update — additional data is returned. 

.. code-block:: javascript

    {
        "message": "Validation errors",
        "code": 245,
        "errors": {
            "first name": [{
                "message": "First name or last name field is required for person and should not be empty",
                "field_id": "5049f697a694620a07000043"
            }]
        }
    }

Here errors are a dictionary, containing information about field that caused the error. Key is field name and values are extended error message and unique id of the field that caused the error.

.. _quota-error:

Quota Error
~~~~~~~~~~~
Sent if user exceeded his quota values. Returns with HTTP code 402 and code field equal to 108.

.. code-block:: javascript

    {
        "message": "You have created the maximum number of contact records allowed for your subscription.\nDon't worry, you can upgrade your account and add more contacts right now.", 
        "code": 108
    }
    
.. _server-error:

Server error
~~~~~~~~~~~~
Sent if unrecoverable Nimble server occurs. Returns with HTTP code 500 and code field equal to 107
This errors are very rare, so our team receives automatical notifications on such errors and fixes them ASAP.

.. code-block:: javascript

    {
        "message": "Internal error handling request", 
        "code": 107
    }