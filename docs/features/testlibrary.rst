The fundamentals
================

The test framework provides a framework for standardizing the creation of test cases.

The main features are:
  - the support of test cases with steps
  - Support extensions to communicate with the system to test or control
  - automatic generation of test reports.
  
Test case
-----------

The creation of a test case in the solution is standardized.

A test case is divided into 4 sections:
  - ``description``: description of the different stages of the test
  - ``prepare``: preparation of adapters and libraries for communicating with the system to be tested or piloted
  - ``definition``: test flow
  - ``cleanup``: cleaning phase
 
The result of a test case is automatically calculated by the framework when the test is completed
according to the different stages defined.

There are 3 possible results:
  - ``PASS``: all the steps of the tests have been successfully executed
  - ``FAILED``: at least one step is in error after execution
  - ``UNDEFINED``: at least one step of the test has not been executed
  
.. note:: The ``cleanup`` section is always called, even if there is an error.

Test steps
--------------

A test case is divided into sub-steps.

A step is defined by:
  - a summary of the action to be carried out
  - the detailed description of the action to be carried out
  - the description of the expected result to validate the step.

The definition of the test steps must be done in the ``description`` section:

.. code-block:: python

  self.step1 = self.addStep(
						expected="Logged in", 
						description="Login throught the rest api", 
						summary="Login throught the rest api", 
						enabled=True
					)
  

The result of a step is to be specified in the ``definition`` section

Example to set the result to ``PASS`` or ``FAILED``

.. code-block:: python

  self.step1.setPassed(actual="step executed as expected")
  
  self.step1.setFailed(actual="error to run the step")

.. warning:: Do not forget to start a step with the function ``start`` otherwise it is not possible to put the result.

.. note:: Do not forget to specify the result of a step, otherwise it will be considered as ``UNDEFINED``.

.. important:: A step set to ``FAILED`` can not become ``PASS`` thereafter in a test.

Cancellation of a test
-------------------

It is possible to force the execution of a test case by using the ``stop`` function in the ``description`` section of your test.

.. code-block:: python

  Test(self).interrupt(err="aborted by tester")
  

Using the ``stop`` feature will stop the test and automatically call the ``cleanup`` section of the test case.
In this case, the ``aborted`` argument is set to True by the framework to indicate the cancellation of the test.

.. code-block:: python

  def definition(self):
	Test(self).interrupt("bad response received")

  def cleanup(self, aborted):
	if aborted: self.step1.setFailed(actual="%s" % aborted)
	

Adding trace
--------------

The framework provides some functions to add messages during the execution of a test.

The following levels are available:

  - Example to display a message of type ``info``
  
	.. code-block:: python
 
		Trace(self).info(txt="hello world")

 - Example to display a ``warning`` message
 
	.. code-block:: python

		Trace(self).warning(txt="hello world")

 - Example to display an ``error`` message
 
	.. code-block:: python
 
		Trace(self).error(txt="hello world")

.. note :: If an error message is displayed then the result will automatically be set to FAILED.

.. note :: Messages appear automatically in the basic report.

Data
--------------------

Public
~~~~~~

A public space is available on the test server. This space makes it possible to provide files that are necessary during the execution of a test.

   .. image:: /_static/images/testlibrary/espace_public.png

The files are stored in the ``[...]/var/public/`` directory on the server.

.. warning :: This space is common to all projects configured on the server.

Private
~~~~~

Private vault only exists while running a test.
It can save logs generated or recovered during the execution of the test.
These logs are automatically made available to the user in a zip file when the test is completed.
They can be retrieved from the client or from the server API.

.. image:: /_static/images/testlibrary/private_storage.png
  
The logs are organized by directory:
  - TC-TESTCASE directory - # <id_tc>: contains the logs generated by the test case
  - ADP directory - # <id_id>: contains the logs generated by the different adapters used during the test
  
.. image:: /_static/images/testlibrary/private_storage_zip.png

Example to save the text `hello world` in a` my_logs` file from the test case

.. code-block:: python
 
  Private(self).saveFile(destname="my_logs", data="hello world")
  

Example to add text to an already existing log file

.. code-block:: python
 
  Private(self).appendFile(destname="my_logs", data="hello world2")
  

.. note:: 
   It is also possible to save files from an adapter.
   They will be automatically stored in a directory with the name of the adapter.
   
  .. image:: /_static/images/testlibrary/adapter_private.png
	
Cache
~~~~~

The test framework allows caching of data in the key/value form.
This function may be necessary to share data between tests when writing a scenario for example.

.. image:: /_static/images/testlibrary/client_cache.png

Example to save a value in the cache

.. code-block:: python
 
  Cache().set(name="my_data", data="hello")
  

Read a value from the cache

.. code-block:: python
 
  my_data= Cache().get(name="my_data")
  Trace(self).warning(my_data)
  

Example to capture a data with a regular expression and with record in the cache

.. code-block:: python
 
  my_data="March, 25 2017 07:38:58 AM"
  
  Cache().capture(data=my_data, regexp=".* (?P<TIME>\d{2}:\d{2}:\d{2}) .*")
  
  Trace(self).info( txt=Cache().get(name="TIME") )
  
.. image:: /_static/images/testlibrary/client_cache_capture.png

It is also possible to rely on a ``custom`` parameter to supply the regular expression.

.. code-block:: python
  
  .*session_id=[!CAPTURE:SESSIONID:];expires.*
  

