Administration
=============

Start/Stop of the server
~~~~~~~~~~~~~~~~~~~~~~

The server can be controled with the following command ``./extensiveautomation``.
This command enables to
 - start or stop the server
 - check the status
 - display the version

Use the following command to start the server ``./extensiveautomation start``.
 
.. code-block:: bash
  
  # ./extensiveautomation start
  
  
Use the following command to stop the server ``./extensiveautomation stop``.

.. code-block:: bash
  
  # ./extensiveautomation stop
  

.. tip::

   More details in logs about the start or stop procedure.
   
  .. code-block:: bash
    
    # tailf [....]/Var/Log/output.log
    2014-12-06 11:00:54,092 - INFO - Extensive Automation successfully started (in 14 sec.)
    ...
    2014-12-06 10:58:51,810 - INFO - Stopping server
    2014-12-06 10:58:51,911 - INFO - Extensive Automation successfully stopped!
  
  
Server status's
~~~~~~~~~~~~~~~~~~~~~~

``./extensiveautomation --status`` enable to check the status of the server, 3 states exists:
 - ``starting``: the server is starting
 - ``running``: the server is running properly
 - ``stopped``: the server is stopped

.. tip:: 
  Don't forget to check the status of your reverse proxy.

Server settings
~~~~~~~~~~~~~~~~~~~~~~

The file ``settings.ini`` contains all parameters to configure the server.
Parameters are separated in several sections:
 - Boot
 - Notifications
 - Client_Channel
 - Agent_Channel
 - WebServices
 - TaskManager
 - Network
 - Paths
 - Bin
 - Server
 - Bind
 - Misc
 - MySql
 - Trace
 - Backups
 - Default
 - Supervision
 - Users_Session