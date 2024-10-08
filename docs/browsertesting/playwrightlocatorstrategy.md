# **Locator Strategy** 
-------------------------------------------

!!! info
    INGenious uses the built-in locator strategy exposed by Playwright and provides an easy interface to configure them

-------------------------------------------

??? note "Role"

    ### **Locate by Role**

    Consider this DOM example :

    ![role1](../img/playwrightLocators/role1.JPG "role1")

    You can locate each element by its implicit role:

    === ":one: Heading"

        ```java
        page.getByRole(AriaRole.HEADING,new Page.GetByRoleOptions().setName("Sign up"))
        ```
        In **INGenious Playwright Studio**, you will add it as this :

        ![role2](../img/playwrightLocators/role2.JPG "role2")

    === ":two: Subscribe checkbox"

        ```java
        page.getByRole(AriaRole.CHECKBOX,new Page.GetByRoleOptions().setName("Subscribe"))
        ```
        In **INGenious Playwright Studio**, you will add it as this :

        ![role3](../img/playwrightLocators/role3.JPG "role3")

    === ":three: Submit Button"

        ```java
        page.getByRole(AriaRole.BUTTON,new Page.GetByRoleOptions().setName("Submit"))
        ```
        In **INGenious Playwright Studio**, you will add it as this :

        ![role4](../img/playwrightLocators/role4.JPG "role4")

        * `Exact` Option

        Sometimes you may have texts or names with partial matches in the DOM. For example :

        - A `Button` with text `Submit`
        - A `Button` with text `Submit Your Application`

        In this case, to identify the first one, you can use the following:

        ```java
        page.getByRole(AriaRole.BUTTON,new Page.GetByRoleOptions().setName("Submit").setExact(true))
        ```
        In **INGenious Playwright Studio**, you will add it as this :

        ![role5](../img/playwrightLocators/role5.JPG "role5")


--------------------------------------------------------------------------------------

??? note "Label"

    ### **Locate by Label**


    Consider this DOM example :

    ![label1](../img/playwrightLocators/label1.JPG "label1")

    You can locate the element by the label text:

    * Password Input Box

    ```java
    page.getByLabel("Password")
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![label2](../img/playwrightLocators/label2.JPG "label2")

    * `Exact` Option

    Sometimes you may have texts or Labels with partial matches in the DOM. For example :

    - A `Label` with text `Address`
    - A `Label` with text `Secondary Address`

    In this case, to identify the first one, you can use the following:

    ```java
    page.getByLabel("Address",new Page.GetByLabelOptions().setExact(true))
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![label3](../img/playwrightLocators/label3.JPG "label3")



--------------------------------------------------------------

??? note "Placeholder"

    ### Locate by Placeholder

    Consider this DOM example :

    ![placeholder1](../img/playwrightLocators/placeholder1.JPG "placeholder1")

    You can locate the element by the placeholder text:

    * Input Box

    ```java
    page.getByPlaceholder("name@example.com")
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![placeholder2](../img/playwrightLocators/placeholder2.JPG "placeholder2")

    * `Exact` Option

    Sometimes you may have placeholder with partial matches in the DOM. For example :

    - A `Placeholder` with text `Email`
    - A `Placeholder` with text `Secondary Email`

    In this case, to identify the first one, you can use the following:

    ```java
    page.getByPlaceholder("Email", new Page.GetByPlaceholderOptions().setExact(true))
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![placeholder3](../img/playwrightLocators/placeholder3.JPG "placeholder3")



-------------------------------------------

??? note "Text"

    ### Locate by Text

    Consider this DOM example :

    ![text1](../img/playwrightLocators/text1.JPG "text1")

    You can locate the element by the text it contains:

    * Span

    ```java
    page.getByText("Welcome, John")
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![text2](../img/playwrightLocators/text2.JPG "text2")

    * `Exact` Option

    Sometimes you may have texts with partial matches in the DOM. For example :

    - A `header` with text `Welcome`
    - A `span` with text `Welcome, John`

    In this case, to identify the first one, you can use the following:

    ```java
    page.getByText("Welcome", new Page.GetByTextOptions().setExact(true))
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![text3](../img/playwrightLocators/text3.JPG "text3")



