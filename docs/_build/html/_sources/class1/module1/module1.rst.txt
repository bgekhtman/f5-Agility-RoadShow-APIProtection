Making API requests with POSTMAN
=========================================


.. toctree::
   :maxdepth: 1
   :glob:

Using Postman to make API requests
----------------------------------

In this module you will learn how to make API requests with the Postman
client to simulate calls that might be made as part of an application,
for instance, a mobile app, native client app, client side webapp, or
server to server API request.

Connect to Client Jumphost and launch Postman
---------------------------------------------

1. RDP to the client jumphost

2. Launch the Postman application. The icon looks like this:

 .. image:: /_static/image1.png

Learn how to use the preconfigured API request collection
---------------------------------------------------------

In this task you will learn how to use the preconfigured set of requests
in the HR API collection.

1. Click Collections

2. Click HR API

3. Click List Departments

4. Click Send

5. Notice the returned list of departments

 .. image:: /_static/image2.png

Learn how to change environment variables
-----------------------------------------

In this task you will learn how to change the environment variables that
are configured to alter which department you are querying data for. In
this case the variables are used in the URI, but there are other
variables used in some queries in the body as well.

Determine Police Department Salary Total
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Click on the Return Department Salary Total request in the collection

2. Click Send

3. Notice the total returned is 1106915639.7999947

Change environment variable for department
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Notice the GET request URI has a variable in it named {{department}}

 .. image:: /_static/image3.png

2. Notice in the top right we have an environment set named “API
   Protection Lab”.

3. Click the gear in the top right, then click “manage environments”.

 .. image:: /_static/image4.png

4. Click API Protection Lab

 .. image:: /_static/image5.png

5. Change the value for department from “police” to “fire” then click
   update

 .. image:: /_static/image6.png

6. Click the X in the top right to close the manage environments window

 .. image:: /_static/image7.png

Determine Fire Department Salary Total
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Click Send

2. Notice the total returned is now 457971613.68

Return the Environment variables to default
---------------------------------------------------

1. Change the department variable back to “police”