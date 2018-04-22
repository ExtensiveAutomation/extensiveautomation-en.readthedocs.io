Architecture
============

The solution is based on a client / server mode.
The tests and adapters are centralized in a server that allows to quickly provide the same
test environment to all users.

The solution consists of several components:
  - A waiter
  - A graphical client
  - Agents
  - Probes
 
.. image:: /_static/images/testlibrary/archi-extensivetesting.png

Server
-------

The server consists of:
  - a reverse proxy (apache)
  - a scheduler
  - a REST API server
  - the test framework
  - adapters and libraries
  - tool extensions
  - a web interface

Graphic Client
----------------

The graphical client uses a single tcp / 443 (https) stream between the client and the server.
The stream is bidirectional and the client can:
  - make calls to the server's REST API
  - receive events from the server via WebSockets.
  
Agents
------

An agent is compulsorily controlled by an adapter via the test server intermediary.
It allows to deport the communication point with the system to test or control.
Agents use a single tcp / 443 (https) stream to communicate with the server.

Probes
------

The probes make it possible to recover during the execution of a test the network traces, configuration files or logs.
Communication with the server only takes place on port tcp / 443 (https).