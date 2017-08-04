hello-openfin-Selenium
===========================
Included in this repository are simple example tests for the 'Hello OpenFin' app using the popular WebDriver JS Bindings, test frameworks and assertion libraries.  

We have modified the latest Chrome driver to work with OpenFin Runtime.

Examples for the following WebDriver JS Bindings are included in this project:
 
1. [WebDriverJs / Selenium-WebDriver](http://www.seleniumhq.org/): test/WebDriverJs/Mocha
2. [WebDriverIO](http://webdriver.io/): test/WebDriverIO/Mocha
3. [WD](http://admc.io/wd/): test/WD/Mocha
4. [Protractor](http://angular.github.io/protractor/#/): test/protractor

## Guidelines

Since all HTML5 applications in the OpenFin environment need to be started with OpenFin API, chromeDriver.get(URL) is not supported.

ChromeDriver, by default, starts Chrome browser with various Chrome arguments, including remote debugging port, before running tests.  ChromeOptions.setBinary needs to be called so ChromeDriver can start OpenFin Runtime properly.  RunOpenFin.bat is an example batch file that can be set as 'binary'.

Given there can be multiple applications/windows active in OpenFin Runtime, tests must begin by selecting the targeted window.  Each test script has a function that
selects the window by matching it's title.

Since the OpenFin Runtime is started by OpenFinRVM, Chromedriver does not have direct control of the OpenFin Runtime.  Chromedriver must be started before any test runs.
Once a test is complete, it needs to shut down OpenFin Runtime by running javascript code "fin.desktop.System.exit();".  driver.quit() does not shut down OpenFin Runtime since
it does not have access.   Moving forward, we will improve how Chromedriver controls OpenFin Runtime in the future release.

In Summary
* Tests must target specific windows
* OpenFin RunTime must be shut down after a test is completed

## Prerequisites for Hello OpenFin demo app

1. Install [Chrome driver](https://sites.google.com/a/chromium.org/chromedriver/) 

1. Install Node.js

2. Download/clone this repository and `cd` into it

3. Install all the dependencies    
 ```bash
 npm install
 ```
 
4. Globally install Mocha test framework
 ```bash
 npm install -g mocha
 ```

5. Globally install grunt command line interface
 ```bash
 npm install -g grunt-cli
 ```

6. Install Hello OpenFin app from https://openfin.co/demos/

## Usage

The following steps will help you run tests:

1. Start chromedriver.exe.  You can specify --verbose command line argument to get more loggings.

2. Run all tests
 ```bash
 grunt
 ```
  
3. Run the test for one bindings (replace [bindings] with WD, WebDriverIO or WebDriverJs)
 ```bash
 mocha test/[bindings]/Mocha/hello-openfin.js
 ```

## Instructions for Protractor

The example code is written for the Super Calculator Angular demo app that is used in Quick Start of Protractor (http://angular.github.io/protractor/#/).

1. Install Node.js

2. Download/clone this repository and `cd` into it

3. Install all the dependencies
 ```bash
 npm install

4. Install Protractor
npm install -g protractor

5. Start chromedriver.exe.  You can specify --verbose command line argument to get more loggings.

6. Run the example
 ```bash
 cd test/protractor
 protractor config.js
 ```

## Getting help

Please contact support@openfin.co
