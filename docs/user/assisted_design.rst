Assisted designs
===================

The client contains a automation assistant to create tests without knownledge in development.
The assistant can be used for:
 - Use the basic functions of the framework
 - Execute system commands (ssh)
 - Test applications with a heavy client
 - Test web applications
 - Run actions on an Android mobile

The test consists of a sequence of actions to perform.
The wizard automatically generates a ``test unit`` or ``test suite``.
An existing test (script) can be updated from the wizard too.

To add an action in the assistant, you have to
  - select the action to perform
  - configure it
  - save the action

 
The wizard natively supports the use of the cache. It is therefore possible
save or retrieve values from the cache.

.. image:: /_static/images/client_assistant/aa_basic_log.png

.. note:: Il est possible de mélanger les différents types d'actions.

.. important:: 
  The wizard allows to generate tests in automatic mode but it is also possible to add its own code inside with the ``USERCODE`` action.

Framework Tabulation
------------------

The ``framework`` tab allows you to use the basic functions of the test framework.

Example of a test done with the assistant:
  1. Display the message "hello" in the test
  2. Ask the user during the execution his first name and save it in the cache with the ``firstname`` key
  3. Display the first name in the test log
  4. Check from the cache if the first name contains a specific value.

.. image :: /_static/images/client_assistant/aa_basic_test.png

List of available actions:

.. note :: In red, the essential actions.

+----------------------+------------------------------------------------------------------+
| ``LOG MESSAGE``      | Displays an informational message during test execution          |
+----------------------+------------------------------------------------------------------+
| LOG WARNING          | Display a warning message during test execution                  |
+----------------------+------------------------------------------------------------------+
| ``SET VALUE``        | Saves a data in the cache                                        |
+----------------------+------------------------------------------------------------------+
| RESET CACHE          | Blank the cache completely                                       |
+----------------------+------------------------------------------------------------------+
| USERCODE             | Add custom code in the test                                      |
+----------------------+------------------------------------------------------------------+
| WAIT DURING          | Wait for xx seconds                                              |
+----------------------+------------------------------------------------------------------+
| ``CHECK IF VALUE``   | Check if the value contains a specific text                      |
+----------------------+------------------------------------------------------------------+
| ASK SOMETHING        | Request a value to the user (interaction mode)                   |
+----------------------+------------------------------------------------------------------+

System tab
-----------------

The ``system`` tab allows you to execute commands on a remote server available via SSH.

Example of a test done with the assistant:
 1. Opening the ssh session on the remote machine 192.186.1.251
 2. Sending the text `su -`
 3. Waits to detect the text `Password:` on the screen
 4. Ask the user for the root password and store it in the cache with the `pwd` key
 5. Send the root password using the value stored in the cache
 6. Waiting to detect on the screen the connection prompt
 7. Close the SSH connection.
 
.. image :: /_static/images/client_assistant/aa_sys_example.png

List of available actions:

.. note :: In red, the essential actions.

+--------------------------+--------------------------------------------------------------------+
| ``OPEN SSH SESSION``     | Open an SSH session                                                |
+--------------------------+--------------------------------------------------------------------+
| CLOSE SESSION            | Close the session                                                  |
+--------------------------+--------------------------------------------------------------------+
| CLEAR SCREEN             | Blank screen                                                       |
+--------------------------+--------------------------------------------------------------------+
| ``SEND TEXT``            | Send a string of characters                                        |
+--------------------------+--------------------------------------------------------------------+
| SEND SHORTCUT            | Sending a keyboard shortcut (to interrupt an action)               |
+--------------------------+--------------------------------------------------------------------+
| ``CHECKING IF SCREEN``   | Check if the screen contains specific text                         |
+--------------------------+--------------------------------------------------------------------+

.. note :: Using the ``OPEN SSH SESSION`` action is mandatory before you can use the others available.

Tabulation application
------------------

The ``application`` tab allows you to automate rich applications by allowing:
 - to simulate the keyboard
 - to simulate the mouse
 - search for graphic elements on the screen
 - to search for text

.. warning :: an agent ``sikulix-server`` is needed to use the actions.

