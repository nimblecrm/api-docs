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

    dictionary describing how field should be presented in Nimble client (can be empty dictionary as well). More details are at :ref:`described here <field-presentations>`.

Example:

.. code-block:: javascript

    {
        "group_id": "5092a4d5084abd46de000725",
        "presentation": {
            "width": "1",
            "type": "single-line-text-box"
        },
        "name": "new field2"
    }

Response: OK
------------
On success, server returns response with HTTP code 200 and, recently updated, encoded field.

.. code-block:: javascript

    {
        "group": "SOme new tab",
        "name": "new field2",
        "label": "new field2",
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
* :ref:`notfound-error` (in case of invalid value in `group_id` or `field_id` parameter).