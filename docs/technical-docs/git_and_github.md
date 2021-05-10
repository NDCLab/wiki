---
layout: default
title: Git + GitHub
parent: Technical Documentation
nav_order: 1
---

# Overview

[Git](https://en.wikipedia.org/wiki/Git) is an [open
source](https://opensource.com/resources/what-open-source) version control system. A Version Control
System is a piece of software that allows you to track changes in text files over the development
lifetime. [GitHub](https://en.wikipedia.org/wiki/GitHub) is an online service that allows people to
host Git repositories (version controlled projects) online so that other team members and community
members have easy access to those repositories. GitHub also offers several additional services like
issue tracking, actions, and project boards which we will be using to manage lab projects. Since the
lab is dedicated to [open science](https://opensource.com/resources/open-science) and all projects
will be open source, GitHub provides these services for free.

Git will be used as the main way to version control projects. Projects will have
[branches](https://www.hostinger.com/tutorials/how-to-use-git-branches/) which are similar to
sandboxes where a contributor to a project can make changes and ultimately upload those changes
requesting them to be added to the main project. Git also provides utilities to display the changes
that have been made to a specific branch, show files have been edited, output a log of all changes.
Additionally all changes are tagged with the author and time to help contributors understand how and
when feature (beneficial change) or fix (change that fixes part of the project) was added.

GitHub is where we will store these repositories. There are several services like GitHub that
provide similar features or features that GitHub does not have. The reason that GitHub was picked
over other services like [GitLab](https://about.gitlab.com/) or [BitBucket](https://bitbucket.org/)
was due to GitHub's its feature set, industry and community usage, and available resources.
Primarily GitHub's usage of Git, its Issue workflow, and its first- and third-party project
management utilities.

## Table of Contents
{: .no_toc .text-delta}

1. TOC
{:toc}

## Prerequisites

[Using a terminal](#)

# Installing

We will be installing the `git` [command-line
interface](https://en.wikipedia.org/wiki/Command-line_interface) (CLI) tool. The reason we will not
be covering the git [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface) clients is because
they can differ in looks and navigation across operating systems. The cli tool has the same
interface across operating systems. The interface for the cli tool rarely changes unlike the GUI
client which could change in looks from one version to another making images used in the
documentation outdated or incorrect.

In the following sections are the main ways to install `git`. These are not all the ways but are the
recommended ways based on the operating system.

## Windows

- [Download](https://git-scm.com/download/win)
- Recommended method: portable version or "thumbdrive edition"
  - [64bit version](https://github.com/git-for-windows/git/releases/download/v2.29.2.windows.2/PortableGit-2.29.2.2-64-bit.7z.exe)

## Mac

- [Download](https://git-scm.com/download/mac)
- Recommended methods for install: Binary or [Homebrew](https://brew.sh/)
  - Download [dmg](https://sourceforge.net/projects/git-osx-installer/files/latest/download) file
  - `brew install git`

[How to](https://www.ofzenandcomputing.com/how-to-install-dmg-files-mac/) install a binary file on
Mac OS.

## Linux

Use the package manager that comes with your distribution and install `git`. For example on
Debian/Ubuntu based distributions do `apt-get install git`.

# Basic Usage

Basic usage will cover how to work with the `git` CLI tool. This section assumes you are inside a
[terminal](https://www.computerhope.com/jargon/t/terminal.htm) that is running
[Bash](https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29). Although Bash is the
[shell](https://en.wikipedia.org/wiki/Shell_(computing)) we will be using, it does not mean that is
the shell that you need to use if you are more comfortable with a different shell. Mac OS
(depending on the version) will be using [Zsh](https://www.zsh.org/) which is very similar to Bash
and most of the information is interchangeable.

> For a more detailed description please reference [Git Usage](#).

The general process for working with a repository is to instantiate or download one. Then create a
new branch with a name similar to `feature-x` or `fix-y` depending on the intended change. Add those
changes to the staging area, and commit them with a message that describes those changes in the
present tense. And lastly push (upload) those changes to a remote branch.

> Any value inside `<` `>` needs to be replaced with a correct value. For example if `<link>` is
> specified, then it needs to be replaced with [URL](#) link like
> `https://github.com/NDCLab/wiki.git` making sure to omit the `<` and `>`.

Common commands:

- `git init`, will instantiate a new repository in the current folder/directory.
- `git clone <link>`, will download a remote repository specified in the link provided. In most cases
	this will be the link that GitHub offers under the green "Code" button.
- `git add <file>`, will add to git's staging area which is can be committed to the VCS later.
- `git commit -m "<commit message>"`, will commit any changes in the staging area with the specified
	`<commit message>`.
- `git branch -m <branch-name>`, will change the name of the current branch to `<branch-name>`.
- `git checkout <branch-name>`, will change to an existing branch. It will bring over unstaged
	changes which can be committed in `<branch-name>`.
- `git checkout -b <branch-name>`, will create a new branch with the name specified and switch over
	to it.
- `git branch`, will list all available branches.
- `git pull`, will attempt to download any new changes in the remote branch to the local branch.
- `git push`, will attempt to upload any new changes from the local branch to the remote branch.

# Workflows

The method that contributors to projects will use to interact with lab projects. Having these
methods standardized helps improve the projects correctness and reproducibility.

## Git in General

As mentioned earlier the main method we will use to interact with local or remote repositories will
be via Git's command line interface. This way the documentation can be more platform and client
independent.

The first thing in any project is creating a repository, whether that is on the GitHub organization
page, on a personal account, or locally. Although it may seem that creating a project is something
that is rarely done. Git repositories are very lightweight, in other words consume very little space
in a computer's storage and zero [CPU](https://en.wikipedia.org/wiki/Central_processing_unit)
resources when not in active use. They can be useful for prototyping ideas before trying them on a
full fledged project. 

To create a new repository on GitHub for a user account or organization, do the following:

- Make sure you are logged in.
- Press the "+", and a drop down will come up.
- Select "New repository".
- Fill out the form.
  - Select the "Owner", this can be a user or an organization.
	- Write a name in the Repository name.
	- Write a short description what the repository is in the "Description" field.
	- Select "Public". \*
- Ignore the other options.
- Press "Create repository" to create the new repository.

> \* Public means it will be available for others to view who are not part of the organization. This
> is to make the project open and keep with the Lab's spirit of open science.

To create a new repository locally on a computer, do the following:

- Open up a terminal with Bash, or Zsh (Mac OS)
- Change to the correct directory/folder where the repository will be stored

`cd <path/to/folder>`

- Initialize the repository

`git init <name-of-repo>`

After the repository has been created, it can start to be used and modified. For repositories that
will use the project template, do the following:

- Make sure to have a copy of the [project template](https://github.com/NDCLab/project-template) in
	a different directory.
- Using a [File manager](https://en.wikipedia.org/wiki/File_manager) copy and paste all the files in
	the project template folder into the new repository.
- Once all the files have been copied, follow the template project [instructions]() for how to
	initialize a new project.
- Once the new project is initialized, add all the new files to the staging area

`git add -A`

- Then commit all the changes in the staging area making sure to provide a useful commit message,
	for example "Initialize new project from project template".

`git commit -m "<commit message>"`

For the more common case where the repository already exists we will want to clone the repository to
the local computer from GitHub. Cloning refers to how git will copy the remote files on GitHub to
the local computer. Although downloading may be more clear in this case, Git can clone from many
different local and remote locations and in those situations it would not make sense to refer to it
as downloading. This To do this, do the following:

For the more common case where a repository for a project already exists, we will want to clone
the repository to the local computer from GitHub.

- Get the [URL](https://en.wikipedia.org/wiki/URL)\* from GitHub.
  - Go to the project repository
	- Select the drop down from the "Code" button
	- Copy the preferred URL link
- Inside a terminal running Bash or Zsh, clone the repository

`git clone <url_link>`

- Change the directory to the local repository

`cd <directory_name>`

With an local repository changes can be made. The lab uses the branching workflow which means we use
topic branches which are discussed in more detail in the [Contributing](#contributing) section. Once
the changes are made they can be added to the staging area and the committed to the feature branch.

The Git Branching Workflow, is useful because it organizes changes into clear and concise groups
that can be tested and reviewed by others without significant overhead. It also groups the changes
into readable chunks in the git history. The Git history being a log of all the commits that have
been made with comments describing those changes. This highlights the importance of clear and
descriptive commit messages, especially when reviewing information that is several months or years
old.

To create branches and make commits do the following:

- Check the status of the repository
  - First see which branch the repository is on

	`git branch`, this will show a list of all branches with the active branch having a \* next to its
	name
  
	- Second check to see if there are any files that are not committed

	`git status`

- Make changes to the necessary files
- Check the status of files

`git status`

- Add files to the staging area

`git add -A` or `git add *`\*\* are applicable

- Once all the files have been added to the staging area, commit the changes. Make sure to use
	present tense, and be descriptive.

`git commit -m <message>`

With committed changes, now it possible to push those commits to the remote repository. This will
mean pushing changes to either the lab repository or a personal repository depending on the level of
access. To do this, do the following:

`git push origin <branch_name>`

At this point review the [Contributing](#contributing) and [Issues](#issues) section for more
information.

> \* The two types of links that are provided by GitHub are
> [HTTPS](https://en.wikipedia.org/wiki/HTTPS) URLs which are the same as websites and sometimes
> will as for a username and password for authentication when cloning. The other type of link that
> GitHub offers is [SSH](https://en.wikipedia.org/wiki/SSH_(Secure_Shell)) which when correctly
> setup offers better ease of use. This is covered in more detailed in [replace-me](#).

> \*\* The \* star in Bash acts as a special character directing the Bash shell to replace it with
> all the current files that are accessible. Accessibility can mean different things in a shell, but
> generally it means all the files in the current working directory.

## Contributing

Contributing in this case refers to how contributors will submit contributions to a lab project that
is hosted on GitHub. In an effort to make projects reproducible and correct submissions need to be
reviewed so that they can be checked and tested with a mixture of automated tools and visual review.

Contributions will come from two groups of individuals with different levels of push access. Push
access being the ability write or edit to repositories. All projects will be open source so there is
no differentiation for pull access or having the ability to read a repository.

For contributors with push access, they will submit contributions in the form of topic branches that
is reviewed and then merged into one of the main branches of the repository for a specific project.
That will involve:

- Cloning a repository, which will download a copy of the project repository from GitHub to the
	local machine.
- Creating a topic branch, for example "feature-a".
- Adding and committing changes to that branch.
- Pushing the local branch to the remote project repository.
- Creating a pull request and adding it to the issue it is meant to resolve.
- Pushing any new changes to requested during the review process.
- Closing the issue with a comment stating why the issue is being closed.

For contributors without push access, they will have a similar process. They will first fork the
repository which means making a copy of the repository on their own account. Then following the same
steps as above but using the forked copy. When submitting the pull request specifying the forked
repository's topic branch instead. In other words:

- Fork the project repository.
- Follow the steps describe above substituting the project repository with the forked version.

> Note: A topic branch is a branch that is meant to be a branch with a small focus for example one
> feature or one fix. Topic branches will have only a small amount of changes in comparison to the
> main or dev branches which usually hold the entire history of the repository.

## Issues

## Actions

# External Resources

[Access Permissions on
GitHub](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/access-permissions-on-github)
[Git Branching](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows)
