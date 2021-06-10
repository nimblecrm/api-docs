====================
Get contacts details
====================

Single and bulk requests ore formatted and returned in the same way. The response format for each field is the same as returned in a contacts listing response. Metadata can be included in the response.

Request
-------

Base endpoint::

    GET https://api.nimble.com/api/v1/contact/<contact_id>[,<contact_id>,<contact_id>,...]

Example::

    GET https://api.nimble.com/api/v1/contact/5049fb9b9b85f669e4000447,5049fb7d9b85f669e4000066,5049fba29b85f669e40004fb 
    
Parameters
----------

All parameters are optional. Unrecognized parameters are ignored. Unrecognized values will return an error.

**meta** — default: 0
    When included and equal to 1, the meta parameter will add an additional component to the response which describes all fields, 
    field types, and possible values available on the record. For further reference see :ref:`legacy_contacts-meta-response`.

**fields** — default: all fields in contact
    Specifies a comma separated list of fields to return. If this parameter is excluded, all fields will be returned. 
    For example: ``fields=first%20name,my%20custom%20field``. For more detailed info on Nimble's fields see :ref:`contact-fields`.

    .. note:: 
      If field name contains "," (comma) it should be shielded with "\\". For example: we have some custom field with name 
      "hello, Jon Doe" it should be HTML-encoded in ``hello%5C%2C%20John%20Doe`` (``hello\, John Doe``).
    
**tags** — default: 1
    Specifies whether tags should be included in the results. 

Response: OK
------------

List and Detail response format is the basically the same. List allows search terms, sort orders, and fields as parameters, whereas detail can only limit fields to return and provide the option of adding metadata. In more details, this format :ref:`described here <contact-details-response>`.

Response: Errors
----------------
Possible errors:

* :ref:`validation-error`
