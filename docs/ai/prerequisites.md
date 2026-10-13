# **Prerequisites**
----------------------

!!! note "Before you start"
    The AI tooling is part of the standard INGenious distributable. There is nothing extra to install for the MCP server itself — but INGenie needs a model provider, and some tools need the usual INGenious runtimes.

## 1. Runtime

|<div style="color:#349651;width:200px">Requirement</div>|<div style="color:#AB0066;width:420px">Notes</div>|
|-----------------------------------|-------------------------------------------|
|[`Java 17+`](#)|Same requirement as the rest of INGenious. Verify with `java -version`.|
|[`ingenious launcher`](#)|`ingenious` / `ingenious.bat` / `ingenious.command` must be on your `PATH`, or referenced by an absolute path.|
|[`A project`](#)|The tools operate on an INGenious project folder. Create one with the IDE or `ingenious project create`.|

## 2. Model provider

The MCP **server** itself needs no model — it only exposes tools. The model is supplied by whatever is driving it.

=== "External MCP client"

    The client brings its own model and subscription:

    * **GitHub Copilot** in VS Code
    * **Claude Desktop**
    * **Cursor**
    * Any client speaking JSON-RPC 2.0 over stdio

=== "INGenie (IDE panel / ingenious ai)"

    Configured through `~/.ingenious/ai.json`:

    ```{ .json .copy }
    {
      "provider": "copilot",
      "model": "gpt-4o",
      "baseUrl": "https://api.openai.com/v1",
      "apiKeyEnv": "OPENAI_API_KEY",
      "mode": "unattended"
    }
    ```

    |<div style="color:#349651;width:140px">provider</div>|<div style="color:#AB0066;width:420px">Authentication</div>|
    |-------------------|---------------------------------------|
    |[`copilot`](#) *(default)*|GitHub **device flow**. Run `/login` in the REPL, or sign in from the INGenie panel. A browser opens, you paste the code — no token to manage by hand.|
    |[`copilot-sdk`](#)|Drives the Copilot CLI through its SDK; the INGenious MCP server is exposed to it automatically.|
    |[`openai`](#)|Any OpenAI-compatible chat-completions endpoint (OpenAI, Azure OpenAI, a local gateway). Set `baseUrl`, `model` and put the key in the environment variable named by `apiKeyEnv`.|

!!! warning "Never commit keys"
    The `openai` provider deliberately reads its key from an **environment variable** rather than from `ai.json`. Keep it that way — `ai.json` lives in your home folder and is easy to leak.

    ```{ .shell .copy }
    export OPENAI_API_KEY="..."
    ```

## 3. Optional runtimes

Only needed by the corresponding tool families:

|<div style="color:#349651;width:200px">Runtime</div>|<div style="color:#AB0066;width:420px">Needed for</div>|
|-----------------------------------|-------------------------------------------|
|[`Playwright browsers`](#)|Browser discovery sessions and browser test execution. Downloaded on first use.|
|[`Appium`](#)|Mobile test execution.|
|[`k6`](#)|Performance tooling (`ingenious_perf_*`).|
|[`Node.js`](#)|Only to build the VS Code extension from source.|

!!! tip "One command to check them all"
    Ask INGenie to *"run doctor"* — or call the `ingenious_doctor` tool / `ingenious doctor` command. It reports the detected JDK, Playwright browsers, drivers and k6 in one go.

## 4. Proxy / network

The device-flow sign-in and any hosted model endpoint need outbound HTTPS. In a corporate network, make sure the usual Java proxy settings are honoured before reporting a sign-in failure.

---

Next up :

[INGenie](assistant.md){ .md-button }
[MCP Server](mcpserver.md){ .md-button }
