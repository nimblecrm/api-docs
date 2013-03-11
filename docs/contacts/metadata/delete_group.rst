============================
Delete fields group
============================

Request
-------
Example::

    DELETE https://api.nimble.com/api/v1/contacts/metadata/groups/<group_id>

Parameters
----------

**group_id**

    id of group we want to delete.

    .. note:: Only custom groups are allowed to be deleted.

Other (single one) parameters are passed as JSON in request body.

**force**

    boolean, this parameter indicated whether we want to remove group even if it has some fields within itself.

    If this parameter omitted in request it will counted as false.

Example:

.. code-block:: javascript

    {
        "force": false,
    }

Response: OK
------------
On success, server returns empty response with HTTP code 200.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `group_id` parameter).