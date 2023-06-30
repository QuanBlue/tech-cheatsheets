<h1 align="center">
  <img src="./assets/ansible-logo.png" alt="icon" height="150"></img>
  <br>
  <b>Ansible Cheatsheet</b>
</h1>

<p align="center">Quick reference guide for understanding and using the syntax and concepts in GitHub Actions for workflow automation.</p>

<!-- Badges -->
<p align="center">
  <a href="https://github.com/quanblue/tech-cheatsheets/graphs/contributors">
    <img src="https://img.shields.io/github/contributors/quanblue/tech-cheatsheets" alt="contributors" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/last-commit/quanblue/tech-cheatsheets" alt="last update" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/network/members">
    <img src="https://img.shields.io/github/forks/quanblue/tech-cheatsheets" alt="forks" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/stargazers">
    <img src="https://img.shields.io/github/stars/quanblue/tech-cheatsheets" alt="stars" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/issues/">
    <img src="https://img.shields.io/github/issues/quanblue/tech-cheatsheets" alt="open issues" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/quanblue/tech-cheatsheets.svg" alt="license" />
  </a>
</p>

<p align="center">
  <b>
      <a href="https://github.com/quanblue/tech-cheatsheets">Home page</a> •
      <a href="https://github.com/quanblue/tech-cheatsheets/tree/master/CI.CD">CI/CD page</a>
  </b>
</p>

<br/>

<details open>
<summary><b>📖 Table of Contents</b></summary>

