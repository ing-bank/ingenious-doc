# **Best Practices**
----------------------

!!! note "Treat INGenie as a fast junior tester"
    It knows every action in the catalog and never gets bored writing boilerplate — but it cannot see your acceptance criteria, your environments or your risk appetite. Give it context, then review what it produces.

## Prompting

:octicons-check-24: **Be concrete about where things go.** Name the project, the scenario and the test case. INGenie will otherwise invent a structure that does not match your conventions.

:octicons-check-24: **Supply a reachable URL or spec.** Browser discovery, OpenAPI and HAR imports produce grounded, real locators. A prompt without a source forces the model to guess.

:octicons-check-24: **One intent per request.** "Create the login test" then "parameterize it" beats one paragraph asking for both — you get a reviewable checkpoint in between.

:octicons-check-24: **Say what "correct" means.** Expected messages, status codes and end states turn into assertions. Without them you get a script that clicks, not a test that verifies.

:octicons-check-24: **State what must *not* change.** When editing an existing test, name the steps that are in scope and the ones that are off limits. INGenie reports the files it touched, not the lines — so the boundary has to come from your prompt.

:material-close-thick: **Avoid open-ended sweeps** such as "fix all failing tests". Scope the work to a scenario or a test set.

## Reviewing output

!!! danger "INGenie does not show you a diff"
    INGenie reports **which** files it touched — it does not show a before/after view of the lines it changed. A summary such as *"updated `Login/LoginSuccessful.csv`"* tells you nothing about which of the fifteen steps were rewritten.

    Two consequences:

    * **Scope the change in the prompt.** Say explicitly which steps may be modified and which must be left alone — for example *"change only steps 4 and 5; do not touch the login steps or the final assertion"*. Without that boundary INGenie may rewrite neighbouring steps it considers related.
    * **Diff it yourself.** Commit (or stash) before the conversation, then review `git diff` afterwards. That is the only reliable view of what actually changed.

* **Always run `ingenious_testcase_validate`** before committing. It applies the same convention catalog the engine enforces at runtime.
* **Read the generated CSV/YAML.** These are ordinary project files — diff them in your pull request like any other change.
* **Check the locators, not just the green run.** A test can pass today on an `nth=3` locator and break next sprint. Ask for role-, label- or test-id-based locators.
* **Verify assertions are meaningful.** "Page loaded" is not an assertion; "order confirmation number is displayed" is.

## Working modes

|<div style="color:#349651;width:200px">Situation</div>|<div style="color:#AB0066;width:420px">Recommended mode</div>|
|-----------------------------|-----------------------------------|
|Authoring something new, on a shared project|**Attended** — approve each mutating tool call.|
|Bulk refactor on a branch you own|**Unattended**, then review the diff in one go.|
|Exploring, asking questions|Read-only prompts (`*_list`, `*_show`, `*_info`) are safe by design.|

!!! tip "Branch first"
    Create a feature branch before an unattended session. Reviewing a diff is far easier than undoing scattered edits — even with `/undo`.

## Project hygiene

* **Keep conventions in one place.** If you change authoring rules, change them in the engine's convention catalog — the MCP handshake, the `ingenious://docs/conventions` resource and the validator all derive from it, so every assistant stays in sync automatically.
* **Prefer reusable components.** Ask INGenie to extract repeated sequences; a flat 60-step test case is as unmaintainable when a model writes it as when a human does.
* **Externalise data deliberately.** Parameterize values that genuinely vary. Constants belong in the step.
* **Name things properly.** Scenario and test case names end up in reports, test sets and CI filters — correct them in the same conversation rather than renaming later.

## Security

:material-shield-lock: **Never paste real credentials, tokens or production data** into a prompt. Model providers may log requests.

:material-shield-lock: **Use environments and Global Data** for secrets, and let INGenie reference them by name.

:material-shield-lock: **Keep API keys in environment variables.** The `openai` provider reads its key from the variable named by `apiKeyEnv` in `~/.ingenious/ai.json` — do not inline it.

:material-shield-lock: **Point execution at test environments.** `ingenious_run` and especially `ingenious_perf_run` generate real traffic. Check the target before approving.

:material-shield-lock: **Review imported collections.** A Postman or cURL import can carry authorization headers straight into your repository.

## Performance and cost

* **Prefer `*_async` for long work.** `ingenious_run` and `ingenious_perf_run` block until completion — an async run plus polling keeps the conversation responsive and lets you cancel.
* **Use `ingenious_run_dry`** to check formatting without spending an execution.
* **Narrow the context.** Ask for a specific test case rather than "show me the project" — smaller tool results mean faster, cheaper, more accurate turns.
* **Clear stale conversations** with `/clear`. Long histories drift and cost more per turn.
* **Tune idle reaping** with `INGENIOUS_MCP_IDLE_REAP_MS` if your client disconnects frequently and leaves orphaned browser sessions behind.

## Troubleshooting

|<div style="color:#349651;width:280px">Symptom</div>|<div style="color:#AB0066;width:340px">Check</div>|
|---------------------------|---------------------------|
|Client shows no INGenious tools|Launcher path and `JAVA_HOME`; start `ingenious server mcp --verbose` manually and read stderr.|
|Tools appear but every call fails|No project set — pass `--project` or include `project` in the prompt.|
|Protocol errors / garbled responses|Something else is writing to stdout. Remove banners or wrappers around the launcher.|
|Sign-in never completes|Corporate proxy blocking the GitHub device flow endpoints.|
|Browser sessions pile up|Idle reaping disabled or too long; check `INGENIOUS_MCP_IDLE_REAP_MS`.|
|Stale tool list after a rebuild|**INGenious: Restart MCP Server** in VS Code, or restart the client.|

!!! tip "Start with doctor"
    `ingenious_doctor` (or `ingenious doctor`) answers most environment questions in a single call.

----------------------

Related topics :

[Examples](examples.md){ .md-button }
[INGenie](assistant.md){ .md-button }
[MCP Server](mcpserver.md){ .md-button }
