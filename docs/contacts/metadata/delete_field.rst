==============
Delete field
==============

Request
-------
Example::

    DELETE https://api.nimble.com/api/v1/contacts/metadata/fields/<field_id>

Parameters
----------

**field_id**

    id of field we want to delete

    .. note:: Only custom fields are allowed to be deleted

Other (single one) parameters are passed as JSON in request body.

**force**

    boolean, this parameter indicated whether we want to remove field even if it has values across some contacts.

    If this parameter omitted in request it will counted as false.

Example:

.. code-block:: javascript

 {
     "force": true,
 }

Response: OK
------------
On success, server returns  emptyresponse with HTTP code 200 and, recently updated, encoded field.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`

.. code-block:: javascript

    {
        "message": "Validation errors",
        "code": 245,
        "errors": {
            "field 5049f697a694620a07000043": {
                "message": "is not custom field, delete of non-custom fields is forbidden!"
            }
        }
    }

* :ref:`notfound-error` (in case of invalid value in `group_id` or `field_id` fields)