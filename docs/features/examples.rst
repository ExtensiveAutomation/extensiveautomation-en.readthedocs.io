Advanced examples
===================

SSH adapter
--------------

The `` SSH`` adapter allows you to connect to remote servers using the SSH protocol.

The configuration of the adapter consists of indicating at least:
  - the ip address of the remote server
  - the remote server port (default 22)
  - the user account
 
The adapter supports the following features:
  - authentication by username and password
  - key exchange authentication
 
Example of configuring the adapter in the `` prepared`` section of the test.

.. code-block:: python
  
  self.ADP_SSH = SutAdapters.SSH.Client(
                                        parent=self, 
                                        login=input('LOGIN'), 
                                        password=input('PWD'),
                                        destIp=input('DEST_IP'), 
                                        destPort=input('DEST_PORT'), 
                                        debug=input('DEBUG'),
                                        agentSupport=input('SUPPORT_AGENT')
                                    )

Example to connect, to authenticate on a remote server and to disconnect:

.. code-block:: python
  
  connected = self.ADP_SSH.doConnect(
                                    timeout=input('TIMEOUT'), 
                                    prompt='~]#'
                                  )
  if not connected: self.abort("ssh connect failed")
  self.info("SSH connection OK" )
  
  disconnected = self.ADP.doDisconnect(timeout=input('TIMEOUT'))
  if not disconnected: self.abort("disconnect failed")
  self.info("SSH disconnection OK" )
  
  
Example to send a command on a remote machine:

.. code-block:: python
  
  rsp = self.ADP_SSH. doSendCommand(
                                    command='date', 
                                    timeout=input('TIMEOUT'), 
                                    expectedData=None, 
                                    prompt='~]#'
                                )
  if rsp is None: self.abort("run command failed")
  self.warning( rsp )
  
.. warning ::
   SSH replies can be split into several events (this depends on the network).
   We must be careful when waiting for a specific response, the use of a buffer may be necessary in this case.

.. note :: Examples are available in the `` / Samples / Tests_Adapters / 05_SSH.tsx`` sample.

HTTP adapter
--------------

The `` HTTP`` adapter is used to send requests and inspect associated responses to a web server.

The configuration of the adapter consists of indicating at least:
  - the ip address of the remote server
  - the remote server port (default 80)
 
The adapter supports the following features:
  - encryption `` tls`` of the communication
  - the use of `` socks4, 5`` proxy and http
  - `` digest`` or `` basic`` authentication
  - reassembly of responses `` chunked``
 
Example of configuring the adapter in the `` prepared`` section of the test.

.. code-block:: python
  
  self.ADP_HTTP = SutAdapters.HTTP.Client(
                                            parent=self, 
                                            debug=input('TRACE'), 
                                            destinationIp=input('DST_IP'), 
                                            destinationPort=input('DST_PORT'),
                                            sslSupport = input('SSL_SUPPORT'), 
                                            agent=agent('AGENT_SOCKET'), 
                                            agentSupport=input('SUPPORT_AGENT')
                                        )

Example to send a `` GET`` type query and a response with the `` 200`` code.

.. code-block:: python
  
  rsp = self.ADP_HTTP.GET( 
                            uri="/", 
                            host=input('HOST'), 
                            timeout=input('TIMEOUT'),
                            codeExpected=200
                        )
  if rsp is None:
    self.step1.setFailed(actual="bad response received")    
  else:
    self.step1.setPassed(actual="http response OK") 
  
Example to send a `` GET`` type query and wait for a response that meets the following criteria:
  - the version must end with 1.1
  - the code must not contain the value 200
  - the sentence must not contain the text `Testing`
  - the body of the answer must contain the text `google`
  - the response must contain a header containing the text `server`, regardless of the value
  
.. code-block:: python
  
  headersExpected = { TestOperators.Contains(needle='server'): TestOperators.Any() }
  
  rsp = self.ADP_HTTP.GET( 
                        uri="/", 
                        host=input('HOST'), 
                        timeout=input('TIMEOUT'),
                        versionExpected=TestOperators.Endswith(needle='1.1') ,
                        codeExpected=TestOperators.NotContains(needle='200') ,
                        phraseExpected=TestOperators.NotContains(needle='Testing') ,
                        bodyExpected=TestOperators.Contains(needle='google') )                                    
                        headersExpected=headersExpected
                        )
  if rsp is None:
    self.step1.setFailed(actual="bad response received")    
  else:
    self.step1.setPassed(actual="http response OK") 

