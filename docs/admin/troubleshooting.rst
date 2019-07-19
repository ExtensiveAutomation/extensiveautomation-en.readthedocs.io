Troubleshooting
=========

Logs
---------------------

Server
~~~~~~~

The server logs are stored on ``[....]/Var/Logs/``.
The logs are set in ``INFO`` mode by default.
The DEBUG level can be activated from the ``settings.ini`` file.

.. code-block::
    [Trace]
    level=DEBUG

.. note :: It is possible to change the level of logs by doing an ``xtcl reload``

Client
~~~~~~~

The client logs are available in ``<Program Files> /Extensive Automation Client/Logs/``
The logs are set in ``INFO`` mode by default.

The DEBUG level can be activated from the client preferences.

.. image:: /_static/images/client/preferences_application_logs.png

.. image:: /_static/images/client/client_logs.png

Toolbox
~~~~~~~~~~~~~~

The logs in the toolbox are available in ``<Program Files>/Extensive Automation Toolbox/Logs/``
The logs are set in ``INFO`` mode by default.

The DEBUG level can be activated from the ``settings.ini`` file.

.. code-block::
    [Trace]
    level=DEBUG
    
.. image:: /_static/images/client/toolbox_logs.png
    
.. note :: A restart of the toolbox is necessary to take into account the change

Frequently Asked Questions
--------------------------

How to change the connection port of the client?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The destination port can be changed from the client preferences.
Or directly from the ``settings.ini`` file.

.. image:: /_static/images/client/preferences_network_ports.png

View the server version?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    ./extensiveautomation version
    Server version: 20.0.0
    
What if my connection to the server does not work?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ ~~~~~~

If the connection from the client to the server does not work, an analysis is necessary.

The first thing to do is to connect to the server in SSH and execute the ``extensiveautomation status`` command to check if the server is running.

1. If the server is running then check:
  - network connectivity in the client and the server
  - a firewall blocking the https flow (443)

2. If the network connectivity is good and the server is working (or not), check the logs.
The file is available in the ``[....]/Var/Logs/output.log`` directory. You must look for messages of type ``ERROR``

How to fix the error "hping3 is not installed"?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ ~~~~~~

This error occurs while running a test when the ``Pinger`` adapter is used.
Indeed requires to have the hping3 system library installed on the server.

You have to retrieve the sources from https://github.com/antirez/hping and compile them:

.. code-block:: bash
  
  cd hping-master
  yum install libpcap-devel-1.5.3-9.el7.x86_64
  ln -s /usr/include/pcap/bpf.h /usr/include/net/bpf.h
  ./configure
  make
  make install