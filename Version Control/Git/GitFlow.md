<h1 align="center">
  <img src="./assets/GitFlow/gitflow-logo.png" alt="icon" height="150"></img>
  <br>
  <b>GitFlow</b>
</h1>

<p align="center"> A branching model for software development.</p>

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
      <a href="https://github.com/quanblue/tech-cheatsheets/tree/master/Version%20Control">Version Control page</a> •
      <a href="https://github.com/QuanBlue/Tech-Cheatsheets/tree/master/Version%20Control/Git">Git page</a>
  </b>
</p>

<br/>

<details open>
<summary><b>📖 Table of Contents</b></summary>

-  [Introduction](#rainbow-introduction)
-  [Branching Model](#robot-branching-model)
   -  [Master](#master)
   -  [Develop](#develop)
   -  [Feature](#feature)
   -  [Release](#release)
   -  [Hotfix](#hotfix)
-  [Benefits](#mechanical_arm-benefits)
-  [Note](#memo-note)
   -  [Using Merge Request](#using-merge-request)
   -  [Reduce Conflicts Code](#reduce-conflicts-code)
-  [Develope Process](#gear-develope-process)
   -  [Prequisites](#prequisites)
   -  [Feature Develop Process](#feature-develop-process)
   -  [Release Process](#release-process)
-  [Credits](#sparkles-credits)

</details>

# :rainbow: Introduction

`GitFlow` is a branching model and workflow for version control using Git. It provides a structured approach to managing software development projects.

<div align="center">

![GitFlow](assets/GitFlow/gitflow.png)
<i> GitFlow </i>

</div>

# :robot: Branching Model

## Master

-  Is the branch that exists throughout the life of the software created by default in Git when we create the repository
-  Contain the application's initialization code and versions that are ready to release for users to use (put tags on each version).
-  Usually configurable for interactive management.

<div align="center">

![Master branch](./assets/GitFlow/master.png)
<i> Master branch </i>

</div>

## Develop

-  Is where ongoing development work takes place. It serves as an integration branch for `features` and `bug fixes`.
-  New features and bug fixes (on branch `feature` and `bugfix`) are merged into develop.

> When the **dev team** _completes_ all the features of a topic, the **teamlead** _reviews_ the application and _merges_ it to the `release` branches to create a product release.

<div align="center">

![Develop branch](./assets/GitFlow/dev.png)
<i>Develop branch </i>

</div>

## Feature

-  Are branches forked from `develop` to work on new features or significant changes.
-  They are prefixed with **"feature/"**.
-  Once a feature is complete, the branch is merged back into `develop`.

> **The dev** makes a _merge request_ to the `develop` branches for **teamlead** _review_ and _merges_ it back into the `develop` branches.

<div align="center">

![Feature branch](./assets/GitFlow/feature.png)
<i>Feature branch </i>

</div>

## Release

-  Is a forked branch from `develop` to prepare a new release
-  They allow for finalizing the release, performing last-minute bug fixes, and preparing for deployment.
-  Once ready, the `release` branch is merged into both `develop` and `master`, then deleted.

> when release the app, **teamlead** will _merge_ to `release` branches to prepare the build release for users.

<div align="center">

![Release branch](./assets/GitFlow/release.png)
<i>Release branch </i>

</div>

## Hotfix

-  Are branches forked from `master` to fix critical bugs in production code.
-  They allow for quick fixes without disturbing ongoing development. Once the hotfix is complete, it's merged into both `develop` and `master`.

> When you need to change the configuration for a hotfix learning release in production, **teamlead** will create a branch base on the `master` branch for _hotfixing_ and then _merge_ it back into the `master` (usually, it will not be possible to change the source code directly on the `master` branch, so you have to change the source code on the `master` branch).

<div align="center">

![Hotfix branch](./assets/GitFlow/hotfix.png)
<i>Hotfix branch </i>

</div>

# :mechanical_arm: Benefits

-  Clear separation of stable and development code
-  Structured approach to feature development
-  Enables parallel development and collaboration
-  Facilitates bug fixing and release preparation
-  Provides a version control history that reflects project milestones

# :memo: Note

## Using Merge Request

-  Create a `merge request` so that the **teamlead** or **reviewer** can _review the source code_ before _merging_ to ensure the integrity of the source code, which is extremely important when developing software with a large team.
-  **The reviewer** will _comment_ directly on the need for changes to the merge request to reduce the exchange time and increase efficiency when working in groups.
-  Create a `merge request` to save the change history of the source code. When there are problems with errors, software quality.... we can review all the above changes from the code line (the This can be checked by checking each commit but commits are many).
-  This is also a place to save reviewers' comments, common mistakes so that members don't make old mistakes again and a place to learn code from each other through reviewing code changes line by line. of another member.

## Reduce Conflicts Code

-  **Split code** into independent modules and limit writing too much code into one file,
-  **Regularly merge code** in branches to make sure the current code is the latest
-  **Merge branches' code** before and after code if there is a conflict, then merge conflict before creating the merge request.

# :gear: Develope Process

[Dev Feature](#feature-develop-process) -> [Release](#release-process)

## Prequisites

Create branch `develop` from `master` branch.

```sh
# Create and Switch to `develop` branch
git checkout -b develop

# Push `develop` branch to remote
git push -u origin develop
```

## Feature Develop Process

> **Note:** `Issue tab` for creating a new task.

**<u>Step 1:</u>** **Teamlead** creates a task for developer.

<div align="center">

![Create todo task](assets/GitFlow/Dev-Proc/create-issue.png)
<i>Create new todo task</i>

</div>

**<u>Step 2:</u>** **Developer** has a task to do.

<div align="center">

![Todo task](assets/GitFlow/Dev-Proc/issue.png)
<i>Todo task - Issue ID: #8</i>

</div>

**<u>Step 3:</u>** **Developer** branches `develop`, let's call it `feature/8-xyz`.

```sh
# Create and Switch to `feature/8-xyz` branch
git checkout -b feature/8-xyz

# Push `feature/8-xyz` branch to remote
git push -u origin feature/8-xyz
```

> **Note:** Feature branch name syntax: `feature/[issueID]-[issueName]`

**<u>Step 4:</u>** Developer works on `feature/8-xyz`.

-  Here is example create a new file `feature-8-xyz.txt` and add content to it.

```sh
echo "feature-8-xyz" > feature-8-xyz.txt
```

-  Developer writes their own unit tests for `feature/8-xyz`.

**<u>Step 5:</u>** Developer publishes `feature/8-xyz`.

-  Developer gets updates from `develop` when needed (by merging `develop` in).

```sh
# commit
git add .
git commit -m "#8 - init feature/8-xyz"

# pull and merge from develop branch
git pull origin develop
```

-  Developer makes sure their unit tests and all regression tests pass locally.
-  Developer pushes `feature/8-xyz`

```sh
# commit
git add .
git commit -m "#8 - solve conflict"

# push
git push origin feature/8-xyz
```

> **Note:** commit message syntax: `#[issueID] - [commit message]`

-  Developer makes sure their unit tests and all regression tests pass on build server.

**<u>Step 6:</u>** Developer create pull request to `develop`.

<div align="center">

![Create pull req](assets/GitFlow/Dev-Proc/create-pull-req.png)
<i>Dev - create Pull Request</i>

</div>

<div align="center">

![Updated Issue](assets/GitFlow/Dev-Proc/updated-issue.png)
<i>Issue updated - after create Pull Request</i>

</div>

**<u>Step 7:</u>** Teamlead merges pull request into `develop` branch.

<div align="center">

![Merge Pull Request](assets/GitFlow/Dev-Proc/merge-pull-req.png)
<i>Merge Pull Request</i>

</div>

<div align="center">

![Confirm merge](assets/GitFlow/Dev-Proc/confirm-merge.png)
<i>Confirm merge</i>

</div>

<div align="center">

![Updated Issue After Merge](assets/GitFlow/Dev-Proc/update-issue-last.png)
<i>Issue updated - after Merge</i>

</div>

-  Build server deletes remote `feature/8-xyz`.

```sh
# Switch to develop branch
git checkout develop

# Delete local feature/8-xyz
git branch -d feature/8-xyz

# Delete remote feature/8-xyz
git push origin --delete feature/8-xyz
```

**<u>Step 8:</u>** Goto **step 1**.

## Release Process

**<u>Step 1:</u>** Checkout to `release` branch from `develop` branch.

```sh
# Create and Switch to `release-v1.0.0` branch
git checkout -b release-v1.0.0 develop

# Push `release-v1.0.0` branch to remote
git push -u origin release-v1.0.0
```

> **Note:** Release branch name syntax: `release-v[version]`

**<u>Step 2:</u>** Create Release Tag

```sh
git tag -a v1.0.0 -m "Release v1.0.0"
```

> **Note:**
>
> -  Git Tag syntax: `git tag -a [tag name] -m "[tag message]"`
> -  Tag name syntax: `v[version]`

**<u>Step 3:</u>** Push Tag

```sh
git push --tag
```

<div align="center">

![Pushed Tag](assets/GitFlow/Dev-Proc/tag.png)
<i>Tag - recent push</i>

</div>

<div align="center">

![Pushed Tag 2](assets/GitFlow/Dev-Proc/tag-2.png)
<i>Tag - detail</i>

</div>

**<u>Step 4:</u>** Create Release Pull request to `master` branch.

```sh
# commit
git add .
git commit -m "create release v1.0.0"

# push
git push
```

**<u>Step 5:</u>** Merge Pull Request to `master` branch.

**<u>Step 6:</u>** Checkout to `master` branch then remove `release` branch.

```sh
# Switch to master branch
git checkout master

# Delete local release-v1.0.0 branch
git branch -d release-v1.0.0

# Delete remote
git push origin --delete release-v1.0.0
```

**Complete! - All Feature are release in `master` branch with newest version**

# :sparkles: Credits

-  [Atlassian](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
-  [codeforlife](https://codeforlife.wixsite.com/itblogger/post/t%C3%ACm-hi%E1%BB%83u-v%E1%BB%81-git-flow-trong-ph%C3%A1t-tri%E1%BB%83n-d%E1%BB%B1-%C3%A1n)


---

> Bento [@quanblue](https://bento.me/quanblue) &nbsp;&middot;&nbsp;
> GitHub [@QuanBlue](https://github.com/QuanBlue) &nbsp;&middot;&nbsp; Gmail quannguyenthanh558@gmail.com
