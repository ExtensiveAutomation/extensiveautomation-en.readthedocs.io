Interoperability
===================

Adapters
-----------

The adapters allow communication with the system to be tested or piloted. The solution embeds several default adapters in different domains:
  - network protocol support
  - application level protocol support
  - communication with databases
  - systems interaction
  - interaction with graphic interfaces
  - telecom protocol support

Adapters have two modes of use:
  - a direct mode: communication is done directly from the test server to the system to be controlled.
  - an agent mode: the communication with the system to be controlled is done through an agent communicating with the test server.

.. note :: The ``Verbose`` mode is enabled by default on all adapters. This mode can be disabled to reduce the number of events during a test.

.. note :: The ``Debug`` mode is not enabled by default. It can be activated in case of problem.

.. note ::
   Examples are available in test samples ``/Samples/Tests_Adapters``
  
List of adapters available by default:

Network Protocols
~~~~~~~~~~~~~~~~~~~~

+----------------+----------------+---------------------------------------------------------------------------------+
| Adapters       | Agents         | Descriptions                                                                    |
+----------------+----------------+---------------------------------------------------------------------------------+
| ARP            | socket         | Sniffer to send and receive ARP packets                                         |
+----------------+----------------+---------------------------------------------------------------------------------+
| ICMP           | socket         | Sniffer to send and receive ICMP packets                                        |
+----------------+----------------+---------------------------------------------------------------------------------+
| Ethernet       | socket         | Sniffer for sending and receiving Ethernet frames                               |
+----------------+----------------+---------------------------------------------------------------------------------+
| IP             | socket         | Sniffer for sending and receiving IPv4 packets                                  |
+----------------+----------------+---------------------------------------------------------------------------------+
| Pinger         | not supported  | Machine life tests via ICMP, TCP or URL                                         |
+----------------+----------------+---------------------------------------------------------------------------------+
| UDP / TCP      | socket         | Sniffer and UDP client and TCP                                                  |
+----------------+----------------+---------------------------------------------------------------------------------+
| NTP            | socket         | Client to request an NTP server                                                 |
+----------------+----------------+---------------------------------------------------------------------------------+
| DNS            | not supported  | Resolver Customer                                                               |
+----------------+----------------+---------------------------------------------------------------------------------+
| SNMP           | socket         | Receiving SNMPv2 Alarms                                                         |
+----------------+----------------+---------------------------------------------------------------------------------+

Network Protocols Applications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+----------------+---------------------------------------------------------------------------------+
| Adapters       | Agents         | Descriptions                                                                    |
+----------------+----------------+---------------------------------------------------------------------------------+
| HTTP           | socket         | Server and client with TLS support and proxy                                    |
+----------------+----------------+---------------------------------------------------------------------------------+
| SOAP           | socket         | Client with TLS support and proxy                                               |
+----------------+----------------+---------------------------------------------------------------------------------+
| REST           | socket         | Client with TLS support and proxy                                               |
+----------------+----------------+---------------------------------------------------------------------------------+
| WebSocket      | socket         | Websocket client                                                                |
+----------------+----------------+---------------------------------------------------------------------------------+
| SoapUI         | soapui         | Client to run SoapUI campaigns                                                  |
+----------------+----------------+---------------------------------------------------------------------------------+

System commands
~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+----------------+---------------------------------------------------------------------------------+
| Adapters       | Agents         | Descriptions                                                                    |
+----------------+----------------+---------------------------------------------------------------------------------+
| Dig            |                | Customer dig                                                                    |
+----------------+----------------+---------------------------------------------------------------------------------+
| Curl           |                | Customer curl                                                                   |
+----------------+----------------+---------------------------------------------------------------------------------+
| Nmap           |                | Nmap client                                                                     |
+----------------+----------------+---------------------------------------------------------------------------------+
| Ncat           |                | Customer ncat                                                                   |
+----------------+----------------+---------------------------------------------------------------------------------+
| Openssl        |                | Openssl client                                                                  |
+----------------+----------------+---------------------------------------------------------------------------------+

User Interfaces
~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-----------------------------------------+---------------------------------------------+
| Adapters       | Agents                                  | Descriptions                                |
+----------------+-----------------------------------------+---------------------------------------------+
| Adb            | adb                                     | Integration with the Android Gateway        |
+----------------+-----------------------------------------+---------------------------------------------+
| Selenium       | selenium2-server or selenium3-server    | Integration with the Selenium project       |
+----------------+-----------------------------------------+---------------------------------------------+
| Sikuli         | sikulix-server                          | Integration with the SikuliX project        |
+----------------+-----------------------------------------+---------------------------------------------+

