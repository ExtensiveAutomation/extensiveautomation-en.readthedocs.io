Troubleshooting
================

Errors codes
------------

**Framework error code**

+----------------------+-------------------------------------------------------------+
| Error code           | Description                                                 |
+----------------------+-------------------------------------------------------------+
| ERR_TE_000           | Generic error during test execution                         |
+----------------------+-------------------------------------------------------------+
| ERR_TE_001           | Generic error during testcase execution                     |
+----------------------+-------------------------------------------------------------+
| ERR_TE_500           | Generic error during script execution                       |
+----------------------+-------------------------------------------------------------+

**Steps errors**

+----------------------+-------------------------------------------------------------+
| Error code           | Description                                                 |
+----------------------+-------------------------------------------------------------+
| ERR_STP_001          | The step is already started, the function `start()`         |
|                      | is called several time in the test.                         |
+----------------------+-------------------------------------------------------------+
| ERR_STP_005          | The test try to set the result bu the step is not started   |
+----------------------+-------------------------------------------------------------+

**Test properties errors**

+----------------------+--------------------------------------------------------------------------+
| Error code           | Description                                                              |
+----------------------+--------------------------------------------------------------------------+
| ERR_PRO_004          | The parameter name for `input` function does not exits                   |
+----------------------+--------------------------------------------------------------------------+

How to fix
---------

Unable to generate the test design of a test
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The generation of the description of a test does not works in some cases:
 - bad version for adapters and libraries
 - syntax error in the test
 - the cache is used in the step definition
