# **MCP Server**
----------------------

!!! note "ingenious server mcp"
    INGenious ships an MCP server that speaks **JSON-RPC 2.0 over stdio**, implementing the `2024-11-05` revision of the Model Context Protocol. Point any MCP client at it and it gains ~100 INGenious tools.

## Starting the server

=== "Windows"

    ```{ .powershell .copy }
    ingenious server mcp --project Demo --verbose
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command server mcp --project Demo --verbose
    ```

|<div style="color:#349651;width:200px">Option</div>|<div style="color:#AB0066;width:420px">Description</div>|
|-----------------------------------|-------------------------------------------|
|`-p, --project`|Default project — name or absolute path. Optional; tools accept a `project` argument too.|
|`-v, --verbose`|Diagnostic logging **to stderr**.|

!!! warning "stdout belongs to the protocol"
    The server writes nothing but JSON-RPC frames to stdout — all diagnostics go to stderr. Don't pipe anything else into the process' stdout, and don't wrap the launcher in a script that prints a banner.

### Companion REST server

Unrelated to MCP, but useful for dashboards and health probes:

```{ .shell .copy }
ingenious server rest --port 8090 --project Demo
ingenious server status --port 8090
```

## Connecting a client

=== "VS Code"

    Install the **INGenious** VS Code extension. It starts and supervises the MCP server for you.

    |<div style="color:#349651;width:220px">Setting</div>|<div style="color:#AB0066;width:140px">Default</div>|<div style="color:#AB0066;width:260px">Description</div>|
    |------------------------|------------|-------------------------|
    |`ingenious.mcp.autoStart`|`true`|Start the MCP server on activation.|
    |`ingenious.cliPath`|`ingenious`|Path to the launcher.|
    |`ingenious.javaHome`|*(empty)*|Optional `JAVA_HOME` override.|
    |`ingenious.defaultBrowser`|`Chromium`|Browser used for runs.|
    |`ingenious.headless`|`false`|Run headless by default.|
    |`ingenious.report.openOnRunEnd`|`true`|Open the report when a run ends.|

    Use **INGenious: Restart MCP Server** from the Command Palette after changing the launcher or rebuilding the engine.

=== "Claude Desktop"

    ```{ .json .copy }
    {
      "mcpServers": {
        "ingenious": {
          "command": "/absolute/path/to/ingenious",
          "args": ["server", "mcp", "--project", "/absolute/path/to/Projects/Demo"],
          "env": {
            "INGENIOUS_MCP_IDLE_REAP_MS": "900000"
          }
        }
      }
    }
    ```

    Restart the client after editing the config, then confirm the `ingenious` server appears in its tool list.

=== "Cursor / other clients"

    Any client that can spawn a subprocess and speak JSON-RPC over stdio works. Register the same `command` + `args` pair shown for Claude Desktop.

=== "Manual smoke test"

    ```{ .shell .copy }
    ingenious server mcp --verbose
    ```

    Then paste, one per line:

    ```{ .json .copy }
    {"jsonrpc":"2.0","id":1,"method":"initialize","params":{}}
    {"jsonrpc":"2.0","id":2,"method":"tools/list","params":{}}
    ```

    `Ctrl+C` to exit.

## Environment

|<div style="color:#349651;width:260px">Variable / property</div>|<div style="color:#AB0066;width:140px">Default</div>|<div style="color:#AB0066;width:260px">Purpose</div>|
|--------------------------|------------|-----------------------|
|`INGENIOUS_MCP_IDLE_REAP_MS`|`900000`|Idle timeout after which orphaned runs and browser sessions are reaped. `0` disables reaping.|
|`-Dingenious.mcp.idleReapMs`|`900000`|System-property equivalent of the above.|

## Tool catalog

Tools follow a strict `ingenious_<area>_<verb>` naming convention, which the engine's own test suite enforces.

