<div align="center">
<h1>
<img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/logo.png" width="200"/>

<b>Datadog for VS Code</b>

</h1>

<h3>The Datadog extension for VS Code integrates with <a href="https://app.datadoghq.com">Datadog</a> to accelerate your development.</h3>

[![Version](https://img.shields.io/visual-studio-marketplace/v/datadog.datadog-vscode?style=for-the-badge&colorA=252525&colorB=6B1DAC)](https://marketplace.visualstudio.com/items?itemName=datadog.datadog-vscode)
[![Installs](https://img.shields.io/visual-studio-marketplace/i/datadog.datadog-vscode?style=for-the-badge&colorA=252525&colorB=6B1DAC)](https://marketplace.visualstudio.com/items?itemName=datadog.datadog-vscode)
[![Downloads](https://img.shields.io/visual-studio-marketplace/d/datadog.datadog-vscode?style=for-the-badge&colorA=252525&colorB=6B1DAC)](https://marketplace.visualstudio.com/items?itemName=datadog.datadog-vscode)
[![Ratings](https://img.shields.io/visual-studio-marketplace/r/datadog.datadog-vscode?style=for-the-badge&colorA=252525&colorB=6B1DAC)](https://marketplace.visualstudio.com/items?itemName=datadog.datadog-vscode)

[Overview](#overview)
| [Requirements](#requirements)
| [License](#license)
| [Help and Feedback](#help-and-feedback)

<br/>

![screenshot](https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/0723/datadog-vscode.png)

</div>

## Overview

The Datadog extension packs several features including:

- [**Code Insights**](#code-insights) to keep you informed about

  - Issues from [Error Tracking][error_tracking]
  - Reports by [Application Vulnerability Management][vulnerability_management]
  - [Flaky tests][flaky_test_management] detected by CI Visibility

- [**Logs Navigation**](#logs-navigation) to allow you to search for logs from your code.

- [**Static Analysis**](#static-analysis) to detect and fix problems even before you commit changes.

- [**Exception Replay**](#exception-replay) to help you debug your production code.

- [**Recent Commits**](#recent-commits) to alert if one of your pushed commits has caused a CI problem and to help keep track of commits that affect your work.

- [**File Insights**](#file-insights) to view the information that Datadog has for the file open on the active editor.

- [**View in VS Code**](#view-in-vs-code) to directly go from file references on the Datadog platform to your source files.

- [**Code Delta**](#code-delta) to more accurately map observability data to your files in VS Code.

## Requirements

- **A Datadog account**: Most features require a Datadog account.
  - If you're new to Datadog, go to the [Datadog website][datadog] to learn more about Datadog's observability tools and sign up for a free trial.
  - If your company uses a [custom sub-domain][custom_subdomain] like `myorg.datadoghq.com`, you must indicate it using the `datadog.connection.oauth.setup.domain` setting.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/sub_domain.mp4" controls loop muted autoplay title="Sub-Domain Setting"></video>

- **VS Code Git**: The extension works better when VS Code Git integration is enabled. You can ensure that the integration is enabled by checking the `git.enabled` setting.

## Code Insights

The **Code Insights** tree displays insights generated by the Datadog platform that are relevant to your code-base. The Code Insights can be grouped by kind, file, priority, and service.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/code_insights.mp4" controls loop muted autoplay title="Datadog Code Insights"></video>

Code Insights include a detailed description for each issue, and links to:

- The related source code location
- The Datadog platform for additional information

You can dismiss individual Code Insights and set filters to view the ones you are most interested in.

## Logs navigation

You can navigate to the [Log Explorer][log_explorer] on the [Datadog platform][datadog] directly from your source code files.

If you're using a supported logging library and VS Code is properly configured for the language, the extension is able to show you code lenses on the lines where it has detected log patterns that match the Datadog platform records:

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/logs_navigation.mp4" controls loop muted autoplay title="Datadog Logs Navigation Demo"></video>

The supported logging libraries are:

- Golang (requires the [Go][extension-go] extension)
  - [standard library log][log-library-go-standard]
  - [Logrus][log-library-go-logrus]
- JavaScript
  - [@datadog/browser-logs][log-library-js-datadog]
  - [Winston][log-library-js-wiston]
  - [Pino][log-library-js-pino]
  - [Bunyan][log-library-js-bunyan]
  - [Log4js][log-library-js-log4js]
- Python (requires the [Python][extension-python] extension)
  - [logging][log-library-python-logging]

Alternatively, you can select some text in your source code, right click, and select **Datadog > Search Logs With Selected Text** option.

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<center>
<br/>
<div><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/0723/log.png" alt="Enabling the Datadog logs explorer feature."/></div>
</center>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

## Static Analysis

The [Static Analysis][static_analysis] integration analyzes your code (locally) against predefined rules to detect and fix problems.

The Datadog extension runs [Static Analysis][static_analysis] rules on your source files as you edit them. The goal is to detect and fix problems such as maintainability issues, bugs, or security vulnerabilities in your code before you commit your changes.

[Static Analysis][static_analysis] supports scanning for many programming languages. For a complete list, see [Static Analysis Rules][static_analysis_rules]. For file types belonging to supported languages, issues are shown in the source code editor, and suggested fixes can be applied directly.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/static_analysis.mp4" controls loop muted autoplay title="Datadog Static Analysis Demo"></video>

### Getting started

When you start editing a source file, the extension checks for [static-analysis.datadog.yml][static_analysis_config_file] at your source repository's root. It prompts you to create it if necessary.

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<div align="center"><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/static-analysis-onboard.png" alt="Static Analysis onboarding message." width="50%"/></div>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

Once the configuration file is created, the static analyzer runs automatically in the background whenever a file is opened. If you need to enable static analysis for a particular language you can use the following command from the Datadog Menu:

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<div align="center"><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/readme_static_analysis_onboading_command.png" alt="Static Analysis onboarding command." width="75%"/></div>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

You can also run a batch analysis for individual folders and even the entire workspace:

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/static_analysis_batch_analysis.mp4" controls loop muted autoplay title="Datadog Static Analysis Demo"></video>

> The Static Analysis feature does not require a [Datadog][datadog] account, as source files are analyzed locally.

## Exception Replay

Exception Replay allows you to inspect the stack trace frames of any Error Tracking code insight and get information about the values of the variables of the code running in production.

In order to get access to this feature, you have to enable [Error Tracking Exception Replay](https://docs.datadoghq.com/tracing/error_tracking/exception_replay) on Datadog.

After the feature has been enabled, you can see an `Exception Replay` button next to the stack trace section of any instrumented Error Tracking code insight. Click the button to:

- access all the information Datadog has about the different frames
- navigate through the production code
- review the value of the different variables involved

Select an Error Tracking code insight from the Code Insights view. Go to the stack trace and click the Exception Replay button. VS Code shows a new activity with two new views:

- **Variables**: displays the variables related to a particular stack trace frame.
- **Stack Trace**: lists the stack frames for navigation.

Select a stack trace frame and inspect the values of all the variables that Datadog captured from your production code.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/exception_replay.mp4" controls loop muted autoplay title="Datadog Exception Replay Demo"></video>

## Recent Commits

The Recent Commits feature enhances your development workflow by leveraging information from Datadog's Software Delivery suite: [CI Visibility][software_delivery_ci], [Test Visibility][software_delivery_test], and [Code Analysis][software_delivery_code].

The Commit Alert monitors your recent commits and displays a notification on the status bar whenever a commit has triggered a CI issue, such as a test failure, a CI pipeline fail, or a new flaky test occurrence (see the setting `datadog.recentCommits.alert.check.notPassedTest` as an example).

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/recent_commit_alert.mp4" controls loop muted autoplay title="Recent Commit Alert"></video>

The Recent Commits view displays your recent commits pushed to any of the repositories currently open in VS Code. Use the "Set Additional Authors" and "Set Additional Repositories" buttons in the view's toolbar to include commits from other authors and repositories.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/recent_commit_view.mp4" controls loop muted autoplay title="Recent Commit View"></video>

The Recent Commits feature aims to keep you informed and boost your productivity by highlighting commits that need your attention. It distinguishes your commits using the email configured in Git (`git config user.email`) and any "email aliases" you set up with the `datadog.recentCommits.setup.userAliases` setting. You can configure these aliases directly on your settings or by clicking the "Set User Aliases" button in the Recent Commits view toolbar.

## File Insights

The File Insights view provides comprehensive information from Datadog about the file currently open in the active editor. Use this view to explore, search, and organize insights, and to quickly navigate to the specific locations in your code where these insights apply.

<video src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/file_insights_view.mp4" controls loop muted autoplay title="Recent Commit View"></video>

## View in VS Code

The **View in VS Code** feature provides a link from Datadog directly to your source files. Look for the button next to frames in stack traces displayed in the UI (for example, in [Error Tracking][error_tracking]):

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<div align="center"><img src="https://github.com/DataDog/datadog-for-vscode/raw/main/assets/images/readme/0723/view-in-vscode.png" alt="A stack trace on the Datadog platform showing the View in VS Code button."/></div>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

> To use this feature, first configure [source code integration][source_code_integration] for your service.

## Code Delta

Code Delta matches the line numbers included in Datadog telemetry to the line numbers of the files you are currently working on in VS Code.

For example, all [View in VS Code](#view-in-vs-code) links on the Datadog platform encode runtime version info, and the extension uses that to compute the corresponding line of code in your editor, taking into account version changes.

You can tweak the Code Delta settings to change how the matching algorithm works. In particular, you can modify the `Minimum Affinity` value, which determines the degree of confidence required to match lines.

## License

Please read this [End-User License Agreement][eula] carefully before downloading or using the Datadog Visual Studio Code Extension.

## Data and Telemetry

Datadog anonymously collects information about your usage of this IDE, including how you interact with it, whether errors occurred while using it, and what caused those errors, in accordance with the [Datadog Privacy Policy][datadog_privacy_policy] and Datadog's [VS Code extension EULA][eula].

If you don't wish to send this data to [Datadog][datadog], you can opt out at any time in the VS Code extension settings: `Datadog > Telemetry > Setup > Enable Telemetry` and select `disabled`.

> The Datadog extension also honors the [VS Code telemetry][vs_code_telemetry] telemetry setting.

## Help and Feedback

To share your feedback, email [team-ide-integration@datadoghq.com][feedback_email] or create an issue in the extension's [public repository][public_repo].

Check out the [issues][known_issues] section to discover known issues.

[custom_subdomain]: https://docs.datadoghq.com/account_management/multi_organization/#custom-sub-domains
[datadog_custom_roles]: https://docs.datadoghq.com/account_management/rbac/?tab=datadogapplication#custom-roles
[datadog_default_roles]: https://docs.datadoghq.com/account_management/rbac/?tab=datadogapplication#datadog-default-roles
[datadog_privacy_policy]: https://www.datadoghq.com/legal/privacy/
[datadog]: https://www.datadoghq.com/
[error_tracking]: https://docs.datadoghq.com/tracing/error_tracking/
[eula]: https://www.datadoghq.com/legal/eula/
[extension-go]: https://marketplace.visualstudio.com/items?itemName=golang.Go
[extension-python]: https://marketplace.visualstudio.com/items?itemName=ms-python.python
[feedback_email]: mailto:team-ide-integration@datadoghq.com
[flaky_test_management]: https://docs.datadoghq.com/continuous_integration/guides/flaky_test_management/
[known_issues]: https://github.com/DataDog/datadog-for-vscode/issues?q=is%3Aissue+label%3A%22known+issue%22
[log_explorer]: https://docs.datadoghq.com/logs/explorer/
[log-library-go-logrus]: https://pkg.go.dev/github.com/sirupsen/logrus
[log-library-go-standard]: https://pkg.go.dev/log
[log-library-js-bunyan]: https://github.com/trentm/node-bunyan
[log-library-js-datadog]: https://docs.datadoghq.com/logs/log_collection/javascript/
[log-library-js-log4js]: https://github.com/log4js-node/log4js-node
[log-library-js-pino]: https://github.com/pinojs/pino
[log-library-js-wiston]: https://github.com/winstonjs/winston
[log-library-python-logging]: https://docs.python.org/3/library/logging.html
[public_repo]: https://github.com/DataDog/datadog-for-vscode
[software_delivery_ci]: https://docs.datadoghq.com/continuous_integration/
[software_delivery_code]: https://docs.datadoghq.com/code_analysis/
[software_delivery_test]: https://docs.datadoghq.com/tests/
[source_code_integration]: https://docs.datadoghq.com/integrations/guide/source-code-integration/
[static_analysis_config_file]: https://docs.datadoghq.com/continuous_integration/static_analysis/?tab=circleciorbs#setup
[static_analysis_rules]: https://docs.datadoghq.com/continuous_integration/static_analysis/rules
[static_analysis]: https://docs.datadoghq.com/continuous_integration/static_analysis
[vs_code_telemetry]: https://code.visualstudio.com/docs/getstarted/telemetry#_output-channel-for-telemetry-events
[vulnerability_management]: https://docs.datadoghq.com/security/application_security/vulnerability_management/
