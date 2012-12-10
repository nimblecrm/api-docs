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

    list, contains ids of fields from group we try to perform update for in needed order.

    If this parameter omitted in request it will counted as empty list.

Example:

.. code-block:: javascript

 {
     "type": "both",
     "name": "grp123_modified",
     "order": []
 }

Response: OK
------------
On success, server returns response with HTTP code 200 and, recently updated, encoded fields group.

.. code-block:: javascript

     {
         "label": "grp123_modified",
         "id": "50c5e684e5ef8305390003b2",
         "name": "grp123_modified",
         "order": []
     }

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `group_id` parameter).