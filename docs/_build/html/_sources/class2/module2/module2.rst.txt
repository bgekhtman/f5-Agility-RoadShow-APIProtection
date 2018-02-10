BIG-IP API requests protection
=========================================

.. toctree::
   :maxdepth: 1
   :glob:

In this module you will examine security policies created for API server protection. 

Logging profile
-----------------------------------

In order to check for logging configuration settings to Security -> Event Logs -> Logging Profiles —> 	prebuilt-API_Lab_Logging and check logging settings. 

 .. image:: /_static/log.png

Application Security Policy
-----------------------------------

Go to Security -> Application Security -> Security Policies —> prebuilt-API_Security_Policy and make sure it is in blocking mode.

 .. image:: /_static/asmpolicy.png

Check hostname configuration for requested secured by this policy. Go to Security -> Application Security -> Headers -> Hostnames and make sure api.vlab.f5demo.com is configured. Any request with different hostname will be blocked by the policy.

.. image:: /_static/hostname.png

Check JSON profile configuration. Go to Security -> Application Security -> Content
   Profiles -> JSON Profiles —> prebuilt-API_LAB_JSON and check its settings.

.. image:: /_static/json.png

Check for allowed URLs in the security policy. Go to Security -> Application Security -> Allowed URLs -> Allowed HTTP URLs. Click on **/department*** and check Header-Based Content Profiles - Make sure prebuilt-API_LAB-JSON content profile is attached to this URL.

.. image:: /_static/urljson.png

Check for allowed parameters in the security policy. Go to Security->Application Security->Parameters->Parameters List. Check length and other settings by clicking into each parameter. For example maximum length for parameter “salary” is 10.

.. image:: /_static/parameter.png

Check attack signatures configuration. Attack signature set is required to limit policy only to relevant signatures for the protected API. Go to Security -> Application Security -> Policy -> Policy Properties and click on Attack Signatures Configuration.

.. image:: /_static/signatures.png

Click on prebuilt-API_Lab_SigSet, scroll down to “Signatures” section and examine the set of signatures.

API DoS Protection Profile 
-----------------------------------

In this section you will check for configuration settings in DoS protection profile that will protect API interface against known bots and DoS attacks.
Navigate to Security -> DoS Protection -> DoS Profiles and click on prebuilt-API_DoS profile. Check for the example of white list for known ip addresses.

.. image:: /_static/whitelist.png

Click on **Application Security** tab and make sure its enabled and Heavy URL Protection is activated. 

.. image:: /_static/dos1.png

Go to **Bot Signatures** section, expand Bot Signature Categories and make sure Benign category is selected for blocking. 

Go to **TPS-based Detection**, make sure it is in blocking mode and Thresholds Mode is set to Manual. Expand “How to detect attackers and which mitigation to use” section and check setting in subsection “By Source IP”.

.. image:: /_static/ratelimit.png

.. HINT:: More information on DoS Prevention available in the manual:

 https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/asm-implementations-12-1-0/1.html


