=================
Get contacts list
=================

Request 
-------
Base endpoint::

    GET https://api.nimble.com/api/v1/contacts/list

Parameters
----------

All parameters are optional. Unrecognized parameters are ignored. Unrecognized values will return an error.

**fields** — default: all fields in contact

  Specifies a comma separated list of fields to return. If this parameter is excluded, all fields will be returned. 
  For example: ``fields=first%20name,my%20custom%20field``. For more detailed info on Nimble's fields see :ref:`contact-fields`.

  .. note:: 
    If field name contains "," (comma) it should be shielded with "\\". For example: we have some custom field with name 
    "hello, Jon Doe" it should be HTML-encoded in ``hello%5C%2C%20John%20Doe`` (``hello\, John Doe``).

**tags** — default: 1

  Specifies whether tags should be included in the results. 


**per_page** — default: 30

  Specifies the number of items to return per page of results.

**page** — default: 1

  Specifies which page to display. Numeration starts from 1. 

**sort** — default: ``name:asc``

  Identifies the sort field and sort order. Sort order is required when this parameter is used. 
  An single sort field can be specified. Any field can be sorted in either ``asc`` or ``desc`` order.
  In addition to sorting on default, there are the special sorts: recently viewed by the authenticated 
  user (as ``recently%20viewed``), first + last name (as ``name``), and record created date (as ``create``).

  .. note:: 
    Only fields that have been indexed by our search engine are sortable. These include all custom fields and most standard fields.

  .. warning::
    When sorting by recently viewed, these parameters are disabled: **keyword**, **record type**, **page** and **per_page**. 
    Nimble stores only the 30 most recently viewed records.

**record_type** — default: ``all``

  Identifies the record type. Possible value are ``person``, ``company``, and ``all``.

**keyword** — default: empty

  Specifies a set of simple search criteria for the query. This simple search is performed on any (indexed in our search engine) fied of contact. For example: ``keyword=Jon%20Smith``
  
**query** — default: empty
  Specifies query for contacts advanced search. Please note, that this parameter not compatible with parameters ``record_type`` and ``keyword``. For more details about search see :ref:`contacts-search-ref`.

Response: OK
------------

List and Detail response format is the basically the same. List allows search terms, sort orders, and fields as parameters, whereas detail returns all of the fields with the option of adding metadata. In more details, this format :ref:`described here <contact-list-response>`.


Response: Errors
----------------
Possible errors:

* :ref:`validation-error`
