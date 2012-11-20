.. _making-requests-tutorial:

=======================================
Tutorial: Making authenticated requests
=======================================

Authenticating your request
---------------------------

When you've received token, using the process described :ref:`here <obtain-token-tutorial>` you are ready to call Nimble API. 

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
 
// TODO specify invalid token or expired token error
