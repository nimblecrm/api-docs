==============
Delete choice
==============

Request
-------
Example::

    DELETE https://api.nimble.com/api/v1/contacts/fields/<field_id>/choices/<id>

Parameters
----------

**field_id**

    id of field that contain choice that need to delete

**id**

    choice to delete

Other (single one) parameters are passed as JSON in request body.

**preflight_checks**

    boolean, this parameter indicated whether we want check if choice is used as value across some contacts.

Response: OK
------------
On success, server returns empty response with HTTP code 200.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `tab_id` parameter).