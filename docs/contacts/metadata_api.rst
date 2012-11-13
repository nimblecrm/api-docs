========================
Contacts metadata API
========================

This documentation page will cover public API for working with Nimble contacts metadata.

Public API for metadata contain three parts:

1. API for retrieving details information about all available :ref:`contacts metadata<get-metadata-call-ref>`.
2. API for working with :ref:`contacts fields<fields-api-ref>` within Nimble.
3. API for working with :ref:`contacts groups<groups-api-ref>` within Nimble.

.. _get-metadata-call-ref:

Get contacts metadata API
============================

Request::

 GET https://api.nimble.com/api/v1/contacts/metadata

Response:

On success, server returns response with HTTP code 201 and JSON-encoded :ref:`metadata information<contacts-meta-response>`.

.. _fields-api-ref:

Contacts fields API
============================

This public API provides CRUD access to contacts fields.

Create Field
----------------------------

.. note:: Nimble allows to create only custom fields. List of default fields can be found :ref:`here<contact-fields>`.

Request
""""""""""""""""""""""""""""
::

 POST https://api.nimble.com/api/v1/contacts/metadata/fields

.. _fields-create-params-api-call-ref:

Parameters
""""""""""""""""""""""""""""

All parameters are passed as JSON in request body. All parameters are mandatory.

**name**

    name for new field.

**group_id**

    id of fields group, new field should belong to.

**presentation**

    JSON-encoded structure describing how field should be presented in Nimble client (can be empty string as well).

Example request parameters:

.. code-block:: javascript

 {
     "group_id": "5092a4d5084abd46de000725",
     "presentation": "{\"width\": \"1\", \"type\": \"single-line-text-box\"}",
     "name": "new field"
 }

.. _fields-create-response-api-call-ref:

Response
""""""""""""""""""""""""""""

On success, server returns response with HTTP code 201 and newly created encoded field structure.

Example response:

.. code-block:: javascript

 {
    "group_id": "5092a4d5084abd46de000725",
    "name": "new field",
    "presentation": "{\"width\": \"1\", \"type\": \"single-line-text-box\"}",
    "modifier": "",
    "type": "custom",
    "id": "509d5400837d4e6700000006",
    "multiples": false
 }


Update Field
----------------------------

.. note:: If update for default field was initiated, Nimble will update only its presentation. Name and group_id are immutable.

Request
""""""""""""""""""""""""""""
::

 PUT https://api.nimble.com/api/v1/contacts/metadata/fields/<field_id>

Parameters
""""""""""""""""""""""""""""

Parameters are the same as for :ref:`create call<fields-create-params-api-call-ref>`.

Response
""""""""""""""""""""""""""""

On success, server returns response with HTTP code 200 and recently updated encoded field structure.

See example :ref:`above<fields-create-response-api-call-ref>`.

Show Field(s)
----------------------------

Allows to list contacts field(s) by provided field id(s).

Request
""""""""""""""""""""""""""""
::

 GET https://api.nimble.com/api/v1/contacts/metadata/fields/<field_id1>,<field_id2>,...

Response
""""""""""""""""""""""""""""

On success, server returns response with HTTP code 200 and list of encoded requested fields.

Request to:
::

    GET https://app.nimble.com/api/v1/contacts/metadata/fields/5049f697a694620a07000054,5049f697a694620a07000058

will respond with:

.. code-block:: javascript

   {
       "resources": [
           {
               "group_id": "5049f696a694620a07000034",
               "name": "phone",
               "presentation": "",
               "modifier": "work",
               "type": "phone",
               "id": "5049f697a694620a07000054",
               "multiples": true
           },
           {
               "group_id": "5049f696a694620a07000034",
               "name": "phone",
               "presentation": "",
               "modifier": "mobile",
               "type": "phone",
               "id": "5049f697a694620a07000058",
               "multiples": true
           }
       ]
   }


Delete Field(s)
----------------------------

Allows to remove field with provided field id.

Request
""""""""""""""""""""""""""""
::

 DELETE https://api.nimble.com/api/v1/contacts/metadata/fields/<field_id>

Parameters
""""""""""""""""""""""""""""

All parameters are passed as JSON in request body. There is only single parameter for this method.

**force**

    should API remove field even if it has associated field values?. Should be boolean value.

Response
""""""""""""""""""""""""""""

On success, server returns response with HTTP code 200.

Example response on attempt to delete field without associated values:

.. code-block:: javascript

    {
        "status": "ok",
        "data": {}
    }

Example response on attempt to delete field with associated values:

.. code-block:: javascript

    {
        "message": "Field 5049f697a694620a07000043 have some data set",
        "code": 245
    }



