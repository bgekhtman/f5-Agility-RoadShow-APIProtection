Implement Coarse-Grain Authorization
------------------------------------

In this module you will implement authorization requirements. You will
require a valid JWT (JSON Web Token) before a client can access the API.
You will then gather a valid JWT and leverage it to make an API request.

Add the policies to the virtual server
--------------------------------------

In this task you will add the policies you created to the virtual
server.

1. Click Local Traffic -> **Virtual Servers**

2. Click **api.vlab.f5demo.com**

3. Change Access Profile from none to **api-psp** (NOT as-psp)

4. Change Per Request Policy from none to **api-prp**

 .. image:: /_static/image19.png

5. Click Update

Test access to the API
------------------------------

In this task you will test your access to the API and find it is blocked
because you do not present a valid JWT.

1. Open Postman on the jumphost client

2. Select List Departments from the HR API collection and send the
   request

3. Review the response, note the 401 unauthorized and the header
   indicating you did not present a valid token

 .. image:: /_static/image20.png

Get a JWT from the Authorization Server
---------------------------------------

1. Click the **type** drop down under the **authorization** tab.

2. Select **OAuth 2.0**

3. Click **Get New Access Token**

 .. image:: /_static/image21.png

Postman provides a mechanism to handle the OAuth client workflow
automatically. This means it will handle getting the authorization code
and then exchange it for an access token, which you will use. Without
this you would make two separate requests, one to get an authorization
code and another to exchange that for an access token.

1. Fields should be prefilled, but verify they match the below:

+------------------------+-----------------------------------------------------+
| Field                  | Value                                               |
+========================+=====================================================+
| Token name             | employeeuser                                        |
+------------------------+-----------------------------------------------------+
| Grant Type             | Authorization Code                                  |
+------------------------+-----------------------------------------------------+
| Callback URL           | https://www.getpostman.com/oauth2/callback          |
+------------------------+-----------------------------------------------------+
| Auth URL               | https://as.vlab.f5demo.com/f5-oauth2/v1/authorize   |
+------------------------+-----------------------------------------------------+
| Access Token URL       | https://as.vlab.f5demo.com/f5-oauth2/v1/token       |
+------------------------+-----------------------------------------------------+
| Client ID              | 9f1d39a8255e066b89a51f56b27506d39442c4f608c2f859    |
+------------------------+-----------------------------------------------------+
| Client Authenticatin   | Send as Basic Auth header                           |
+------------------------+-----------------------------------------------------+

Most of this data is provided by the authorization server. The callback
URL specified here is a special callback URL that the Postman client
intercepts and handles rather than calling out to the getpostman.com
website.

 .. image:: /_static/image22.png

1. Click **Request Token**

2. Select **employeeuser** in the authentication window that pops up and
   click **Logon**

3. Click the **X** to close this window

4. Make sure **employeeuser** is selected under Available Tokens drop
   down

5. Select **Request Headers** from the Add Authorization Data To drop
   down

6. Click **Preview Request**, the result should be this:

 .. image:: /_static/image23.png

7. Go to the **Headers** tab and review the inserted **Bearer** token
   header:

 .. image:: /_static/image24.png

Send the request with JWT and review response
---------------------------------------------

1. Click **Send** and review the response.

2. Note that now it is a 200 OK instead of 401 Unauthorized and that you
   have response data in the body.

 .. image:: /_static/image25.png

You have now implemented coarse grained authorization and are requiring
clients to request a JWT from a trusted authorization server before
allowing access to the API.

