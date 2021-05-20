---
layout: default
title: Git + GitHub
parent: Technical Documentation
nav_order: 1
---

#### Contents
1. [Overview](#overview)
2. [Opening a Shell](#opening-a-shell)
3. [Installing Git](#installing-git)
4. [Setting Up SSH Keys](#setting-up-ssh-keys)
5. [Basic Commands](#basic-commands)
6. [Markdown](#markdown)
7. [SCM Best Practices](#scm-best-practices)
8. [Additional Resources](#additional-resources)

## Overview

[Git](https://en.wikipedia.org/wiki/Git) is an [open source](https://opensource.com/resources/what-open-source) version control system. A version control system is a piece of software that allows you to track changes in text files over the development lifetime. [GitHub](https://en.wikipedia.org/wiki/GitHub) is an online platform that allows people to host Git repositories (that is, version controlled projects) online so that other team members and community members have easy access to those repositories. GitHub also offers several additional services like issue tracking, actions, and project boards which we use to manage lab projects. Since the lab is dedicated to [open science](https://opensource.com/resources/open-science) and all projects are open source, GitHub provides these services for free.

Git is used as the main way to version control projects within our lab. Projects have [branches](https://www.hostinger.com/tutorials/how-to-use-git-branches/), which are similar to sandboxes where a contributor to a project can safely make changes before requesting that their changes be reviewed by a colleague and ultimately added to the main project. Git also provides utilities to display the changes that have been made to a specific branch, show how files have been edited, and output a log of all changes. All changes are tagged with the author and time to help contributors understand how and when a feature (beneficial change) or a fix (change that corrects a problem) was added.

GitHub is where we will store these repositories. There are several alternatives that provide similar features or features that GitHub does not have. The reason that we picked GitHub over its alternatives (like [GitLab](https://about.gitlab.com/) or [BitBucket](https://bitbucket.org/)) was due to GitHub's particular feature set, industry and community usage, and available resources, primarily: usage of Git, issues workflow, and first- and third-party project management utilities.

## Opening a Shell

Read the guide [here](https://ndclab.github.io/wiki/docs/technical-docs/shell.html).

This Git tutorial focuses on using the [command-line
interface](https://en.wikipedia.org/wiki/Command-line_interface) (CLI) tool. We will not be covering any [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface) clients because these clients can differ in looks and navigation across operating systems and may be frequently updated whereas the CLI tool has the same interface across operating systems and rarely changes in appearance. (Plus, it's very handy to know how to use the command line!)

## Installing Git

**Mac**

1. Open Terminal.
2. Install Homebrew by following the [instructions on the Homebrew homepage](https://brew.sh/) to paste a specific command into your Terminal.
3. Still inside your Terminal, type: `$ brew install git`
4. If you encounter issues, check out the [main download page](https://git-scm.com/download/mac), direct from Git.

**Windows**

1. Determine whether your computer is 32-bit or 64-bit. This information is available in your system settings under "About." If you don't know where to find this, do some quick googling.
2. [Download](https://git-scm.com/download/win) the "thumbdrive edition" for your computer's system type.
3. Install as you would any other application.

**Linux**

Use the package manager that comes with your distribution and install `git`. See specific instructions [here](https://git-scm.com/download/linux).

--------QUESTION (asked wiki #36, 5/12)
## Setting Up SSH Keys

SSH keys are a form of authentication like username and passwords that simplify the process of working with git repositories.

If you have SSH keys already, please make sure to check the names beforehand to avoid overriding them.

To create an SSH key pair (a private key and a public key), you will need to complete the following steps:

1. Open up a shell.
2. Copy and paste the following commands:

```sh
# The "comment" should either be an email "username@email.com" or user@hostname "username@mycomputer"
ssh-keygen -t ed25519 -C "comment"
```

Note on the key type: the current (as of 2020) recommendation is ED25519 over RSA.

3. At this point, you will be prompted for two things:
  - Where to save the private/public key (the default location is displayed)
  - A passphrase for the key (the passphrase can be excluded but it is recommended that you use one for improved security)

Further resources: the [GitHub guide to SSH keys](https://docs.github.com/en/github-ae@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).
--------QUESTION

## Basic Commands

Git has several common commands that will be necessary to properly work with the the lab's repositories. These are `status`, `add`, `commit`, `push`, `pull`, and `checkout`.

### `status`

This command is your best friend. It will list files and their state within git. Use it often!

Files can either be ignored, untracked, unstaged, or staged. *Ignored* means that the file satisfies a rule in the `.gitignore` file and Git pretends it isn't there.  *Untracked* refers to files that Git is not ignoring but have never been committed; this is normal for newly created files. *Unstaged* files are tracked files that currently have changes but haven't been placed in the staging area for the next commit. *Staged* files are ready for the next commit.

Example:

```sh
git status
```

### `add`

This command will add any file (tracked or untracked) to the staging area for the next commit.

Example:

```sh
git add some_file.txt
```

### `clone`

This command creates a clone of the remote repository on your local machine so that you can make changes (which you will ultimately upload back to the remote repository to share with collaborators).

Example:

```sh
# in local folder into which you want the copy the GitHub contents
git clone <link to remote repository to be cloned>
# new folder is added to your local folder
```

### `checkout`

This command changes the contents of the local repository to match the branch that you "checkout". It will leave changed files untouched so that you can commit them to the branch you are checking out. This is useful when you accidentally made changes to "branch\_b" thinking you were on "branch\_a".

Example:

```sh
# on branch_b
git checkout branch_a
# on branch_a
# changes were brought over
```


### `commit`

This command will commit your changes to the repository. There are two important options for commit `-m` (required) and `-a` (optional).
* `-m` is for adding the commit message, which you should always do
* `-a` means that git will automatically add any tracked files to the staging are and include in your commit (even if you forgot to add them to the staging area yourself). If you don't always check `git status` before you commit, you may want to use `-a` to ensure you don't leave changes behind.

Example:

```sh
# Staged files: s.txt
# Unstaged files: u.txt
# Untracked and unstaged files: uu.txt

# first example
git commit -m "Update s file"
# Commits only changes for s.txt

# Reset
# Second example
git commit -am "Update s and u file"
# Adds u.txt to staging area
# Commits changes for s.txt and u.txt
```

### `push`

This command will push all committed changes from your local computer to the remote repository.

Example:

```sh
# Your working branch is feature-joe
git push origin feature-joe
# Changes are uploaded from your local to the remote
```

### `pull`

This command will "pull" changes from the remote repository to your local. Pull will try to fetch any new changes and merge them. Generally, as long as you have not diverged from the remote repository this will work fine.

Example:

```sh
# Local repository is behind remote repository but has not diverged
git pull
# Git will download new changes and merge them automatically
```

## Markdown

GitHub supports [markdown](https://en.wikipedia.org/wiki/Markdown), which allows you format text in text-based .md files so that GitHub renders them beautifully online. The [Get with Git training](https://ndclab.github.io/wiki/docs/Onboarding/get-with-git.html) includes a module on markdown. Here are some other helpful guides:
[GitHub Guide to Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
[GitHub Markdown Cheatsheet](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## SCM Best Practices

When working with Git and GitHub for the lab, remember these best practices for source code management (SCM):

#### Commit often.
Don’t make too many changes without commits, since it can be destructive if one change within the commit is bad. Commit often and leave a detailed comment about what part of the code was changed.

#### Check your version.
Make sure you are working on the latest version. Use the latest version to avoid accidentally changing an old version and causing confusion.

#### Be obsessive about note-taking.
Make detailed notes/comments about everything you do. This should be 2-3 sentences that thoroughly describe the changes made (what was changed, why it was changed, etc.).
>Example:
>Added indentation on Line 13 for readability.
>Corrected error, changed dog.jpg to dog.jpg on Line 27. 

#### Review changes before committing.
Be 100% sure you want to commit the changes made before doing so!

#### Use branches.
Work independently but communicate what you are working on by creating a new branch and naming it according to the lab's nomenclature.

#### Agree on a team workflow.
Decide with your team who is editing code, what they are editing, and why they are editing. Communicate frequently to stay on track.

## Additional Resources
There are hundreds of Git resources available online. If you get stuck, do some targeted Googling. If you still can't find what you're looking for, ask your labmates in #tech.
