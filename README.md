# Assistive Technology Test Adapter (ATTA) for Microsoft UI Automation (UIA)
Assistive Technology Test Adapter (ATTA) for use in testing ARIA implementation using the [web platform test suite](http://w3c-test.org/tools/runner/index.html).

This project contains an ATTA for Microsoft UI Automation (UIA) accessibility APIs for the Microsoft Windows operating system and are designed to support automated testing of W3C [Acessible Rich Internet Application 1.1](https://www.w3.org/TR/wai-aria-1.1/) and W3C [CORE Accessibility API Mapping](https://www.w3.org/TR/core-aam-1.1/) (CORE-AAM) implementation in browsers implementing UIA.   

## Python Requirements

* Install Python version 2.7.x
* Setup a [virtual environment](http://docs.python-guide.org/en/latest/dev/virtualenvs/) for python
* Requirements file for virtual environment:

```
  uiautomation==1.1.3
```

## Supported Browsers

* Microsoft Edge

NOTE: The ATTA can be tweaked to work with the latest versions of Firefox and Chrome at the time of writing, but the results obtained on browsers other than Microsoft Edge have not been tested. You might need to follow instructions provided [here](https://github.com/illinois-dres-aitg/atta-msaa-iaccessible2#enabling-accessibility-apis-on-chrome) to make Chrome expose Accessibility API information.

## Running WPT with ATTA to get ARIA 1.1 and CORE AAM test results

1. Start Chrome or Firefox (e.g. typically canary or firefox nightly) to start a test run
1. Go to the [W3C WPT Test Runner](http://w3c-test.org/tools/runner/index.html )
1. To run the [ARIA 1.1 test cases](https://www.w3.org/wiki/ARIA_1.1_Testable_Statements), enter  ```/wai-ara/``` to the textbox label ```Run tests under path```.
1. Start the ATTA for UIA (see command below)
1. Press the ```Start``` button in the WPT Test Runner

Command prompt command:

```
python atta_uia.py
```

1. To run the [CORE AAM test cases](https://www.w3.org/wiki/Core_AAM_1.1_Testable_Statements) use the same proceedure as for ARIA 1.1, but for the textbox labelled ```Run tests under path``` use ```/core-aam/```.


## Updating a local copy of the test cases for ARIA 1.1

Install and configure a local copy of [W3C Web Platform Tests](https://github.com/w3c/web-platform-tests).

The following instructions are assuming you are in the WPT root directory.

1. Generate all tests and put them in a temporary directory.

```
mkdir temp; perl wai-aria/tools/make_tests.pl -d temp -s aria11
```   

2. Remove certain test files that have been updated by hand

```
rm temp/*activedescendant*
```

Note: Assuming you have no changes to make to the active descendant tests.
   This is needed because I've had to hand-edit the those tests to add
   the step to change focus. You'll overwrite that if you replace the
   hand-edited tests with the generated tests. This is a known issue
   which we'll hopefully fix soon.

3. Copy updated test files to ```wai-aria``` directory 

```
cp temp/* wai-aria
```

4. Having done the above, you'll have a local copy of the regenerated tests. To get them added to the official repo, you'll need to do a pull request for the upstream (w3c's official) web-platform-tests repo.



