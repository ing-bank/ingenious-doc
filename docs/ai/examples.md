# **Examples**
----------------------

!!! note "How to read these"
    Each example shows the prompt you type and the tools INGenie (or any connected MCP client) calls on your behalf. You never invoke tools by hand — but knowing which ones exist makes your prompts much sharper.

## 1. Author a browser test from a description

> **You:** Create a test under scenario `Login` called `LoginSuccessful` for `https://practice.expandtesting.com/login`. Sign in with `practice` / `SuperSecretPassword!` and assert the success banner.

|<div style="color:#349651;width:60px">#</div>|<div style="color:#AB0066;width:280px">Tool</div>|<div style="color:#AB0066;width:280px">Effect</div>|
|---|-----------------------|-----------------------|
|1|`ingenious_browser_discover`|Opens a real browser and walks the flow.|
|2|`ingenious_browser_session_save`|Writes stable locators to `ObjectRepository/LoginPage.yaml`.|
|3|`ingenious_testcase_create`|Creates `TestPlan/Login/LoginSuccessful.csv` with linked steps.|
|4|`ingenious_testcase_validate`|Checks the result against the authoring conventions.|
|5|`ingenious_run`|Executes it and returns the report.|

!!! tip "Give it the URL"
    Discovery is far more reliable than guesswork. If you supply a reachable URL, INGenie derives locators from the live DOM instead of inventing them.

## 2. Convert manual test steps

> **You:** Convert these manual steps into a test case under `Checkout` / `GuestCheckout`:
> ```
> 1. Open the shop homepage
> 2. Add the first product to the basket
> 3. Continue as guest
> 4. Fill in the delivery address
> 5. Verify the order confirmation number is displayed
> ```

Uses the `convert_manual_steps` prompt → `ingenious_action_search` (to map each sentence to a real action) → `ingenious_testcase_create` → `ingenious_testcase_validate`.

## 3. Make a test data-driven

> **You:** Parameterize `Login/LoginSuccessful` so it runs for admin, standard and locked-out users.

|<div style="color:#349651;width:60px">#</div>|<div style="color:#AB0066;width:340px">Tool</div>|<div style="color:#AB0066;width:280px">Effect</div>|
|---|-------------------------|-----------------|
|1|`ingenious_testcase_parameterize` *(mode `scan`)*|Proposes which literals should become columns.|
|2|`ingenious_data_sheet_create`|Creates the data sheet.|
|3|`ingenious_testcase_parameterize` *(apply)*|Rewrites the steps to `Sheet:Column` references.|
|4|`ingenious_data_row_add`|Adds one row per user type.|

!!! warning "Review the scan first"
    Run the `scan` mode, read the proposal, *then* apply. Blanket parameterization tends to externalise values that are genuinely constant.

## 4. Build an API test from a cURL command

> **You:** Import this cURL into scenario `Users` and turn it into a test case that asserts HTTP 200 and that `email` is present.

```{ .shell .copy }
curl -X GET "https://api.example.com/users/42" -H "Authorization: Bearer $TOKEN"
```

→ `ingenious_import_curl` → `ingenious_testcase_create` → `ingenious_testcase_validate` → `ingenious_run`.

The same flow works with `ingenious_import_postman`, `ingenious_import_bruno`, `ingenious_gen_from_openapi` and `ingenious_gen_from_har`.

!!! danger "Secrets stay out of the repo"
    Replace tokens with an environment or Global Data reference *before* you let INGenie create the test case. A cURL pasted verbatim will otherwise be committed with the bearer token inside it.

## 5. Run a suite and explain the failures

> **You:** Run the `Regression` test set on Chromium and tell me why things failed.

|<div style="color:#349651;width:60px">#</div>|<div style="color:#AB0066;width:300px">Tool</div>|<div style="color:#AB0066;width:300px">Effect</div>|
|---|--------------------|--------------------|
|1|`ingenious_run_async`|Starts the run, returns a `runId`.|
|2|`ingenious_run_status`|Polled until the run completes.|
|3|`ingenious_report_failures`|Ranks the top failure reasons.|
|4|`ingenious_report_compare`|Diffs against the previous run to separate regressions from known failures.|

## 6. Harden a flaky test

> **You:** `Checkout/GuestCheckout` is flaky — harden it.

Uses the `harden_test` prompt: `ingenious_testcase_show` → `ingenious_object_show` → replaces index-based locators, removes fixed sleeps in favour of explicit waits, adds assertions → `ingenious_testcase_validate`.

## 7. Turn a functional test into a load test

> **You:** Build a k6 load test from `Login/LoginSuccessful` with a spike profile.

|<div style="color:#349651;width:60px">#</div>|<div style="color:#AB0066;width:280px">Tool</div>|<div style="color:#AB0066;width:320px">Effect</div>|
|---|----------------|-------------------------|
|1|`ingenious_perf_export`|Generates the k6 script.|
|2|`ingenious_perf_validate`|Dry-runs with 1 VU / 1 iteration.|
|3|`ingenious_perf_run_async`|Starts the load test, returns a dashboard URL.|
|4|`ingenious_perf_status`|Live VUs, RPS, p95 and error rate.|
|5|`ingenious_perf_compare`|Regression check against a baseline.|

!!! warning "Load testing is not a dry run"
    `ingenious_perf_run` generates real traffic against a real system. Confirm the target is a test environment, and that you are allowed to load it, before approving the tool call.

## 8. Extract reusable components

> **You:** Look across the `Checkout` scenario and pull repeated step sequences into reusable components.

Uses the `extract_reusable` prompt → `ingenious_testcase_list` / `_show` → creates reusable scenarios → rewrites the callers with `Execute` steps.

## 9. Health check

> **You:** Is my setup complete?

→ `ingenious_doctor` reports the detected JDK, Playwright browsers, drivers and k6, and tells you exactly what is missing.

---

Next up :

[Best Practices](bestpractices.md){ .md-button }
[MCP Server](mcpserver.md){ .md-button }
