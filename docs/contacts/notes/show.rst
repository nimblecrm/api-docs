===================
Show single note
===================

Request 
-------
Base endpoint::

    GET https://api.nimble.com/api/v1/contacts/notes/<note_id>
    
Parameters
----------

**note_id** 

  Single note id to show

.. code-block:: javascript

    GET https://api.nimble.com/api/v1/contacts/notes/508a4750084abd28bc00016f

Response: OK
------------

Response to this request is dictionary with JSON serialised note body.

.. include:: /data_structures/contacts/note.rst

Response example
~~~~~~~~~~~~~~~~~

.. code-block:: javascript

    {
        "created": "2012-11-29T10:16:46+0000",
        "contacts": [
            {
                "id": "508a4750084abd28bc00016f",
                "name": "Jack Daniels"
            }
        ],
        "note_preview": "note 1",
        "author_name": "Nimble API test",
        "note": "%3Cfont%20face%3D%22Arial%2C%20Tahoma%2C%20Verdana%2C%20Helvetica%2C%20sans-serif%22%3Enote%201%3C%2Ffont%3E",
        "id": "50b7360e837d4e4404000013",
        "owner_id": "5049f696a694620a0700001c"
    }


Response: Errors
----------------
Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error`
