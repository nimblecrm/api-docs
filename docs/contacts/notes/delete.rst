===================
Delete single note
===================

Request
-------
Base endpoint::

    DELETE https://api.nimble.com/api/v1/contacts/notes/<note_id>

Parameters
----------

**note_id**

  Single note id to delete

.. code-block:: javascript

    DELETE https://api.nimble.com/api/v1/contacts/notes/508a4750084abd28bc00016f

Response: OK
------------

Response to this request is dictionary with id of deleted note.

Response example
~~~~~~~~~~~~~~~~~

.. code-block:: javascript

    {
        "id": "508a4750084abd28bc00016f"
    }
    
Response: Errors
----------------
Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error`
