Projects
=======

The solution is multi-project. It is therefore possible to organize the tests by projects and grant access rights for
users.

.. note:: The ``Common`` project exists by default, it is accessible by all users and can not be deleted.

Add a project
-----------------

Only an administrator can add a new project.
Creating a project requires specifying its name and can be done via the web interface or the API

.. image:: /_static/images/webinterface/add_project.png

Delete a project
----------------------

Only an administrator can remove a project. 
This action can be done throught the web interface or the web api.

.. image:: /_static/images/webinterface/delete_project.png

.. note:: If the project is associated with a user, deletion is not allowed.

Link a project to a user
------------------------

A user can access to several projects. From the profile of a user, you can select 
all the projects authorized. It's possible to define the default one.
