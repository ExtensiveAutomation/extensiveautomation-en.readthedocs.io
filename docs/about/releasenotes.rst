Changes Logs
================

Current version
---------------

.. note::

 **Version 21.0.0 available since 08/25/2019**
 
 - No more return settings file content from rest api
 - Continue code cleanup
 - Disable email test result notification on Windows platform
 - Variables encryption database has been removed, prefer another way to do it.
 - Salt used on user's password is now re-generated each time during database creation
 - Folders for projects are automatically created if missing during start of the server
 - Users manager: default users can be now removed
 - Cleanup on the model of the user table
 - Default users, projects, and global variables can be now modified from json files
 - Support remote ldap simple bind and ntlm authentication for user session 
 - Test library: test manipulator feature removed

A complete release notes is available in the server package.

Previous versions
-------------------

..

 **Version 21.0.0 available since 08/10/2019**
 
 - Full support for python3 on server side and test framework
 - Windows support for server side execution
 - Backups folder removed from var, no more needed
 - Reorganization of the project files with new python import
 - Merge test interop in sut adapters
 - New docker image of the server based python3
 - New distribution for plugins server on pypi
 - New distribution of the server on pypi

..

 **Version 20.0.0 available since 07/20/2019**
 
 - Image docker available
 - Rest API: support for CORS feature 
 - No more automatic installation provided 
 - Maximum of dependancies with libraries removed
 - No more plugins provided by default
 - Probes features removed, replaced by agent
 - MySQL database removed, replaced by sqlite
 - Optimization of the framework to reduce the CPU usage
 - New major version for the Qt client application, user interface improvment
 - New major version for the toolbox
 - New major version for the web interface, no more provided by default
 - Several bugs fixed

..

 **Version 19.0.1 available since 08/09/2018**
 
 - Bug fix on deployment server, pip command integration
 - New name ExtensiveAutomation for the solution
 - All tests files are stored in XML by default (no more zlib compression) 
 - Bugs fixes and improvement in REST API
 - Initial docker support
 - Python 2.6 no more supported on server side
 - Cache preview from the client during test writing
 - Simplification of tests parameters with "text" and "json"
 - SQL queries optimization on server side
 - Begin to support python 3.5 on server side
 - The client is no more embedded in the server side by default
 - New feature to set a security banner on login page of the web interface and app client
 - Update of selenium in 3.13.0
 - New major version for the app client
 - New major version for the toolbox 

..

 **Version 18.0.0 released on 02/11/2018**
 
 - API XmlRPC is removed from the server
 - Big improvment of the API REST
 - New major client based on the API Rest
 - Full support of Qt5.9 for the toolbox and graphical client
 - Full support of python 3.6 for the toolbox and graphical client
 - Code cleanup
 - Several bugs fixed
 - Update of selenium in 3.9.0
 - The toolbox is no more embedded in the server side by default

..

 **Version 17.1.0 released on 10/22/2017**
 
 - Improvment in the REST api
 - New features in the test framework library
 - Several bugs fixed
 - Improvment of the graphical interface of the client
 - Experimental Ubuntu Support for the graphical client

..

 **Version 17.0.0 released on 06/04/2017**
 
 - 64bits support by default for the client and toolbox
 - New major features in the test framework library
 - New swagger for the REST api
 - Update of selenium 3 et 2 in the toolbox
 - Several bugs fixed

..
 
 **Version 16.1.0 released on 03/30/2017**
 
 - Several bugs fixed
 - Improvment of the graphical interface of the client
 - Installation improvment
 
..

 **Version 16.0.0 released on 25/02/2017**
 
 - Several bugs fixed
 - Improvment of the REST api
 - Changes on core server
 - New features in the test framework library
 - Optimization in server side to reduce the number of SQL requests
 - Improvment of the graphical interface of the client
 - 64bits Support for the graphical client and toolbox
 
..

 **Version 15.0.3 released on 04/11/2016**
 
 - Several bugs fixed
 - New plugins for the graphical client
 - Improvment of the REST API
 - New features in the test framework library
 - New interop module in test library
 
..

 **Version 14.0.0 released on 27/08/2016**
 
 - Several bugs fixed
 - New features in the test framework library
 - New major features on the REST api
 - No more new feature in the XmlRPC api, just bug fix
 - New features in the web interface
 - Python2.7 no more supported on windows for the graphical client and toolbox
 - Integration of the REST api in the graphical client
 - Improvment of the graphical interface of the client
 - New HP QC ALM plugin for the graphical client
 
..

 **Version 13.0.0 released on 23/06/2016**
 
 - Several bugs fixed
 - New REST api on the server side
 - New features in the test framework library
 - Improvment in the core server
 - Plugins support for the client and toolbox
 - Improvment of the graphical interface of the client
 
..

 **Version 12.1.0 released on 29/04/2016**
 
 - Several bugs fixed
 - New features in the test framework library
 - Minors update on the XmlRPC API
 - Improvment of the graphical interface of the client
 
..

 **Version 12.0.0 released on 12/02/2016**
 
 - Several bugs fixed
 - New features on the XmlRPC API
 - New features in the test framework library
 - New features in the web interface
 
