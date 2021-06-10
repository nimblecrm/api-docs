==============
Update field
==============

Request
-------
Example::

    PUT https://api.nimble.com/api/v1/contacts/fields/<field_id>

Parameters
----------

**field_id**

    id of field we want perform an update for.

Other parameters are passed as JSON in request body.

**name**

    name for new field.

    .. note:: Name should be unique.

**group_id**

    id of fields group, new field should belong to.

**tab_id**

    id of fields tab, new field should belong to.

**presentation**

    dictionary describing how field should be presented in Nimble client (can be empty dictionary as well). More details are at :ref:`described here <field-presentations>`.

**insert_after**

    If not null, move field after another field or group with specified id. If null, then moved field to be the first one

Example:

.. code-block:: javascript

    {
      "group_id": "string",
      "insert_after": "string",
      "name": "string",
      "presentation": {
        "number_type": "integer"
      },
      "tab_id": "string"
    }

Response: OK
------------
On success, server returns response with HTTP code 200 and, recently updated, encoded fields metadata.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `tab_id`, `group_id`, `field_id` or `insert_after`).