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

    JSON-encoded structure describing how field should be presented in Nimble client (can be empty string as well).

Example:

.. code-block:: javascript

 {
     "group_id": "5092a4d5084abd46de000725",
     "presentation": "{\"width\": \"1\", \"type\": \"single-line-text-box\"}",
     "name": "new field"
 }

Response: OK
------------
On success, server returns response with HTTP code 201 and, newly created, encoded field.

.. code-block:: javascript

     {
         "field_type": "single-line-text-box",
         "group": "SOme new tab",
         "name": "new field",
         "label": "new field",
         "values": null,
         "modifier": "",
         "id": "50a2d10b837d4e051a000006"
     }

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `group_id` parameter).