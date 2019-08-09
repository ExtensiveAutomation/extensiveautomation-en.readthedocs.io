Toolbox
==============

The toolbox allows you to start agents on dedicated workstations.

  - Agents are required to run tests with Selenium on dedicated workstations or to deport the execution of a test.

.. image :: /_static/images/toolbox/toolbox.png
   
Deployment
-----------

This window allows you to choose the agent or probe to start. The type of agent or probe to start can be chosen
in the drop-down list. Finally, an agent or probe needs to be registered with the test server in order to use it.

An agent will allow you to perform a distributed run of your tests.
For example, an agent deployed on several machines will allow to run the same test on different environment to test or pilot.

The complete list of available agents are described in the `Server Add-ons> Agents` chapter.

.. note :: The agent name or probe must be unique for successful registration.

.. tip ::
   For a better visibility of the agents available, it is advisable to respect the following formalism
   for the names:
     [Agent | probe] [Environment] [prénom_testeur] [name] [instance-number]...
    
     Example:
         agent.win.denis.socket01

Example of a deployed and running agent:

.. image :: /_static/images/toolbox/agent_deployed.png

More
-----------

The toolbox can be enriched with new plugins.

To do this, follow the procedure described in the chapter `Contributions> Development plugins> Toolboxes`.
Plugins are to be dropped into the ``Plugins`` directory.

.. image :: /_static/images/toolbox/toolbox_plugins_install.png

After restarting the toolbox, the add-in appears in the list of "external" agents

.. image :: /_static/images/toolbox/toolbox_plugins.png