Telnet adapter
--------------

The `` Telnet`` adapter is used to connect to machines with a telnet interface.

The configuration of the adapter consists of indicating at least:
  - the ip address of the remote server
  - the remote server port (default 23)
 
Example of configuring the adapter in the `` prepared`` section of the test.

.. code-block:: python
  
  self.ADP_TELNET = SutAdapters.Telnet.Client(
                                            parent=self, 
                                            destIp=input('TELNET_IP'), 
                                            destPort=input('TELNET_PORT'),
                                            debug=input('DEBUG'),
                                            agentSupport=input('SUPPORT_AGENT')
                                            )
   
   
Example to connect or disconnect from the remote server

.. code-block:: python
  
  self.ADP_TELNET.connect()
  connected = self.ADP_TELNET.isConnected( timeout=input('TIMEOUT') )
  if not connected: Test(self).interrupt( 'unable to connect' )

  self.ADP_TELNET.disconnect()
  disconnected = self.ADP_TELNET.isDisconnected( timeout=input('TIMEOUT') )
  if not disconnected: Test(self).interrupt( 'unable to disconnect' )
  

Example showing how to wait for the receipt of a particular text.

.. code-block:: python
  
  rsp = self.ADP_TELNET.hasReceivedData( 
                                        timeout=input('TIMEOUT'), 
                                        dataExpected=TestOperators.Contains(needle='Password:') )
                                        )
  if rsp is None: Test(self).interrupt( 'Password prompt not found' )
  

Example to send data to the remote server

.. code-block:: python
  
  tpl = self.ADP_TELNET.sendData(dataRaw="exemple")
  

.. warning: telnet responses can be split into multiple events, so be careful when
search for a particular text. To guard against this problem, we must add an intermediary buffer, there is a
complete example with the `` Catalyst`` adapter.

.. note :: An example is available in the test samples `` / Samples / Tests_Adapters / 12_Telnet.tsx``.

MySQL adapter
--------------

The `` MySQL`` adapter allows you to connect to a remote database.

The configuration of the adapter consists of indicating at least:
  - the ip address of the remote server
  - the remote server port (by default 3306)
  - the user name
  - the associated password
 
Example of configuring the adapter in the `` prepared`` section of the test.

.. code-block:: python
  
  self.ADP_MYSQL = SutAdapters.Database.MySQL(
                                        parent=self, 
                                        host=input('HOST_DST'), 
                                        user=input('MYSQL_LOGIN'),
                                        password=input('MYSQL_PWD'), 
                                        debug=input('DEBUG'), 
                                        verbose=input('VERBOSE'),
                                        agent=agent('AGENT_DB'), 
                                        agentSupport=input('SUPPORT_AGENT')
                                        )
  

Example to connect or disconnect from the remote server:

.. code-block:: python
  
  self.ADP_MYSQL.connect(dbName=input('MYSQL_DB'), timeout=input('TIMEOUT'))

  self.ADP_MYSQL.disconnect()
  

Example to execute an SQL query in the database:

.. code-block:: python
  
  query = 'SELECT id FROM `%s-users` WHERE login="admin"' % input('TABLE_PREFIX')
  self.ADP_MYSQL.query(query=query)
  rsp = self.ADP_MYSQL.hasReceivedRow(timeout=input('TIMEOUT'))
  

.. note :: An example is available in the `` / Samples / Tests_Adapters / 15_Database.tsx`` test samples.

SNMP adapter
--------------

The SNMP adapter allows you to receive SNMP v1 or v2 alarms.

The configuration of the adapter consists of indicating at least:
  - the listening address
  - the listening port
 
Example of configuring the adapter in the `` prepared`` section of the test.

.. code-block:: python
  
  self.ADP_SNMP = SutAdapters.SNMP.TrapReceiver(
                                                parent=self, 
                                                bindIp=get('SRC_IP'), 
                                                bindPort=get('SRC_PORT'), 
                                                debug=get('DEBUG'),
                                                agent=agent('AGENT_SOCKET'), 
                                                agentSupport=input('SUPPORT_AGENT')
                                                )
  

Example to start listening to the server

.. code-block:: python
  
  self.ADP_SNMP.startListening()
  listening = self.ADP_SNMP.udp().isListening( timeout=get('TIMEOUT') )
  if not listening: Test(self).interrupt( 'UDP not listening' )
  

