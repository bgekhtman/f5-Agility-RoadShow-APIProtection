BIG-IP Authorization access control configuration
=========================================

.. toctree::
   :maxdepth: 1
   :glob:

BIG-IP APM can be used as authorization server as well resource server. On the diagram below this is shown as separate hardware components. 

 .. image:: /_static/scheme.png

Although hardware segregation is not a strict requirement and those components can be hosted on the same BIG-IP, only VIPs should be different. In this lab we have used  **api.vlab.f5demo.com** as resource server and **as.vlab.f5demo.com** as an authorization server. 
Check the steps below in order to configure coarse-grain authorization. 

Creation of JWK (JSON Web Key)
-----------------------------------

In this task you will check configuration settings for JWK which is used for validating the sent JWT.In this lab we have used Octet and a shared secret, but options includesolutions like public/private key pair as well.

Go to Access -> Federation -> JSON Web Token -> Key Configuration -> prebuilt-api-jwk

It is configured according to data below

+---------------------+-----------+
| Field               | Value     |
+=====================+===========+
| Name                | api-jwk   |
+---------------------+-----------+
| ID                  | lab       |
+---------------------+-----------+
| Type                | Octet     |
+---------------------+-----------+
| Signing Algorithm   | HS256     |
+---------------------+-----------+
| Shared Secret       | secret    |
+---------------------+-----------+

OAuth provider
--------------------------------

In this task you will check configuration settings for an OAuth provider so that JWT can be validated.

Go to Access -> Federation -> OAuth Client/Resource Server ->
   Provider -> prebuilt-as-provider

The configuration settings is shown below.

 .. image:: /_static/auth2.png

Most of these settings have been discovered automatically from Authorization Server with the use of OIDC.

Token Configuration
-------------------------------------

In this task you will check the configuration of some of the values retrieved automatically via OIDC discover tool. Those values had to be adjusted manually because the OIDC AS cannot provide you with the values specific to your audience.

1. Go to Access -> Federation -> JSON Web Token -> Token Configuration
   -> auto_jwt_prebuilt-as-provider

2. Make sure **https://api.vlab.f5demo.com** have been defined as Issuer 

 .. image:: /_static/jsontoken.png

3. Under Additional Key make sure prebuilt-api-jwk is added into Allowed

 .. image:: /_static/apijwk.png

The object prebuilt-as-jwk was precreated for the authorization server
function. It matches api-jwk (and prebuilt-api-jwk) exactly because a
shared key is needed on both the authorization server and resource side.
In this case you could have reused it instead of making a new one, but
in production your authorization server may not be the Big-IP you are
protecting the API server on, and you would need to create it as shown
here.

JWT Provider
-----------------------------

In this task you will check configuration for a JWT provider that can be selected in a per request or per session policy for JWT validation.

Go to Access -> Federation -> JSON Web Token -> Provider List -> prebuilt-as-jwt-provider

Make sure prebuilt-as-provider is selected

 .. image:: /_static/provider.png

Per-session policy
-----------------------------

In this task you will check per session policy which validating the
JWT token and collecting the claims data from parameters inside the JWT.

Go to Access -> Profiles/Policies -> Access Profiles (Per-Session Policies) -> prebuilt-api-psp

Make sure profile type is set to OAuth-Resource Server and Profile Scope is Profile.

 .. image:: /_static/policy1.png

Also make sure that the User Identification Method is set to OAuth token and default language is English.

 .. image:: /_static/policy2.png

Click **Access Policy** tab and then click **Edit Access Policy for Profile “prebuilt-api-psp”**. Examine the policy and click on OAuth Scope.
Make sure Token Validation Mode is set to “Internal” and JWT Provider List is set to as-jwt-provider. The validation mode is set to be internal because JWT token will be validated internally instead of making an external call.

 .. image:: /_static/policy3.png

Per-request policy
-----------------------------

You will check a per request policy to validate authorization on each request by checking for the presence and validity of a JWT.

Go to Access -> Profiles/Policies -> Per-Request Policies -> prebuilt-api-prp —> Click **Edit**

 .. image:: /_static/request1.png

Click on **URL Branching** and and then **Branch Rules**. Note the URL expression.

 .. image:: /_static/request2.png

Click on **Group Check** and and then **Branch Rules**. Note the expression.

 .. image:: /_static/request3.png

Close the tab in the browser