Data base
~~~~~~~~~~~~~~~~

+-----------------+----------------+---------------------------------------------------------------------------------+
| Adapters        | Agents         | Descriptions                                                                    |
+-----------------+----------------+---------------------------------------------------------------------------------+
| Microsoft SQL   | database       | Communication with a base of type Microsoft SQL                                 |
+-----------------+----------------+---------------------------------------------------------------------------------+
| MySQL           | database       | Communication with a MySQL/MariaDB database                                     |
+-----------------+----------------+---------------------------------------------------------------------------------+
| PostgreSQL      | database       | Communication with a PostgreSQL database                                        |
+-----------------+----------------+---------------------------------------------------------------------------------+

System controls
~~~~~~~~~~~~~~~~~~~
+-------------------+----------------+---------------------------------------------------------------------------------+
| Adapters          | Agents         | Descriptions                                                                    |
+-------------------+----------------+---------------------------------------------------------------------------------+
| SSH / SFTP        | ssh            | SSH console                                                                     |
+-------------------+----------------+---------------------------------------------------------------------------------+
| TELNET            | socket         | Customer to send and receive text                                               |
+-------------------+----------------+---------------------------------------------------------------------------------+
| FTP               | ftp            | Customer with TLS support                                                       |
+-------------------+----------------+---------------------------------------------------------------------------------+
| System File       | file           | Allows interaction with Linux or Windows system files                           |
+-------------------+----------------+---------------------------------------------------------------------------------+
| System Win / Unix | command        | Lets you control Linux and Windows systems (wmic)                               |
+-------------------+----------------+---------------------------------------------------------------------------------+
| Cisco Catalyst    | ssh            | Configuration Client, based on the Telnet adapter                               |
+-------------------+----------------+---------------------------------------------------------------------------------+

Telecom Protocols
~~~~~~~~~~~~~~~~~~~~~

+----------------+----------------+---------------------------------------------------------------------------------+
| Adapters       | Agents         | Descriptions                                                                    |
+----------------+----------------+---------------------------------------------------------------------------------+
| SMS Gateway    | gateway-sms    | Receive or send SMS using an Android smartphone                                 |
+----------------+----------------+---------------------------------------------------------------------------------+
| SIP            | socket         | SIP Phone                                                                       |
+----------------+----------------+---------------------------------------------------------------------------------+
| RTP            | socket         | Module for sending and receiving audio and video streams                        |
+----------------+----------------+---------------------------------------------------------------------------------+
Bookstores
----------

A library makes it possible to quickly make available functions for
  - support data encryption methods
  - support existing compression formats
  - support authentication functions
  - manipulate the different format of date, time and units
  - support codecs (XML, JSON, etc ...)
  - support data hash functions

A library does not communicate directly with the system to be tested or piloted. It is used:
  - directly from the tests
  - from the adapters.

.. tip :: If several adapters need the same functions, it is advisable to factor them in a library.

List of libraries available by default:

Encryption
~~~~~~~~~~

+-------------+-----------------------------------------+
| AES         | Encryption or decryption support        |
+-------------+-----------------------------------------+
| Blowfish    | Encryption or decryption support        |
+-------------+-----------------------------------------+
| OpenSSL     | Execute SSL command                     |
+-------------+-----------------------------------------+
| RC4         | Encryption or decryption support        |
+-------------+-----------------------------------------+
| XOR         | Encryption or decryption support        |
+-------------+-----------------------------------------+
| RSA         | RSA Key Generator                       |
+-------------+-----------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/02_Ciphers``
  
Codecs
~~~~~~

+----------------+--------------------------------------------------+
| Base64         | Encode or decode in base64 format                |
+----------------+--------------------------------------------------+
| Excel          | Excel file reading                               |
+----------------+--------------------------------------------------+
| G711A          | Encode or decode the audio codec                 |
+----------------+--------------------------------------------------+
| G711U          | Encode or decode the audio codec                 |
+----------------+--------------------------------------------------+
| JSON           | Encode or decode text in JSON format             |
+----------------+--------------------------------------------------+
| XML            | Encode or decode text in XML format              |
+----------------+--------------------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/03_Codecs``

