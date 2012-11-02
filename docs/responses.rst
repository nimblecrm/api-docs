====================
Nimble API responses
====================

.. contents::

.. _contact-details:

Contacts details
----------------

Typical response to this request is a dictionary with 2 keys (if other doesn't specified by request to API): meta and resources. 

.. _contact-metadata:

Contact metadata
~~~~~~~~~~~~~~~~

Add here

.. _contact-resources:

Contact resources
~~~~~~~~~~~~~~~~~

This field usually contains all data for the contacts, you've requested. Here is typical example of Nimble contact

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
    
Let's see keys of this dictionary in details. 

    **updated**
        Timestamp of contact's last update time
        
    **created**
        Timestamp of contact's creation time
        
    **fields**
        Dictionary, containing contact's fields data. Keys are field names, and values are lists of field values. All default contact fields in 
        details :ref:`described here <contact-fields>`.
    
    **object_type**
        String, specifying document type. For contacts, it's predictably ``contact``.
    
    **id**
        Unique contact id in BSON format.
        
    **last_contacted**
        Information about last outbound message to this contact (if any). Contains following fields.
            * *last_contacted* — timestamp of last outbound message
            * *thread_id* — unique id of message thread in BSON format
            * *message_id* — unique id of message in BSON format
                        
    **record_type**
        Type of contact, can have one of two values: ``person`` and ``company``.
        
    **creator**
        Name of the person, created contact
        
    **children**
        For ``company`` contacts, this field contains list of ``person`` contacts, associated with this company.
        
    **tags**
        List of tags, associated with this contact. Each tag represented by dictionary, having following keys.
            * *tag* — tag's text
            * *id* — unique id of tag in BSON format
        
    **owner_id**
        Id of person, owning the contact in BSON format
        
.. _contacts-meta:

Contacts metadata
~~~~~~~~~~~~~~~~~

Contact's metadata contains information about all basic and custom fields, created in Nimble for user, making request. Here is it's typical structure. Please note, that this listing doesn't contain full metadata, as it's very big, so only typical records left here. All default contact fields in details :ref:`described here <contact-fields>`.

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
    
Let's see keys of this dictionary in details.
    
    **fields**
        Information about fields in Nimble. Represented by dictionary, where keys are fields names, and values are lists, containing details about 
        all possible modifications of this field. If field have no modifiers (like ``first name`` on example above), this list contains only one element.
        
        Information stored in dictionaries with following keys:
            * *field_type* — type of the field, if this is specially treated field, ``None`` otherwise. ``lead status`` is typical specially treated field. In more details, field types :ref:`described here <field-types>`.
            * *group* — unique name of the group, containing this field.
            * *label* — unique name, representing the field in human-readable form.
            * *values* — possible values, for specially treated fields. More details are :ref:`described here <field-types>`.
            * *modifier* — name of the field's modifier
            * *id* — unique id of the field in BSON format
        
    **groups**
        Information about field groups. Represented by dictionary, where keys are unique group names, and values are dictionaries with more info. ``Basic Info`` represents typical group, and all default groups :ref:`described here <field-groups>`. Groups info dictionary contains following fields:
            * *id* — unique id of the group in BSON format.
            * *order* — list, containing names of the fields, as they appeared in group.
            * *name* — unique name of the group. (Outdated, as we have field name as the key of ``groups`` dictionary.)
            * *label* — unique name, representing the field in human-readable form.
    
    **meta_last_modified**
        Outdated field, used to contain last metadata modification timestamp. Now for this purposes used E-Tag mechanism.
    

.. _contact-list:

Contact list
------------

Add here

.. _api-errors:

API Errors
----------

Add here