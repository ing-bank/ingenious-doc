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
    |[`copilot-sdk`](#setting-up-the-copilot-sdk-provider)|Reuses the **GitHub Copilot CLI** login on your machine (`copilot auth login`). The INGenious MCP server is exposed to it automatically — see [setup below](#setting-up-the-copilot-sdk-provider).|
    |[`openai`](#)|Any OpenAI-compatible chat-completions endpoint (OpenAI, Azure OpenAI, a local gateway). Set `baseUrl`, `model` and put the key in the environment variable named by `apiKeyEnv`.|

### Setting up the `copilot-sdk` provider

The `copilot-sdk` provider does **not** sign in by itself — it drives the official **GitHub Copilot CLI** installed on your machine and reuses the CLI's own authentication. Install and log in once, and every INGenious session picks it up.

=== "1. Install the Copilot CLI"

    The CLI ships as an npm package, so you need **Node.js 22+** and **npm 10+** first:

    ```{ .shell .copy }
    node --version
    npm --version
    ```

    Then install it globally:

    ```{ .shell .copy }
    npm install -g @github/copilot
    ```

    If your `.npmrc` sets `ignore-scripts=true`, install with:

    ```{ .shell .copy }
    npm_config_ignore_scripts=false npm install -g @github/copilot
    ```

    Verify that the `copilot` binary is on your `PATH`:

    ```{ .shell .copy }
    copilot --version
    ```

=== "2. Log in"

    Authenticate the CLI from your normal shell:

    ```{ .shell .copy }
    copilot auth login
    ```

    A browser window opens for the GitHub device flow — approve the request, and the token is stored by the CLI itself. You can also start `copilot` and run `/login` inside it.

    Check the result at any time:

    ```{ .shell .copy }
    copilot auth status
    ```

    !!! note "`/login` inside INGenie"
        Running `/login` in the INGenious REPL while `copilot-sdk` is selected only reminds you to use the CLI — INGenious never stores a Copilot token for this provider.

=== "3. Point INGenious at it"

    In `~/.ingenious/ai.json`:

    ```{ .json .copy }
    {
      "provider": "copilot-sdk",
      "model": "claude-sonnet-4.5",
      "mode": "unattended"
    }
    ```

    Or switch at runtime from the REPL:

    ```{ .copy }
    /model provider copilot-sdk
    /model list
    ```

    `/model list` queries the CLI for the models your subscription allows and lets you pick one. When the provider starts, INGenious automatically exposes its own MCP server to the CLI, so all `ingenious_*` tools are available to the model.

!!! warning "Requires an active Copilot subscription"
    The CLI needs Copilot Pro, Pro+, Business or Enterprise. If startup fails with *"Could not start the Copilot CLI via the SDK"*, re-check `copilot --version` and `copilot auth login` in the same shell that launches INGenious.

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
|[`Node.js`](#)|The GitHub Copilot CLI (`copilot-sdk` provider, needs Node 22+), and building the VS Code extension from source.|

!!! tip "One command to check them all"
    Ask INGenie to *"run doctor"* — or call the `ingenious_doctor` tool / `ingenious doctor` command. It reports the detected JDK, Playwright browsers, drivers and k6 in one go.

## 4. Proxy / network

The device-flow sign-in and any hosted model endpoint need outbound HTTPS. In a corporate network, make sure the usual Java proxy settings are honoured before reporting a sign-in failure.

---

Next up :

[INGenie](assistant.md){ .md-button }
[MCP Server](mcpserver.md){ .md-button }
