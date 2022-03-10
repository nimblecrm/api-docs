=================================================
Full description of Nimble default contact fields
=================================================

.. _default-type:

Default fields
~~~~~~~~~~~~~~

Simple text fields, like ``first name``, ``last name``, ``title``, ``description``, etc.


.. _contact-fields:

Nimble default fields
---------------------
.. list-table:: Full list of Nimble standard fields
   :widths: 15 15 5 15 45
   :header-rows: 1

   * - Field Name
     - Type
     - Multiple field
     - Modificators
     - Notes
   * - first name
     - :ref:`default <default-type>`
     - \-
     - N/A
     - For person contact
   * - last name
     - :ref:`default <default-type>`
     - \-
     - N/A
     - For person contact
   * - middle name
     - :ref:`default <default-type>`
     - \-
     - N/A
     -
   * - company name
     - :ref:`default <default-type>`
     - \-
     - N/A
     - For company contact
   * - title (deprecated, use :ref:`contact employment <contact-employment-type>` instead)
     - :ref:`default <default-type>`
     - \-
     - N/A
     -
   * - parent company (deprecated, use :ref:`contact employment <contact-employment-type>` instead)
     - :ref:`parent company <parent-company-type>`
     - \-
     - N/A
     -
   * - contact employment 
     - :ref:`contact employment <contact-employment-type>`
     - \-
     - N/A
     -
   * - domain
     - :ref:`domain <domain-type>`
     - \-
     - N/A
     - Unique. For company contact
   * - phone
     - :ref:`default <default-type>`
     - \+
     - * work
       * home
       * mobile
       * main
       * home fax
       * work fax
       * other
     -
   * - email
     - :ref:`default <default-type>`
     - \+
     - * work
       * personal
       * other
     -
   * - skype id
     - :ref:`default <default-type>`
     - \+
     - N/A
     -
   * - twitter
     - :ref:`social <social-type>`
     - \+
     - N/A
     -
   * - facebook
     - :ref:`social <social-type>`
     - \+
     - N/A
     -
   * - linkedin
     - :ref:`social <social-type>`
     - \+
     - N/A
     -
   * - google plus
     - :ref:`social <social-type>`
     - \+
     - N/A
     -
   * - foursquare
     - :ref:`social <social-type>`
     - \+
     - N/A
     -
   * - address
     - :ref:`address <address-type>`
     - \+
     - * work
       * home
       * other
     -
   * - hubspot
     - :ref:`default <default-type>`
     - \-
     - N/A
     -
   * - URL
     - :ref:`default <default-type>`
     - \+
     - * work
       * personal
       * blog
       * other
     -
   * - description
     - :ref:`default <default-type>`
     - \+
     - * other
       * twitter
       * facebook
       * linkedin
       * google+
       * foursquare
     - If possible, fetches descriptions from social networks
   * - annual revenue
     - :ref:`default <default-type>`
     - \-
     - N/A
     -
   * - # of employees
     - :ref:`dropdown <dropdown-type>`
     - \-
     - N/A
     -
   * - lead status
     - :ref:`dropdown <dropdown-type>`
     - \-
     - N/A
     -
   * - rating
     - :ref:`dropdown <dropdown-type>`
     - \-
     - N/A
     -
   * - lead source
     - :ref:`dropdown <dropdown-type>`
     - \-
     - N/A
     - 
   * - lead type
     - :ref:`dropdown <dropdown-type>`
     - \-
     - N/A
     - 
   * - birthday
     - :ref:`default <default-type>`
     - \-
     - N/A
     - 

.. _field-tabs:

Nimble default field tabs
--------------------------

