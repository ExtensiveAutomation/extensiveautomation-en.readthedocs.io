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
It's possible to generate a new key in the server, to do that you can use the script ``/opt/xtc/current/Scripts/generate-apikey.py``.

.. code-block:: bash
  
  ./generate-apikey.py --user=admin
  API Key ID: admin
  API Key Secret: c025e7a501f144a2e1b40f9f3a91c10a47c8b1d3
  API Key: YWRtaW46YzAyNWU3YTUwMWYxNDRhMmUxYjQwZjlmM2E5MWMxMGE0N2M4YjFkMw==

After that, add the header ``Authorization`` in your HTTP request.

.. code-block:: bash

  Authorization: Basic <my_api_key>

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

+-------------------------+-----------------------------------------------------------------------------------------------------------------+
|/rest/session/login      | `Details <https://demo.extensivetesting.org/web/common-api-rest/index.html#api-Session-sessionLogin>`_          |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+
|/rest/session/logout     | `Details <https://demo.extensivetesting.org/web/common-api-rest/index.html#api-Session-sessionLogout>`_         |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+

**Execute a test**

+-------------------------+-----------------------------------------------------------------------------------------------------------------+
|/rest/tests/schedule     | `Details <https://demo.extensivetesting.org/web/tester-api-rest/index.html#api-Tests-testsSchedule>`_           |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+
|/rest/tests/schedule/tpg | `Details <https://demo.extensivetesting.org/web/tester-api-rest/index.html#api-Tests-testsScheduleTpg>`_        |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+

**Read the result of a test executed**

+-------------------------+-----------------------------------------------------------------------------------------------------------------+
|/rest/results/reports    | `Details <https://demo.extensivetesting.org/web/tester-api-rest/index.html#api-Reports-resultsReports>`_        |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+
|/rest/results/status     | `Details <https://demo.extensivetesting.org/web/tester-api-rest/index.html#api-Results-resultsStatus>`_         |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+
|/rest/results/verdict    | `Details <https://demo.extensivetesting.org/web/tester-api-rest/index.html#api-Results-resultsVerdict>`_        |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+



















