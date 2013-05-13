==============
Create field
==============

Request
-------
Example::

    POST https://api.nimble.com/api/v1/contacts/metadata/fields

Parameters
----------

All parameters are passed as JSON in request body. All parameters are mandatory.

**name**

    name for new field.

    .. note:: Name should be unique.

**group_id**

    id of fields group, new field should belong to.

**presentation**

    dictionary describing how field should be presented in Nimble client (can be empty dictionary as well). More details are at :ref:`described here <field-presentations>`.

Example:

.. code-block:: javascript

    {
        "group_id": "5092a4d5084abd46de000725",
        "presentation": {
            "width": "1",
            "type": "single-line-text-box"
        },
        "name": "new field"
    }


Response: OK
------------
On success, server returns response with HTTP code 201 and, newly created, encoded field.

.. code-block:: javascript

     {
         "group": "Some new tab",
         "name": "new field",
         "label": "new field",
         "modifier": "",
         "presentation": {
             "width": "1",
             "type": "single-line-text-box"
         },
         "id": "50cf3eca084abd0f070013ae",
         "multiples": false
     }

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `group_id` parameter).