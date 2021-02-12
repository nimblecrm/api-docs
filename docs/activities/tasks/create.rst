===================
Create task
===================

Request
-------
Base endpoint::

    POST https://api.nimble.com/api/v1/activities/task

Parameters
----------

All parameters are passed as JSON in request body and could be omitted except `subject`.

**subject** — mandatory

  Subject (short description) of new task. Field length should be between 2 and 128 chars.

**notes**

  Any additional text (notes) for task. 

**related_to**

  List with contact ids we want to bind this task with. 

**due_date**

  Due date for new task. Should be passed in format like "YYYY-MM-DDTHOURS:MINUTES:SECONDS". Example: "2013-04-04T13:50:00"

Example:

.. code-block:: javascript

    {
        "due_date": "2013-04-04T13:50:00",
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
       "assigned_to" : {
          "avatar_url" : null,
          "email" : "person@nimble.com",
          "is_active" : true,
          "name" : "fname lname",
          "user_id" : "6010abc0f92ea1334da2fe5c"
       },
       "comments" : [],
       "company_id" : "4e4cbe3925dc8166c3d576c0",
       "completed" : false,
       "completed_time" : null,
       "created" : "2021-02-12T19:18:59+00:00",
       "due_date" : "2021-04-12T19:16:44+00:00",
       "due_date_text" : null,
       "id" : "6026d4a3f92ea10ab60e38b1",
       "is_important" : false,
       "notes" : "description 2",
       "owner" : {
          "avatar_url" : null,
          "email" : "person@nimble.com",
          "is_active" : true,
          "name" : "fname lname",
          "user_id" : "6010abc0f92ea1334da2fe5c"
       },
       "owner_id" : "6010abc0f92ea1334da2fe5c",
       "related" : {
          "contacts" : [
             {
                "avatar_url" : "https://app.nimble.com/api/avatars/company_default",
                "contact_type" : "company",
                "email" : [],
                "id" : "602452e4f92ea106d3454c8c",
                "is_viewable" : true,
                "name" : "XPO Logistics, Inc.",
                "phones" : [],
                "subtitle" : null,
                "title" : null
             }
          ],
          "deals" : []
       },
       "related_to" : [
          "602452e4f92ea106d3454c8c"
       ],
       "starred" : false,
       "subject" : "t1 curl",
       "tags" : [],
       "updated" : "2021-02-12T19:18:59.674000+00:00",
       "version" : 2
    }
    
Where  

**assinged_to** 

    Contains short information about a team member this task assigned to.  
    
**comments** 

    Always empty when created a task using this API call. .
    
**company_id** 

    The ID of a company in Nimble.
    
**completed** 

    A flag indicating if the task is completed (always *false* when created using this API call).

**completed_time** 

    Always *null* when created a task using this API call.   

**created**
    
    A timestamp of when the task was created.
    
**due_date**
    
    A timestamp of when the task is due (the same value you passed on creating this task).
    
**due_date_text**
    
    Always *null* when created a task using this API call. 
    
**id**

    A unique ID of this task.
    
**is_important**
    
    Always *false* when created a task using this API call. 
    
**notes**
    
    Any additional text (notes) for this task.
    
**owner**

    Short info of a team member owning this task
    
**owner_id** 

    A unique ID of the owner

**related**
    
    A structure that contains information about entities related to this task. When created with some contact IDs in the *related_to* field, this structure will include a list with short information about related contacts under the *contacts* key.

**related_to** 
    
    A list with IDs of related entities.
    
**starred**

    Always *false* when created a task using this API call. 

**subject**

   The subject (short description) of this task.
    
**tags**
   
   Always empty when created a task using this API call. 

**updated**
    
    A timestamp of when this task was last updated.



Response: Errors
----------------
Possible errors:

* :ref:`validation-error`
