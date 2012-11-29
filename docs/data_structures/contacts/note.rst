Contact note
~~~~~~~~~~~~~

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
    
Keys meaning:

**id**
    Id of the note. Can be used to identify it in update and delete operations.

**created**
    Date and time when the note was created encoded in ISO 8601

**contacts**
    List of ``id``-``name`` pairs for each of contacts associated with the note

**note_preview**
    Note content with all formatting removed

**note**
    Note content with all formatting mark up in place

**author_name**
    Readable name of company user who created this note

**owner_id**
    Id of company user who created this note