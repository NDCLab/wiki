---
layout: default
title: Contributing
nav_order: 6
---

# Contributing

## Overview

Contributing to a project can be divided into two categories. Contributing with push access and
without push access. Since lab projects are open source anyone can view the source code but not
everyone can push changes to the repository.

In both situations a new branch will be created and submitted as a pull requests. After which a
second person will review the pull request to make sure it adheres to the Lab standards and to check
for correctness.

## Workflow for those with Push Access

If you have push access to a project repository that means you can push changes to the repository
but you should not push changes into the main or development branch without having those changes
reviewed. To do this we will use branches and pull requests.

Following these steps:

- Clone the repository
- Create a new branch following the labs naming conventions
- Commit changes to that branch
- Push the new branch to the repository
- Create a new pull request and assign someone to review the pull request
  - In most cases this will be someone else in the same team or another lab member
- Push revisions if necessary

> Note: You do not need to create a new pull request and start the review process again to submit
> revisions. Simply pushing to the same branch being reviewed will append changes to the discussion.

- Once approved either the reviewer or the one who created the submission will close the pull
	request
  - To close an issue, a comment must be provided stating why the pull request was completed

## Workflow for those without Push Access

If you do not have push access to a project that means you will have to fork the repository first
before submitting changes for review. To do this we will use forks, branches, and pull requests.

Following these steps to submit changes:

- Fork the repository on GitHub (this will require having an account)
  - [Signing up for Github](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/signing-up-for-a-new-github-account)
- Clone the repository in your account
- Follow the same steps as described above starting from "Creating a new branch..."

## Naming Convention for Branches

Branches will follow a naming convention so that everyone in the lab, and those contributing to lab
projects can more easily understand how projects are being developed. Also to stay organized, for
example knowing that although main may have the most current changes the `dev` branch is the one to
pay attention to if you would like to contribute since that branch is the one with all the active
pull requests.

Branches:

- main: We will use main as the branch to generate release instances. Will gaurantee within what is
	reasonable that the code has been tested and works well.
- dev: The development branch will be used to merge features and fixes, and will be eventually
	merged into main. Does not garauntee that the code will always be functional
- feature: Branches created with a `feature-` prefix will be new functionality that will be added to
	the project. It will also require maintanence to keep the feature working correctly in the future.
- fix: Branches created with a `fix-` prefix will add changes that fix a issue with the project.
	Fixes should not add new functionality.

There will only be one `main` and `dev` branch. There can be many `feature` and `fix` branches. As
mentioned, `feature` and `fix` branches will have the prefix of the category name followed by a
descriptive name; `<category>-<name>` or `feature-add-lights`.

## Edge Case: Working on a Feature that Depends on Another Feature

If you are working on a feature or fix that depends on something that is still in the process of
being reviewed the approach we will use is
[rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing).

Rebasing is similar to merging in that it merges changes from the initial point that was used to
make a branch.

To do this, do the following:

> Note: feature-b is dependent to feature-a

- If not already on feature-b, `git checkout feature-b`
- Then rebase changes, `git rebase feature-a`
- Then just follow the steps as mentioned above

This method can be used on any branch that is dependent on any other branch but tends to be more
useful branches that have not been merge into main or dev. And can be useful if either the main or
dev branch are moving quickly while developing the feature or fix.