Example to wait for the reception of an alarm:

.. code-block:: python
  
  trap = self.UDP_ADP.hasReceivedTrap(
                                        timeout=input('TIMEOUT'), 
                                        version=SutAdapters.SNMP.TRAP_V1, 
                                        community=None, 
                                        agentAddr=None, 
                                        enterprise=None,
                                        genericTrap=None, 
                                        specificTrap="17", 
                                        uptime=None, 
                                        requestId=None, 
                                        errorStatus=None, 
                                        errorIndex=None
                                      )
  if trap is None:  Test(self).interrupt("trap expected not received")
  

.. note :: An example is available in the `` / Samples / Tests_Adapters / 18_SNMP.tsx`` test samples.

    
FTP adapter (s)
--------------

The `` FTP`` adapter allows you to connect to remote servers and supports the following functions:
  - TLS connection
  - Download or recover files or directories
  - Add / delete and rename files or directories
  - List the contents of a directory
  - Detect the appearance of a file or directory with the support of regular expressions.

The configuration of the adapter consists of indicating at least:
  - the ip address of the remote server
  - the username to login
  - the password
 
Example of configuring the adapter in the `` prepared`` section of the test.

.. code-block:: python
  
  self.ADP_FTP = SutAdapters.FTP.Client(
                                        parent=self,
                                        debug=input('DEBUG'),
                                        destinationIp=input('FTP_HOST'),
                                        user=input('FTP_USER'), 
                                        password=input('FTP_PWD') ,
                                        agentSupport=input('SUPPORT_AGENT')
                                        )
  


Example to connect or disconnect from the FTP server:

.. code-block:: python
  
  self.ADP_FTP.connect(passiveMode=True)
  if self.ADP_FTP.isConnected(timeout=input('TIMEOUT')) is None:
      Test(self).interrupt("unable to connect")

  self.ADP_FTP.login()
  if self.ADP_FTP.isLogged(timeout=input('TIMEOUT')) is None:
      Test(self).interrupt("unable to login")
  Trace(self).info("SFTP connection OK" )
  

.. code-block:: python
  
  self.ADP_FTP.disconnect()
  if self.ADP_FTP.isDisconnected(timeout=input('TIMEOUT')) is not None:
     Test(self).interrupt("disconnect failed")
  Trace(self).info("FTP disconnection OK" )
  

Example to list the contents of a directory:

.. code-block:: python
  
  self.ADP_FTP.listingFolder()
  if self.ADP_FTP.hasFolderListing(timeout=input('TIMEOUT')) is not None:
      Trace(self).error("unable to get listing folder")
  

Example to detect a file in a directory with a regular expression:

.. code-block:: python
  
  self.ADP_FTP.waitForFile(
                            path='/var/log/', 
                            filename='^messages-.*$', 
                            timeout=input('TIMEOUT')
                        )


  found = self.ADP_FTP.hasDetectedFile(
                                        path=None, 
                                        filename=None, 
                                        timeout=input('TIMEOUT')
                                    )
  if found is None: Trace(self).error("file not found")
  

.. note :: An example is available in the test samples `` / Samples / Tests_Adapters / 21_Ftp.tsx``.

SFTP adapter
---------------

The `` SFTP`` adapter allows you to connect to servers with an SSH interface.
The following features are supported:
  - Download or recover files or directories
  - Add / delete and rename files or directories
  - List the contents of a directory
  - Detect the appearance of a file or directory with the support of regular expressions.
 
The configuration of the adapter consists of indicating at least:
  - the ip address of the remote server
  - the username to login
  - the password
 
Example of configuring the adapter in the `` prepared`` section of the test.

.. code-block:: python
  
  self.ADP_SFTP = SutAdapters.SFTP.Client(
                                            parent=self, 
                                            login=input('LOGIN'), 
                                            password=input('PWD'),
                                            destIp=input('DEST_IP'), 
                                            destPort=input('DEST_PORT'), 
                                            debug=input('DEBUG'),
                                            agentSupport=input('SUPPORT_AGENT')
                                        )
  

Example to connect and disconnect from the server:

.. code-block:: python
  
  connected = self.ADP_SFTP.doConnect(timeout=input('TIMEOUT'))
  if not connected: Test(self).interrupt("sftp connect failed")
  self.info("SFTP connection OK" )

  disconnected = self.ADP_SFTP.doDisconnect(timeout=input('TIMEOUT'))
  if not disconnected: Test(self).interrupt("disconnect failed")
  self.info("SFTP disconnection OK" )
  

