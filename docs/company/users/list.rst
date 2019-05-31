====================
Get company users short information
====================

We provide an opportunity to get shortened information about the users of the company.

Request
-------
Example::

    GET https://api.nimble.com/api/v1/company/users

Response: OK
------------
On success, server returns response with HTTP code 200

.. code-block:: javascript

    {
        "users": [
            {
                "avatar_url": "https://app.nimble.com/api/v1/company/user/5ce69c1fceee1836160c2887/avatar?version=1",
                "is_active": true,
                "name": "Amayak Akopyan",
                "email": "fake_person@nimble.com"
            }
        ]
    }