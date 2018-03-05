====================
Get user information
====================

For many use-cases it is useful to obtain basic user information. For that purpose we provide the `GET /api/v1/myself` endpoint.

Request 
-------
Example::

    GET https://api.nimble.com/api/v1/myself
    
Response: OK
------------
On success, server returns response with HTTP code 200

.. code-block:: javascript

    {
      "user_id": "4f2acc3142a053dda595f00b",
      "company_id": "4c2118ad54397f271b000000",
      "email": "some@user.com",
      "name": "John Doe",
      "company_size": 3
    }