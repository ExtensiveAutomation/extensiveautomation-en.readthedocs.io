Tests Snippets
===================

The interest of reusable tests
  - factorize the test database
  - reuse the tests
  - limit scripting to design scenarios

These types of tests are to be used in ``test plan`` mode.

Shared data between tests
-----------------

Add in the cache a new data
~~~~~~~~~~~~~~~~~~~~~~~~~~
   
.. important:: path of the reusable test ``/Snippets/Cache/01_Set_Cache.tux``

This reusable test consists of saving a value in the data cache during the execution of a test.

Parameter(s) to configure:

+-----------------+-----------------------------------------------------------+
|Parameters       |   Description                                             |
+-----------------+-----------------------------------------------------------+
| DATAS           |   Contains the list of backup valuesr             |
+-----------------+-----------------------------------------------------------+

The ``DATAS`` parameter contains the list of values to save with the format:

.. code-block:: bash
  
  # my comment
  [!TO:CACHE:<MA_CLE>:];my value
  

Example

.. code-block:: bash
  
  # Save misc data
  [!TO:CACHE:EXAMPLE:];hello world

  # Save server information in the cache
  [!TO:CACHE:SERVER_DESCRIPTION:];[!FROM:INPUT:TEST_PURPOSE:]
  
  
.. note:: It is possible to save several values with this test.


Display a value from the cache
~~~~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Cache/02_Log_Cache.tux``

This reusable test makes it possible to display the value of a key present in the cache during the execution of the test.

Parameter(s) to configure:

+-----------------+-----------------------------------------------------------------------+
|Parameters       |   Description                                                         |
+-----------------+-----------------------------------------------------------------------+
| MESSAGES        |   Contains the list of parameters to log in the test                  |
+-----------------+-----------------------------------------------------------------------+
 
.. code-block:: bash
  
  # display cache 
  [!FROM:CACHE:EXAMPLE:]
  
  # log timeout input
  [!FROM:INPUT:TIMEOUT:]
  

.. note:: It is possible to display multiple values at one time

Reset the cache
~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Cache/03_Reset_Cache.tux``

This reusable test makes it possible to totally empty the cache.
No parameters to configure.

.. note:: This test can be used when several scenarios are chained together in a global test.

Checking a value in the cache
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Cache/04_Checking_Cache.tux``

This reusable test makes it possible to check the value in a key present in the cache.

Parameter(s) to configure:

+-----------------+------------------------------------------------+
|Parameters       |   Description                                  |
+-----------------+------------------------------------------------+
| CHECKING        | List of values to check in the cache           |
+-----------------+------------------------------------------------+

Operators available:

+-----------------+-----------------------------------------------------------------------+
|Parameters       |   Description                                                         |
+-----------------+-----------------------------------------------------------------------+
| contains        | Check if the value contains a string                                  |
+-----------------+-----------------------------------------------------------------------+
| matches         | Check if the value matches the regular expression                     |
+-----------------+-----------------------------------------------------------------------+
| ==              | Check if the value equals                                             |
+-----------------+-----------------------------------------------------------------------+
| ! =             | Check if the value is different from                                  |
+-----------------+-----------------------------------------------------------------------+
| >               | Check if the value is greater than                                    |
+-----------------+-----------------------------------------------------------------------+
| <               | Check if the value is less than                                       |
+-----------------+-----------------------------------------------------------------------+
| > =             | Check if the value is greater than                                    |
+-----------------+-----------------------------------------------------------------------+
| <=              | Check if the value is less than                                       |
+-----------------+-----------------------------------------------------------------------+

.. code-block:: bash
  
  # Check if value contains the test string
  [!FROM:CACHE:EXAMPLE:] contains test
  

.. note:: It is possible to check multiple values at one time

Delete entry from the cache
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Cache/02_Delete_Cache.tux``

This reusable test is used to delete a entry in the cache according to the key.

Parameter(s) to configure:

+-----------------+------------------------------------------+
|Parameters       |   Description                            |
+-----------------+------------------------------------------+
| MESSAGES        |  List of keys to delete                  |
+-----------------+------------------------------------------+
 
.. code-block:: bash
  
  # delete the key EXEMPLE from the cache
  [!FROM:CACHE:EXEMPLE:]
   

.. note:: It is possible to delete several keys at one time

Basics actions
----------------

Hold on a test
~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Do/01_Wait.tux``

This reusable test allows you to wait for xx seconds while the test runs.

Parameter(s) to configure:

+-----------------+---------------------+
|Parameters       |   Description       |
+-----------------+---------------------+
| DURATION        | duration in seconds |
+-----------------+---------------------+

Stop a test
~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Do/02_Terminate.tux``

This reusable test makes it possible to force the stopping of a scenario on error occurences.

