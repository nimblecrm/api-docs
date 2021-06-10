==============
Delete tab
==============

Request
-------
Example::

    DELETE https://api.nimble.com/api/v1/contacts/tabs/<tab_id>

Parameters
----------

**tab_id**

    id of tab we want to delete.

Other (single one) parameters are passed as JSON in request body.

**preflight_checks**

    boolean, this parameter indicated whether we want check if fields in tab has values across some contacts.

Response: OK
------------
On success, server returns empty response with HTTP code 200.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `tab_id` parameter).