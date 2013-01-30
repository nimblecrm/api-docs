===================
Create task
===================

Request
-------
Base endpoint::

    POST https://api.nimble.com/api/v1/activities/task

Parameters
----------

All parameters are passed as JSON in request body.

**subject**

  Subject (short description) of new task. Parameter is **mandatory**.

**notes**

  Any additional text (notes) for task. Parameter can be omitted.

**related_to**

  List with contact ids we want to bind this task with. Parameter can be omitted.

**due_date**

  Due date for new task. Should be passed in format like "YYYY-MM-DD HOURS:MINUTES". Parameter can be omitted.

Example:

.. code-block:: javascript

    {
        "due_date": "2013-04-04 13:50",
        "notes": "Blah blah blah blah \u0440\u0443\u0441\u0441\u043a\u0438\u0439 \u0442\u0435\u043a\u0441\u0442 8168949",
        "related_to": [
            "508a4750084abd28bc00016f"
        ],
        "subject": "Hello task! 2423056"
    }

Response: OK
------------

Response to this request is dictionary with JSON serialised task body.

Response example
~~~~~~~~~~~~~~~~~

.. code-block:: javascript

    {
        "related_to": [
            "508a4750084abd28bc00016f"
        ],
        "due_date": "2013-04-04 13:50",
        "notes": "Blah blah blah blah \u0440\u0443\u0441\u0441\u043a\u0438\u0439 \u0442\u0435\u043a\u0441\u0442 8168949",
        "id": "5108f1cc837d4e3930e297fb",
        "subject": "Hello task! 2423056"
    }


Response: Errors
----------------
Possible errors:

* :ref:`validation-error`