Example of a test done with the assistant:
 1. Send the keyboard shortcut `Win + R` to open the run window
 2. Write the text `cmd`
 3. Send the `Enter` keyboard shortcut to open a cmd window.
 4. Waiting to detect the icon of the cmd window
 5. Write the text `cls & ver` to display the version of Windows
 6. Send the `Enter` keyboard shortcut to validate
 7. Send the keyboard shortcut `Ctrl + A` to select the text in the window
 8. Send the keyboard shortcut `Ctrl + C` to copy the selected text to the clipboard
 9. Get the text from the clipboard and save it in the cache
 10. Displays the text copied from the cache
 11. Write the `exit` text in the cmd window
 12. Send the `Enter` keyboard shortcut to close the window.

.. image :: /_static/images/client_assistant/aa_app_example.png

List of available actions:

.. note :: In red, the essential actions.

**Mouse control**

+-----------------------------+--------------------------------------------------------------------+
| ``CLICK ON POSITION``       | Click on the position (x, y)                                       |
+-----------------------------+--------------------------------------------------------------------+
| DOUBLE CLICK ON POSITION    | Double click on the position (x, y)                                |
+-----------------------------+--------------------------------------------------------------------+
| RIGHT CLICK ON POSITION     | Right click on the position (x, y)                                 |
+-----------------------------+--------------------------------------------------------------------+
| MOUSE WHEEL DOWN            | Turn the mouse wheel down                                          |
+-----------------------------+--------------------------------------------------------------------+
| MOUSE WHEEL UP              | Turn the mouse wheel up                                            |
+-----------------------------+--------------------------------------------------------------------+
| MOVE TO POSITION            | Move the cursor to the position (x, y)                             |
+-----------------------------+--------------------------------------------------------------------+
 
**Keyboard control**

+-----------------------------+--------------------------------------------------------------------+
| ``TYPE TEXT``               | Writes text                                                        |
+-----------------------------+--------------------------------------------------------------------+
| TYPE PATH                   | Writes text (to use for paths)                                     |
+-----------------------------+--------------------------------------------------------------------+
| TYPE PASSWORD               | Writes text (to be used to type a password)                        |
+-----------------------------+--------------------------------------------------------------------+
| GET TEXT FROM CLIPBOARD     | Retrieves the text present in the clipboard                        |
+-----------------------------+--------------------------------------------------------------------+
| ``KEYBOARD SHORTCUT``       | Allows you to type a keyboard shortcut                             |
+-----------------------------+--------------------------------------------------------------------+

**String control**

+-----------------------------+--------------------------------------------------------------------+
| CLICK ON WORD               | Search a word on the screen and click on it                        |
+-----------------------------+--------------------------------------------------------------------+
| DOUBLE CLICK ON WORD        | Search for a word on the screen and double-click on it             |
+-----------------------------+--------------------------------------------------------------------+
| RIGHT CLICK ON WORD         | Search for a word on the screen and right-click on it              |
+-----------------------------+--------------------------------------------------------------------+
| WAIT WORD                   | Search a word until it appears                                     |
+-----------------------------+--------------------------------------------------------------------+
| WAIT AND CLICK ON WORD      | Search a word until it appears and click on it                     |
+-----------------------------+--------------------------------------------------------------------+

**Image Control**

+-------------------------------+--------------------------------------------------------------------------------+
| CLICK ON IMAGE                | Search an image and click on it                                                |
+-------------------------------+--------------------------------------------------------------------------------+
| DOUBLE CLICK ON IMAGE         | Search an image and double-click on it                                         |
+-------------------------------+--------------------------------------------------------------------------------+
| RIGHT CLICK ON IMAGE          | Search an image and right-click on it                                          |
+-------------------------------+--------------------------------------------------------------------------------+
| WAIT IMAGE                    | Search an image until you see it on the screen                                 |
+-------------------------------+--------------------------------------------------------------------------------+
| ``WAIT AND CLICK ON IMAGE``   | Search an image until you see it on the screen and click on it                 |
+-------------------------------+--------------------------------------------------------------------------------+
| HOVER MOUSE ON                | Find an image and move the mouse cursor over it                                |
+-------------------------------+--------------------------------------------------------------------------------+
| DRAG IMAGE AND DROP TO        | Find an image and drag and drop to position (x, y)                             |
+-------------------------------+--------------------------------------------------------------------------------+

Browser Tabulation
----------------

The ``browser`` tab allows you to automate web applications by allowing:
 - to control browsers (firefox, internet explorer, chrome, edge)
 - to simulate the keyboard

.. warning :: an agent ``selenium3-server`` or ``selenium2-server`` is needed to use the actions.

