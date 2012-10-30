=================
Get contacts list
=================

Request 
-------
``GET https://api.nimble.com/api/v1/contacts/list``

Parameters
----------

All parameters are optional. Unrecognized parameters are ignored. Unrecognized values will return an error.

**fields** — default: all fields are returned

Specifies a comma separated list of fields to return. If this parameter is excluded, all fields will be returned. For example: ``fields=first%20name,my%20custom%20field``

*Note:* if field name contains "," (coma) it should be shielded with "\\". For example: we have some custom field with name "hello, Jon Doe" it should be HTML-encoded in ``hello%5C%2C%20John%20Doe`` (``hello\, John Doe``).

**tags** — default: 1

Specifies whether tags should be included in the results. 

**per_page** — default: 30

Specifies the number of items to return per page of results.

**page** — default: 1

Specifies which page to display.

**sort** — default: name:asc

Identifies the sort field and sort order. Sort order is required when this parameter is used. An single sort field can be specified. Any field can be sorted in either ``asc`` or ``desc`` order.  In addition to sorting on default and custom fields, there are the special sorts: recently viewed by the authenticated user (as ``recently%20viewed``), first + last name (as ``name``), and record created date (as ``create``).

*Note:* Only fields that have been indexed by our search engine are sortable. These include all custom fields and most standard fields.

When sorting by recently viewed, these parameters are disabled: **keyword**, **record type**, **page** and **per_page**. Nimble stores only the 30 most recently viewed records.

**record_type** — default: all

Identifies the record type. Possible value are ``person``, ``company``, and ``all``.

**keyword** — default: empty

Specifies a set of simple search criteria for the query. This simple search is performed on basic contact info fields, which includes name, email, and address. For example: ``keyword=Jon%20Smith``

Response: OK
------------

List and Detail response format is the basically the same. List allows search terms, sort orders, and fields as parameters, whereas detail returns all of the fields with the option of adding metadata.

Example: request on https://app.nimble.com/api/contacts/last_viewed?_cb=1345564526886&limit=30

