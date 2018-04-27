Administration
=============

Start/Stop of the server
~~~~~~~~~~~~~~~~~~~~~~

The server can be controled with the following command ``xtctl``.
This command enables to
 - start or stop the server
 - check the status
 - deploy a new graphical client or toolbox
 - display the version

Use the following command to start the server ``xtctl start``.
 
.. code-block:: bash
  
  # xtctl start
  Checking database                                          [  OK  ]
  Saving current adapters                                    [  OK  ]
  Saving current libraries                                   [  OK  ]
  Starting Extensive Testing                                 [  OK  ]
  
  
Use the following command to stop the server ``xtctl stop``.

.. code-block:: bash
  
  # xtctl stop
  Saving current adapters                                    [  OK  ]
  Saving current libraries                                   [  OK  ]
  Stopping Extensive Testing                                 [  OK  ]
  

.. tip::

   More details in logs about the start or stop procedure.
   
  .. code-block:: bash
    
    # tailf /opt/xtc/current/Var/Log/output.log
    2014-12-06 11:00:54,092 - INFO - Extensive Testing successfully started (in 14 sec.)
    ...
    2014-12-06 10:58:51,810 - INFO - Stopping server
    2014-12-06 10:58:51,911 - INFO - Extensive Testing successfully stopped!
  
  
Server status's
~~~~~~~~~~~~~~~~~~~~~~

``xtctl`` enable to check the status of the server, 3 states exists:
 - ``starting``: the server is starting
 - ``running``: the server is running properly
 - ``stopped``: the server is stopped

.. tip:: 
  Don't forget to check the status of ``httpd`` and ``mysql`` services.
  
New packages deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The solutions make available all additionnals package needed for users:
 - The graphical client
 - The toolbox
 - Plugins

When a new client is available, it's possible to put it in the server and notify 
all users of this new package.

Packages must be uploaded in the following folder ``<INSTALL_PATH>/current/Packages/``

+-----------------+-------------------------------------------------+
|Client           | Portable version and installation               |
+-----------------+-------------------------------------------------+
|ClientPlugins    | Plugins                                         |
+-----------------+-------------------------------------------------+
|Toolbox          | Portable version and installation               |
+-----------------+-------------------------------------------------+
|ToolboxPlugins   | Plugins                                         |
+-----------------+-------------------------------------------------+

Packages are automatically available from the web interface. It's possible to execute the command ``xtctl deploy`` in the server
to make it available to all.

.. code-block:: bash
  
  ./xtctl deploy
  Deploying clients.(ExtensiveTestingClient_X.X.X_Setup.exe)
  Deploying tools.(ExtensiveTestingToolbox_X.X.X_Setup.exe)
  Deploying portable clients... (No client)
  Deploying portable tools... (No client)

Server settings
~~~~~~~~~~~~~~~~~~~~~~

The file ``settings.ini`` contains all parameters to configure the server.
Parameters are separated in several sections:
 - Boot
 - Notifications
 - Client_Channel
 - Agent_Channel
 - Probe_Channel
 - WebServices
 - TaskManager
 - Network
 - Paths
 - Bin
 - Server
 - Web
 - Bind
 - Misc
 - MySql
 - Trace
 - Backups
 - Default
 - Csv_Test_Results:
 - Tests_Framework
 - Events_Colors
 - Supervision
 - Users_Session
  
Automatic backups
~~~~~~~~~~~~~~~~~~~~~~
  
The solution make a backup of all tests, adapters and libraries every days.
Backups are stored in the folder ``/opt/xtc/current/Var/Backups``.

The interval of backup can be configured from the section ``Backups`` in the file ``settings.ini``.

.. code-block:: bash
  
  [Backups]
  ; tests repository
  ; 0=disable 1=enable
  tests=1
  ; backup zip name
  tests-name=tests-automatic-backup
  ; backup weekly on sunday at 23:40:00
  tests-at=6|23,40,00
  
Scheduler type:
 - 7: weekly
 - 6: daily
 - 5: hourly
 
Crontab scripts
~~~~~~~~~~~~~~~~~~~~

``cron.backup-tables``: this script allows to save the tables of the solution

``cron.cleanup-backups``: this script allows you to delete backups older than 14 days.
The number of days is configurable.

``cron.cleanup-testsresult``: this script allows you to delete results older than 30 days.
The number of days is configurable.

Security banner
~~~~~~~~~~~~~~~~

It is possible to configure a security banner on the web interface of the server and on the
portable client login window.

For this you have to configure the file ``BANNER`` present in
  - in the ``/opt/xtc/current/Web/`` web directory for the server
  - the connection of the execution file for the graphical client.