Example to list the contents of a directory:

.. code-block:: python
  
  self.ADP_SFTP.listingFolder(
                            path="/var/log/", 
                            extended=False
                            )


  rsp = self.ADP_SFTP.hasFolderListing(timeout=input('TIMEOUT'))
  if rsp is None: Trace(self).error("unable to get listing folder")
  self.warning( rsp.get("SFTP", "result") )
  

Example to detect a file in a directory with a regular expression:

.. code-block:: python
  
  self.ADP_SFTP.waitForFile(
                            path='/var/log/', 
                            filename='^messages-.*$', 
                            timeout=input('TIMEOUT')
                        )


  found = self.ADP_SFTP.hasDetectedFile(
                                        path=None, 
                                        filename=None, 
                                        timeout=input('TIMEOUT')
                                    )
  if found is None: Trace(self).error("file not found")
  

.. note :: An example is available in the test samples `` / Samples / Tests_Adapters / 22_Sftp.tsx``.

ChartJS librairies
-------------------

The `` ChartJs`` adapter, based on the javascript library of the same name, allows you to
generate graphics that can be integrated into an html page.
The main interest of this library is to be able to integrate graphs in the test report.

Example configuration of the library in the `` prepared`` section of the test.

.. code-block:: python
  
  self.LIB_CHART = SutLibraries.Media.ChartJS(parent=self, name=None, debug=False)
  

Example to generate a bar chart and integrate it into the report

.. code-block:: python
  
  # génération de données 
  labelsAxes = ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"]
  dataA = [12, 19, 3, 5, 2, 3]
  dataB = [22, 49, 3, 5, 23, 3]
  legendDatas = ["tets", "test"]
  backgroundColor = '#4BC0C0'
  borderColor = '#36A2EB'

  # génération du grahique
  myChart = self.LIB_CHART.barChart(
                                    labelsAxes=labelsAxes, 
                                    datas=[dataA, dataB], 
                                    legendDatas=legendDatas, 
                                    width=400, 
                                    height=300,
                                    backgroundColors=[borderColor, backgroundColor], 
                                    borderColors=[borderColor, backgroundColor],
                                    chartTitle="test"
                                )
                                
  # ajout du graphique dans le résultat de l'étape
  self.step1.setPassed(actual="chart", chart=myChart)
  

The chart is automatically inserted into the advanced report.

.. image:: /_static/images/examples/report_chart.png

  
Custom test parameter
-------------------

The `` custom`` parameter is used to construct values calling other variables.

For example, consider a test containing the following 2 variables:
  - DEST_IP with the value 192.168.1.1
  - DEST_PORT with the value 8080

.. image :: /_static/images/examples/custom_inputs.png
 
The `` custom`` type will allow us to build a 3rd variable
  - DEST_URL with the value
 
    .. image :: /_static/images/examples/custom_config.png

The keyword `` [! INPUT: <VARIABLE_NAME:] `` allows calling another incoming variable.
The framework will replace at the time of execution of the test the various keywords with the associated value.
We will obtain the value https://192.168.1.1:8080/welcome for the variable DEST_URL.

.. image:: /_static/images/examples/custom_example.png

To go further, it is also possible to add a value available from the cache.
Assuming that the value "welcome? User = hello" is in the cache and accessible via the key "url_params".
It is possible to integrate in the parameter as below

.. image:: /_static/images/examples/custom_config_cache.png

Example of result after execution:

.. image:: /_static/images/examples/custom_example_cache.png


Parameter of "alias" tests
-------------------

The `` alias`` parameter can be used to define a new name for an already existing parameter.
This mechanism can be used in `` plan test`` to avoid overloading all parameters with the same name.

Example of use

 1. Before execution
   ::
    
    Scenario (TIMEOUT_A(int)=2 seconds)
     ---> Test 1 (TIMEOUT_A(int)=10 seconds)
     ---> Test 2 (TIMEOUT_A(int)=30 seconds)
     ---> Test 3 (TIMEOUT_A(int)=20 seconds)
 
 2. After running the test
   
   ::
     
     Scenario (TIMEOUT_A(int)=2 seconds)
       ---> Test 1 (TIMEOUT_A(int)=2 seconds)
       ---> Test 2 (TIMEOUT_A(int)=2 seconds)
       ---> Test 3 (TIMEOUT_A(int)=2 seconds)
     
     
