<div align="center">

# Datadog for VS Code & Cursor

[Overview](#overview)
| [Requirements](#requirements)
| [License](#license)
| [Help and Feedback](#help-and-feedback)

</div>

## Overview

The Datadog extension for VS Code and Cursor brings Datadog to your code editor to accelerate your development.

![Datadog extension for VS Code and Cursor](https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/datadog-vscode-3.png)

The extension includes these features:

- [**Code Security**](#code-security): Detect and fix security vulnerabilities, bugs, and exposed secrets before you commit changes.

- [**Model Context Protocol (MCP) Server**](#mcp-server-setup): Connect the AI agent to production telemetry, tools, and contexts from Datadog.

- [**Code Insights**](#code-insights): Stay informed about code and library vulnerabilities without leaving the code.

- [**View in IDE**](#view-in-ide): Jump directly from code references in Datadog to your source files.

- [**Fix in Chat**](#fix-in-chat): Fix code errors, vulnerabilities, and flaky tests with AI-powered suggestions and explanations.

- [**Log Annotations**](#log-annotations): Gauge log volumes and search logs from your code.

- [**Exception Replay**](#exception-replay): Debug your production code.

- [**Live Debugger**](#live-debugger): Add non-breaking, auto-expiring logpoints to running services to capture runtime data without redeploying.

> Unless stated otherwise, all extension features are available for both VS Code and any other IDEs based on VS Code forks, such as Cursor.

## Requirements

- **Datadog account**: Most features require a Datadog account.
  - New to Datadog? [Learn more][datadog] about Datadog's monitoring and security tools and sign up for a free trial.
  - If your organization uses a [custom sub-domain][custom_subdomain] such as `myorg.datadoghq.com`, you must indicate it using the `datadog.connection.oauth.setup.domain` setting in the IDE.

- **Git**: The extension works better when Git is enabled in the IDE. Ensure this is enabled by checking the `git.enabled` setting.

## MCP Server setup

The extension includes access to the [Datadog Model Context Protocol (MCP) Server][mcp_server]. Enable the MCP Server to enhance your IDE's AI capabilities with your specific Datadog environment.

### In Cursor

Install the [Datadog Cursor Plugin][cursor_plugin] from the Cursor marketplace. The plugin configures the Datadog MCP Server in Cursor automatically.

### In VS Code

Follow the [Datadog MCP Server setup guide][mcp_server] to configure the Datadog MCP Server in VS Code.

## Code Security

The **Code Security** features analyze your code locally to detect and fix security issues and vulnerabilities before you commit your changes. The extension supports two complementary scan types: [Static Code Analysis](#static-code-analysis) and [Secret Scanning](#secret-scanning).

### Static Code Analysis

[Static Code Analysis][static_analysis] analyzes your source files against predefined rules to catch security vulnerabilities, bugs, and maintainability issues.

The extension runs Static Code Analysis rules on the source files you have open in your workspace. Static Code Analysis supports scanning for many programming languages. For a complete list, see [Static Code Analysis Rules][static_analysis_rules]. Issues are shown in the source code editor, and you can directly apply suggested fixes.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/static_analysis.mp4" controls loop muted autoplay style="width:100%" title="Datadog Static Analysis Demo"></video>

#### Get started with Static Code Analysis

When you start editing a source file, the extension checks for [`static-analysis.datadog.yml`][static_analysis_config_file] at your source repository's root. It prompts you to create it if necessary.

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<div align="center"><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/static-analysis-onboard.png" alt="Onboarding banner for setting up Static Code Analysis with Python files" width="50%"/></div>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

After you create the configuration file, the analyzer runs automatically in the background whenever you open a file. If you need to enable Static Code Analysis for a particular language, search for the command `Datadog: Configure Static Analysis Languages` in the command palette (`Shift` + `Cmd/Ctrl` + `P`).

You can also run a batch analysis for individual folders and even the entire workspace. In the IDE's file explorer view, right-click a folder and select **Datadog Code Security \> Analyze Folder** or **Analyze Workspace**.

#### Rule editor

Write and test custom [Static Code Analysis rules][static_analysis_custom_rules] without leaving your IDE. Use the **Datadog DDSA Rule Editor** to design detection logic for internal standards, security patterns, or maintainability checks specific to your codebase.

To open the rule editor, run the `Datadog: New DDSA Rule` command from the command palette (`Shift` + `Cmd/Ctrl` + `P`), or right-click a YAML file and select **Datadog Code Security \> Open in DDSA Rule Editor**.

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<div align="center"><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/code_security/static-analysis-rule-editor.jpg" alt="DDSA Rule Editor in VS Code"/></div>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

### Secret Scanning

[Secret Scanning][secret_scanning] detects exposed credentials — API keys, tokens, and passwords — in your source files before you commit them. File contents are scanned locally against rules fetched from your Datadog organization, and findings appear in the editor as you type.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/code_security/secret_scanning.mp4" controls loop muted autoplay style="width:100%" title="Datadog Secret Scanning Demo"></video>

Secret Scanning is enabled by default and runs in the background whenever you open a source file. No local configuration is required — scan rules are fetched from the Datadog backend. All text files are scanned; binary files are skipped automatically.

You can also scan an entire folder or workspace at once. In the IDE's file explorer view, right-click a folder and select **Datadog Code Security \> Analyze Folder** or **Analyze Workspace**.

> Secret Scanning requires you to be signed in to Datadog, because detection rules are fetched from your Datadog organization.

#### Review findings

Detected secrets are shown in three places:

- **Inline in the editor**: each finding appears as an underline on the detected secret, with severity derived from the rule's priority.
- **Problems panel**: all findings are listed with the source `Datadog`.
- **File Insights view**: findings are grouped alongside other Code Security issues.

#### Suppress a finding

To suppress an individual detection, use the code action for the flagged secret to insert a `no-dd-secrets` comment on the line above. The comment suppresses all secret findings on the immediately following line.

#### Turn Secret Scanning on or off

To toggle Secret Scanning, run the `Datadog: Turn on Secret Scanning` or `Datadog: Turn off Secret Scanning` command from the command palette (`Shift` + `Cmd/Ctrl` + `P`), or change the `datadog.codeSecurity.setup.secretScanning.enabled` setting.

## Code Insights

**Code Insights** displays vulnerabilities in your code and dependencies, as detected by [Code Security][code_security].

The extension identifies vulnerabilities in the code with colored squiggles; hover over the line for more details.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/code-insights-inline-hover.mp4" controls loop muted autoplay style="width:100%" title="Hovering over inline code insights"></video>

The **Code Insights** view in the Datadog sidebar lists all the issues found in the repository. Select an item to view the full insight, and use the links to jump to the related source code location or open the code insight in Datadog.

You can group code insights by kind, file, priority, or service. You can also ignore individual code insights and set filters to view the ones you're most interested in.

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<div align="center"><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/code-insights-2.png" alt="The Code Insights view"/></div>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

For specific insights about the file currently open in the active editor, check the **File Insights** view in the IDE's file explorer. This view also lists issues discovered by [Code Security](#code-security) within the file.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/file_insights_view-2.mp4" controls loop muted autoplay style="width:100%" title="Datadog Code Insights"></video>

### Other insight types

The following insight types are in limited support:

- Runtime errors collected by [Error Tracking][error_tracking]
- Flaky tests detected by [Test Optimization][test_optimization]

## View in IDE

> This feature is only available for VS Code and Cursor. Other forks of VS Code are not supported.

The **View in VS Code** or **View in Cursor** feature provides a link from Datadog directly to your source files. Look for the button next to frames in stack traces displayed in the UI (for example, in [Error Tracking][error_tracking]):

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<div align="center"><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/view-in-vscode-2.png" alt="A stack trace in Datadog showing the View in VS Code button"/></div>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

You can also use this feature to open your source files from an insight (such as an error from Error Tracking):

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<div align="center"><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/view-in-vscode-error.png" alt="An Error Tracking issue in the Datadog showing the View in VS Code button"/></div>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

> To use this feature, first configure [source code integration][source_code_integration] for your service.

## Fix in Chat

The **Fix in Chat** button appears in several contexts when the extension identifies errors or issues. Click the button to generate an AI chat prompt that summarizes the problem, includes relevant details and context, and gives specific instructions for the agent.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/cursor_fix_in_chat.mp4" controls loop muted autoplay style="width:100%" title="Using Fix in Chat to fix an inline code error"></video>

## Log annotations

> This feature is in limited support.

Use **Log Annotations** to gauge the volume of logs generated by a given log line in your code. The extension adds annotations above your code to detected logging patterns that match log records in Datadog. Click an annotation to open the [Log Explorer][log_explorer] in Datadog and view the matching logs.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/logs_navigation.mp4" controls loop muted autoplay style="width:100%" title="Datadog Logs Navigation Demo"></video>

You can also search Datadog logs from within VS Code. Select any text in the code editor, then right-click and select **Datadog \> Search Logs With Selected Text**.

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<center>
<br/>
<div><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/0723/log.png" alt="Using the Datadog logs explorer feature."/></div>
</center>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

## Exception Replay

> This feature is in limited support.

**Exception Replay** allows you to inspect the stack trace frames of any Error Tracking code insight and get information about the values of the variables of the code running in production.

To access this feature, you must enable [Error Tracking Exception Replay](exception_replay) on Datadog.

After the feature has been enabled, you can see an **Exception Replay** button next to the stack trace section of any instrumented Error Tracking code insight. Click the button to:

- Access all the information Datadog has about the different frames.
- Navigate through the production code.
- Review the value of the different variables involved.

Select an Error Tracking code insight from the Code Insights view. Go to the stack trace and click the Exception Replay button. The IDE shows a new activity with two new views:

- **Variables**: Displays the variables related to a particular stack trace frame.
- **Stack Trace**: Lists the stack frames for navigation.

Select a stack trace frame and inspect the values of all the variables that Datadog captured from your production code.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/exception_replay.mp4" controls loop muted autoplay style="width:100%" title="Datadog Exception Replay Demo"></video>

## Live Debugger

> This feature is in limited support.

The **Live Debugger** lets you add **logpoints** — auto-expiring, non-breaking breakpoints — to your running services to collect information for debugging. Logpoints are set dynamically, so you don't need to redeploy your code to investigate an issue. Logpoints are grouped into **sessions**, and you can activate, edit, deactivate, or delete sessions (or individual logpoints) at any time. All sessions and logpoints automatically deactivate after 60 minutes, and log events are rate-limited to one execution per second.

To use this feature, your service must be set up for [Datadog Dynamic Instrumentation][dynamic_instrumentation], and remote code is matched to your local files using [Source Code Integration][source_code_integration].

<!-- VIDEO: short overview of the "Datadog Live Debugger" activity in the sidebar, panning across the Sessions, Logpoints, Log Events, and Variables views with a logpoint actively capturing data from a running service. -->

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/live_debugger_overview.mp4" controls loop muted autoplay style="width:100%" title="Datadog Live Debugger Overview"></video>

### The Datadog Live Debugger activity

The extension contributes a dedicated **Datadog Live Debugger** activity to the IDE sidebar, with the following views:

- **Sessions**: lists existing sessions and lets you activate, deactivate, delete, or refresh them, and open them in the Datadog UI. The view can be filtered to show only **your sessions**, only **active sessions**, and/or only sessions whose service repositories are open in the workspace.
- **Logpoints**: lists the logpoints belonging to the selected session. From here you can enable, disable, edit, or delete a logpoint, jump to its source location, copy its id or link, or open it in Datadog.
- **Log Events**: shows recent log events generated by the selected logpoint. You can open events in the Datadog UI or use **Generate Unit Test** to turn captured runtime values into a unit test (see below).
- **Variables**: shows the variables captured for the selected log event as a searchable tree. You can copy values or jump to the variable's source location.
- **Logpoint Editor**: a webview form used to create or edit a logpoint (service, environment, message template, condition, capture variables depth).

### Source editor integration

For lines that have a logpoint defined in the current session, the extension shows a status icon in the editor gutter and a code lens above the line, and lets you act on the logpoint from the line-number context menu:

- **Right-click on the line number** of any line of code and select **Datadog Live Debugger \> Create Logpoint** to start creating a logpoint on that line.
- For a line that already has a logpoint, the same submenu offers **Edit**, **Delete**, and either **Enable** or **Disable** depending on the logpoint's current state.
- Click the code lens above the line to reveal the logpoint in the **Live Debugger** views.

<!-- VIDEO: right-clicking on a line number in the editor, choosing "Datadog Live Debugger > Create Logpoint", filling out the Logpoint Editor (service, environment, message template, condition, capture variables depth), saving, and seeing the new logpoint marker appear next to the line and the logpoint show up in the Logpoints view. -->

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/live_debugger_create.mp4" controls loop muted autoplay style="width:100%" title="Creating a Datadog Live Debugger logpoint"></video>

### Creating a logpoint

To add a logpoint, right-click the line number for a line of code in the source editor and select **Datadog Live Debugger \> Create Logpoint**. The logpoint is added to the current session, or a new session is created if needed.

The **Logpoint Editor** webview shows the following fields:

- **Service** and **Environment**: target the service and environment where the logpoint will run. The list of services is filtered by the current file's language to show only compatible services.
- **Message template**: descriptive text with variable references using the Dynamic Instrumentation expression language. The message is built from the runtime state immediately _before_ the line of code is executed. Generated messages automatically pass through the Dynamic Instrumentation Sensitive Data Scanner.
- **Condition** (optional): when defined, a log event is emitted only if the expression evaluates to `true`. Use it to capture events based on runtime state (for example, a particular user or transaction id).
- **Capture variables depth**: controls how deeply hierarchical data structures are traversed when capturing runtime values. Higher values provide more useful information but require more capacity.

The editor warns you when no service or environment matches the file's language, or when the **remote service is associated with a different repository** than the local workspace — you can still create the logpoint in those cases.

#### Local and remote versions

The remote running code may be a different revision compared to the source you are editing. The extension uses Git commit information to map line numbers from your local file to the remote revision, so logpoints land on the correct line even if the remote is on a different commit. This requires your service to be tagged with Git information.

> **Tip**: checking out locally the same revision that is running remotely shows you the same code in the IDE that is running in production, which simplifies the live debugging experience — but it isn't required.

### Editing, enabling, disabling, and deleting

- **Edit**: right-click a logpoint (in the editor or in the **Logpoints** view) and select **Edit** to update its message template, condition, or capture depth. Changing the service or environment requires deleting the logpoint and creating a new one. Saving an edit also extends the expiration to 60 minutes.
- **Enable / Disable**: toggle a logpoint or a whole session from the views or the line-number context menu. Re-enabling a logpoint extends its expiration to 60 minutes.
- **Delete**: deleting a logpoint does not delete the events it has already generated. Deleting a session deletes all of its logpoints and cannot be undone. The extension asks for confirmation before deleting (you can suppress these prompts in the extension settings).

The gutter icon reflects the current status of each logpoint:

| Icon                                                                                                                                                     | Status       | Meaning                                                                                                                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/live_debugger/probe_active_dark.png" alt="Active" width="16"/>     | **Active**   | The logpoint is installed and emits log events when the line of code is about to run.                                                                                                                |
| <img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/live_debugger/probe_warning_dark.png" alt="Warning" width="16"/>   | **Warning**  | The logpoint may not be generating events yet. This is shown when the backend hasn't processed a recent change (`WAITING`) or no tracer agents are reporting for the targeted service (`NO_AGENTS`). |
| <img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/live_debugger/probe_error_dark.png" alt="Error" width="16"/>       | **Error**    | The logpoint is not generating events because of an error, or its status is unknown.                                                                                                                 |
| <img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/live_debugger/probe_disabled_dark.png" alt="Disabled" width="16"/> | **Disabled** | The logpoint is inactive — either you disabled it manually or it has expired.                                                                                                                        |

### Generate a unit test from a log event

From the **Log Events** view, the **Generate Unit Test** action sends the runtime values captured by a logpoint (variables and arguments) to the chat agent with a prompt to produce a unit test that reproduces the captured state. This is useful to turn a real production event into a regression test.

<!-- VIDEO: in the Live Debugger activity, selecting a Log Event with captured variables, right-clicking and choosing "Generate Unit Test", and showing the chat agent producing a unit test from the captured runtime values. -->

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/live_debugger_test_with_ai.mp4" controls loop muted autoplay style="width:100%" title="Creating a test using AI from Live Debugger-captured values"></video>

## License

Read the [End-User License Agreement][eula] carefully before downloading or using this extension.

## Data and Telemetry

Datadog collects certain information about your usage of this IDE, including how you interact with it, whether errors occurred while using it, what caused those errors, and user identifiers in accordance with the [Datadog Privacy Policy][datadog_privacy_policy] and Datadog's [VS Code extension EULA][eula]. This data is used to help improve the extension's performance and features, including transitions to and from the extension and the applicable Datadog login page for accessing the Services.

If you don't wish to send this data to [Datadog][datadog], you can disable this at any time in the extension's settings: `Datadog > Telemetry > Setup > Enable Telemetry` and select `disabled`.

> The Datadog extension also honors the [VS Code telemetry][vs_code_telemetry] setting.

## Help and Feedback

Help us improve the extension by sharing your feedback using the [feedback form][feedback_form], email us at [team-ide-integration@datadoghq.com
][feedback_email], or create an issue in our [public repository][public_repo].

Check out the [issues][known_issues] section to discover known issues.

Do you use [Cursor][cursor], or another fork of VS Code? Find the extension on the [Open VSX Registry][vsx_extension].

[custom_subdomain]: https://docs.datadoghq.com/account_management/multi_organization/#custom-sub-domains
[datadog_privacy_policy]: https://www.datadoghq.com/legal/privacy/
[datadog]: https://www.datadoghq.com/
[error_tracking]: https://docs.datadoghq.com/tracing/error_tracking/
[eula]: https://www.datadoghq.com/legal/eula/
[feedback_email]: mailto:team-ide-integration@datadoghq.com
[feedback_form]: https://docs.google.com/forms/d/e/1FAIpQLSc5SYEKKTADkGm-5v-m0I9fmMnnumgWEqLhsUhPCYlcPva4lQ/viewform
[known_issues]: https://github.com/DataDog/datadog-for-vscode/issues?q=is%3Aissue+label%3A%22known+issue%22
[log_explorer]: https://docs.datadoghq.com/logs/explorer/
[public_repo]: https://github.com/DataDog/datadog-for-vscode
[source_code_integration]: https://docs.datadoghq.com/integrations/guide/source-code-integration/
[static_analysis_config_file]: https://docs.datadoghq.com/security/code_security/static_analysis/setup/#customize-your-configuration
[static_analysis_rules]: https://docs.datadoghq.com/security/code_security/static_analysis/static_analysis_rules/
[static_analysis]: https://docs.datadoghq.com/security/code_security/static_analysis/setup/
[static_analysis_custom_rules]: https://docs.datadoghq.com/security/code_security/static_analysis/custom_rules/
[secret_scanning]: https://docs.datadoghq.com/security/code_security/secret_scanning/
[vs_code_telemetry]: https://code.visualstudio.com/docs/getstarted/telemetry#_output-channel-for-telemetry-events
[cursor]: https://www.cursor.com
[vsx_extension]: https://open-vsx.org/extension/datadog/datadog-vscode
[mcp_server]: https://docs.datadoghq.com/mcp_server/
[cursor_plugin]: https://cursor.com/marketplace/datadog
[exception_replay]: https://docs.datadoghq.com/tracing/error_tracking/exception_replay/
[code_security]: https://docs.datadoghq.com/security/code_security/
[test_optimization]: https://docs.datadoghq.com/tests/explorer/
[dynamic_instrumentation]: https://docs.datadoghq.com/dynamic_instrumentation/
