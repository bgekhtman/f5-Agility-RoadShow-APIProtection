Getting Started
---------------

Instructor will provide you with access credentials to training portal as well as login page. 

 .. image:: /_static/portal1.png

Once logged in you should tap on “View”. You should be able to see Virtual Machines as shown below. Copy DNS name of Windows jumpbox to clipboard and use your Remote Desktop client to connect. 

 .. image:: /_static/portal2.png

.. NOTE::
	 All work for this lab will be performed exclusively from the Windows
	 Jumpbox. No installation or interaction with your local system is
	 required.

Lab Credentials
~~~~~~~~~~~~

The following table lists access credential for all required components:

.. list-table::
    :widths: 20 20
    :header-rows: 1
    :stub-columns: 1

    * - **Component**
      - **Credentials**
    * - Windows Jumpbox
      - ``admin``/``admin``
    * - F5 BIG-IP VE
      - ``admin``/``admin``

The BIG-IP VE is accessible from the Windows Jumpbox at https://192.168.1.5


Lab Topology
~~~~~~~~~~~~

The following components have been included in your lab environment:

- 1 x F5 BIG-IP VE (v13.1)
- 1 x Linux Webserver (xubuntu 14.04)
- 1 x Windows Jumphost

On the picture below you can see network topology. Basically, you will be sending various API calls to API server proxied through BIG-IP VE.

 .. image:: /_static/diagram.png

Traffic from Windows Jumpbox will be proxied through the BIG-IP to API Server. 

