===============================
Tutorial: Obtain Nimble API Key
===============================

.. contents::

.. _obtain-token-tutorial:

Introduction
------------

This document will describe authorization flow that return the authorization token that allow to make requests to Nimble API and access resources 
to which access has been granted for user. For For authorization Nimble use OAuth 2.0 protocol with bearer tokens. All technical details can be 
read in `RFC6749 <http://tools.ietf.org/html/rfc6749>`_ and `RFC6750 <http://tools.ietf.org/html/rfc6750>`_, but you don't need to read them 
(unless you want to know more details on OAuth 2.0) — every detail that need to obtain access token and use this token for requesting resource on 
behalf of user will be described in this document.
 

Terminology
-----------
**User**
    Person who has an account inside Nimble and owner of resources to which API provide access

**Client**
    Service that request a token and want to make requests to the Nimble API on behalf of User

**Authorization server**
    Server that allow User to grant access for Client to use his resources

**Resource server**
    Server that returns User's resources to Client if it was granted for access by User

**Bearer token**
    Token that Client received after User has granted access. Possession of this token allows client to make requests to Resource server in order 
    to receive Client's resources.


Prerequisites
-------------
In order to create a Client for Nimble API you need to have to register your application in our DB and get Client Secret and Client Id. 
Its can be done on the page with this link: https://developers.nimble.com/user/register. You probably have done this already.


Authorization process overview
------------------------------
For giving you a good overview of process we will use scheme and give a brief explanation to the each step on scheme. Steps are shown by the arrows and has a letters assigned to each step on scheme.

.. _auth-process-image:
.. image:: _static/auth_project.png
    :scale: 40%
    :alt: oauth process chart
    :align: center

Let's go over a scheme step by step.

* **Step A** — You have some product (Client) that wants to use Nimble Data for some purposes. User wants to use Client and you need to retrieve a grant of user to operate the data from Nimble on his behalf. So, user has something that allows to initiate this process from Client.

* **Step B** — Your client open a page that points to Authorization Server providing a params specified on scheme. As a params, you need to send  your API key and URI of client to which Authorization Grant Code will be returned. For details see: :ref:`request-grant-code`.

* **Step C** — Auth server using your API Key (Client Key) creates a link to which user will be directed and send a redirect response. User will be automatically redirected to the page where he can put his credentials and grant access. Note that now user is on side of Authorization Server.

* **Step D** — As soon as user finished a process of providing access, Authorization Server takes a redirect URI that you specified on step B and sends code to that URI. Response details :ref:`explained here <token-response-details>`.

* **Step E** — Using this code you make a `application/x-www-form-urlencoded` request to the Authorization Server where in body you put code retrieved on previous step, your Client Secret, Client Id and Grant Type you want to receive. It is always `authorization_code`. For details see: :ref:`request-access-token`.

* **Step F** — If everything is valid then you will receive response from server with Access Token and Refresh Token. Now you are able to do a requests to the Nimble API using Access Token until it valid. Using Refresh Token you will be able to renew this token without involving User second time. For details see: :ref:`token-refresh`.

.. _request-grant-code:

Requesting Authorization Grant Code
-----------------------------------
You should use this request on step B of :ref:`Authorization Process<auth-process-image>`. You need to open a page for user with this endpoint and provide a Redirect URI on which your handler will be able to catch the code from Authorization Server that will be returned when User successfully grant you a permission to use Nimble API.

**Endpoint**::

   GET https://api.nimble.com/oauth/authorize


**Params**:
    **client_id** 
        *required* — Your Client Key from Application Page.
    **redirect_uri** 
        *required* — URI where you have a handler who will catch a code and finish the Process, see note below.
    **response_type**
        *required* — must be set to ``code``. We don't support Implicit Flow, so ``code`` is the only available option now. 
    **scope**
        *optional* — for now there is only one scope for Nimble API, so skip this parameter for now.
 
    .. note:: Please note, that main value for redirect URL is specified in application settings on developer portal. ``redirect_uri`` parameter in URL could be used only to overwrite path part in redirect URL. So, ``redirect_uri`` should have exactly same URI, as specified in application settings. 
    
    
**Example request**::

    GET https://api.nimble.com/oauth/authorize?client_id=5f96b5e9adaxzca93x1213123132&redirect_uri=https%3A%2F%2Fyourportal.com%2Fauth%2Fpassed&response_type=code


**Successful response**:

    First, user will be redirected to the page on Authorization Server with hostname ``https://api.nimble.com/oauth/authorize``

    As soon as he provided his credentials, you will receive a request like listed below on your ``Redirect URI``::

       https://yourportal.com/auth/passed?code=LTM4M 


