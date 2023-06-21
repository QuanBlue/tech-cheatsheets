<h1 align="center">
  <img src="./assets/Git-logo.png" alt="icon" height="150"></img>
  <br>
  <b>Git Cheatsheet</b>
</h1>

<p align="center"> Powerful, distributed version control system for tracking changes in code repositories efficiently.</p>

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
      <a href="https://github.com/quanblue/tech-cheatsheets/tree/master/Version%20Control">Version Control page</a>
  </b>
</p>

<br/>

<details open>
<summary><b>📖 Table of Contents</b></summary>

-  [:rainbow: Introduction](#rainbow-introduction)
-  [Git CLI Cheatsheet](#git-cli-cheatsheet)
   -  [Setup](#setup)
   -  [Git Basic](#git-basic)
   -  [Undo Changes](#undo-changes)
   -  [Rewrite History](#rewrite-history)
   -  [Branch \& Merge](#branch--merge)
   -  [Share \& Update](#share--update)
   -  [Inspect \& Compare](#inspect--compare)
      -  [Git log](#git-log)
      -  [Git diff](#git-diff)
      -  [Git show](#git-show)
   -  [Tracking Path Change](#tracking-path-change)
-  [Gitignore Cheatsheet](#gitignore-cheatsheet)
-  [GitFlow](#gitflow)
-  [Commit convention](#commit-convention)
-  [:sparkles: Credits](#sparkles-credits)
</details>

# :rainbow: Introduction

**Git** is a widely used version control system that helps track changes in code repositories. It provides a collaborative platform for developers to manage code, merge changes, and work efficiently in teams.

# Git CLI Cheatsheet

## Setup

Configuring user information used across all local repositories

```sh
# Define the author name to be used for all commits by the current user.
git config --global user.name [name]

# Define the author email to be used for all commits by the current user
git config --global user.email [email]

# Create shortcut for a Git command.
# E.g. alias.glog “log --graph --oneline” will set ”git glog”equivalent to ”git log --graph --oneline.
git config --global alias. [alias-name] [git-command]

# Set text editor used by commands for all users on the machine.
# [editor] arg should be the command that launches the desired editor (e.g., vi).
git config --system core.editor [editor]

# Open the global configuration file in a text editor for manual editing.
git config --global --edit
# set automatic command line coloring for Git for easy reviewing
git config color.ui auto
```

## Git Basic

```sh
# Create empty Git repo in specified directory.
# Run with no arguments to initialize the current directory as a git repository
git init [directory]

# Clone repo located at [repo] onto local machine.
# Original repo can be located on the local filesystem or on a remote machine via HTTP or SSH
git clone [repo]

# Stage all changes in [directory] for the next commit.
# Replace [directory] with a [file] to change a specific file
git add [directory]

# Commit the staged snapshot, but instead of launching a text editor, use [message] as the commit message.
git commit -m "[summary_message]" -m "[description_message]"

# List which files are staged, unstaged, and untracked.
git status

# Push the branch to [remote], along with necessary commits and objects.
# Creates named branch in the remote repo if it doesn’t exist
git push [remote] [branch]

# fetch and merge any commits from the tracking remote branch
git pull
```

## Undo Changes

```sh
# Create new commit that undoes all of the changes made in [commit], then apply it to the current branch.
git revert [commit]

# Remove [file] from the staging area, but leave the working directory unchanged. This unstages a file without overwriting any changes.
git reset [file]

# Shows which files would be removed from working directory.
# Use the -f flag in place of the -n flag to execute the clean.
git clean -n
```

## Rewrite History

Rewriting branches, updating commits and clearing history

```sh
# Replace the last commit with the staged changes and last commit combined. Use with nothing staged to edit the last commit’s message.
git commit --amend

# Apply any commits of current branch ahead of specified one
git rebase [branch]

# clear staging area, rewrite working tree from specified commit
git reset --hard [commit]

# Show a log of changes to the local repository’s HEAD.
# Add --relative-date flag to show date info or --all to show all refs
git reflog
```

## Branch & Merge

Isolating work in branches, changing context, and integrating changes

```sh
# List all of the branches in your repo.
# Add a [branch] argument to create a new branch with the name [branch].
git branch

# Switch to another branch and check it out into your working directory
# Add -b to Create and check out a new branch named [branch].
git checkout [branch]

# Merge the specified branch’s history into the current one
git merge [branch]
```

## Share & Update

Retrieving updates from another repository and updating local repos

```sh
# Create a new connection to a remote repo. After adding a remote
# You can use [name] as a shortcut for [url] in other commands
git remote add [name] [url]

# Fetches a specific <branch>, from the repo.
# Leave off <branch> to fetch all remote refs.
git fetch [remote] [branch]

# merge a remote branch into your current branch to bring it up to date
git merge [alias]/[branch]
```

## Inspect & Compare

Examining logs, diffs and object information

### Git log

```sh
# Limit number of commits by <limit>.
git log -[limit]

# Condense each commit to a single line.
git log --oneline

# Display the full diff of each commit.
git log -p

# Include which files were altered and the relative number of lines that were added or deleted from each of them
git log --stat

# Only display commits that have the specified file
git log -- [file]

# show the commits on [branchA] that are not on [branchB]
git log [branchB]..[branchA]

# show the commits that changed file, even across renames
git log --follow [file]
```

### Git diff

```sh
# Diff of what is changed but not staged
git diff

# Diff of what is staged but not yet committed
git diff --staged

# Show the diff of what is in [branchA] that is not in [branchB]
git diff [branchB]...[branchA]
```

### Git show

```sh
# show any object in Git in human-readable format
git show [SHA]
```

## Tracking Path Change

Versioning file removes and path changes

```sh
# delete the file from project and stage the removal for commit
git rm [file]

# change an existing file path and stage the move
git mv [existing-path] [new-path]

# show all commit logs with indication of any paths that moved
git log --stat -M
```

# Gitignore Cheatsheet

The `.gitignore` file is a configuration file used by Git to determine which files and directories should be ignored and not tracked by version control. It allows you to specify patterns for files or directories that you don't want to include in your Git repository.

```sh
# .gitignore file

# Ignore specific file
file.txt

# Ignore all files in a specific directory
directory/

# Ignore all files with a specific extension
*.extension

# Ignore files in the current directory, but not subdirectories
/*

# Ignore files in all directories with a specific name
**/directory/

# Ignore files in all subdirectories with a specific name
directory/**

# Negation pattern: Include a previously ignored file
!included-file.txt

# Negation pattern: Include a previously ignored directory
!included-directory/

# Ignore files with names starting with a specific prefix
prefix*

# Ignore files with names ending with a specific suffix
*suffix

# Ignore files with names containing a specific string
*substring*

# Ignore files with names matching a specific pattern
pattern?

# Ignore files with names matching multiple patterns
{pattern1,pattern2}

# Ignore files with names matching a range of characters
[a-z]
```

# GitFlow

Check out [GitFlow](https://github.com/QuanBlue/Tech-Cheatsheets/blob/master/Version%20Control/Git/GitFlow.md)

# Commit convention

Check out [Commit Convention](https://github.com/QuanBlue/Tech-Cheatsheets/blob/master/Version%20Control/Git/Commit%20Convention.md)

# :sparkles: Credits

This software uses the following open source packages:

-  [Github education](https://education.github.com/git-cheat-sheet-education.pdf)
-  [Git tutorial](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)

---

> Bento [@quanblue](https://bento.me/quanblue) &nbsp;&middot;&nbsp;
> GitHub [@QuanBlue](https://github.com/QuanBlue) &nbsp;&middot;&nbsp; Gmail quannguyenthanh558@gmail.com
