============================
Create fields tab
============================

Request
-------
Example::

    POST https://api.nimble.com/api/v1/contacts/fields/tabs

Parameters
----------

All parameters are passed as JSON in request body. All parameters are mandatory.

**tab_name**

    name for new fields tab.

**insert_after**


    If not null, inserts a new tab after another tab with specified id. If null, then tab is inserted as the first one

**contact_types**

    list of contact types accepted for fields in the tab. Possible types are: `person`, `company`.



Example:

.. code-block:: javascript

    {
      "contact_types": [
        "person"
      ],
      "insert_after": "string",
      "tab_name": "string"
    }

Response: OK
------------
On success, server returns response with HTTP code 200 and fields metadata with newly created tab.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`