**Error response**:

    If the request is missing or has incorrect parameters, the user-agent will be redirected back to the redirect URI provided.
    The redirection will contain parameters specifying the error.

    *Example Invalid Authorization Request Redirect*::
    
        http://www.myapp.com/oauth?error=invalid_request&error_description=Invalid%20URL

    After selecting Login, the user will be validated. If user validation is successful, a consent page is displayed. If user validation is unsuccessful, 
    the user-agent will be redirected to the redirect URI provided in the initial request. This redirection will include additional parameters 
    specifying the error.

    *Example Unsuccessful Validation Redirect*::
    
        http://www.myapp.com/oauth?error=access_denied&error_descripton=Validation%20errors

    If user click Deny on the grant permission page then another error will be sent.

    *Example Deny Consent Redirect*::
    
        http://www.myapp.com/oauth?error=access_denied&error_description=User%20denied%20access
        
 
.. _request-access-token:

Requesting Access Token
-----------------------
As soon as User complete step C your handler will catch step D. You need to listen for redirect on your Redirect URI. **Code returned to you isn't access token yet!** You still need to obtain the authorization token. Note, that this code is valid for a short period time and if you not intiate request to access token as soon as you receive a code then received code can become invalid and User will need to reinitiate a process once again. So, on step E you need to receive access to token for which user granted you. 

The Client should use the authorization code obtained to request an access token. When requesting an access token, you SHOULD specify required data as form parameters. Client application secret is needed for client authentication. When specifying client_id and client_secret as form parameters, the ``Content-Type`` header MUST be set to ``application/x-www-form-urlencoded``. Request should be done via HTTPS only.


**Endpoint**::

 POST https://api.nimble.com/oauth/token


**Parameters:**

    **grant_type**
        *required* — must be set to ``authorization_code``. You need to receive an Access token.
    **code**
        *required* — code that you received on step D. This code has a short-valid time, so initiate request for token as soon as you receive it.
    **redirect_uri**
        *required* — redirect URI for your application. Should be equal to ``redirect_uri``, provided during :ref:`request-grant-code`.
    **client_id**
        *required* — your Client API key.
    **client_secret**
        *required* — your Client API secret key.

**Headers**:

    ``Content-Type: application/x-www-form-urlencoded; charset=UTF-8``
        *required* — you need to specify this header always 

**Example Request**::

    POST /oauth/token HTTP/1.1
    Host: api.nimble.com
    Content-Type: application/x-www-form-urlencoded; charset=UTF-8

    Body : client_id=5f96b5e9a6b7478e15ee574a426aa063&redirect_uri=http%3A%2F%2Flocalhost%3A3000%2Fauth&code=LTM4M&grant_type=authorization_code&client_secret=89bb4ffb4f264bff

 
.. _token-response-details:

*Successfull Response JSON*:

.. code-block:: javascript

    {
        "access_token": "bf086611-9e97-4d11-9cd7-3c86dec0bbd4",
        "token_type": "bearer",
        "expires_in": 599,
        "refresh_token": "515ac59b-6518-49a2-81d6-54f91ee74c4a",
        "scope": "read write"
    }



API requests using Access Token
-------------------------------
Now when we have Access Token Received you need to store it and use for any requests for Nimble Data on behalf of user. This process described in :ref:`second part of our tutorial <making-requests-tutorial>`.

 
.. _token-refresh:

Refresh token after expiration without user input
-------------------------------------------------
The application uses the refresh token to extend the validity of the access token provided with the refresh token. When refreshing an access token, you should specify required data as a form parameters. Client application secret is needed for client authentication. ``Content-Type`` header must be set to ``application/x-www-form-urlencoded``.
  
Parameters:

    **client_id** 
        Client identifier used to obtain the authorization code
    **client_secret** 
        Client secret code
    **grant_type** 
        Must be set to ``refresh_token``
    **refresh_token**
        Refresh token obtained from the access token request
    **redirect_uri**
        *required* — redirect URI for your application. Should be equal to ``redirect_uri``, provided during :ref:`request-grant-code`.

Example Request::

    POST /oauth/token HTTP/1.1
    Host: https://api.nimble.com/
    Content-Type: application/x-www-form-urlencoded; charset=UTF-8
    
    client_id=3e8471e7516a0c85ef35ab1d23f1bdf1&client_secret=737d10deba3fd124&grant_type=refresh_token&refresh_token=5f752714eddb07a3e41c2a3311f514e1&redirect_uri=http%3A%2F%2Flocalhost%3A3000%2Fauth

Example Response:

.. code-block:: javascript

    {
        "access_token": "1d7bc7328b402f4826e17607e364bc6a",
        "expires_in": 559,
        "refresh_token": "f35c2165112fda74f79b408cc253485fcdfd888a"
    }


Examples
--------
For your convinience we created some examples:

`Python authorization example <https://github.com/nimblecrm/python-example>`_. Actual code implementation on Python and Tornado

`Ruby authorization example <https://github.com/nimblecrm/ruby-example>`_. Implementation of authorization process in Ruby

Troubleshooting & Feedback
--------------------------
If you have any problems or want to submit feedback feel free to go to our support forum or email us at api-support@nimble.com

