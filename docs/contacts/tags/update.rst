===================
Update contact note
===================

Request 
-------
Base endpoint::

    PUT https://api.nimble.com/api/v1/contacts/<contact_id>/tags
    
Parameters
----------

This parameter is mandatory and must be passed as JSON in request body.

**tags**

  List of text strings which will be attached to contact as contact tags.
  Be careful! Contact tags which are not included in the request tags will be removed from the contact.
  
Example:

.. code-block:: javascript

    {
        "tags": ["Delightfully tag", "Embarrassing tag"],
    }

Response: OK
------------

Response to this request is empty JSON body ({}).

Response: Errors
----------------
Possible errors:

* :ref:`validation-error`
