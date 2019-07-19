Tests definitions
============

The solution is based on different types of tests for:
  - enable the construction of advanced tests
  - decrease the use of script
  
.. image:: /_static/images/testlibrary/testing_approach.png
   
Test Unit
---------

The ``test unit`` (tux) allows you to write a test case with several steps.
This format is oriented development.

.. image:: /_static/images/testlibrary/tux.png

.. note: ``Python`` is used as the test design language.

Test Suite
---------

The ``test suite`` (tsx) allows you to write several test cases with several steps.
This format is oriented development.

.. image:: /_static/images/testlibrary/tsx.png

.. note: ``Python`` is used as the test design language.

Test Plan
----------

The ``plan test`` (tpx) allows you to write test cases.
The design is realized by nesting the tests `abstract`, `unit` and `suite`
This test format requires no knowledge in development.

.. image:: /_static/images/testlibrary/tpx.png

Test Global
----------

The ``global test`` (tgx) allows you to write test campaigns.
The preparation of the campaigns is carried out by importing the tests `plans`.

.. image:: /_static/images/testlibrary/tgx.png

.. note:: It is also possible to import other types of tests.

	
	