.. list-table:: Nimble default field tabs
   :widths: 10 20 15
   :header-rows: 1

   * - Tab Name
     - Description
     - Fields
   * - Personal Info
     - Personal contact's details
     - * first name,
       * last name,
       * middle name,
       * title,
       * parent company,
       * birthday
       * employment
   * - Company Info
     - Extended information about contact's company
     - * annual revenue,
       * company name,
       * domain,
       * # of employees
   * - Contact Info
     - How to reach this contact
     - * phone,
       * email,
       * skype id,
       * twitter,
       * facebook,
       * linkedin,
       * google+,
       * foursquare,
       * address,
       * description,
       * URL,
       * hubspot
   * - Lead Details
     - Information about contact as lead
     -  * rating,
        * lead stage
   * - Additional Lead Fields
     - Legacy fields
     -  * lead status,
        * lead source,
        * lead type
   * - Extra Info
     - Contact's extended information
     - * Files
.. _social-type:

Social fields
~~~~~~~~~~~~~

For creation of contacts with social fields, all field values should correspond specific rules. 

**Twitter**
    Value should be twitter's username, e.g. ``nimble`` or ``twitter``
**Facebook**
    Value should be users's Facebook profile URL, e.g. ``http://www.facebook.com/grigori.rasputin``
**LinkedIn**
    Value should be users's LinkedIn profile URL, e.g. ``http://ua.linkedin.com/in/grigori.rasputin``
**Google+**
    Value should be users's Google+ profile URL, e.g. ``https://plus.google.com/265456261827029907830/``
**Fousquare**
    Value should be: user's id in Foursquare, user's screen name (if set) or Foursquare profile URL. 

In response, for every contact, Nimble adds additional information to fields, fetched from social network:

**avatar_url**
    URL of users's avatar in this social network.
**user_id**
    Network-specific unique ID of user's account.
**user_name**
    User's name, obtained from social account. 
    
.. warning::
    To correctly get data from social networks, user should connect appropriate social network account in Nimble. If no account connected — Nimble sometimes 
    could be not able to fetch data.

Example:

.. code-block:: javascript

    "facebook": [
        {
            "avatar_url": "http://graph.facebook.com/210857648102/picture",
            "group": "Contact Info",
            "user_id": "210857648102",
            "user_name": "Nimble",
            "modifier": "",
            "field_id": "4eabb2494fb88d3352011a82",
            "value": "http://www.facebook.com/nimble",
            "label": "facebook"
        }
    ]


.. _parent-company-type:

Parent company (DEPRECEATED, use :ref:`contact employment <contact-employment-type>`)
~~~~~~~~~~~~~~

Usual string, representing parent company for this person's contact. If company with corresponding name (search are case-insensitie) not found — it will be created. Value record for this field contains additional key ``extra_value``, holding unique ID of parent company.


.. _domain-type:

Domain
~~~~~~

The domain field. Example: ``nimble.com``.
This field satisfies the following conditions:

 * Unique in terms of team. It is possible to have only one company record with particular value in the whole account.
 * Properly formatted. No protocol or path is allowed, it can have 3rd level domain at most.
 * It can be assigned to company records only


.. _dropdown-type:


.. _field-type:

Nimble fields type
--------------------------

Show data about field type. You can't change it after creation. It is a dictionary with at least one field - field_kind.

* **field_kind** — represents type of field in nimble. It can have one of the following values:

    * string — simple field with one line of text
    * long_string — field, containing multiline text
    * choice — drop-down list with predefined values, require additional parameter ``values``. Value of the field contains id of one of choice values
    * number - field with integer or decimal number
    * datetime - string formatted in ISO 8601
    * boolean - field with true/false value
    * address — field with address, that will allow input of address in Nimble default format
    * user - field, containing id of the Nimble user


Examples:

.. code-block:: javascript

    "field_type": {
        "field_kind": "string"
    }

.. code-block:: javascript

    "field_type": {
        "field_kind": "choice",
        "values": {
            "ordering_type": "ordinal",
            "values": [{"id": "string", "value": "string"}]
        }
    }

.. _field-presentations:

Nimble fields presentation
--------------------------

To control, how contacts will look in Nimble, special parameter ``presentation`` included in fields metadata. Usually it is a dictionary with few fields. You can change presentation after field creation. Must match to corresponding field_type. Date and number fields must have an appropriate presentation. There is no presentation for other types

