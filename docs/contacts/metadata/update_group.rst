============================
Update fields group
============================

Request
-------
Example::

    PUT https://api.nimble.com/api/v1/contacts/fields/groups/<group_id>

Parameters
----------

**group_id**

    id of fields group we want to perform update for

**name**

    name for new fields group.

**insert_after**

    If not null, inserts a new group after another group or field with specified id. If null, then tab is inserted as the first one

**logo_id**

    id of logo to show

**tab_id**

    id of fields tab, new group should belong to.

Example:

.. code-block:: javascript

    {
      "insert_after": "string",
      "logo_id": "string",
      "name": "string",
      "tab_id": "string"
    }


Response: OK
------------
On success, server returns response with HTTP code 200.


Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `group_id` parameter).