# **AI Tools & MCP**
----------------------

!!! note "Premise"
    INGenious exposes its **entire automation surface** — projects, scenarios, test cases, object repositories, test data, execution, reports and performance testing — to AI assistants through a built-in **MCP (Model Context Protocol) server**.

    You describe what you want in plain English. INGenie — or any connected MCP client — calls the same engine APIs the IDE uses, so everything it creates is a *real* INGenious artifact — valid CSV/YAML test cases, repository objects and data sheets that you can open, edit and run by hand afterwards.

## Why MCP?

[Model Context Protocol](https://modelcontextprotocol.io) is an open standard that lets an LLM client (GitHub Copilot, Claude Desktop, Cursor, …) discover and call tools offered by an external application.

INGenious implements an MCP server so that **any** MCP-capable assistant becomes an INGenious authoring agent — without plugins, glue code or prompt engineering on your side. The conventions the engine enforces are shipped to the model during the protocol handshake, so the assistant authors tests the INGenious way from its very first response.

```
  AI client                    INGenious
  (INGenie / Copilot /         ┌──────────────────────────────┐
   Claude / Cursor)            │  MCP tool facade             │
        │                      │    ├─ project / scenario     │
        │  JSON-RPC 2.0        │    ├─ test case / steps      │
        └────── stdio ────────▶│    ├─ object repository      │
                               │    ├─ test data              │
                               │    ├─ run / reports          │
                               │    └─ performance (k6)       │
                               └──────────────────────────────┘
                                          │
                                          ▼
                             Real project files + execution engine
```

## Three ways to use AI with INGenious

|<div style="color:#349651;width:200px">Surface</div>|<div style="color:#AB0066;width:420px">What it is</div>|
|-----------------------------------|-------------------------------------------|
|`INGenie`|The AI assistant built into the INGenious Studio. A chat panel that calls the MCP tools **in-process** — no server to start.|
|`ingenious ai`|INGenie as a conversational REPL in your terminal, over the same tool set.|
|`ingenious server mcp`|A standalone MCP server on stdio, for external clients such as VS Code, Claude Desktop or Cursor.|

!!! tip "Same engine, same tools"
    All three surfaces share one implementation. Whatever INGenie can do, an external MCP client can do as well — and vice versa.

## What you can ask for

* **Author** — create scenarios, test cases and steps from plain-English descriptions or manual test steps.
* **Discover** — drive a live browser session, capture stable locators and save them straight into the Object Repository.
* **Import** — turn a cURL command, a Postman/Bruno collection, an OpenAPI spec, a HAR file or a Playwright recording into runnable tests.
* **Parameterize** — extract hard-coded values into data sheets and wire the steps to `Sheet:Column` references.
* **Execute** — run test cases or test sets, synchronously or asynchronously, and stream back the logs.
* **Explain** — read the latest report, rank the top failure reasons and propose fixes.
* **Load test** — export a test case to a k6 script, validate it, run it and compare against a baseline.
* **Review** — validate a test case against INGenious authoring conventions before you commit it.

## Guardrails

* **Conventions are enforced, not suggested.** `ConventionCatalog` in the engine is the single source of truth. It feeds the MCP handshake instructions, the `ingenious://docs/conventions` resource *and* the `ingenious_testcase_validate` tool — so the model cannot drift.
* **Read vs. write separation.** Query tools (`*_list`, `*_show`, `*_info`, `*_search`) run freely; mutating tools (`*_create`, `*_update`, `*_delete`) are subject to approval in INGenie.
* **Nothing is hidden.** Every artifact the assistant produces is a plain file in your project, under version control, reviewable in a pull request.

---

Make sure to check out the following topics :

[Prerequisites](prerequisites.md){ .md-button }
[INGenie](assistant.md){ .md-button }
[MCP Server](mcpserver.md){ .md-button }
[Examples](examples.md){ .md-button }
[Best Practices](bestpractices.md){ .md-button }
