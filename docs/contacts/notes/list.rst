=======================
Get contact notes list
=======================

Request 
-------
Base endpoint::

    GET https://api.nimble.com/api/v1/contact/<contact_id>/notes
    
Example:

    GET https://api.nimble.com/api/v1/contact/5049fba29b85f669e40004fb/notes

Parameters
----------

All parameters are optional. Unrecognized parameters are ignored. Unrecognized values will return an error.

**per_page** — default: 5

  Specifies the number of items to return per page of results.

**page** — default: 1

  Specifies which page to display. Numeration starts from 1. 

Response: OK
------------

Response to this request is dictionary formed out of two keys: ``meta`` and ``resources``. Metadata coming under ``meta`` key is common structure used among different listing in Nimble. Value under ``resources`` key is list of notes entries.

.. include:: /data_structures/commons/paging_metadata.rst
.. include:: /data_structures/contacts/note.rst

Response example
~~~~~~~~~~~~~~~~~

.. code-block:: javascript

    {
        "meta": {
            "per_page": 5,
            "total": 1,
            "pages": 1,
            "page": 1
        },
        "resources": [{
            "created": "2012-11-29T10:16:46+0000",
            "contacts": [{
                "id": "508a4750084abd28bc00016f",
                "name": "Jack Daniels"
            }],
            "note_preview": "note 1",
            "author_name": "Nimble API test",
            "note": "%3Cfont%20face%3D%22Arial%2C%20Tahoma%2C%20Verdana%2C%20Helvetica%2C%20sans-serif%22%3Enote%201%3C%2Ffont%3E",
            "id": "50b7360e837d4e4404000013",
            "owner_id": "5049f696a694620a0700001c"
        }]
    }



Response: Errors
----------------
Possible errors:

* :ref:`validation-error`
