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
    3. [Off to the Races](#off-to-the-races)

## Overview

There are two template repositories available in GitHub for the launching of new projects. Before using these templates, ensure that you have approval from the lab director to open a new project. Each lab project requires time and resources, so the balance across the lab must be carefully maintained to ensure that each project is a success.

## Setting Up a New Project

### GitHub

1. Start with [brainBox](https://github.com/NDCLab/brainBox)

This is where all great ideas get incubated. If you believe that the brainBox process is not appropriate for your idea, talk to the lab manager before creating any new repository on GitHub.

2. When you get the green-light from the PI, create a new repo using the appropriate template repository:

**research projects:** https://github.com/NDCLab/template-tool
**tool development:** https://github.com/NDCLab/template-research

Be sure to name your new repository in accordance with the [project naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html).

_______________________FARUKH ADD INSTRUCTIONS
To use a template repository, simply select

Update settings to delete head branches
_______________________FARUKH ADD INSTRUCTIONS

6. Within the `main` branch, draft the readme file that guides the development of your project.

Every repository should have a succinct `readme.md` file that serves as a roadmap for the project. This is the first thing you will commit to your new repository. The readme should include:

* a description of the project goal
* a roadmap for all the planned project releases
* major contributors to the project

The template repository that you have used contains a template readme.md file that will guide you through the initial process of drafting the readme.

As the project progresses, the readme will be updated to include information for any content included on the `main` branch, such as pre-registrations, conference posters, or working software releases

7. Within the `main` branch, draft the contributing.md file that informs visitors of how to contribute. The template repository that you have used contains a template contributing.md file that will guide you through the initial process of drafting.

At this initial setup stage, the `main` branch will be empty except for the readme.md and contributing.md files.

_______________________FARUKH ADD INSTRUCTIONS

3. Create sub-branches off main:
    tool: dev
    research: project-specific

4. Add branch protection rules to main, dev, and any other branches that must require a review before content is merged

_______________________FARUKH ADD INSTRUCTIONS

### ZenHub

While you wait for approval of your planned roadmap, you can set up ZenHub.

1. Click the ZenHub tab within your new repository. This automatically opens a page so you can set up a new ZenHub workspace. Input your project name as the workspace name and a short descriptor. ZenHub automatically connects to the GitHub repository where you started. Click "Create Workspace."

![zh_new-workspace](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/zh_new-workspace.png)

2. Unfortunately, ZenHub does not automatically use the NDCLab's default pipelines when creating a new workspace, so you will need to customize your new workspace immediately. Adjust pipeline names and descriptors to match the table [here](https://ndclab.github.io/wiki/docs/technical-docs/zenhub.md#tour-of-the-pipelines). You can change the names and descriptors by clicking the three vertical dots at the top of each pipeline. This same menu lets you delete any unnecessary pipelines. Additional pipelines can be added at the far right of the screen, then dragged-and-dropped into the appropriate position.

3. Create a [ZenHub Epic](https://ndclab.github.io/wiki/docs/technical-docs/zenhub.md#defining-epics) for each planned project release, as outlined in your readme roadmap.

4. Plan all project issues (which may be large and abstract at this stage) and assign them to the appropriate Epic.

5. Organize the Project Backlog pipeline in ZenHub by putting the earliest Epic at the top, followed by its associated issues in priority order. This is followed by the next earliest Epic with its issues, and so on.

6. Launch the first Epic by moving the "Epic" issue and its associated issues to the Release Backlog in ZenHub.

### Off to the Races

Once the lab director has approved your planned roadmap and merged it into `dev`, and you have set up the project in ZenHub, initiate a pull request, tagging the lab technician (for tool projects) or the lab manager (for research projects), who will verify that all the technical details of your project are properly set up. Once confirmed, he/she will merge your readme file into the main branch.

Set up your [sprints inside ZenHub](https://ndclab.github.io/wiki/docs/technical-docs/zenhub.md#planning-sprints) and plan your first sprint meeting with your team! 

