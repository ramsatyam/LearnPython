# Testing:
* Unit testing
* Integration Testing
---
* Test Scenario
* Test Suite
* Test case

1. Test Scenario: Login functionality
	* case 1. valid user name and valid password.
	* case 2. valid user name and invalid password
	* case 3. invalid user name and valid password
	* case 4. invalid u.name and invalid password
	* case 5. empty u.name and empty password.

Test suite: Automatic testing of all test cases.

##  How to perform unit testing in python
* module name: unittest
class name: TestCase
instance methods:3 methods
    * setUp()	-	to setup/build the testing environment required for testing
	* test()	-	test scenario to be tested.
    * tearDown()	-	after testing, this is the cleaning actions of the testing environment.
* setUp, tearDown methods shouldn't be change, but test can be changed but prefixed with tear ex. test_method1, test_method2...
* for every test method setUp() and tearDown() methods get executed before and after test case.
* Example
	* setUp(): Open chrome browser
	* test1(): test login functionality in google chrome
	* tearDown(): close chrome browser

	* setUp(): Open firefox browser
	* test2(): test login functionality in firefox
	* tearDown(): close firefox browser
---
* setUpClass(cls):
--->setUpClas method will be executed only once for all test methods.
* test1: test login functionality in chrome with valid user name and password
* test2: test login functionality in chrome with invalid user name and invalid password.
* tearDownClass(cls):
--->after all test methods tearDownClass will be executed only once .
---

Lets say 10 test methods are there
* setUp() ---> 			10	times executed
* tearDown() --->			10
* setUpClass() ---> 		1
* tearDownClass() ---> 	1

---------------------------------------------------------------

## Manual testing:
## Automated testing: Automatically done using writing scripts
	Selenium: Functional testing tool
	QTP: 
	Load Runner: Performance tesing tools
```
import unittest
from selenium import webdriver
import time
driver=None
class GoogleSearch(unittest.TestCase):

	def setUp(self):
		global driver
```
--------------------------------------
# Selenium
Selenium: www.seleniumhq.org
It's a Fucntional Testing Automation Tool. 
Selenium: It's a package
Webdriver: Module in Selenium: to test functionality of web application.
## Basic methods
```
1. driver.get(url)	-> to open specified url
2. driver.maximize_window()	-> to maximize window
3. driver.title	-> to get title of the page
4. driver.current_url	-> To get the current URL
5. driver.refresh()	-> To refresh
	driver.get(driver.current_ur)	-> Another way to refresh the page.
6. driver.back()	-> Goes one step back in browers history
7. driver.forward()	-> Goes one step forward in history.
8. driver.close()	-> Closes current window.
9. driver.quit()	-> To exit browser.
## How to locate web elements
1. driver.find_element_by_id('id')
2. driver.find_element_by_name('name')
3. driver.find_element_by_xpath('xpath')
4. driver.find_element_by_css_selector('css')
5. driver.find_element_by_link_text('text')
or
1. drive.find_element(By.ID, 'id')
2. drive.find_element(By.NAME, 'named')
3. drive.find_element(By.LINK_TEXT, 'xpath')
4. drive.find_element(By.CSS_SELECTOR, 'css')
5. drive.find_element(By.LINK_TEXT, 'text')
```

# Limitations of Unit Testing:
1. Test results will be displayed to the console only and it is not possible to generate reports.
2. unittest framework always executes test methods in aplabetical order only and it is not possible to customize execution order.
3. As the part of batch execution(TestSuite), all test methods from the specified TestCase classes will be executed and it is not possible to specify particular methods.
4. In unittesting only limited setUp and tearDown methods are available.
	* setUpClass() -> Before executing all test methods of TestCase class
	* tearDownClass() -> After executing all test methods of TestCase class
	* setUp() -> Before every test method execution
	* tearDown() -> After every test method execution

	If we want to perform any activity before executing testsuite and after executing testsuite, unittest framework does not define any methods.

# PyTest Framework:

It is advanced version of unittest.

## TestSuite:

A group of testcases is called TestSuite.
Built on unittest framework
Not available by default. we have to 
```pip install pytest```

