==============
Create contact
==============

Request 
-------
Example::

    POST https://api.nimble.com/api/v1/contact
    
Parameters
----------

All parameters are passed as JSON in request body. Both parameters are mandatory.

**type**
    Specifies the type of contact to create - the record type. This parameter could be one of two values: ``company`` or ``person``.

**fields**
    Describes a dictionary organized in the same structure as a contact listing response. In this structure, each key is field name. 
    Values are lists of dictionaries, having two fields: value - actual value to store in contact field, modifier - field modifier to use, 
    if field can have one. 

Example:

.. code-block:: javascript

    {
        'fields': {
            'first name': [{
                'value': 'Jack',
                'modifier': '',
            }],
            'last name': [{
                'value': 'Daniels',
                'modifier': '',
            }],
            'phone': [{
                'modifier': 'work',
                'value': '123123123',
            }, {
                'modifier': 'work',
                'value': '2222',
            }],
        },
        'type': 'person',
    }
    
Response: OK
------------
On success, server returns response with HTTP code 201 and newly created contact resource. 

.. code-block:: javascript

    {
        'updated': '2012-11-07T16:50:04+0200',
        'created': '2012-11-07T16:50:04+0200',
        'fields': {
            'last name': [{
                'field_id': '5049f697a694620a07000045',
                'modifier': '',
                'group': 'Basic Info',
                'value': 'Daniels',
                'label': 'last name'
            }],
            'phone': [{
                'field_id': '5049f697a694620a07000054',
                'modifier': 'work',
                'group': 'Contact Info',
                'value': '123123123',
                'label': 'phone'
            }, {
                'field_id': '5049f697a694620a07000054',
                'modifier': 'work',
                'group': 'Contact Info',
                'value': '2222',
                'label': 'phone'
            }],
            'source': [{
                'field_id': '5049f697a694620a0700004f',
                'modifier': '',
                'group': 'Basic Info',
                'value': 'm',
                'label': 'source'
            }],
            'first name': [{
                'field_id': '5049f697a694620a07000043',
                'modifier': '',
                'group': 'Basic Info',
                'value': 'Jack',
                'label': 'first name'
            }]
        },
        'object_type': 'contact',
        'id': '509a751c262b37af05000011',
        'last_contacted': {
            'last_contacted': null,
            'thread_id': null,
            'message_id': null
        },
        'record_type': 'person',
        'creator': 'Nimble API test',
        'children': [],
        'tags': [],
        'owner_id': '5049f696a694620a0700001c'
    }

For more details see: :ref:`contact-resources-response`.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`quota-error`
