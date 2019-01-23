===================
Create contact note
===================

Request 
-------
Base endpoint::

    POST https://api.nimble.com/api/v1/contacts/notes
    
Parameters
----------

All parameters are passed as JSON in request body. All parameters are mandatory.

**contact_ids** 

  List of contacts' IDs in BSON format to which the note will be attached. Contacts count should be between 1 and 10.

**note**

  Sting, containing note itself.
  
**note_preview**

  Short version of note, that will be used for preview purposes. 
  
Example:

.. code-block:: javascript

    {
        "contact_ids": ["50c07a69e5ef834edb000080", "50c07a53084abd5f61000aac"],
        "note": "Just contact note, with some longer text",
        "note_preview": "Just contact note"
    }

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
                "avatar_url": "https://app.nimble.com/api/contacts/avatars/5049fb849b85f669e40000dc",
                "subtitle": "CEO",
                "name": "Jack Daniels",
                "contact_type": "person",
                "phones": [
                    {
                        "value": "123456789",
                        "label": "work"
                    }
                ],
                "title": "CEO",
                "id": "5c459c56ceee1868ee3ab46f",
                "email": [
                    "care@nimble.com"
                ]
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
