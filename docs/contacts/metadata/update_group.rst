============================
Update fields group
============================

Request
-------
Example::

    PUT https://api.nimble.com/api/v1/contacts/metadata/groups/<group_id>

Parameters
----------

**group_id**

    id of fields group we want to perform update for

All parameters are passed as JSON in request body.

**type**

    type of fields group (only for contacts persons, only for companies or for both). Possible types are: `person`, `company`, `both`.

**name**

    mame of new fields group.

    .. note:: Name should be unique.

**order**

    list, contains names of fields from group we try to perform update for in needed order.

    If this parameter omitted in request it will counted as empty list.

Example:

.. code-block:: javascript

 {
     "type": "both",
     "name": "grp525496_m2",
     "order": []
 }

Response: OK
------------
On success, server returns response with HTTP code 200 and, recently updated, encoded fields group.

.. code-block:: javascript

     {
         "name": "grp525496_m2",
         "label": "grp525496_m2",
         "is_standard": false,
         "order": [],
         "type": "both",
         "id": "50cf3ecce5ef833f4f000341"
     }

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `group_id` parameter).