## PyTest Naming Rules

1. File Name should start or end with 'test'
	ex. test_google_search.py
	google_search_test.py
2. Class name should start with 'Test'
	TestGoogleSearch
	TestCaseDemo
3. Test method name should start with 'test'
	test_method()
	test_method2()

## Testing using PyTest
PyTest executes all the files existing in the folder.
Navigate to the folder where the test files are available and the execute the test using the following command.

```
py.test
py.test filename01
py.test -s -v
-s -> meant for print statement output
-v -> meant for verbose output. 
```
Pytest: setUp(), tearDown(), setUpClas() and tearDownClass()
## How to implement setUp and tearDown method in pytest:
By using some decorator
```
@pytest.fixture()
def fn_name():
	setUp activity
	yeild
	tearDown activity
```
**Here the method name doesn't need to be setUp**
*And setUp methods needs to be associated to the testmethods*
## Deprecated methods:
By using decorate
```
@pytest.yield_fixture()
```
**This decorator is for both setUp and tearDown**
```
@pytest.yield_fixture()
def method():
	setUp activity
	yeild
	tearDown activity
```
**yield** keyword differentiates setUp and tearDown activites.
*if no **yield** is mentioned all activities are setUp activities*
* In the above method, setUp and tearDown activies are executed for each test case.
## To create a setUp class and tearDown class 
* A keyword is to be passed in the decorator.
```
@pytest.fixture(scope='module')
def method():
	setUp activity
	yeild
	tearDown activity
```
## How to implement setUp, tearDown and setUpClass, tearDownClass functionality simultaneously in pyTest:
* We can call both module level setUp and tearDown activities and method level setUp and tearDown activities simultaneously by called both of them in the fucntion definition
```
def test_method_name(module_level_fixture, method_level_fixture)
```
## Configuration test file - conftest.py
* Common setUp and tearDown activities are defined in this file.
* It is automatically available to all test scripts.
* It helps in code re usability.
* It should be available at the same location as test scripts.
**The name of the file should be conftest.py only.**
## Various possible ways to run pytest test scripts
* `py.test -v -s` To run all test methods present in all test scripts of current working directory.
* `py.test -v -s test.py` To run test methods of a particular test script. 
* `py.test -v -s test01.py test02.py` To run multiple test scripts.
* `py.test -v -s test01.py::test_methodA` To run only particular method in a particular test script.
## Customizing order of test in pytest
* All test methods in **top to bottom** approach in contrast with unittest where methods are executed in alphanetical order.
* To customize the order of execution in pytest we need another module called pytest-ordering module
* `pip install pytest-ordering` to install the module
* `@pytest.mark.run(order=n)` decorator is used to set the preference order
```
@pytest.mark.run(order=3)  
def test_methodC():
	activity
@pytest.mark.run(order=1)
def test_methodC():
	activity
@pytest.mark.run(order=2)
def test_methodC():
	activity
```
* This is not available in unittest.
## Generate test results in HTML form
* We can generate a HTML test report. In unittest it is not possible and results are always display in the console only. This requires a another module to be installed.
* For this we just need to use arguments during test. Nothing is required to change in the test scripts.
```
pip install pytest-html
pytest -v -s test.py --html=results.html  ==> will generate a HTML file
```
# Django Testing
* Django testing us based on unittest module. In each app we have a test.py file to write our test cases, setUp etc.
* To test the test scripts we use the command `py manage.py test`
```
from django.test import TestCase
```
# Django Rest Frame(DRF) Application testing
```
from rest_framwork.test import APITestCase
from testapp.models import hydjobs

class JobsAPITestCase(APITestCase):
	def setUp(self):
		hydjobs.objects.create(date="2019-03-04, company="IBMSOFT"...)
	def test_get_method(self):
		url="127.0.0.1:8000/api/hydjobsinfo/"
		response = self.client.get(url)
		self.assertEqual(response.status_code, 200)
		qs = hydjobs.objects.filter(company="IBMSOFT)
		self.assertEqual( qs.count(), 1)
	
```
* To execute this test in DRF applicatoin, the server should be up and running, then we run
```
py manage.py test testapp.api.tests
```