Projects
=======

The solution is multi-project. Il est donc possible d'organiser les tests par projets et d'accorder des droits d'accès pour les 
utilisateurs.

.. note:: The ``Common`` project exists by default, il est accessible par l'ensemble des utilisateurs et ne peux pas être supprimé.

Add a project
-----------------

Only an administrator can add a new project. 
La création d'un projet nécessite de préciser son nom et peut se faire via l'interface web ou bien l'API

.. image:: /_static/images/webinterface/add_project.png

Delete a project
----------------------

Only an administrator can remove a project. 
This action can be done throught the web interface or the web api.

.. image:: /_static/images/webinterface/delete_project.png

.. note:: Si le projet est associé à un utilisateur, la suppression n'est pas autorisée.