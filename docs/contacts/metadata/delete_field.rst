==============
Delete field
==============

Request
-------
Example::

    DELETE https://api.nimble.com/api/v1/contacts/fields/<field_id>

Parameters
----------

**field_id**

    id of field we want to delete.

    .. note:: Only custom fields are allowed to be deleted.

Other (single one) parameters are passed as JSON in request body.

**preflight_checks**

    boolean, this parameter indicated whether we want check if field has values across some contacts.

Response: OK
------------
On success, server returns empty response with HTTP code 200.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `field_id` parameter).