.. tip ::
 To click on an HTML element, it is advisable to use systematically
 the ``WAIT VISIBLE AND CLICK ON HTML ELEMENT`` function.

Example of a test done with the assistant:
 1. Get the name from the cache and send it to the HTML element found by the xpath
 2. Click on the HTML element found by the xpath
 3. Find the HTML element found by the xpath and click on it as soon as it is visible on the screen.
 
.. image :: /_static/images/client_assistant/aa_web_example.png

.. note ::
  It is possible to open multiple browsers in parallel on the same extension to define a new session.
  The name of the session is defined by the `` OPEN BROWSER`` action.
  Then use the `` SWITCH TO SESSION`` action to switch sessions.

Available actions:

.. note :: In red, the essential actions.

**Browser Control**

+-----------------------------+--------------------------------------------------------------------+
| ``OPEN BROWSER`` | Open the browser and load the specified url |
+-----------------------------+--------------------------------------------------------------------+
| ``CLOSE BROWSER`` | Closes the browser |
+-----------------------------+--------------------------------------------------------------------+
| MAXIMIZE BROWSER | Enlarges the browser window |
+-----------------------------+--------------------------------------------------------------------+

**Navigation actions**

+-----------------------------+--------------------------------------------------------------------+
| REFRESH PAGE | Refresh the page |
+-----------------------------+--------------------------------------------------------------------+
| GO BACK | Backspace |
+-----------------------------+--------------------------------------------------------------------+
| GO FORWARD | Go forward |
+-----------------------------+--------------------------------------------------------------------+
| ACCEPT ALERT | Validate the javascript alert |
+-----------------------------+--------------------------------------------------------------------+
| DISMISS ALERT | Dismiss the javascript alert |
+-----------------------------+--------------------------------------------------------------------+
| CLOSE CURRENT WINDOW | Closes the current window |
+-----------------------------+--------------------------------------------------------------------+
| SWITCH TO NEXT WINDOW | Toggle on next window |
+-----------------------------+--------------------------------------------------------------------+
| SWITCH TO FRAME | Toggle on the next frame |
+-----------------------------+--------------------------------------------------------------------+
| SWITCH TO SESSION | Toggles to another selenium session |
+-----------------------------+--------------------------------------------------------------------+
| SWITCH TO WINDOW | Toggle on the next frame |
+-----------------------------+--------------------------------------------------------------------+
 
**javascript actions**

+--------------------------------------+---------------------------------------------------------------------+
| EXECUTE JAVASCRIPT ON HTML ELEMENT | Allows you to inject javascript script on an html element |
+--------------------------------------+---------------------------------------------------------------------+

**Actions on html elements**

+---------------------------------------------+--------------------------------------------------------------------------+
| WAIT HTML ELEMENT | Wait for the appearance of a precise HTML element |
+---------------------------------------------+--------------------------------------------------------------------------+
| WAIT AND CLICK ON HTML ELEMENT | Wait for the appearance of a precise HTML element and click on it |
+---------------------------------------------+--------------------------------------------------------------------------+
| WAIT VISIBLE HTML ELEMENT | Wait for an HTML element to be visible to the user |
+---------------------------------------------+--------------------------------------------------------------------------+
| WAIT NOT VISIBLE HTML ELEMENT | Wait until an HTML element is not visible to the user |
+---------------------------------------------+--------------------------------------------------------------------------+
| ``WAIT VISIBLE AND CLICK ON HTML ELEMENT`` | Wait for an HTML element to be visible to the user and click on it |
+---------------------------------------------+--------------------------------------------------------------------------+
| HOVER ON HTML ELEMENT | Move the mouse cursor over a specific HTML element |
+---------------------------------------------+--------------------------------------------------------------------------+
| CLICK ON HTML ELEMENT | Click on a specific HTML element |
+---------------------------------------------+--------------------------------------------------------------------------+
| DOUBLE CLICK ON HTML ELEMENT | Double click on a specific HTML element |
+---------------------------------------------+--------------------------------------------------------------------------+
| CLEAR TEXT ON HTML ELEMENT | Empty the text on a specific HTML element |
+---------------------------------------------+--------------------------------------------------------------------------+
| ``SELECT ITEM BY TEXT`` | Select item according to the text (for combolist or list) |
+---------------------------------------------+--------------------------------------------------------------------------+
| ``SELECT ITEM BY VALUE`` | Select item according to the value attribute (for combolist or list) |
+---------------------------------------------+--------------------------------------------------------------------------+

