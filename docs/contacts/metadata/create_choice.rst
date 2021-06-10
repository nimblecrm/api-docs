==============
Create choice
==============

Request
-------
Example::

    POST https://api.nimble.com/api/v1/contacts/fields/<field_id>/choices

Parameters
----------

**field_id**

    id of field (with choice type)

**id**

    unique id between field choices of the field

**value**

    value for choice

**insert_after**

    If not null, inserts a new choice after another choice with specified id. If null, then inserted choice to be the first one in field



Response: OK
------------
On success, server returns response with HTTP code 200.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `field_id` parameter).