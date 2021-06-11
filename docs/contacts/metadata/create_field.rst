==============
Create field
==============

Request
-------
Example::

    POST https://api.nimble.com/api/v1/contacts/fields

Parameters
----------

All parameters are passed as JSON in request body.

**name**

    name for new field.

    .. note:: Name should be unique.

**field_type**

    dictionary describing field type. More details are at :ref:`described here <field-type>`.

**presentation**

    dictionary describing how field should be presented in Nimble client. More details are at :ref:`described here <field-presentations>`.

**group_id**

    id of fields group, new field should belong to. Could be null if field should be without group.

**tab_id**

    id of fields tab, new field should belong to.

**insert_after**

    If not null, inserts a new field after another field or group with specified id. If null, then inserted field to be the first one


Example:

.. code-block:: javascript

    {
  "field_type": {
    "field_kind": "string"
  },
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
On success, server returns response with HTTP code 200 and fields metadata with newly created field.

.. code-block:: javascript

     {
  "tab_id": "string",
  "tab_name": "string",
  "contact_types": "person",
  "is_standard": true,
  "members": [
    {
      "type": "group",
      "name": "string",
      "group_id": "string",
      "logo_id": "string",
      "fields": [
        {
          "type": "field",
          "name": "string",
          "field_id": "string",
          "modifier": "string",
          "multiples": true,
          "read_only": true,
          "field_type": {
            "field_kind": "string"
          },
          "presentation": {
            "number_type": "integer"
          },
          "available_actions": "edit_all"
        }
      ]
    }
  ],
  "available_actions": "edit_all"
    }

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `tab_id`, `group_id` or `insert_after`).