Global variables
=======================

Global variables (or shared variables) are sued to describe test environment.
Variables are accesible from a test from the pamarater of the type ``global`` or ``list-global``.

Add/delete a variable
-----------------

The adding or removing of a variable can be done from the web interface or the REST API.
``JSON`` must be used in variable. There are autommatically availables from tests in properties.

.. image:: /_static/images/webinterface/read_variable.png


Describe environment test
--------------------------

The description of a test environment must be respect the following rules.
This type of init must be used with the reusable test ``/Snippets/Do/03_Initialize.tux`` 

Node declaration ``SAMPLE_NODE``:

.. code-block:: python

 {
	"COMMON": {
		"HOSTNAME": "extensiveautomation"
	},
	"INSTANCES": {
		"SSH": {
			"ADMIN": {
				"SSH_DEST_HOST": "127.0.0.1",
				"SSH_DEST_PORT": 22,
				"SSH_DEST_LOGIN": "root",
				"SSH_DEST_PWD": "",
				"SSH_PRIVATE_KEY": null,
				"SSH_PRIVATE_KEY_PATH": null,
				"SSH_AGENT_SUPPORT": false,
				"SSH_AGENT": {
					"type": "ssh",
					"name": "agent.ssh01"
				}
			}
		}
	}
 }

Data test declaration ``SAMPLE_DATASET_AUTH``:

.. code-block:: python

 {
		 "login":         "admin",
		 "password":      ""
 }

Environment declaration ``SAMPLE_ENVIRONMENT``:

.. code-block:: python

 {
	"PLATFORM": {
		"CLUSTER": [
			{ "NODE": "Common:SAMPLE_NODE" }
		]
	},
	"DATASET": [
		{ "AUTH": "Common:SAMPLE_DATASET_AUTH" }
	]
 }


Import/export variables
---------------------------

It's possible to export or import in mass the variables from the web interface in CSV format

.. warning:: Variables are encoded in base64.