or in ``greedy`` mode

.. code-block:: python
  
  .*session_id=[!CAPTURE:SESSIONID:.*?];.*
  
  
.. important:: The cache exists only during the execution of a test.

Put on hold
-----------------

This function allows you to pause while running a test.

Example of holding for 10 seconds:

.. code-block:: python
 
  Time(self).wait(timeout=10)
	
Standby example until the current date and time match the specified date:

.. code-block:: python
 
  Time(self).waitUntil(dt='2016-09-12 02:00:00', fmt='%Y-%m-%d %H:%M:%S', delta=0)
	

Interaction with the tester
---------------------------

The framework makes it possible to write semi-automatic tests, ie in interaction mode.
This function can be interesting for a test in interactive mode (eg configuration of a device)

Example asking the name of the person:

.. code-block:: python

  user_rsp = Interact(self).interact(ask="Your name?", timeout=30.0, default=None)
	
From the client, the ``Interact`` tab automatically appears to answer the question asked during
the execution of the test. This window is available from the analysis window.

.. image:: /_static/images/testlibrary/client_interact.png

.. note::  If no response is provided within the interval, it is possible to provide a default value with the ``default`` argument.

Parameters of a test
-----------------------

Inputs
~~~~~~~~~~~~~~~~~~

Input parameters are used to add variables to a test.
They are configurable from the client.

There are several types of parameters:

+------------------+-------------------------------------------------------------+
| Type             | Description use                                             |
+------------------+-------------------------------------------------------------+
| json             | returns a value in JSON format                              |
+------------------+-------------------------------------------------------------+
| text             | multiline string                                            |
+------------------+-------------------------------------------------------------+
| global           | advanced parameter                                          |
+------------------+-------------------------------------------------------------+
| str / pwd        | string                                                      |
+------------------+-------------------------------------------------------------+
| list             | list of strings                                             |
+------------------+-------------------------------------------------------------+
| bool             | Boolean value                                               |
+------------------+-------------------------------------------------------------+
| hex              | hexadecimal value                                           |
+------------------+-------------------------------------------------------------+
| none             | null value                                                  |
+------------------+-------------------------------------------------------------+
| alias            | shortcut parameter                                          |
+------------------+-------------------------------------------------------------+
| shared           | value from the project variables                            |
+------------------+-------------------------------------------------------------+
| list-shared      | list of project variable values                             ​​|
+------------------+-------------------------------------------------------------+
| cache            | key to a value in the cache                                 |
+------------------+-------------------------------------------------------------+
| int              | integer                                                     |
+------------------+-------------------------------------------------------------+
| float            | decimal                                                     |
+------------------+-------------------------------------------------------------+
| dataset          | includes a file of type dataset                             |
+------------------+-------------------------------------------------------------+
| remote-image     | incorporates an image present in the test repository        |
+------------------+-------------------------------------------------------------+
| local-image      | integrates an image present locally on a post               |
+------------------+-------------------------------------------------------------+
| snapshot-image   | includes a screenshot                                       |
+------------------+-------------------------------------------------------------+
| local-file       | includes a file locally present on the post                 |
+------------------+-------------------------------------------------------------+
| date             | date                                                        |
+------------------+-------------------------------------------------------------+
| time             | hour                                                        |
+------------------+-------------------------------------------------------------+
| date-time        | date and time                                               |
+------------------+-------------------------------------------------------------+
| self-ip          | list of server IP addresses                                 |
+------------------+-------------------------------------------------------------+
| self-mac         | list of server MAC addresses                                |
+------------------+-------------------------------------------------------------+
| sef-eth          | list of server network interfaces                           |
+------------------+-------------------------------------------------------------+


The variables are accessible from a test with the ``input (...)`` function

.. code-block:: python

  input('DEBUG')
  
**The text parameter**

The ``text`` type is used to construct parameters that use other parameters or the cache.
It is therefore possible to use keywords that will be interpreted by the test framework
at the time of execution.

List of available keywords:

+---------------------+-----------------------------------------------------------------------+
| Keywords            | Description                                                           |
+---------------------+-----------------------------------------------------------------------+
| ``[! INPUT::]``     | Retrieves the value of a parameter present in the test                |
+---------------------+-----------------------------------------------------------------------+
| ``[! CACHE::]``     | Retrieves a value present in the cache                                |
+---------------------+-----------------------------------------------------------------------+

.. note :: The name of a parameter is unique and must be capitalized.

The agents
~~~~~~~~~~~~~~

.. image:: /_static/images/examples/client_agent_support.png


The list of agents can be accessed from a test using the ``()`` key mode.

.. code-block:: python

  self.ADP_REST= SutAdapters.REST.Client(
                                            parent=self,
                                            destinationIp=input('HOST'),
                                            destinationPort=input('PORT'),
                                            debug=input('DEBUG'),
                                            sslSupport=input('USE_SSL'),
                                            agentSupport=input('SUPPORT_AGENT'), 
                                            agent=input('AGENT_SOCKET')
                                           )

Define the agent parameter with json like that {'name': 'agent1', 'type': 'socket'}

Import / export settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The test parameters can be exported to a dedicated ``testconfig`` (tcx) file type.
It is therefore possible to prepare the parameters without having the test.

.. image :: /_static/images/client/client_testconfig_export.png

It is possible to import a configuration file into a test.
The import will overwrite all the parameters if the name is the same.

.. image:: /_static/images/client/client_testconfig_import.png