-  [Introduction](#rainbow-introduction)
-  [Usage](#toolbox-usage)
-  [Github Actions Cheatsheet](#page_facing_up-github-actions-cheatsheet)
   -  [Workflow File Basics](#workflow-file-basics)
   -  [Workflow Syntax](#workflow-syntax)
      -  [Name](#name)
      -  [Default](#default)
      -  [On](#on)
         -  [Manual](#manual)
         -  [Automated](#automated)
      -  [Job](#job)
         -  [Runs-on](#runs-on)
         -  [Steps](#steps)
   -  [Workflow Context](#workflow-context)
   -  [Secrets](#secrets)
      -  [Setup Secrets](#setup-secrets)
      -  [Use Secrets](#use-secrets)
   -  [Conditional Execution](#conditional-execution)
   -  [Artifacts](#artifacts)
   -  [Matrix Strategy](#matrix-strategy)
   -  [Parallel Execution](#parallel-execution)
-  [Github Marketplace Actions](#classical_building-github-marketplace-actions)
-  [Example](#bookmark_tabs-example)
-  [Useful links](#chains-useful-links)
-  [Credits](#sparkles-credits)
</details>

# :rainbow: Introduction

**GitHub Actions** is a powerful workflow automation tool provided by GitHub. It allows you to define custom workflows using `YAML` syntax, enabling you to _automate tasks, build, test, and deploy_ your projects directly from your repositories.

# :toolbox: Usage

Create **Workflow file** at `.github/workflows/<workflow_name>.yml`

> **Note:**
>
> -  **Workflow file** must be:
>    -  In the `.github/workflows` directory
>    -  Have a `.yml` or `.yaml` file extension
> -  We can create **multiple workflow**

You can also check out **Workflow files** in `.github/workflows`.

# :page_facing_up: Github Actions Cheatsheet

## Workflow File Basics

```yml
name: [Workflow Name]
on:
   event: [trigger]

defaults:
   run:
      shell: [shell]
      working-directory: [directory]

jobs:
   [job_name]:
      runs-on: [os]
      steps:
         - name: [Step Name]
           uses: [action]
           with:
              key: [value]
         - name: [Another Step]
           run: |
              command 1
              command 2
```

## Workflow Syntax

-  `name`: Specifies the name of the workflow.
-  `default`: Specifies the default value for an input or environment variable for steps in the workflow.
-  `on`: Defines the event that triggers the workflow.
-  `jobs`: Contains one or more jobs to be executed.
-  `runs-on`: Specifies the operating system for the job.
-  `steps`: Lists the individual steps in the job.

### Name

```yml
name: [workflow_name]
```

### Default

`default` is used to specify a default value for an input or environment variable if no value is provided. It allows you to define a fallback value that will be used when the variable is not explicitly set.

```yml
defaults:
   run:
      shell: [shell]
      working-directory: [directory]
```

For example, if you want to use `bash` as the default shell and work directory `./client/` as the default work directory for all steps in the workflow, you can define it as follows:

```yml
defaults:
   run:
      shell: bash
      working-directory: ./client/
```

### On

> **Note:** [Event trigger workflow](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)

4 common event trigger workflow `push`, `pull_request`, `schedule`, `workflow_dispatch`

-  `push`: Triggered when code is pushed to the repository.
-  `pull_request`: Triggered when a pull request is created or updated.
-  `schedule`: Triggered at specified cron schedule.
-  `workflow_dispatch`: Triggered manually through the GitHub UI.

#### Manual

```yml
on: workflow_dispatch
```

#### Automated

```yml
on:
   # On push action
   push:
      branches: [<branch1>, <branch2>, ...]
      paths:
         # Exclude
         - "!<filename>" #exclude file
         - "!<folder>/**-<tail>" # exclude files in the `<folder>` folder that end in `-<tail>`
         # Include (ony run workflow when file changed)
         - "<filename>" #include file
         - "<folder>/**" # include folder
   # On pull request action
   pull_request:
      branches: [<branch1>, <branch2>, ...]
```

### Job

```yml
jobs:
   [job_name]:
      runs-on: [os]
      steps:
         - name: [step_1_name]
           uses: [action]
           with:
              key: [value]
         - name: [step_2_name]
           run: |
              command 1
              command 2
```

#### Runs-on

```yml
runs-on: [operate_system] # ubuntu-latest, windows-latest, macos-latest
```

#### Steps

-  `name`: Describes the step.
-  `uses`: Executes an action from the GitHub Marketplace or a specific repository.
-  `run`: Executes shell commands directly in the step.
-  `with`: Provides input parameters for an action.
-  `env`: Sets environment variables for the step.

## Workflow Context

-  `github`: Provides access to GitHub context information like repository, event payload, etc.
-  `env`: Gives access to environment variables.

## Secrets

-  `secrets`: Stores sensitive information like API keys or passwords.
-  We only see it's value when we set it up.

### Setup Secrets

-  Follow this step for setup secrets:  
   `Setting > Secrets and Variables > Actions > New repository secret`

<div align="center">

![set up secrets](./assets/setup%20secrets.png)

  <div>
    <i>Figure 1. Set up secrets</i>
  </div>
</div>

-  Add new secret key:
   -  `Name`: Name of secret key
   -  `Secret`: Value of secret key

### Use Secrets

Usage: `${{ secrets.<secret_name> }}`

## Conditional Execution

-  `if`: Allows conditional execution based on expressions.
-  `env`: Enables checking environment variables.

## Artifacts

-  `upload-artifact`: Saves files from a job to be used in subsequent jobs.
-  `download-artifact`: Retrieves files uploaded as artifacts.

## Matrix Strategy

-  `strategy`: Enables defining a matrix of configurations for a job.
-  `matrix`: Specifies the different values for the matrix.

## Parallel Execution

-  `jobs.<job_id>.needs`: Defines job dependencies for parallel execution.
-  `jobs.<job_id>.strategy.matrix.<key>`: Accesses matrix values in a job.
-  This cheatsheet provides a quick overview of the syntax and concepts in GitHub Actions. Refer to the official GitHub Actions documentation for more details and advanced features.

Happy automating with GitHub Actions!

# :classical_building: Github Marketplace Actions

-  Go to the GitHub Marketplace website: https://github.com/marketplace.
-  Find the action you want to use.
-  Follow the instructions of the action to include the action in your workflow.

# :bookmark_tabs: Example

Please check out **Workflow files** in `.github/workflows`.

Explain in detail: [Example.md](./Example.md)

# :chains: Useful links

-  [Filter pattern](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#filter-pattern-cheat-sheet)
-  [Event trigger workflow](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)

# :sparkles: Credits

This software uses the following open source packages:

-  [Workflow-syntax-for-github-actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
-  Emojis are taken from [here](https://github.com/arvida/emoji-cheat-sheet.com)

---

> Bento [@quanblue](https://bento.me/quanblue) &nbsp;&middot;&nbsp;
> GitHub [@QuanBlue](https://github.com/QuanBlue) &nbsp;&middot;&nbsp; Gmail quannguyenthanh558@gmail.com
