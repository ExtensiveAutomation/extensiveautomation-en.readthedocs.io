Users
============

The solution is multi-user, 3 users exists by default:
 - ``Admin``
 - ``Tester``
 - ``Monitor``

.. note:: Don't forget to disable default account in a production environment.

Add user
----------------------

Only an administrator can add a new user. 
La création d'un utilisateur nécessite à minima les paramètres suivants et peut se faire via l'interface web ou bien l'API
 - nom d'utilisateur
 - mot de passe

.. image:: /_static/images/webinterface/add_user.png

.. note:: L'email est utilisée par la solution pour envoyer les rapports de tests et résultats.

.. note:: Il est possible de configurer plusieurs adresses email pour un utilisateur en les séparants avec ``;``

Delete a user
----------------------

Only an administrator can remove a user. This action can be done throught the web interface or the web api.

.. image:: /_static/images/webinterface/delete_user.png