.. note :: It is possible to customize the stop message by setting the variable ``STOP_TEST_MSG``.

Load test environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Do/03_Initilize.tux``

This reusable test is used to load the test environment data into the cache
(ip addresses, server access account, etc.).

An environment is described with 4 levels:
  - ``environment``
  - ``cluster``
  - ``node``
  - ``instance``
  
An ``environment`` may consist of one or more clusters.

.. code-block:: json
  
  {
    "PLATFORM": {
                   "NOM_CLUSTER_1": [ .. ],
                   "NOM_CLUSTER_2": [ .. ]
        }
  }
  

A ``cluster`` consists of a list of nodes.

.. code-block:: json
  
  {
    "NOM_CLUSTER_1": [
                  { "NOM_NOEUD_1": { .. },
                  { "NOM_NOEUD_2": { .. }
        ]
  }
  

A ``node`` consists of one or more instances.

.. code-block:: json
  
  {
    "NOM_NOEUD_1": {
                  "COMMON": { ... },
                  "INSTANCES": {....}
        }
  }
  

An ``instance`` is made up of several keys / values.

.. code-block:: json
  
  {
    "INSTANCES": {
                  "TYPE_INSTANCE_1": {
                                        "NOM_INSTANCE_1": { ...},
                                        "NOM_INSTANCE_2": { ...}
                                    },
                  "TYPE_INSTANCE_2": { ... }
        }
  }
  

Parameter(s) to configure:

+-----------------+-----------------------------------------------------------------------------------------+
|Parameters       |   Description                                                                           |
+-----------------+-----------------------------------------------------------------------------------------+
| ENVIRONMENT     |  Link to a shared variable or directly contains ``JSON``.                               |
+-----------------+-----------------------------------------------------------------------------------------+
       
Example of a test environment containing an http server with an instance of type rest.
After loading into the cache, the REST instance is accessible by using the ``NODE_HTTP_REST`` key.
All keys in ``COMMON`` are automatically copied to each instance.

.. code-block:: json
  
  {
    "PLATFORM": {
      "CLUSTER": [
        { "NODE": {
                    "COMMON": {
                        "HOSTNAME": "httpbin"
                    },
                    "INSTANCES": {
                        "HTTP": {
                            "REST": {
                                "HTTP_DEST_HOST": "httpbin.org",
                                "HTTP_DEST_PORT": 443,
                                "HTTP_DEST_SSL": true,
                                "HTTP_HOSTNAME": "httpbin.org",
                                "HTTP_AGENT_SUPPORT": false,
                                "HTTP_AGENT": null
                            }
                        }
                    }
                 }
            }
    ]
  },
  "DATASET": [    ]
  }
  

The ``DATASET`` key can contain datasets.

Data Generators
-----------

Hash SHA
~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Generators/01_Gen_Sha.tux``

This reusable test is used to generate a hash of a value and store it in the cache.

Parameter(s) to configure:

+-----------------+----------------------------------------------------------+
|Parameters       | Description                                              |
+-----------------+----------------------------------------------------------+
| DATA_IN         | Hash character string                                    |
+-----------------+----------------------------------------------------------+
| CACHE_KEY       | Key name                                                 |
+-----------------+----------------------------------------------------------+
| SHA             | Type of hash realize (sha1, sha256, sha512)              |
+-----------------+----------------------------------------------------------+

Hash MD5
~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Generators/02_Gen_Md5.tux``

This reusable test is used to generate md5 hash and store it in the cache.


Parameter(s) to configure:

+-----------------+--------------------------------------------------------------+
|Parameters       |   Description                                                |
+-----------------+--------------------------------------------------------------+
| DATA_IN         | Hash character string                                        |
+-----------------+--------------------------------------------------------------+
| CACHE_KEY       | Name of the key or the result will be saved in the cache     |
+-----------------+--------------------------------------------------------------+

UUID
~~~~

.. important:: path of the reusable test ``/Snippets/Generators/03_Gen_Uuid.tux``

This reusable test is used to generate an uuid and store it in the cache.

Parameter(s) to configure:

+-----------------+-----------------------------------------------------------+
|Paramètres       |   Description                                             |
+-----------------+-----------------------------------------------------------+
| CACHE_KEY       | Name of the key to save the result in the cache           |
+-----------------+-----------------------------------------------------------+
 
BASE64
~~~~~~

.. important:: path of the reusable test ``/Snippets/Generators/04_Gen_Base64.tux``

This reusable test is used to encode or decode a string and store the result in the cache.

Parameter(s) to configure:

+-------------------+----------------------------------------------------------------------------------------+
|Parameters         |   Description                                                                          |
+-------------------+----------------------------------------------------------------------------------------+
| CACHE_KEY         | Name of the key to save the result in the cache                                        |
+-------------------+----------------------------------------------------------------------------------------+
| DECODE            | Set to True to encode                                                                  |
+-------------------+----------------------------------------------------------------------------------------+
| ENCODE            | To set to True to decode                                                               |
+-------------------+----------------------------------------------------------------------------------------+
| URLSAFE           | Set to True if the result after encoding is to be used in an url                       |
+-------------------+----------------------------------------------------------------------------------------+
| STR_BASE64        | Character string to encode / decode                                                    |
+-------------------+----------------------------------------------------------------------------------------+

Networks protocols
------------------

SSH
~~~

.. important:: path of the reusable test ``/Snippets/Protocols/01_Send_SSH.tsx``

This reusable test is used to send a sequence of ssh commands.
It is used in conjunction with the reusable test ``/Snippets/Do/03_Initilize.tux`` to load an environment into the cache.

Parameter(s) to configure:

+-----------------+----------------------------------------------------------+
|Parameters       |   Description                                            |
+-----------------+----------------------------------------------------------+
| SERVERS         | List of servers to contact                               |
+-----------------+----------------------------------------------------------+
| COMMANDS        | List of commands to run on the remote machine            |
+-----------------+----------------------------------------------------------+
| TIMEOUT_CONNECT | Max time to connect to the remote machine                |
+-----------------+----------------------------------------------------------+

The `COMMANDS` parameter is waiting for one or more blocks of 4 lines.
Each block must respect the following formalism:
  1. A comment explaining the action, this information is used to initialize the test step
  2. The command to execute
  3. The string expected on the screen, if the expected value is not found then the step will be in error. (optional line)
  4. empty
 
.. warning:: Each block will be executed even if the previous one is in error.
    
The following example performs the following actions:
  1. Send 3 pings on the remote machine whose ip is stored in the ``DEST_HOST`` cache
  2. Verification of having the message on the screen indicating that the 3 packets have been sent. Then the mddev value is stored in the cache with the ``STATS`` key
  3. The second block clears the screen by sending the clear command.
  4. Finally the test is waiting to find the prompt on the screen
  
.. code-block:: bash
  
  # send a ping 
  ping -c 3 [!CACHE:SVR:DEST_HOST:]
  .*3 packets transmitted, 3 received, 0% packet loss.*mdev = [!CAPTURE:STATS:] ms.*
  
  # clear the screen
  clear
  .*root@.*
  

.. note:: It is possible to run the test multiple times by providing a server list.

.. note:: 
   By default, the test waits for a maximum of 20 seconds to find the expected string.
   This value can be configured with the ``TIMEOUT`` parameter.
  
.. note:: 
   By default, the test waits 10 seconds to connect to the remote server.
   This value can be configured with the ``TIMEOUT_CONNECT`` parameter.

HTTP
~~~~

.. important:: path of the reusable test ``/Snippets/Protocols/02_Send_HTTP_CURL.tsx``

This reusable test makes it possible to send an HTTP request by checking the response received.

Parameter (s) to configure the HTTP request to send:

+-----------------+---------------------------------+
|Parameters       |   Description                   |
+-----------------+---------------------------------+
| HTTP_REQ_HOST   | URL destination                 |
+-----------------+---------------------------------+
| HTTP_REQ_BODY   | Body of the query               |
+-----------------+---------------------------------+
| HTTP_REQ_HEADERS| List of headers to add          |
+-----------------+---------------------------------+
| HTTP_REQ_METHOD | HTTP method (GET, POST, etc.)   |
+-----------------+---------------------------------+

Parameter (s) to configure the expected HTTP response (and which will allow to consider the test as valid):

+-------------------+----------------------------------------------------+
|Parameters         |   Description                                      |
+-------------------+----------------------------------------------------+
| HTTP_RSP_BODY     | Body of the expected answer.                       |
+-------------------+----------------------------------------------------+
| HTTP_RSP_BODY_JSON| JSON expected in the answer with json path         |
+-------------------+----------------------------------------------------+
| HTTP_RSP_BODY_XML | XML expected in the answer with xpath              |
+-------------------+----------------------------------------------------+
| HTTP_RSP_CODE     | The expected HTTP code. 200 by default             |
+-------------------+----------------------------------------------------+
| HTTP_RSP_HEADERS  | List of expected headers                           |
+-------------------+----------------------------------------------------+
| HTTP_RSP_PHRASE   | The expected HTTP sentence. OK by default          |
+-------------------+----------------------------------------------------+
| HTTP_RSP_VERSION  | The expected HTTP version. HTTP / 1. [0|1] default |
+-------------------+----------------------------------------------------+

.. image:: /_static/images/examples/snippets_http_rsp.png

.. note:: 
  The use of regular expressions is possible to check or save a value in the body of the answer or in the headers.
  
  .. image:: /_static/images/examples/snippets_http_capture.png

User Interface
---------------------

Open application in Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/UI/01_Win_OpenApp.tux``

This snippet enable to open a application on a Windows or Linux machine.
The parameter ``AGENT_GUI`` must be configured with the agent to use.

Parameter(s) to configure:

+-----------------+--------------------------------------------------------+
|Parameters       |  Description                                           |
+-----------------+--------------------------------------------------------+
| APP_PATH        |  Application path to open                              |
+-----------------+--------------------------------------------------------+

.. warning: a`sikulix-server` agent is mandatory.

Close an application in Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/UI/02_Win_CloseApp.tux``

This snippet enable to close a application on a Windows or Linux machine.
The parameter ``AGENT_GUI`` must be configured with the agent to use.

Parameter(s) to configure:

+-----------------+---------------------------------------------+
|Parameters       |   Description                               |
+-----------------+---------------------------------------------+
| APP_NAME        |  Name of the application to close           |
+-----------------+---------------------------------------------+

.. warning: un agent de type ``sikulix-server`` est obligatoire.


Open a web browser
~~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/UI/03_OpenBrowser.tux``

This snippet enable to open a browser on a Windows or Linux machine.
The parameter ``AGENT_GUI_BROWSER`` must be configured with the agent to use.

Parameter(s) to configure:

+-----------------+--------------------------------------+
|Parameters       |   Description                        |
+-----------------+--------------------------------------+
|LOADING_URL      |  Website url to load                 |
+-----------------+--------------------------------------+

It's possible to select the browser to user, the following browsers are supported:
 - Firefox
 - Chrome
 - Internet Explorer
 - Opera
 - Edge

.. image:: /_static/images/examples/selenium_browser.png
 
.. note:: the url must started with ``http://`` or ``https://``

.. warning: a ``selenium(2|3)-server`` agent is mandatory.


Close a web browser
~~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/UI/03_CloseBrowser.tux``

This snippet enable to close a browser on a Windows or linux machine.
The parameter ``AGENT_GUI_BROWSER`` must be configured with the agent to use.

.. warning: a ``selenium-server`` agent is mandatory.


Checks
-------------

XML checks
~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Verify/01_Check_XML.tux``

This snippet enable to check a XML content with xpath.

Parameter(s) to configure:

+-----------------+------------------------------------+
|Parameters       | Description                        |
+-----------------+------------------------------------+
| XML_STR         | raw XML to inspect                 |
+-----------------+------------------------------------+
| XML_XPATH       | xpath                              |
+-----------------+------------------------------------+
| XML_NAMESPACES  | namespaces definitions             |
+-----------------+------------------------------------+

Example of value for the ``XML_STR`` parameter:

.. code-block:: xml
  
  <NewDataSet>
  <Table>
    <Country>France</Country>
    <City>Le Touquet</City>
  </Table>
  <Table>
    <Country>France</Country>
    <City>Agen</City>
  </Table>
  <Table>
    <Country>France</Country>
    <City>Cazaux</City>
  </Table>
  <Table>
    <Country>France</Country>
    <City>Bordeaux / Merignac</City>
  </Table>
  <Table>
    <Country>France</Country>
    <City>Bergerac</City>
  </Table>
  </NewDataSet>
  
Example of value for the ``XML_XPATH`` parameter.

.. code-block:: json
  
  (//NewDataSet/Table)[1]/City	[!CAPTURE:CITY:]
  
The value will be accessible from the cache with the ``CITY`` key.

JSON checks
~~~~~~~~~~~~~~~~~~~~

.. important:: path of the reusable test ``/Snippets/Verify/01_Check_JSON.tux``

This snippet enable to check JSON content with jsonpath

Parameter(s) to configure:

+-----------------+---------------------------------------+
|Parameters       |   Description                         |
+-----------------+---------------------------------------+
| JSON_STR        | Json to inspect                       |
+-----------------+---------------------------------------+
| JSON_XPATH      | jsonpath                              |
+-----------------+---------------------------------------+

Example of value for the ``JSON_STR`` parameter:

.. code-block:: json
  
  {
   "args": {}, 
   "headers": {
   "Connection": "close", 
   "Host": "httpbin.org", 
   "User-Agent": "ExtensiveTesting"
  }, 
   "origin": "190.117.217.129", 
   "url": "https://httpbin.org/get"
  }
  
Example of value for the ``JSON_XPATH`` parameter. 

.. code-block:: json
  
  headers.Connection	[!CAPTURE:CX:]

The value will be accessible from the cache with the ``CX`` key.
