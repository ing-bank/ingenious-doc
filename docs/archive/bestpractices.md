# **Best Practices** 
----------------------------------------------
!!! Documentation on this is currently in progress

-----------------------------------------------

## Use locators

In order to write end to end tests we need to first find elements on the webpage. We can do this by using Playwright's built in locators. Locators come with auto waiting and retry-ability. Auto waiting means that Playwright performs a range of actionability checks on the elements, such as ensuring the element is visible and enabled before it performs the click. To make tests resilient, we recommend prioritizing user-facing attributes and explicit contracts.

```java
page.getByRole('button', { name: 'submit' });

```

Locators can be chained to narrow down the search to a particular part of the page.

```java
const product = page.getByRole('listitem').filter({ hasText: 'Product 2' });
```

You can also filter locators by text or by another locator.