When executing the above scenario, test 1, 2 and 3 are automatically set to 2 seconds for the TIMEOUT_A parameter.
This is the behavior provided by the test framework.

** How to do if you want the test 2 to keep the value 30 seconds against the test 1 and 2 inherit the value of the scenario? **

You have to use an `` alias`` parameter, they are not overloaded by the framework.

  1. Before execution
   ::
    
    Scenario (TIMEOUT_A(int)=2 seconds et TIMEOUT_B(int)=30 seconds)
     ---> Test 1 (TIMEOUT_A(int)=10 seconds)
     ---> Test 2 (TIMEOUT_A(alias)=TIMEOUT_B et TIMEOUT_B(int) = 0 seconds)
     ---> Test 3 (TIMEOUT_A(int)=20 seconds)
 
 2. After running the test
   
   ::
     
    Scenario (TIMEOUT_A(int)=2 seconds et TIMEOUT_B(int)=30 seconds)
     ---> Test 1 (TIMEOUT_A(int)=2 seconds)
     ---> Test 2 (TIMEOUT_A(alias)=TIMEOUT_B et TIMEOUT_B(int)= 30 seconds)
     ---> Test 3 (TIMEOUT_A(int)=2 seconds)
     


Dataset test parameter
-------------------

The `` dataset`` parameter is used to import `` tdx`` files.
A `` dataset`` file is just a text file, it can be created from the graphical client and saved to the remote test repository.

.. image:: /_static/images/client/client_new_tdx.png 

Sample content of a dataset file with the csv format

.. code-block:: python
  
  a;1;administrator
  b;2;tester
    

This file can be used in a test that is important in the settings.

.. image:: /_static/images/examples/client_testdata.png


Example to read the variable:

.. code-block:: python
  
  for d in input('DATA').splitlines():
      Trace(self).info( d ) 
  
"Shared" test setting
-------------------

The `` shared`` parameters are added from the web interface or from the REST API.
They are shared and accessible by all the tests of the same project. The expected value
for this parameter is of `` JSON`` type.

A selection window in the graphical client allows you to select the parameter to be used in the test.

.. image:: /_static/images/examples/client_params_shared.png

In the example below, the `` MY_SERVER`` test parameter contains the value of the `` IP`` key present in the variable
shared `` MY_SERVER`` which is itself present in the `` Common`` project.

.. image:: /_static/images/examples/client_param_shared.png

.. tip :: To have a test parameter that contains a list of elements, use the `` list-shared`` type.

Using a probe
-------------------

To use a probe, you need 2 things:
  - Deploy the toolbox and start the desired probe.
  - Declare the probe in the test.
 
To select the probe in the test, it must be activated and configured in the test (tab `` Miscellaneous> Probes``)

.. image:: /_static/images/examples/probe_tab.png

When a probe is activated on a test, running the test automatically initializes the probe.

.. image:: /_static/images/examples/probe_starting.png

After execution, all the files collected by the probe are downloaded to the server and accessible from the graphical client.

.. image:: /_static/images/examples/probe_test_archives.png

.. note :: It is possible to use multiple probes in one test.

Using an agent
-------------------

To use an agent, you need two things:
  - Deploy the toolbox and select the desired agent.
  - Declare the agent in the test
  - Configure the adapter to use the agent.

Agents are to be declared from the client in the tab `` Miscellaneous> Agents``

.. image:: /_static/images/examples/client_properties_agent.png


Enabling agent mode on adapters is done with the `` agentSupport`` and `` agent`` arguments.

.. code-block:: python
  
  agentSupport=input('SUPPORT_AGENT'), 
  agent=agent('AGENT_SOCKET')
  

.. code-block:: python
  
   self.ADP_REST= SutAdapters.REST.Client(
                                        parent=self,
                                        destinationIp=input('HOST'),
                                        destinationPort=input('PORT'),
                                        debug=input('DEBUG'),
                                        sslSupport=input('USE_SSL'),
                                        agentSupport=input('SUPPORT_AGENT'), 
                                        agent=agent('AGENT_SOCKET')
                                        )
   
   

In the analysis window, it is possible to see the agent used for each event:

.. image:: /_static/images/examples/client_events_logger_agent.png

.. note:: 
  It is advisable to put in test parameter the use of the agent mode.
  
  .. image:: /_static/images/examples/client_agent_support.png