|<div style="color:#349651;width:180px">Area</div>|<div style="color:#AB0066;width:440px">Representative tools</div>|
|-----------------------|--------------------------------------------|
|**Projects & config**|`ingenious_project_list`, `ingenious_project_info`, `ingenious_project_create`, `ingenious_config_get/set/show`, `ingenious_config_drivers`|
|**Scenarios**|`ingenious_scenario_list/create/info/delete`, `ingenious_scenario_tags_add`|
|**Test cases**|`ingenious_testcase_list/show/create/delete`, `ingenious_testcase_add_step`, `_insert_step`, `_edit_step`, `_remove_step`, `_move_step`, `ingenious_testcase_validate`, `ingenious_testcase_parameterize`|
|**Test sets**|`ingenious_testset_list/show/create/add`|
|**Actions**|`ingenious_action_list/search/info/categories`|
|**Object Repository**|`ingenious_object_list/show/search/add/update/delete`, `ingenious_object_import_page`|
|**Test data**|`ingenious_data_sheet_create`, `ingenious_data_row_add/delete`, `ingenious_data_column_add`, `ingenious_data_show/get/set`, `ingenious_data_import`, `ingenious_data_generate`|
|**Environments**|`ingenious_env_list/create/delete`|
|**Execution**|`ingenious_run`, `ingenious_run_async`, `ingenious_run_status/logs/cancel`, `ingenious_run_dry`, `ingenious_doctor`|
|**Reports**|`ingenious_report_latest/history/failures/show/compare/export`|
|**Imports**|`ingenious_import_curl/postman/bruno/playwright`|
|**API collections**|`ingenious_apicollection_create/list/show/import`, `_requests_add`, `_env_set`, `_run`, `_request_run`, `_to_testcase`|
|**Browser discovery**|`ingenious_browser_discover`, `ingenious_browser_session_start/do/snapshot/save/export/close`, `ingenious_browser_inspect`|
|**Generation**|`ingenious_gen_list`, `ingenious_gen_testcase`, `ingenious_gen_from_openapi`, `ingenious_gen_from_har`|
|**Performance (k6)**|`ingenious_perf_export/validate/run/run_async/status/logs/cancel/scale/report/compare`, `ingenious_perf_record_start/stop`|
|**Database**|`ingenious_db_connection_add`|
|**Skills**|`ingenious_skill_list`, `ingenious_skill_read`|

!!! tip "Always current"
    Ask your client for the tool list (`tools/list`, or `/tools` in the REPL) rather than trusting a document — the catalog grows with every release.

## Resources

Read-only context the model can pull on demand, under the `ingenious://` scheme:

|<div style="color:#349651;width:300px">URI</div>|<div style="color:#AB0066;width:340px">Content</div>|
|----------------------------|---------------------------|
|`ingenious://docs/conventions`|**Authoritative** authoring reference — step grammar, prefixes, naming.|
|`ingenious://docs/getting-started`|Workflow primer.|
|`ingenious://docs/step-schema`|Step field layout.|
|`ingenious://docs/best-practices`|Locator, wait and assertion conventions.|
|`ingenious://catalog/actions`|Full action catalog with categories.|
|`ingenious://catalog/archetypes`|Test archetype templates.|
|`ingenious://project/<name>/summary`|Summary of the default project, when one is set.|

## Prompts

The server also publishes ready-made prompt templates. In most clients they show up as slash commands or a prompt picker:

|<div style="color:#349651;width:240px">Prompt</div>|<div style="color:#AB0066;width:400px">Purpose</div>|
|--------------------------|------------------------------|
|`create_test_case`|Build a test case from a plain-English description.|
|`convert_manual_steps`|Turn a numbered manual test into INGenious steps.|
|`record_browser_test`|Author a browser test hands-free from a live session.|
|`discover_browser_flow`|Deterministically discover a flow and generate the Web OR objects.|
|`author_by_archetype`|Generate from a template, validate and run.|
|`make_data_driven` / `build_data_driven_suite`|Externalise hard-coded values into data sheets.|
|`extract_reusable`|Find repeated sequences and extract reusable components.|
|`harden_test`|Replace brittle locators and sleeps, add waits and assertions.|
|`review_test_case` / `debug_test`|Best-practice review and step-by-step risk analysis.|
|`explain_failure` / `triage_run`|Diagnose failures and regressions, propose fixes.|
|`run_and_summarize`|Run a target and summarise the outcome.|
|`suggest_locator`|Propose a stable Playwright locator.|
|`author_load_test`|Export, validate and run a k6 load test.|
|`bootstrap_project`|Create a project seeded with sample tests.|

## Assistants that are not MCP clients

If your tool cannot speak MCP, ship it the conventions manually. The distributable contains ready-made copies under `Resources/ai/`:

|<div style="color:#349651;width:260px">File</div>|<div style="color:#AB0066;width:380px">Use it for</div>|
|--------------------------|-------------------------------|
|`INGenious.skill.md`|Drop into a skills folder, e.g. `.github/skills/ingenious-authoring/SKILL.md`.|
|`copilot-instructions.md`|Append to your repository's `.github/copilot-instructions.md`.|
|`skills/`|Task-specific, tool-first skills: browser tests, API tests, plugin creation, customization detection.|

!!! note "Single source of truth"
    These files mirror `ConventionCatalog` in the engine. An MCP-connected client receives the same content automatically — you only need the copies for tools outside the protocol.

---

Next up :

[Examples](examples.md){ .md-button }
[Best Practices](bestpractices.md){ .md-button }
