==============
Delete contact
==============

Simple contacts delete
----------------------

Performs deletion of contacts by their ids.

Request
~~~~~~~

Example::
    
    DELETE https://api.nimble.com/api/v1/contacts/<id>,<id>,<id>...
    
Parameters
~~~~~~~~~~

None, all contact's IDs specifies in URL, separated by comma

Response: OK
~~~~~~~~~~~~

Request returns HTTP code 200, body contains OK status and list of IDs of deleted contacts.

Example:

.. code-block::javascript

    {
        'status': 'ok',
        'data': {
            'ids': ['384348', '2343434', '34343']
        }
    }

Response: Errors
~~~~~~~~~~~~~~~~

Possible errors:

* :ref:`validation-error`


Advanced contacts delete
------------------------

Allows bulk removal of contacts by keyword or advanced search query.

Request
~~~~~~~

Example:: 

    DELETE https://api.nimble.com/api/v1/contacts/list

Parameters
~~~~~~~~~~

Parameters are similar to contact's listing ones.

**keyword** 
    Delete all contacts where fields are containing value from this parameter
    
**record_type** — default: ``all``
    Delete all contacts with provided record_type (``person`` or ``company``).
    This parameter could be combined with keyword parameter in order to delete contacts of specific record_type
    
**query**
    Json-encoded advanced search query to find contact for deletion. Only query or keyword parameter could be specified in the same time. 
    For more details on query syntax, see :ref:`advanced-search-ref`.
    
    .. note::
        If ``query`` parameter presented in request — ``record_type`` parameter will be ignored.
    
**limit** — default: number of contacts, matching criteria
    Number of contacts to delete by specified criteria (``query``, ``keyword``, ``record_type``).

.. warning::
    ``query`` and ``keyword`` parameters are mutually exclusive. If you'll try to specify both — validation error will be returned. 
    
Response: OK
~~~~~~~~~~~~

Example request:: 
    
    DELETE https://app.nimble.com/api/v1/contacts/list?keyword=DoeAPItest

Response will be:

.. code-block::javascript

    {
        "status": "ok", 
        "data": {
            "ids": [
                "50941746837d4e3df20001d1", 
                "50941746837d4e3df1000144"
            ]
        }
    }

Response: Errors
~~~~~~~~~~~~~~~~

Possible errors:

* :ref:`validation-error`
