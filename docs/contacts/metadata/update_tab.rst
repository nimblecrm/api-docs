============================
Update fields tab
============================

Request
-------
Example::

    PUT https://api.nimble.com/api/v1/contacts/fields/tabs/<tab_id>

Parameters
----------

**tab_id**

    id of fields tab we want to perform update for

**tab_name**

    name for new fields group.

**insert_after**

   Moves tab after another tab with specified id. If null, then move tab to the first position

**contact_types**

     list of contact types accepted for fields in the tab. Possible types are: `person`, `company`.


Example:

.. code-block:: javascript

    {
      "contact_types": "person",
      "insert_after": "string",
      "tab_name": "string"
    }


Response: OK
------------
On success, server returns response with HTTP code 200.


Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `group_id` parameter).