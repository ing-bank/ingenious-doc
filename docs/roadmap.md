# **Release Notes**  
-----------------------------------
## Release Notes : 1.0
---------------------------------------

1. Browser List
2. Bonigarcia's Webdriver Manager
3. Data Column Reordering
4. Capabilities/Options
5. Timeouts and Waits
6. Selenium 4.10.0 Upgrade
7. Whitelisting
8. Data Sheet Search

## Release Notes : 1.1
---------------------------------------

1. Selenium 4.11.0 Upgrade
2. Import Google Chrome Recorder

## Release Notes : 1.2
---------------------------------------

1. Selenium 4.13.0 Upgrade
2. Fixed Object Repository Load issue while importing Google Chrome Recording
3. Search Bar will show focussed testcase and datasheet names
4. Search Bar focus is more accurate now
5. Following methods added to enhance API testing :
    - `storeJsonElementCountInDataSheet()`
    - `assertJSONelementCount()`
    - `assertJSONelementContains()`
    - `assertXMLelementContains()`
6. API request header parameterization
7. Assert API exception codes
8. Reports API response time for each request
9. Disable Object Grouping    

## Release Notes : 1.3
---------------------------------------

1. Selenium 4.16.1 Upgrade
2. Fixed Object Repository issue - Object was not getting copy-pasted from one `page` to another
3. Removed unwanted logging for `ingme_regular.ttf` file as the time INGenious start-up
4. Refresh/Reload in Execution Pane will assign the execution status of each tests to 'No Run'
5. Following Runtime Functions have been added to enhance testing experience:
    - `ToLower()` : To convert a String to lowercase
    - `ToUpper()` : To convert a String to uppercase
    - `getLength()` : To get length of a String
    - `getOccurance()` : To get the number of occurance of a substring in a String
    - `Trim()` : To trim a String
    - `Replace()` : To replace a String with another target String
6. Proxy setup for API Testing can now be done from Configuration window in INGenious GUI
7. Fixed issue faced while launching INGenious in MAC
8. Introduced `x-www-form-urlencoded` POST/PUT request
9. HTML Report now shows an overlay for every API request/response step. We can see the Request/Response bodies from the overlay.

-------------------------------------------

## Release Notes : 2.0
---------------------------------------

1. Selenium 4.20.0 Upgrade
2. Engine changed to a Maven project
3. INGenious extension for recording added
4. Following Runtime Functions have been added/updated to enhance testing experience:   
    - `Replace()` : Issue fixed to work with variables
    - `Substring()` : To get subset or part of String
    - `Split()` : To split given string
5. Column header can be searched from datasheet's search box
6. HttpUrlConnection replaced with HttpClient 

-------------------------------------------

## Release Notes : INGenious Playwright Studio 1.0
---------------------------------------

INGenious with latest version of Playwright has been released. Currently it caters to Browser and API testing only. 

-------------------------------------------

## Release Notes : INGenious Playwright Studio 1.1
---------------------------------------

Cosmetic Changes only

-------------------------------------------

## Release Notes : INGenious Playwright Studio 1.2
---------------------------------------

### Some key features added

* Perform **Mocking of network traffic** without the need of any mocking server
* Use **Storage State** to directly authenticate to browser without having to perform login steps for every test
* Use Basic Authentication out of the box to instantiate a Browser Context
* Switch between pages seamlessly
* Switch between browser contexts within the same test, seamlessly
* Use Mavenized engine for local and Azure DevOps execution
* One click extraction of Azure DevOps Yaml
* Initiate Recording from any step of the test
* Generate Files from data parameterization, out of the box
* Pass browser capabilities via command line - for example `capability.chromium.setheadless=true`


### New Actions Added

1. `Locator.scrollIntoViewIfNeeded()` has been added to `highlightElement()`
2. `RecordFromHere()` added as a new action
3. `CheckIfVisible()` added as a new action
4. `SetCheckedifDataExists()` added as a new action
5. `Page.waitForLoadState()` has been added to `clickByJSifVisible()` 
6. `ClickIfExists()` has been removed
7. `Page.waitForLoadState()` has been added to `ClickIfVisible()`
8. `ClickIfDataExists()` added as a new action
9. `RouteFulfillEndpoint()` added as a new action
10. `RouteFulfillSetBody()` added as a new action
11. `SelectSingleByTextIfDataExists()` added as a new action
12. `SelectSingleByTextIfVisible()` added as a new action
13. `clickAndSwitchToNewPage()` added as a new action
14. `createAndSwitchToNewPage()` added as a new action
15. `createAndSwitchToNewContext()` added as a new action
16. `switchToPageByIndex()` added as a new action
17. `switchToContextByIndex()` added as a new action
18. `switchToContextByPageTitle()` added as a new action
19. `switchToContextByPageURL()` added as a new action
20. `switchToMainPage()` added as a new action
21. `FillIfExists()` has been removed
22. `FillIfDataExists()` added as a new action
23. `FillIfVisible()` added as a new action
24. `waitForLoadState()` added as a new action
25. `closePage()` added as a new action
26. `closeBrowserContext()` added as a new action
27. `split()` added as a new dynamic data generator
28. `subString()` added as a new dynamic data generator

### Bug Fixes

1. Previously browsers did not close at the end of the execution in a Mac machine. This issues has been fixed. `playwright.close()` is being called at the end to free up all resources

2. Previously Playwright Recorder was not getting launched in Mac. But now this has been fixed


-------------------------------------------

# **Roadmap** 

New features being worked on :

- Using Playwright as the execution engine - Phase 1 has been rolled out. Phase 2 is WIP
- Dark mode
- Object identification via AI