Compression
~~~~~~~~~~

+----------+----------------------------------------------------+
| GZIP     | Compression or decompression in GZIP format        |
+----------+----------------------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/09_Compression``
  
Hashing
~~~~~~~~~~

+------------+---------------------------------------------+
| Checksum   | Checksum Generator                          |
+------------+---------------------------------------------+
| HMAC       | Creating a hash md5, sha1 and sha256        |
+------------+---------------------------------------------+
| MD5        | Creating a md5 hash                         |
+------------+---------------------------------------------+
| SHA        | Creating a hash sha1, sha256 and sha512     |
+------------+---------------------------------------------+
| CRC32      | Checksum Generator                          |
+------------+---------------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/05_Hashing``
  
Identifiant
~~~~~~~~~~

+--------------------+------------------------------------------------+
| SessionID          | Session Builder ID                             |
+--------------------+------------------------------------------------+
| UUIDS              | UUID Generator (Universally Unique IDentifier) |
+--------------------+------------------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/07_Identifiers``
  
Média
~~~~~

+----------------+-----------------------------------------+
| ChartsJS       | Visible graph generator in test reports |
+----------------+-----------------------------------------+
| DialTones      | Tone generator                          |
+----------------+-----------------------------------------+
| Image          | Manipulation of images                  |
+----------------+-----------------------------------------+
| Noise          | Noise generator                         |
+----------------+-----------------------------------------+
| SDP            | Decodes or encodes SDP messages         |
+----------------+-----------------------------------------+
| WavContainer   | Creating audio file type WAV            |
+----------------+-----------------------------------------+
| Waves          | Simple wave generator                   |
+----------------+-----------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/04_Media``

Date
~~~~

+--------------------+------------------------------------------+
| Today              | Retrieves today's date                   |
+--------------------+------------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/11_Date``
  
Security
~~~~~~~~~~

+---------------+---------------------------------------------------------+
| Basic         | Decode or encode the authorization                      |
+---------------+---------------------------------------------------------+
| Digest        | Decode or encode the authorization                      |
+---------------+---------------------------------------------------------+
| Hmac          | Decode or encode the authorization                      |
+---------------+---------------------------------------------------------+
| Oauth         | Decode or encode the authorization                      |
+---------------+---------------------------------------------------------+
| Wsse          | Decode or encode the authorization                      |
+---------------+---------------------------------------------------------+
| Certificate   | Decodes certificates in a readable format               |
+---------------+---------------------------------------------------------+
| JWT           | Decode or encode tokens                                 |
+---------------+---------------------------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/01_Security``
  
Time
~~~~~

+--------------------+----------------------------------------------------------------------------+
| Timestamp          | Generate a timestamp or convert to a readable value                        |
+--------------------+----------------------------------------------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/06_Time``
  
Units
~~~~~~

+--------------------+---------------------------------------------------------------+
| Bytes              | Convert fromtes to readable                                   |
+--------------------+---------------------------------------------------------------+

.. note:: 
  An example is available in test samples ``/Samples/Tests_Libraries/08_Units``
  
Third party tools
---------------

The product comes at the base with a number of plugins to interface with
other existing tools (defect tracking, test management, etc.).

These plugins can be used directly from a test.

List of supported tools:

+--------------------+---------------------------------------------------------------+
| Git                | Clone / commit file on remote repository                      |
+--------------------+---------------------------------------------------------------+
| Jira               | Ticket creation                                               |
+--------------------+---------------------------------------------------------------+
| HP ALM QC          | Test run, ticket creation. Version 12 minimum                 |
+--------------------+---------------------------------------------------------------+
| ExtensiveAutomation| Test execution, variable creation                             |
+--------------------+---------------------------------------------------------------+
| Jenkins            | Running tests before or after a build                         |
+--------------------+---------------------------------------------------------------+
| VSphere            | VM creation or supression on VMware                           |
+--------------------+---------------------------------------------------------------+

.. note:: 
    The solution has a REST API, it can be driven also by these tools.
      - Jenkins Plugin: https://wiki.jenkins.io/display/JENKINS/ExtensiveTesting+Plugin

HP ALM
~~~~~~

This plugin allows you to export test results in the HP ALM tool.
It can be used from an etst to export results without user intervention.

Example of use:

