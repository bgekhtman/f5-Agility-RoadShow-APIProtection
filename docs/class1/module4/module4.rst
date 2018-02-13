API Protection By ASM
==============================================

.. toctree::
   :maxdepth: 1
   :glob:


In this module, you will demonstrate how ASM can protect JSON API
against JSON parser attack, SQL Injection, Directory Traversal and DoS
attacks.

Apply API Protections Profiles
-----------------------------------------

In this task, you will apply the DoS protection profile for the API
interface that will protect against known bots and DoS attacks.

1. Navigate to Local Traffic->Virtual Servers->Virtual Server List->
   api.vlab.f5demo.com
2. Open Security->Policies tab.
3. Change the state of **Application Security Policy** to Enable and make sure prebuilt-API_Security_Policy is selected. 
4. Change the state of **DoS Protection Profile** to Enable and select **prebuilt-API_DoS** from the dropdown menu.
5. Change the state of **Log Profile** to Enable. Highlight **Prebuilt-API_Lab_Logging** from the list of available profiles and tap **<<** to move it into Selected.

 .. image:: /_static/image38.png

6. Click Update

Running DoS Attack
------------------

In this task, you will simulate DoS attack with Postman Runner and
observe how it’s been mitigated by Application DoS profile.

1. On the Windows client choose HR\_API\_DoS collection then DoS
   request.

2. Select token “employeeuser” from the list of available tokens and send the API call. Make sure you are getting response http code 200 and list of departments.

3. Click **Save** to save the request with new access token.

4. Click Runner on the top of the window:

 .. image:: /_static/image72.png

5. Choose HR\_API\_DoS collection and use the screenshot below to configure parameters. Ensure right environment has been chosen, iterations updated and Log responses as “For no requests”. Once the parameters have been selected click Run HR_API_DoS. 

 .. image:: /_static/image73.png

6. After a short period of time Postman Runner may report failing
   transactions (it may not and gracefully handle the rate limiting,
   proceed to check logs in next step anyway):

 .. image:: /_static/image74.png

7. On the BIG-IP navigate to Security->Event Logs-> DoS -> Application
   Events

   Look at the details of the attack detection and mitigation
   applied.

 .. image:: /_static/image75.png

Accessing Disallowed URL
--------------------------------

In this task, you will try accessing URL not allowed by ASM policy.

1. On the client machine Postman app proceed to “HR_API_Illigal” collection and select Disallowed URL request.

2. Use previously retrieved access token by setting Authorization Type
   to Oath 2.0 and Available Tokens to hruser (similar to Module 3 Task
   5 without getting a new token).

3. Click Send. ASM should return a blocking page as below:

 .. image:: /_static/image76.png


4. On the BIG-IP navigate to Security->Event Logs->Application
   ->Requests. Click on the last (top) request and look at the violation
   details:

 .. image:: /_static/image77.png

Illegal JSON parameter value - 1
----------------------------------------

In this task, you will simulate attack by running request with illegal
JSON parameter.

1. On the client machine Postman app chose JSON Parsing Array request.

2. Use previously retrieved access token by setting Authorization Type
   to Oauth 2.0 and Available Tokens to hruser (similar to Module 3 Task
   5 without getting a new token).

3. Click Send. ASM should return a blocking page as below:

 .. image:: /_static/image78.png

4. On the BIG-IP navigate to Security->Event Logs->Application
   ->Requests. Click on the last (top) request and look at the violation
   details:

 .. image:: /_static/image79.png


Illegal JSON parameter value - 2 
-----------------------------------------

In this task, you will simulate another attack by running request with
illegal JSON parameter.

1. On the client machine Postman app chose Parameter Length&Signatures
   request.

2. Use previously retrieved access token by setting Authorization Type
   to Oath 2.0 and Available Tokens to hruser (similar to Module 3 Task
   5 without getting a new token).

3. Click Send. ASM should return a blocking page as below:

 .. image:: /_static/image80.png

4. On the BIG-IP navigate to Security->Event Logs->Application
   ->Requests. Click on the last (top) request and look at the violation
   details:

 .. image:: /_static/image81.png

Non-JSON request 
-------------------------

In this task, you will simulate attack by running non JSON request.

1. On the client machine Postman app chose Non-JSON request.

2. Use previously retrieved access token by setting Authorization Type
   to Oath 2.0 and Available Tokens to hruser (similar to Module 3 Task
   5 without getting a new token).

3. Click Send. ASM should return a blocking page as below:

 .. image:: /_static/image82.png

4. On the BIG-IP navigate to Security->Event Logs->Application
   ->Requests. Click on the last (top) request and look at the violation
   details:

 .. image:: /_static/image83.png


Shellshock request 
---------------------------

In this task, you will simulate Shellshock attack by running request
with specific header.

1. On the client machine Postman app chose Shellshock request.

2. Use previously retrieved access token by setting Authorization Type
   to Oath 2.0 and Available Tokens to hruser (similar to Module 3 Task
   5 without getting a new token).

3. Click Send. ASM should return a blocking page as below:

 .. image:: /_static/image84.png

1. On the BIG-IP navigate to Security->Event Logs->Application
   ->Requests. Click on the last (top) request and look at the violation
   details:

 .. image:: /_static/image85.png


More information about BIG-IP configuration settings available here :ref:`F5 BIG-IP configuration deep dive`


