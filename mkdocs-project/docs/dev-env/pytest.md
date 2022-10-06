# Development Environment / pytest #

**`pytest` is not currently used for testing but may be used in the future.
This documentation is retained in case it is useful in the future.**

The `pytest` software is a useful tool that provides enhanced unit test features,
which can can also be used for functional testing of Python and other software (in this case StateMod).  See also:

* [pytest documentation](https://doc.pytest.org/en/latest/)
* [Comparison of Python testing frameworks](https://pythontest.com/transcripts/2-pytest-vs-unittest-vs-nose/)

**pytest has not yet been adopted as the testing tool but may be evaluated.
It may also be possible to use a Fortran unit test tool, but Fortran tools seem limited.
TSTool and other tools may also be used for functional testing.**

This documentation contains the following sections:

* [Prerequisites](#prerequisites)
* [Install `pytest`](#install-pytest)
* [Additional `pytest` Configuration](#additional-pytest-configuration)
* [Writing `pytest` Tests](#writing-pytest-tests)

-------------

## Prerequisites ##

The `pytest` software depends on [Python and `pip`](python.md) being installed.

## Install `pytest` ##

To install `pytest` for the installed Python 3 environment and assuming `pip` is installed, run the following on
Windows (normal command shell window, not MinGW), Cygwin, or Linux.  On Windows, run as administrator.

```com
> pip install -U pytest
Collecting pytest
  Downloading pytest-3.0.5-py2.py3-none-any.whl (170kB)
    100% |################################| 174kB 3.3MB/s
    Requirement already up-to-date: colorama; sys_platform == "win32" in c:\program files\python35\lib\site-packages (from pytest)
Collecting py>=1.4.29 (from pytest)
  Downloading py-1.4.32-py2.py3-none-any.whl (82kB)
    100% |################################| 92kB 5.9MB/s
Installing collected packages: py, pytest
Successfully installed py-1.4.32 pytest-3.0.5
```

Test that `pytest` was installed:

```com
> pytest --version
This is pytest version 3.0.5, imported from c:\program files\python35\lib\site-packages\pytest.py
```

## Additional `pytest` Configuration ##

The following may be useful:  [improve slow startup](https://stackoverflow.com/questions/30768254/pytest-py-test-very-slow-startup-in-cygwin).

## Writing `pytest` Tests ##

See the [Development Tasks / Testing](../dev-tasks/testing.md#automated-testing-using-pytest) documentation for examples of tests.
