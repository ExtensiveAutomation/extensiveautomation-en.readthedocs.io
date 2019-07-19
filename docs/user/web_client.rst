Web interface
=============

Tests part
------------

Global variables
~~~~~~~~~~~~~~~~~~~~~~~

The shared variables enable to describe your dataset. ``JSON`` format must be used.
These variables are reachable from all tests.

Admin part
---------------------

Users
~~~~~~~~~~~~

Users account must be created to use properly the product.
The creation of users can be done through the web interface or from the rest api.

Some parameters must be provided: 
 - username
 - password
 - privilegies (admin, monitor, tester)
 - authorized projects

.. note:: Tests results can be received by email if the account is configured with an email.

.. warning: Don't forget to change passwords for default users.

Projects
~~~~~~~

Tests files can be organized per project.
The adding or removing of a project can be done from the web interface or the REST api.

.. note:: The ``Common`` project exists by default and can be read from all users, this project cannot be removed.