**Text Recovery**

+----------------------------------+--------------------------------------------------------------------+
| GET TEXT ALERT | Retrieves the text of an alert message javascript |
+----------------------------------+--------------------------------------------------------------------+
| ``GET TEXT FROM HTML ELEMENT`` | Retrieves the text an exact html element |
+----------------------------------+--------------------------------------------------------------------+
| GET PAGE TITLE | Retrieves the title of the page |
+----------------------------------+--------------------------------------------------------------------+
| GET PAGE URL | Get the URL of the page |
+----------------------------------+--------------------------------------------------------------------+
| GET PAGE SOURCE CODE | Get the source code page |
+----------------------------------+--------------------------------------------------------------------+

**Keyboard simulation**

+---------------------------------+--------------------------------------------------------------------+
| TYPE KEYBOARD SHORTCUT | Sends a keyboard shortcut to a specific HTML element |
+---------------------------------+--------------------------------------------------------------------+
| ``TYPE TEXT ON HTML ELEMENT`` | Sends text on a specific HTML element |
+---------------------------------+--------------------------------------------------------------------+

Android Tabulation
--------------

The ``android`` tab allows you to automate mobile applications by enabling:
  - to simulate the keyboard
  - to simulate the use of the fingers on the screen
  - to control the system and the applications

.. warning :: an adb agent is needed to use the actions.

Overview of the agent

.. image :: /_static/images/client_assistant/aa_mob_preview.png

Example of a test done with the assistant:
  1. Wake up the device
  2. Unlock the device
  3. Click on the `HOME` button
  4. Stop the application
  5. Click on the 'Play Store` app to open it
  6. Wait for the application to open and search the `APPS & GAMES` menu
  7. Click on the text `ENTERTAINMENT`
  8. Click on the menu 'MOVIES & TV`
  9. Wait for 5 seconds
  10. Research the image
  11. Put the device to sleep.

.. image:: /_static/images/client_assistant/aa_sys_mobile.png

Available actions:

.. note:: In red, mandatory actions.

**Mobile controls**
	
+-----------------------------+--------------------------------------------------------------------+
| ``WAKE UP AND UNLOCK`` | Wake up and unlock the device |
+-----------------------------+--------------------------------------------------------------------+
| REBOOT | Restarting the device |
+-----------------------------+--------------------------------------------------------------------+
| SLEEP | Paused |
+-----------------------------+--------------------------------------------------------------------+

**Texts** 	

+--------------------------------+--------------------------------------------------------------------+
| ``TYPE SHORTCUT``              | Simulates a shortcut                                               |
+--------------------------------+--------------------------------------------------------------------+
| ``TYPE TEXT ON XML ELEMENT``   | Sends text on a specific element of the interface                  |
+--------------------------------+--------------------------------------------------------------------+
| GET TEXT FROM XML ELEMENT      | Retrieves the text of a specific element of the interface          |
+--------------------------------+--------------------------------------------------------------------+

**Contrôles des éléments XML**

+-------------------------------------+------------------------------------------------------------------------------------+
| CLEAR XML ELEMENT                   | Removes text from a specific element of the interface                              |
+-------------------------------------+------------------------------------------------------------------------------------+
| CLICK ON XML ELEMENT                | Click on a specific element of the interface                                       |
+-------------------------------------+------------------------------------------------------------------------------------+
| LONG CLICK ON XML ELEMENT           | Long-term click on a specific element of the interface                             |
+-------------------------------------+------------------------------------------------------------------------------------+
| ``WAIT AND CLICK ON XML ELEMENT``   | Wait for the appearance of a specific element of the interface and click on it     |
+-------------------------------------+------------------------------------------------------------------------------------+

**Tap on screen** 

+-----------------------------+--------------------------------------------------------------------+
| ``CLICK TO POSITION``       | Click on the position x, y                                         |
+-----------------------------+--------------------------------------------------------------------+
| DRAG FROM POSITION          | Drag from position x1, y1 to x2, y2                                |
+-----------------------------+--------------------------------------------------------------------+
| SWIPE FROM POSITION         | Swipe from position x1, y1 to x2, y2                               |
+-----------------------------+--------------------------------------------------------------------+
