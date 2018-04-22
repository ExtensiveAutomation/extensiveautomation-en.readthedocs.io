Get started
=============================

Connection to the server
------------------------------

After the oppening of the client, the first step is to connect to the remote server.
To do that, you new an account and the remote address.

The connection windows is available from the ``Get Started > Connect`` menu or from the welcome tabulation.
If the connection is successfull, the user can be see the remote tests availables.

.. image:: /_static/images/client/client_connect.png

.. note:: The ``admin`` user can be used in the discover of the solution.

Write a test
---------------------------------

The first utilization consists to create a very simple testcase and display a parameter.

1. Create a test of the type ``Unit``
   
   .. image:: /_static/images/client/client_new_tux.png

2. Add the parameter MON_PARAMETRE of the type ``str`` with the value "bonjour"
   
   .. image:: /_static/images/client/client_new_param.png

3. Change the test at the `` definition`` section to display the value of the parameter.
   
   .. image:: /_static/images/client/client_new_trace.png
   
   
   .. note:: 
   
     It is possible to check the syntax of the test before execution by clicking on the button ``Syntax``.
       
     .. image:: /_static/images/client/check_syntax.png
   
4. Save the test in the repository with the name "Test_A" in the `` Sandbox`` directory
   
   .. image:: /_static/images/client/client_new_save.png

Write a scenario
----------------------

.. note:: This mini guide assumes that you have followed the chapter `` Writing a script test``.

The following example explains how to create its first scenario with an overload of test variables.

1. Create a `` Plan`` type test.

   .. image:: /_static/images/client/client_new_tpx.png

2. Insert test "Test_A" in the scenario. Click on the `` Insert Child`` button and select the `Test_A` test.

   .. image:: /_static/images/client/client_new_insert.png

3. After insertion, click on the `Test_A` test and insert the same test again.

   .. image:: /_static/images/client/client_new_insert_again.png

4. Save the scenario in the test repository with the name "Scenario_A" in the `` Sandbox`` directory.

5. Add the parameter MON_PARAMETRE with the value "goodbye" at the scenario level.

.. tip:: 
  Do not hesitate to define an alias for the name of the test to make the scenario more readable.

  .. image:: /_static/images/client/snippets_alias.png

Execute a test
-------------------

.. note:: This mini guide assumes that you have followed the chapters `Writing a script test` and` Writing a scenario`.

You can run a test by clicking the `` Execute`` button.
Open the `Test_A` and` Scenario_A` tests and run them.

.. image:: /_static/images/client/client_execute.png

Analyse des résultats
---------------------

.. note:: This mini guide assumes that you have followed the chapters `Writing a script test` and` Writing a scenario`.

The first analysis window shows the execution of the test "Test_A" and in particular the message "hello".

.. image:: /_static/images/client/test_result_simple.png

The 2nd analysis window shows the execution of the "Scenario_A" test and in particular the "goodbye" message.

.. image:: /_static/images/client/test_result_surcharge.png

This first usage shows how to run a test and a scenario as well as the overloading of the test variables.

Best practices
---------------------

.. tip::

   To keep readability in script type tests, do not use `try / except`.
   The framework catches all the exceptions at its level.
  
.. tip::
  
  It is essential to take the time to declare the test steps because they allow
    - quickly understand the test without the script.
    - to have relevant and understandable test reports.
   
.. tip::

   To facilitate the maintenance of your tests and make them reusable,
    you should not have hard value in your test.
    It is necessary to systematically put them in test parameters, it is done for.
   
