Contact note
~~~~~~~~~~~~~

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

    
Keys meaning:

**id**
    Id of the note. Can be used to identify it in update and delete operations.

**created**
    Date and time when the note was created encoded in ISO 8601

**contacts**
    List of objects that are a shortened contact data view

**note_preview**
    Note content with all formatting removed

**note**
    Note content with all formatting mark up in place

**author_name**
    Readable name of company user who created this note

**owner_id**
    Id of company user who created this note