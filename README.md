<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<div align="center">
<img src="https://github.com/DataDog/datadog-for-vscode/blob/e485aba69d802efd566d87f34571584589185ff2/assets/images/logo.png" width="120">
<h1> Datadog for VS Code </h1>
</div>
<!-- markdownlint-enable MD041 -->
<!-- markdownlint-enable MD033 -->

The [Datadog](https://www.datadoghq.com/) VS Code extension helps bring the power of Synthetic tests to your local environment. Now you can run Synthetic HTTP API and Browser tests against your local code and no longer need to wait for CI/CD runs. With this reduced feedback loop, developers can be better assured of the impact their code changes will have on their applications.

> **DISCLAIMER**
>
> This is a **Public Beta** version of the Datadog extension, intended for Datadog customers that use the [Synthetic Tests](https://docs.datadoghq.com/synthetics/). We currently only support [HTTP API tests](https://docs.datadoghq.com/synthetics/api_tests/http_tests/?tab=requestoptions) and [Browser tests](https://docs.datadoghq.com/synthetics/browser_tests/?tab=requestoptions).

![synthetic tests](https://github.com/DataDog/datadog-for-vscode/blob/e485aba69d802efd566d87f34571584589185ff2/assets/images/readme/readme_synthetic_tests_01.png)

![synthetic tests](https://github.com/DataDog/datadog-for-vscode/blob/e485aba69d802efd566d87f34571584589185ff2/assets/images/readme/readme_synthetic_tests_02.png)

## Features

- Run Synthetic Tests targeting your local environments
- Use custom parameters without altering the original test definition
- See test results locally as well as on Datadog Platform for additional information
- Test only what matters by executing relevant tests at the same time
- Create a list of most frequently used tests by adding them to Favorites  

---

## Requirements

### Datadog Account

The extension requires a datadog account. If you're new to the Datadog suite of products, you can go to the [Datadog website](https://www.datadoghq.com/) to learn more about our observability tools and sign up for a free trial.

### Synthetic Tests

The extension currently only supports execution of synthetic tests. If you don’t use synthetic tests already, you can [create them on Datadog](https://app.datadoghq.com/synthetics/tests).

---

## Getting Started

1. Sign in with your Datadog Account
1. Select a test to execute. You can also find the specific tests you are looking for by searching for them.
1. Update test configuration like pointing the start url to localhost
1. Execute the test

---

## Help and Feedback

For any feedback send an email to [team-ide-integrations@datadoghq.com](mailto:team-ide-integrations@datadoghq.com)
