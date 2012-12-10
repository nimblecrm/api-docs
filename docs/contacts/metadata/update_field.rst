==============
Update field
==============

Request
-------
Example::

    PUT https://api.nimble.com/api/v1/contacts/metadata/fields/<field_id>

Parameters
----------

**field_id**

    id of field we want perform an update for.

Other parameters are passed as JSON in request body. All parameters are mandatory.

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
On success, server returns response with HTTP code 200 and, recently updated, encoded field.

.. code-block:: javascript

     {
         "field_type": "single-line-text-box",
         "group": "SOme new tab",
         "name": "new field",
         "label": "new field",
         "values": null,
         "modifier": "",
         "id": "50c5e683084abd5a0200007a"
     }

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `group_id` or `field_id` parameter).