.. 

 **Version 11.2.0 released on 22/11/2015**
 
 - Several bugs fixed
 - New features in the test framework library
 - Improvment of the scheduler
 - New public repository for the test framework library
 - Offline installation support
 - Minor changes on the XmlRPC api
 
..

 **Version 11.1.0 released on 18/10/2015**
 
 - Several bugs fixed
 - New features on the XmlRPC API
 - New features on the web interface 
 
.. 

 **Version 11.0.0 released on 14/09/2015**
 
 - Several bugs fixed
 - New features in the web interface
 - Merge of agents and probes in the toolbox
 - Update in the XmlRPC API
 - Python 3.4 support for the graphical client and toolbox
 
..

 **Version 10.1.0 released on 12/07/2015**
 
 - Several bugs fixed
 - CentOS 4 et 5 no more supported
 - New features in the test framework library
 - New features in the web interface
 
..

 **Version 10.0.0 released on 28/05/2015**
 
 - Several bugs fixed
 - New features in the web interface
 - Minor changes in the core server
 - Update of the documentations
 - Improvment of the graphical interface of the client
 
.. 

 **Version 9.1.0 released on 22/03/2015**
 
 - Several bugs fixed
 - New features in the test framework library
 - Product installation improved
 - Improvment of the graphical interface of the client
 
..

 **Version 9.0.0 released on 05/01/2015**
 
 - Several bugs fixed
 - New features in the test framework library
 - Python 2.4 no more supported
 - New features in the web interface
 - Improvment of the graphical interface of the client
 
..

 **Version 8.0.0 released on 25/10/2014**
 
 - Several bugs fixed
 - Improvment of the graphical interface of the client
 - New features in the test framework library
 - Minors changes in the XmlRPC API
 - New features in the web interface
 
..

 **Version 7.1.0 released on 20/09/2014**
 
 - Several bugs fixed
 - Documentations updated
 - Optimization in server side to prepare a test
 - New features in the core
 - New features in the test framework library
 - Improvment of the graphical interface of the client
 
.. 

 **Version 7.0.0 released on 08/08/2014**
 
 - Several bugs fixed
 - Improvment in the scheduler
 - Reverse proxy added on the front of the server
 - Websockets support, activated by default
 - New documentations
 - tcp/443 used by default on all components
 - SSL proxy support
 - SSL used by default for agents and probes
 - Improvment of the graphical interface of the client
 
.. 

 **Version 6.2.0 released on 02/06/2014**
 
 - Several bugs fixed
 - Agents update
 - Minors changes in the XmlRPC API
 - New features in the test framework library
 - Improvment of the scheduler
 
..

 **Version 6.1.0 released on 25/04/2014**
 
 - Several bugs fixed
 - New features in the web interface
 - New features in the test framework library
 - Agents improvments
 
..

 **Version 6.0.0 released on 23/03/2014**
 
 - Several bugs fixed
 - New packages for adapters and libraries
 - New features in the XmlRPC API
 - New features in the test framework library
 - No more link with the twisted library
 - SSL support on XmlRPC api
 - Proxy socks4 support 
 - Agents Support
 
..

 **Version 5.2.0 released on 12/01/2014**
 
 - Several bugs fixed
 - New minors features in the core server
 
..

 **Version 5.1.0 released on 08/12/2013**
 
 - New features in the web interface
 - Several bugs fixed
 - New features in the test framework library
 
.. 

 **Version 5.0.0 released on 15/09/2013**
 
 - Several bugs fixed
 - New major features in the test framework library
 - Improvment of the scheduler

.. 

 **Version 4.2.0 released on 08/04/2013**
 
 - Several bugs fixed
 - New features in the web interface
 
..

 **Version 4.1.0 released on 10/03/2013**
 
 - Several bugs fixed
 - New features in the web interface
 - CentOS 6 Support
 - Improvment of the scheduler
 
..

 **Version 4.0.0 released on 30/01/2013**
 
 - Several bugs fixed
 - New features in the test framework library
 - SSL support for the web interface
 - New authentification method with sha1 and salt
 - New features in the XmlRPC API
 
.. 

 **Version 3.2.0 released on 29/09/2012**
 
 - Several bugs fixed
 - New features in the test framework library
 
..

 **Version 3.1.0 released on 14/07/2012**
 
 - Several bugs fixed
 - New features in the test framework library
 - Improvment of the scheduler
 - New features in the XmlRPC API
 
..

 **Version 3.0.0 released on 09/06/2012**
 
 - Several bugs fixed
 - New features in the XmlRPC API
 - Improvment of the scheduler
 - New repositories for adapters and backups
 
.. 

 **Version 2.2.0 released on 28/03/2012**
 
 - New majors features in the XmlRPC API
 - Several bugs fixed
 - New features in the test framework library
 
..

 **Version 2.0.0 released on 27/02/2012**
 
 - New features in the XmlRPC API
 - Documentation added for the test framework and adapters
 - Several bugs fixed
 - Probes support
 
..

 **Version 1.2.0 released on 14/01/2012**
 
 - Improvment of the scheduler
 - New features in the XmlRPC API
 - New features in the test framework library
 - Interface web added
 - Several bugs fixed
 
..

 **Version 1.0.0 released on 13/12/2011**
 
 - First official version
 - CentOS 5 support
 - Several bugs fixed
 
.. 

 **Version 0.1.0 released on 17/05/2010**
 
 - First beta