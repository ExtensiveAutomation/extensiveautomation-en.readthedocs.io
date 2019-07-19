Users
============

The solution is multi-user, 3 users exists by default:
 - ``Admin``
 - ``Tester``
 - ``Monitor``

.. note:: Don't forget to disable default accounts in a production environment.

Add user
----------------------

Only an administrator can add a new user. 
The creation of a user requires at least the following parameters and can be done via the web interface or the API
  - username
  - password

.. note :: Email is used by the solution to send test reports and results.

.. note :: It is possible to configure multiple email addresses for a user by separating them with ``;``

Delete a user
----------------------

Only an administrator can remove a user. This action can be done throught the web interface or the web api.