::
    HP ALM ------> Call REST API -----> AND
     ^                                   |
     |                                   v
     |                       Execution of the requested test
     |                                   v
     + <-------- Push the result --------+
    
    
.. note ::
   An example is available in the test samples ``/Samples/Tests_Interop/02_HP_QC``
   
Jenkins
~~~~~~

This plugin allows to launch a build from the Extensive solution.

.. note ::
   An example is available in test samples ``/Samples/Tests_Interop/06_Jenkins``
  
VSphere
~~~~~~

This plugin allows you to control a VMware virtual environment. It can be used for:
  - create virtual machines automatically
  - remove machines

.. note ::
   An example is available in test samples ``/Samples/Tests_Interop/05_VSphere``

ExtensiveTesting
~~~~~~~~~~~~~~~~

This plugin makes it possible to make a link between several environment (dev, integration, qualification) by allowing
to run tests from one environment to another.

.. note ::
   An example is available in test samples ``/Samples/Tests_Interop/03_ExtensiveTesting``

Jira
~~~~

This plugin makes it possible to create tickets following the execution of a test in the tool Jira.

.. note ::
   An example is available in test samples ``/Samples/Tests_Interop/01_Jira``

Git
~~~~

This plugin allows you to recover or push files from a source repository.
It can be used as a prerequisite for a test.

.. note ::
   An example is available in test samples ``/Samples/Tests_Interop/04_Git``

Agents
------

Agents are available from the toolbox. They are to be used together with the adapters
  - to communicate with the system to test or control when it is not accessible live by the test server (ex: a web page)
  - run a test on several different environments.
 
.. note :: The ``dummy`` agent is to be used as a basis for developing a new agent.

.. tip: It is advisable to limit the use of agents because the implementation of tests is more complex.


Network Protocols
~~~~~~~~~~~~~~~~~~

+--------------------+------------------------------------------------------------------------------------------+
| socket             | Lets you start TCP / UDP sockets                                                         |
+--------------------+------------------------------------------------------------------------------------------+
| ftp                | Connect to an FTP server(s)                                                              |
+--------------------+------------------------------------------------------------------------------------------+
| database           | Queries databases (MySQL, Microsoft SQL and PostgreSQL)                                  |
+--------------------+------------------------------------------------------------------------------------------+
| ssh                | Connect to machines via SSH or SFTP                                                      |
+--------------------+------------------------------------------------------------------------------------------+

Systems
~~~~~~~

+--------------------+------------------------------------------------------------------------------------------+
| command            | Execute system commands on Windows or Linux                                              |
+--------------------+------------------------------------------------------------------------------------------+
| file               | Allows you to recover files on Windows or Linux systems                                  |
+--------------------+------------------------------------------------------------------------------------------+

Third party tools
~~~~~~~~~~~~

+--------------------+------------------------------------------------------------------------------------------+
| sikulix-server     | Interactions with heavy applications                                                     |
+--------------------+------------------------------------------------------------------------------------------+
| selenium3-server   | Allows you to control the latest generation web browsers                                 |
+--------------------+------------------------------------------------------------------------------------------+
| selenium2-server   | Allows you to control web browsers                                                       |
+--------------------+------------------------------------------------------------------------------------------+
| soapui             | Allows you to run SoapUI tests                                                           |
+--------------------+------------------------------------------------------------------------------------------+
| adb                | Allows you to control Android smartphones                                                |
+--------------------+------------------------------------------------------------------------------------------+
| gateway-sms        | Send or receive SMS                                                                      |
+--------------------+------------------------------------------------------------------------------------------+

.. note :: Using the ``Selenium3-Server`` agent requires at least ``Java 8`` on the machine.

Probes
------

The probes are available in the toolbox. The main goal is to recover
automatically logs (network trace, files) during the execution of a test.

+------------------+----------------------------------------------------------------------------------------------+
| textual          | Allows follow-up of log files on Windows or Linux (tailf)                                    |
+------------------+----------------------------------------------------------------------------------------------+
| network          | Take network traces, probe based on tcpdump on linux, or tshark on Windows                   |
+------------------+----------------------------------------------------------------------------------------------+
| file             | Recovery of configuration files on Windows or Linux                                          |
+------------------+----------------------------------------------------------------------------------------------+

The use of a probe in a test is to be defined in the properties.
 
.. note :: The ``dummy`` agent is to be used as a basis for developing a new agent.