* Date presentation:

    * date_format — strftime-like format template as described in https://docs.python.org/2.7/library/datetime.html#strftime-and-strptime-behavior or null if client should use date format from user settings
    * ignore_specific_time — show if time should be presented in the field. Applicable only if date_format is None. Must be null if date_format specified

    Examples:

    .. code-block:: javascript

        "presentation": {
            "date_format": null,
            "ignore_specific_time": false
        }

    .. code-block:: javascript

        "presentation": {
            "date_format": "%Y-%m-%dT%H:%M:%S",
            "ignore_specific_time": null
        }
* Number presentation:

    * number_type — possible values: "integer", "decimal", "percentage", "financial"
    * fraction_digits — integer >= 1 that shows count of digits after comma. Applicable for decimal and percentage only.

    Examples:

    .. code-block:: javascript

        "presentation": {
            "number_type": "integer",
        }

    .. code-block:: javascript

        "presentation": {
           "number_type": "decimal",
           "fraction_digits": 2
        }

    .. code-block:: javascript

        "presentation": {
           "number_type": "percentage",
           "fraction_digits": 1
        }
    .. code-block:: javascript

        "presentation": {
           "number_type": "financial"
        }



Dropdown fields (Choice type)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Fields, showing as drop-down lists in Nimble. In metadata they have ``field_type`` equal ``choice``. Also, their metadata contains field ``values``, representing drop-down content. This field contains list of dictionaries, having two keys:

**id**
    Value, to be stored in field
**value**
    String, corresponding to this value

Example:

.. code-block:: javascript

    {
  "read_only": false,
  "field_type": {
    "values": {
      "ordering_type": "ordinal",
      "values": [
        {
          "id": "1",
          "value": "Analyst"
        },
        {
          "id": "2",
          "value": "Competitor"
        },
        {
          "id": "3",
          "value": "Customer"
        },
        {
          "id": "4",
          "value": "Investor"
        },
        {
          "id": "5",
          "value": "Lead"
        },
        {
          "id": "6",
          "value": "Partner"
        },
        {
          "id": "7",
          "value": "Press"
        },
        {
          "id": "8",
          "value": "Prospect"
        },
        {
          "id": "9",
          "value": "Reseller"
        },
        {
          "id": "10",
          "value": "Other"
        },
        {
          "id": "12",
          "value": "7"
        }
      ]
    },
    "field_kind": "choice"
  },
  "name": "lead type",
  "available_actions": "edit_choices_only",
  "field_id": "6023b729ec8d835bb32ee4c9",
  "modifier": "",
  "type": "field",
  "multiples": false
    }

.. _address-type:

Address
~~~~~~~

All values represented as dictionary with following keys: ``street``, ``city``, ``state``, ``zip``, ``country``. This dictionary should be dumped to JSON string, and this string should be used as field's value.

Example:

.. code-block:: javascript

    {
        "type": "person",
        "fields": {
            "address": [{
                "value": "{\"street\":\"Test\", \"city\":\"Testing\", \"country\":\"Togo\"}",
                "modifier": "other"
            }]
        }
    }
    
.. _contact-employment-type:

Contact Employment
~~~~~~~

All values represented as dictionary with following keys: ``company_name``, ``title``, ``start_date``, ``end_date``. Where ``start_date`` and ``end_date`` are dates (in the format mm/yyyy) to indicate in what period of time this employment took place. These fields are optional; however, at least one of ``company_name`` or ``title`` must have a non-null value. 

This dictionary should be dumped to JSON string, and this string should be used as field's value.

Example:

.. code-block:: javascript

    {
        "type": "person",
        "fields": {
            "contact employment": [{
                "value": "{\"company_name\": \"4tree GmbH (a wholly owned subsidiary of McKinsey & Company)\", \"end_date\": \"01/2022\", \"is_present\": false, \"start_date\": \"07/2019\", \"title\": \"HR\"}",
            }]
        }
    }



User
~~~~


Field, containing id of the Nimble user.
Example of value:

.. code-block:: javascript

    [
      {
        "is_primary": false,
        "modifier": "",
        "value": "602aaa34f92ea11bb5cebae1",
      }
    ]
