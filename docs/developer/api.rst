API
===

Authentication
----------------

Authentication in the API REST can be done with 2 methods:
 - By using the function login to obtain a session cookie
 - with basic auth
 
Basic
~~~~~~~~

The basic auth must be used with the api key available through the web interface.
The re-generation of the api key can be done for now only on the server.

.. code-block:: bash
  
  python extensiveautomation.py --apikey admin
  API Key ID: admin
  API Key Secret: d30278d49e4845e45daa748873e2171b14a0c55a

After that, add the header ``Authorization`` in your HTTP request.

.. code-block:: bash

  Authorization: Basic base64(key_id:key_secret)

.. note:: With the basic auth, it's not necessary to call the login function.

Session cookie
~~~~~~~~~~~~~~~~~

The authentication by cookie can be done by calling the function ``login`` to generate a cookie for the session.
This cookie must be present on all next http request in the header ``Cookie``.

.. code-block:: bash

  Cookie: session_id=NjQyOTVmOWNlMDgyNGQ2MjlkNzAzNDdjNTQ3ODU5MmU5M
  
Usage example
----------------

The REST api is available throught the tcp port ``443`` (https) with the uri ``/rest``.

The following example show how to execute a test with the basic auth.

.. code-block:: json
  
  POST /rest/tests/schedule HTTP/1.1
  [...]
  Authorization: Basic YWRtaW46N2UwMDExY2I3Y2ZhMGQ1MjM4NGQ1YWYyM2QyODBiMjUyM2EzMTA3ZA==
  Content-Type: application/json; charset=utf-8 
  [...]
  
  {
    "project-id": 1,
    "test-extension": "tux",
    "test-name": "01_Wait",
    "test-path": "/Snippets/Do/",
    "test-inputs": [ {"name": "DURATION", "type": "int", "value": 5} ]
  }
  

Received response:

.. code-block:: json
  
  {
    "cmd": "/tests/schedule",
    "message": "background"
    "test-id": "a3f19398-b463-41e8-9e43-af86aac44a59",
    "task-id": 17,
    "tab-id": 0
    "test-name": "01_Wait"
  }
  


Ressources
----------

Description of most important functions:

**Authentication**

+-------------------------+----------------------------------------------------------------+
|/rest/session/login      |    |
+-------------------------+----------------------------------------------------------------+
|/rest/session/logout     |    |
+-------------------------+----------------------------------------------------------------+

**Execute a test**

+-------------------------+------------------------------------------------------------------+
|/rest/tests/schedule     |    |
+-------------------------+------------------------------------------------------------------+
|/rest/tests/schedule/tpg |    |
+-------------------------+------------------------------------------------------------------+

**Read the result of a test executed**

+-------------------------+----------------------------------------------------------------------------+
|/rest/results/reports    |    |
+-------------------------+----------------------------------------------------------------------------+
|/rest/results/status     |    |
+-------------------------+----------------------------------------------------------------------------+
|/rest/results/verdict    |    |
+-------------------------+----------------------------------------------------------------------------+



















