============================
Delete fields group
============================

Request
-------
Example::

    DELETE https://api.nimble.com/api/v1/contacts/fields/groups/<group_id>

Parameters
----------

**group_id**

    id of group we want to delete.

    .. note:: Only custom groups are allowed to be deleted.

Other (single one) parameters are passed as JSON in request body.

**preflight_checks**

    boolean, this parameter indicated whether we want check if fields in this group has values across some contacts.

Response: OK
------------
On success, server returns empty response with HTTP code 200.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `group_id` parameter).