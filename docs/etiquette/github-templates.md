---
layout: default
title: GitHub Templates
parent: Etiquette
nav_order: 4
---

### Contents

1. [Overview](#overview)
2. [Setting Up a New Project](#setting-up-a-new-project)
    1. [GitHub](#github)
    2. [ZenHub](#zenhub)
    3. [Slack](#slack)
    4. [HPC](#hpc)
    5. [Google Drive](#google-drive)
    6. [Off to the Races](#off-to-the-races)

## Overview

All new projects require the creation of a new Github repository by the lab manager or lab technician. New project repositories are typically initiated using one of the two template repositories available in GitHub (template-tool or template-research). Approval from the lab director is required prior to opening a new project repository. Each lab project requires time and resources, so the balance across the lab must be carefully maintained to ensure that each project is a success.

## Setting Up a New Project

### GitHub

#### Start with [brainBox](https://github.com/NDCLab/brainBox).

This is where all great ideas get incubated. If you believe that the brainBox process is not appropriate for your idea, talk to the lab manager or PI.

#### Create a new repo.

When you get the green-light from the lab director, ask the lab manager to create a new repo using the appropriate template repository:

* research projects: https://github.com/NDCLab/template-tool
* tool development: https://github.com/NDCLab/template-research

Be sure to tell the lab manager:
* the appropriate name for your new repository (which meets the requirements for [project naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html))
* a pithy description of the project that will appear on the main lab GitHub page
* who will be leading the project and who will be part of the initial project team (so that everyone gets the correct access level on the new repository)

#### Prepare your new repo for use.

Before you begin using your new repository, there are several settings that need to be implemented:

##### 1. Create `dev` branch.
Create a new branch named `dev` off the basis of the `main` branch. This is identical to how you created your own branch for updating the wiki who's-who page with your own information when you were [onboarded to GitHub](https://ndclab.github.io/wiki/docs/Onboarding/get-with-git.html).

##### 2. Add branch protection rules to `main` and `dev` branches.

Inside your repository on GitHub, click the 'Settings' button and select 'Branches' from the left-hand menu. You will need to "Add rule" twice, once for `dev` and once for `main`. In both cases, select "Require pull request reviews before merging" and set the number of required approving reviews at "1." Once complete, your branch protection rules should look like this:

![gh_branch-protection](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/gh_branch-protection.png)

These branch protection rules ensure that content must undergo a review before any branch is merged into `dev` or `main`.

##### 3. Automatically delete head branches

You will want to [check this option in your repository settings](https://docs.github.com/en/github/administering-a-repository/configuring-pull-request-merges/managing-the-automatic-deletion-of-branches) so that, when you review and merge the work of team members into `dev`, GitHub automatically deletes the branch they were working on (which has now been merged). This keeps your branch tree tidy. Don't worry: the branch protection rules you set up above prevent `dev` from being automatically deleted when it gets merged to `main`.

#### Draft the `readme` file.

Within the `dev` branch, draft the `readme.md` file that guides the development of your project.

Every repository should have a succinct `readme.md` file that serves as a roadmap for the project. This is the first thing you will commit to your new repository. The readme should include:

* a description of the project goal
* a roadmap for all the planned project releases
* major contributors to the project

The template repository used to create your new project repo contains a template `readme.md` file that will guide you through the initial process of drafting the readme.

As the project progresses, the readme must be updated to include information for any content included on the `main` branch, such as pre-registrations, conference posters, or working software releases.

#### Draft the `contributing` file.

Within the `dev` branch, draft the `contributing.md` file that informs visitors of how to contribute. The template repository used to create your new project repo contains a template `contributing.md` file that will guide you through the initial process of drafting.

At this initial setup stage, the `main` branch will be empty (except for the files that came with the default template, such as the license). The `dev` branch, however, will now contain your `readme.md` and `contributing.md` files.

#### Request the launch review.

Once you are satisfied with the `readme` and `contributing` files, initiate a pull request. Tag both the lab director and the lab manager.
* The lab director will perform a [level 2 review](https://ndclab.github.io/wiki/docs/etiquette/github-etiquette.html#terminology) (or delegate such a review to another appropriate lab member) to approve your planned roadmap and merge `readme.md` and `contributing.md` to `main`.
* The lab manager will confirm that your repository is set up with all the correct settings to ensure a smooth project launch.

### ZenHub

While you wait for approval of your planned roadmap, you can set up ZenHub.

1. Click the ZenHub tab within your new repository. This automatically opens a page so that you can set up a new ZenHub workspace. Input your project name as the workspace name and the short descriptor. ZenHub automatically connects to the GitHub repository where you started. Click "Create Workspace."

![zh_new-workspace](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/zh_new-workspace.png)

2. Unfortunately, ZenHub does not automatically use the NDCLab's default pipelines when creating a new workspace, so you will need to customize your new workspace immediately. Adjust pipeline names and descriptors to match the table [here](https://ndclab.github.io/wiki/docs/technical-docs/zenhub.md#tour-of-the-pipelines). You can change the names and descriptors by clicking the three vertical dots at the top of each pipeline. This same menu lets you delete any unnecessary pipelines. Additional pipelines can be added at the far right of the screen, then dragged-and-dropped into the appropriate position.

3. Create a [ZenHub Epic](https://ndclab.github.io/wiki/docs/technical-docs/zenhub.md#defining-epics) for each planned project release, as outlined in your readme roadmap.

4. Plan project issues (which may be large and abstract at this stage) and assign them to the appropriate Epic.

5. Organize the Project Backlog pipeline in ZenHub by putting the earliest Epic at the top, followed by its associated issues in priority order. This is followed by the next earliest Epic with its issues, and so on.

6. Launch the first Epic by moving the "Epic" issue and its associated issues to the *Release Backlog* in ZenHub.

### Slack
When you request the new repo from the lab manager, a new Slack channel will be created. Appropriate permissions will be granted to the project lead(s) and other project team members.

### HPC
When you request the new repo from the lab manager, a project-specific folder(s) will also be created on the HPC using the standard NDCLab filing structure. Appropriate permissions will be granted to the project lead(s) and other project team members.

### Google Drive
When you request the new repo from the lab manager, a project-specific folder(s) will also be created on the Google Drive. Appropriate permissions will be granted to the project lead(s) and other project team members.

### Off to the Races

Once the lab director has approved your planned roadmap and merged it into `main`, you have set up the project's ZenHub workspace, and your project has been added to the HPC, Google Drive, and Slack, you are ready to launch. Set up your [sprints inside ZenHub](https://ndclab.github.io/wiki/docs/technical-docs/zenhub.md#planning-sprints) and plan your first sprint meeting with your team! 