.. code:: javascript

    {
        "resources": [{
            "updated": "2012-04-11T17:38:23+0300",
            "creator": "Anton Koval",
            "object_type": "contact",
            "record_type": "person",
            "children": [],
            "created": "2011-06-06T14:26:42+0300",
            "fields": {
                "last contacted": [{
                    "group": "Basic Info",
                    "modifier": "",
                    "field_id": "4f211756ee4d5d6e47001fc3",
                    "value": 1328288250.0,
                    "label": "last contacted"
                }],
                "parent company": [{
                    "extra_value": "4d6b7aff02c3c06b14000037",
                    "group": "Basic Info",
                    "modifier": "",
                    "field_id": "4eabb2484fb88d3352011a66",
                    "value": "Nimble",
                    "label": "parent company"
                }],
                "description": [{
                    "group": "Extra Info",
                    "modifier": "other",
                    "field_id": "4eabb2494fb88d3352011a90",
                    "value": "Front-End developer at Nimble",
                    "label": "description"
                }],
                "first name": [{
                    "group": "Basic Info",
                    "modifier": "",
                    "field_id": "4eabb2484fb88d3352011a5c",
                    "value": "Sergei",
                    "label": "first name"
                }],
                "last name": [{
                    "group": "Basic Info",
                    "modifier": "",
                    "field_id": "4eabb2484fb88d3352011a5e",
                    "value": "Shvets",
                    "label": "last name"
                }],
                "title": [{
                    "group": "Basic Info",
                    "modifier": "",
                    "field_id": "4eabb2484fb88d3352011a64",
                    "value": "developerr",
                    "label": "title"
                }],
                "URL": [{
                    "group": "Extra Info",
                    "modifier": "other",
                    "field_id": "4eabb2494fb88d3352011a8e",
                    "value": "http://bear-z.blogspot.com",
                    "label": "URL"
                }],
                "linkedin": [{
                    "avatar_url": "",
                    "group": "Contact Info",
                    "user_id": "QV6hf90I0Z",
                    "user_name": "sergey-shvets",
                    "modifier": "",
                    "field_id": "4eabb2494fb88d3352011a84",
                    "value": "http://www.linkedin.com/pub/sergey-shvets/18/78a/89a",
                    "label": "linkedin"
                }],
                "source": [{
                    "group": "Basic Info",
                    "modifier": "",
                    "field_id": "4eabb2484fb88d3352011a68",
                    "value": "g",
                    "label": "source"
                }],
                "avatar": [{
                    "value": "https://app.nimble.com/api/contacts/avatars/4decb9721ff786760f000021",
                    "label": "avatar"
                }],
                "email": [{
                    "group": "Contact Info",
                    "modifier": "work",
                    "field_id": "4eabb2494fb88d3352011a7c",
                    "value": "sergey.shvets@nimble.com",
                    "label": "email"

                }, {
                    "group": "Contact Info",
                    "modifier": "other",
                    "field_id": "4eabb2494fb88d3352011a79",
                    "value": "sergey.shvets@postindustria.com",
                    "label": "email"
                }]
            },
            "tags": [{
                "tag": "wrk",
                "id": "4d6b7afea8461f985fcb550e"
            }, {
                "tag": "nmbl",
                "id": "4decb96f1ff786760f000002"
            }, {
                "tag": "from_gnimble",
                "id": "4f859764b2964f1cc4000069"
            }, {
                "tag": "google",
                "id": "4d7689c5a8461f985fcb70c8"
            }],
            "id": "4decb9721ff786760f000021",
            "last_contacted": {
                "last_contacted": "2012-08-21T15:00:54+0300",
                "thread_id": "b2924a8b0826b1e60de1c79b8d6738f5",
                "message_id": "b81b7a68afb31a676b3d0097"
            },
            "owner_id": "4d18532006d79555f500004a"
        }, {
            "updated": "2012-02-04T12:20:30+0200",
            "creator": "Anton Koval",
            "object_type": "contact",
            "record_type": "company",
            "children": ["4decb98702c3c049e6000045", "4d6b7af802c3c06b1400000e", "4decb9731ff786760f000025", "4d89d28062100461f8000ddd", "4e7b1ef0a697c8721a000088", "4e7b1f13a697c87525000075", "4e173eb0a697c8718b00000c", "4d6b7af802c3c06b14000014", "4e2dd1f27834d8048e0006a5", "4eb9204b746ca51d0b0002e2", "4edcf270b0393424ab0002a6", "4e2dd1bc8ae030171f000003", "4ef771d3ee4d5d2c7c0001ef", "4f1e6cdcee4d5d66ca002a15", "4f2a9fe3d8569b27b300016a", "4f2d0603ee4d5d11a70030e3", "4f396a37d8569b79da000a89", "4decb9701ff786760f00000d", "4f706641ee4d5d49b1000109", "4eafdb55746ca50b2e0003d2", "4fce15244699c12ad3000367", "4fcf47789abaa72b38000059", "50086e0e5eee183713000d1a", "4eae5cd6ddf9414c450000dc", "5016970d5eee18748e0001c4", "5023945406fa1c07570005ef"],
            "created": "2011-02-28T12:37:51+0200",
            "fields": {
                "description": [{
                    "group": "Extra Info",
                    "modifier": "other",
                    "field_id": "4eabb2494fb88d3352011a90",
                    "value": "Nimble combines the best of high-end CRM, social media & collaborative tools into one simple and affordable SaaS solution. Tweets by @jon_ferrara & @ilovegarick",
                    "label": "description"
                }],
                "URL": [{
                    "group": "Extra Info",
                    "modifier": "work",
                    "field_id": "4eabb2494fb88d3352011a8a",
                    "value": "www.nimble.com - Join us in private beta!",
                    "label": "URL"
                }],
                "twitter": [{
                    "avatar_url": "http://a2.twimg.com/profile_images/568369673/twitter_normal.png",
                    "group": "Contact Info",
                    "user_id": "Nimble",
                    "user_name": "Nimble",
                    "modifier": "",
                    "field_id": "4eabb2494fb88d3352011a80",
                    "value": "Nimble",
                    "label": "twitter"
                }],
                "facebook": [{
                    "avatar_url": "http://graph.facebook.com/210857648102/picture",
                    "group": "Contact Info",
                    "user_id": "210857648102",
                    "user_name": "Nimble",
                    "modifier": "",
                    "field_id": "4eabb2494fb88d3352011a82",
                    "value": "http://www.facebook.com/nimble",
                    "label": "facebook"
                }],
                "avatar": [{
                    "value": "https://app.nimble.com/api/contacts/avatars/4d6b7aff02c3c06b14000037",
                    "label": "avatar"
                }],
                "address": [{
                    "group": "Contact Info",
                    "modifier": "work",
                    "field_id": "4eabb2494fb88d3352011a86",
                    "value": "{\"street\": \"Los Angeles\"}",
                    "label": "address"
                }],
                "company name": [{
                    "group": "Basic Info",
                    "modifier": "",
                    "field_id": "4eabb2484fb88d3352011a62",
                    "value": "Nimble",
                    "label": "company name"
                }]
            },
            "tags": [{
                "tag": "wrk",
                "id": "4d6b7afea8461f985fcb550e"
            }, {
                "tag": "tw2",
                "id": "4e7746f3d874030e2b000004"
            }, {
                "tag": "pgmail",
                "id": "4decb98102c3c049e6000002"
            }, {
                "tag": "nmbl",
                "id": "4decb96f1ff786760f000002"
            }, {
                "tag": "tw1",
                "id": "4e7746f3d874030e2b000002"
            }, {
                "tag": "tag1 tag2 tag3",
                "id": "4e7746fed874030e2b000045"
            }, {
                "tag": "twitter",
                "id": "4e725812d8740345e0000002"
            }, {
                "tag": "google",
                "id": "4d7689c5a8461f985fcb70c8"
            }, {
                "tag": "PI",
                "id": "4d6b7afca8461f985fcb550c"
            }],
            "id": "4d6b7aff02c3c06b14000037",
            "last_contacted": {
                "last_contacted": null,
                "thread_id": null,
                "message_id": null
            },
            "owner_id": "4d18532006d79555f500004a"
        }]
    }

Response: Errors
----------------
Links to possible errors here