# **Authentication with Playwright** 
-------------------------------------------

<span style="color:Green">There are 2 interesting Authentication techniques in INGenious Playwright Studio</span>

--------------------------------------------

## Basic Authentication

 ![basicAuth](img/specialfeatures/BasicAuth.png "basicAuth")

When working with Basic authentication prompts, which are browser based popups, it is advisable to instantiate an "authenticated" playwright browser context.
In INGenious Playwright Studio, you can do this, by simply navigating to **Run Settings** >> **Authicate Context** and then fill up the details as below :


 ![basicAuth1](img/specialfeatures/BasicAuth1.png "basicAuth1")

After this, you can simply add a test step like :

`Browser` `Open` `@yourURL`

You will see, your browser gets logged in to the system without the actual prompts as shown above.


## Storage State

Playwright executes tests in isolated environments called browser contexts. This isolation model improves reproducibility and prevents cascading test failures. Tests can load existing authenticated state. This eliminates the need to authenticate in every test and speeds up test execution.

**Signing in before each test**

The following example logs into an application. Once these steps are executed, the browser context will be authenticated.

 ![Login](img/specialfeatures/Login.png "Login")

 Redoing login for every test can slow down test execution. To mitigate that, reuse existing authentication state instead.

 The last step (`StoreStorageState`) in the above example, stores the authenticated state in a file `a.json`

 **Reusing signed in state**

Playwright provides a way to reuse the signed-in state in the tests. That way you can log in only once and then skip the log in step for all of the tests.

Web apps use cookie-based or token-based authentication, where authenticated state is stored as cookies or in local storage. Playwright provides BrowserContext.storageState() method that can be used to retrieve storage state from authenticated contexts and then create new contexts with pre-populated state.

Cookies and local storage state can be used across different browsers. They depend on your application's authentication model: some apps might require both cookies and local storage.

The following setting snippet retrieves state from an authenticated context and creates a new context with that state.

 ![authenticate](img/specialfeatures/Authenticate.png "authenticate")