-------------------------------------------

??? note "Alt Text"

    ### Locate by Alt Text

    Consider this DOM example :

    ![alttext1](../img/playwrightLocators/alttext1.JPG "alttext1")

    You can locate the element by the alt text:

    * Image

    ```java
    page.getByAltText("playwright logo")
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![alttext2](../img/playwrightLocators/alttext2.JPG "alttext2")

    * `Exact` Option

    Sometimes you may have alt texts with partial matches in the DOM. For example :

    - An `img` with alt test `ING`
    - An `img` with alt text `ING Lion`

    In this case, to identify the first one, you can use the following:

    ```java
    page.getByAltText("ING", new Page.GetByAltTextOptions().setExact(true));
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![alttext3](../img/playwrightLocators/alttext3.JPG "alttext3")



-----------------------------------------------------------

??? note "Title"

    ### Locate by Title


    Consider this DOM example :

    ![title1](../img/playwrightLocators/title1.JPG "title1")

    You can locate the element by the title :

    * Image

    ```java
    page.getByTitle("Issues count")
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![title2](../img/playwrightLocators/title2.JPG "title2")

    * `Exact` Option

    Sometimes you may have titles with partial matches in the DOM. For example :

    - A `span` with title `Payments`
    - An `span` with title `Domestic Payments`

    In this case, to identify the first one, you can use the following:

    ```java
    page.getByTitle("Payments", new Page.GetByTitleOptions().setExact(true))
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![title3](../img/playwrightLocators/title3.JPG "title3")



-------------------------------------------

??? note "Test Id"

    ### Locate by Test Id

    Consider this DOM example :

    ![testid1](../img/playwrightLocators/testid1.JPG "testid1")

    You can locate the element by the title :

    * Button

    ```java
    page.getByTestId("directions")
    ```
    In **INGenious Playwright Studio**, you will add it as this :

    ![testid2](../img/playwrightLocators/testid2.JPG "testid2")


-------------------------------------------

??? note "XPath or CSS"

    ### Locate by XPath or CSS


    * For CSS :

    In **INGenious Playwright Studio**, you will add it as this :

    ![css](../img/playwrightLocators/css.JPG "css")

    * For Xpath :

    In **INGenious Playwright Studio**, you will add it as this :

    ![xpath](../img/playwrightLocators/xpath.JPG "xpath")



-------------------------------------------

??? note "Piercing Shadow DOM"

    ### Locate in Shadow DOM

    All locators in Playwright by default work with elements in Shadow DOM. The exceptions are:

    * Locating by **XPath** does not pierce shadow roots.
    * Closed-mode shadow roots are not supported.

    Consider the following example with a custom web component:

    ```html
    <x-details role=button aria-expanded=true aria-controls=inner-details>
    <div>Title</div>
    #shadow-root
        <div id=inner-details>Details</div>
    </x-details>
    ```
    You can locate in the same way as if the shadow root was not present at all.

    ```java
    page.getByText("Details")
    ```

    In **INGenious Playwright Studio**, you will add it as this :

    ![shadowDom](../img/playwrightLocators/shadowdom.JPG "shadowDom")


-------------------------------------------

??? note "Frames"

    ### Locate in Frames

    All locators in Playwright by default work with elements inside a frame/iframe. But first you need to let the page locate the `frame` using the `framelocator` function.

    You can do that in this way : 

    ```java
    page.frameLocator("iframe[name='firstFr']").getByPlaceholder("Enter name")
    ```

    In **INGenious Playwright Studio**, you will add it as this :

    ![singleframe](../img/playwrightLocators/singleframe.JPG "singleframe")

    If there are nested frames, then just add the frame locators separated by semicolon, in the Frame box :

    ![multipleframes](../img/playwrightLocators/multipleframes.JPG "multipleframes")




--------------------------------------------------------------------------------------------------------------------------------------------------
