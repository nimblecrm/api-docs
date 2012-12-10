============================
Create fields group
============================

Request
-------
Example::

    POST https://api.nimble.com/api/v1/contacts/metadata/groups

Parameters
----------

All parameters are passed as JSON in request body. All parameters are mandatory.

**type**

    type of fields group (only for contacts persons, only for companies or for both). Possible types are: `person`, `company`, `both`.

**name**

    name for new fields group.

    .. note:: Name should be unique.

Example:

.. code-block:: javascript

 {
     "type": "both",
     "name": "grp123"
 }

Response: OK
------------
On success, server returns response with HTTP code 201 and, newly created, encoded fields group.

.. code-block:: javascript

     {
         "label": "grp123",
         "id": "50c5e684084abd59fc000027",
         "name": "grp123",
         "order": []
     }

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`