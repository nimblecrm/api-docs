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

    id of field we want to delete.

    .. note:: Only custom fields are allowed to be deleted.

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
On success, server returns empty response with HTTP code 200.

Response: Errors
----------------

Possible errors:

* :ref:`validation-error`
* :ref:`notfound-error` (in case of invalid value in `field_id` parameter).