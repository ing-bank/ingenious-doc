# **Auto-waiting**

!!! info 
    Playwright performs a range of actionability checks on the elements before making actions to ensure these actions behave as expected. It auto-waits for all the relevant checks to pass and only then performs the requested action. If the required checks do not pass within the given `timeout`, action fails with the `TimeoutError`.

For example, for `click()` action, Playwright will ensure that:

* locator resolves to an exactly one element
* element is Visible
* element is Stable, as in not animating or completed animation
* element Receives Events, as in not obscured by other elements
* element is Enabled

Here is the complete list of actionability checks performed for each action:

Action|Visible|	Stable|	Receives Events	|Enabled|	Editable|
------|-------|-------|-----------------|-------|---------|
**Check**|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	-|
**Click**|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	-|
**Double Click**|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	-|
**setChecked**|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	-|
**Tap**	|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	-|
**Uncheck**	|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	-|
**Hover**	|:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	-|	-|
**dragTo**	|:white_check_mark:|	:white_check_mark:|	:white_check_mark:|	-|	-|
**Screenshot**	|:white_check_mark:|	:white_check_mark:|	-|	-	|-|
**Fill**	|:white_check_mark:|	-|	-|	:white_check_mark:|	:white_check_mark:|
**Clear**	|:white_check_mark:|	-|	-|	:white_check_mark:|	:white_check_mark:|
**selectOption**	|:white_check_mark:|	-	|-	|:white_check_mark:|	-|
**selectText**	|:white_check_mark:|	-|	-|	-|	-|
**scrollIntoViewIfNeeded**|	-|	:white_check_mark:|	-|	-|	-|
**Blur**	|-|	-|	-|	-|	-|
**dispatchEvent**	|-|	-|	-|	-|	-|
**Focus**	|-|	-|	-|	-|	-|
**Press**|-|	-|	-|	-|	-|
**pressSequentially**	|-|	-|	-|	-|	-|
**setInputFiles**	|-|	-|	-|	-|	-|

:material-file-document: Checkout the Playwright documentation [here](https://playwright.dev/docs/actionability)