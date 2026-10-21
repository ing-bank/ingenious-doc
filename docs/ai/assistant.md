# **INGenie**
----------------------

!!! note "Meet INGenie"
    **INGenie** is the AI assistant built into the INGenious Studio. It is backed by the same MCP tool set an external client gets — so anything INGenie can do, a connected MCP client can do too.

    INGenie has two conversational surfaces: the chat panel in the IDE, and the `ingenious ai` REPL in your terminal. Pick the panel when you are authoring visually, and the REPL when you are already in a shell or running headless.

## INGenie in the INGenious Studio

1. Launch the IDE (`ingenious.command` on macOS/Linux, `ingenious.bat` on Windows).
2. Open or create a project.
3. Open the **INGenie** panel from the toolbar.
4. Sign in the first time — the GitHub **device flow** opens your browser with a one-time code.
5. Type your request.

The panel offers:

|<div style="color:#349651;width:180px">Control</div>|<div style="color:#AB0066;width:440px">Purpose</div>|
|---------------------------|----------------------------------------------|
|`Model selector`|Switch the provider/model for the current session.|
|`Agent mode`|Let INGenie chain tool calls on its own instead of answering a single question.|
|`Attended mode`|Pause at checkpoints and ask you before applying changes. Turn it off for autonomous runs.|
|`Prompt library`|One-click starter prompts (create test case, convert manual steps, explain failure, suggest locator, review test case, …).|
|`History`|Reload a previous conversation. Conversations are stored as JSON under `~/.ingenious/aichat/`.|
|`Connection bulb`|Shows whether the provider is reachable and signed in.|

!!! tip "In-process, not over a socket"
    In the Studio, INGenie calls the tool facade directly inside the IDE process. There is no MCP server to start, no port to open, and the tool behaviour is identical to the stdio server.

## INGenie in the terminal — `ingenious ai`

```{ .shell .copy }
ingenious ai --project Demo
```

`ingenious ai` is also the default when you launch `ingenious` with no arguments from an interactive terminal. Aliases: `ingenious chat`, `ingenious assistant`.

|<div style="color:#349651;width:200px">Option</div>|<div style="color:#AB0066;width:420px">Description</div>|
|-----------------------------------|-------------------------------------------|
|`-p, --project`|Project to work with (name or absolute path).|
|`--mode`|`attended` (pause at checkpoints) or `unattended` (work autonomously). Skips the startup prompt.|
|`--no-banner`|Suppress the welcome banner — handy in CI logs.|

### Slash commands

|<div style="color:#349651;width:160px">Command</div>|<div style="color:#AB0066;width:440px">Description</div>|
|-------------------------|----------------------------------------------|
|`/help`|Overview of everything below.|
|`/login`|Sign in with GitHub (device flow).|
|`/project`|Switch the active project.|
|`/tools`|List the available INGenious tools.|
|`/workflows`|Deterministic workflows that need no model at all.|
|`/plan` / `/approve`|Inspect the pending plan, then execute it.|
|`/mode`|Toggle attended / unattended.|
|`/model`|Switch provider, model or base URL — e.g. `/model provider openai`, `/model url https://…`.|
|`/context` / `/history`|Session memory and recent turns.|
|`/undo` / `/redo`|Roll a change back or forward.|
|`/status` / `/config`|Provider, project, pending plan, undo depth.|
|`/clear`|Start a fresh conversation.|
|`/exit`|Quit.|

### Example session

```{ .text .copy }
› /project Demo
› Create a browser test that logs into https://practice.expandtesting.com/login
  with the demo credentials and asserts the welcome banner.

  ▸ ingenious_browser_session_start     opened Chromium
  ▸ ingenious_browser_session_do        filled #username, #password, clicked Login
  ▸ ingenious_browser_session_save      5 objects → ObjectRepository/LoginPage.yaml
  ▸ ingenious_testcase_create           TestPlan/Login/LoginSuccessful.csv (7 steps)
  ▸ ingenious_testcase_validate         OK — 0 violations

› /approve
› Run it and show me the report.
```

---

Next up :

[MCP Server](mcpserver.md){ .md-button }
[Examples](examples.md){ .md-button }
