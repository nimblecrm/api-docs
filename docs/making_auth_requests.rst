.. _making-requests-tutorial:

=======================================
Tutorial: Making authenticated requests
=======================================

When you've received token, using the process described :ref:`here <obtain-token-tutorial>` you are ready to call Nimble API. You can use one of two ways, described below. They both are equal. 

Authenticating your request with URL parameter
----------------------------------------------

In order to use this token code you just add it into URL as request parameter with name ``access_token``.

**Endpoint**:

Any of available endpoint of Nimble API
 
**Params**:

No matter what request ``POST``, ``GET`` or any other HTTP method, just add an ``access_token`` as parameter to URL.

    **access_token**
        *required* — put a token for user under this parameter. 
 

**Example Request**::

    POST https://api.nimble.com/api/v1/contacts?access_token=e0f7b053200672c2ff6ede59c8e2bfc7

**Successful Response**:

All API responses described on their corresponding pages. 
 
Authenticating your request with HTTP header
--------------------------------------------

You can also pass your token in HTTP header ``Authorization`` in format: ``Bearer <your token>``.

**Example request**::

    PUT /api/v1/contact/4f60a873fcf7b752ed006b7a HTTP/1.1
    Accept: application/json
    Accept-Encoding: gzip, deflate, compress
    Authorization: Bearer c0b5f46631455b543c309b8cb18b8dae
    Content-Type: application/json; charset=utf-8

    {
        "fields": {
            "first name": [
                {
                    "modifier": "", 
                    "value": "1name"
                }
            ]
        }
    }

// TODO specify invalid token or expired token error
