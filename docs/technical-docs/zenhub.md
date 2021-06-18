---
layout: default
title: ZenHub
parent: Technical Documentation
nav_order: 2
---

### Contents
1. [Overview](#overview)
2. [Installing](#installing)
3. [Tour of the Pipelines](#tour-of-the-pipelines)
4. [Defining Epics](#defining-epics)
5. [Planning Sprints](#planning-sprints)
6. [Monitoring Progress](#monitoring-progress)
6. [Tips and Tricks](#tips-and-tricks)

## Overview

ZenHub is a plug-in for your browser that connects to GitHub. It offers [Kanban](https://en.wikipedia.org/wiki/Kanban_board)-style boards, called a "workspaces," which the NDCLab uses to visually manage projects.  When an issue is created inside GitHub, it automatically appears on the "New" pipeline on an associated ZenHub workspace. In general, each repository is connected to one workspace, but it is possible to connect multiple repositories in special circumstances where this would be beneficial to project management.

## Installing

1. Before you install ZenHub, [get yourself with git](https://ndclab.github.io/wiki/docs/Onboarding/get-with-git.html). It is important that you are already a member of the NDCLab organization on GitHub before you install the ZenHub extension.
2. Download the ZenHub extension, which is currently available for Chrome and Firefox. You can do this directly from the browser extension store or using the [link available from ZenHub](https://help.zenhub.com/support/solutions/articles/43000507578-installing-the-zenhub-extension-for-cloud).
3. During this process, you will need to authorize ZenHub to see your personal and organization repositories.
4. After installing, you'll probably find yourself within the ZenHub app. Some lab members prefer to operate in this interface, but you will want to hop back over to GitHub to get your bearings first. On the same browser where you installed ZenHub, re-navigate to the NDCLab GitHub page. If you click on any repository, you should now see the "ZenHub" tab within that repository.
___________________________IMAGE 

## Tour of the Pipelines


## Defining Epics

To view existing Epics, click on Roadmap from the left-hand navigation pane. If no epics have been defined, the page will look like this:
___________________________IMAGE 

However, if one or more Epics has previously been established, you will see a [Gantt-style chart](https://en.wikipedia.org/wiki/Gantt_chart), like this:
___________________________IMAGE 
In this example, a single Epic has been defined based on an end date. Epics can be named by date in this way, or they can be named with a descriptive name. In both cases, Epics should be given a beginning and an end date.

You can define multiple Epics at the same time, either back-to-back or overlapping. To create a new Epic:

1. Click the green `+` button and select "New Epic."
2. Input the name (end date or descriptor). 
3. Hover your cursor to the right of the name and click the three vertical dots that appear. Select "Set start and end date" from the dropdown.
4. Input the dates of this Epic and click "Set Timeline."

All planned project releases should be defined as Epics in ZenHub at project launch in order to provide all team members with a visual overview of where the project is going and what progress has already been made in achieving the project goals.

The creation of an Epic also creates a GitHub issue for the Epic. This is really just a visual tile for the ZenHub board. Place the Epic associated with the next release at the top of the Release Backlog pipeline. Place all other Epics into the Project Backlog pipeline. Issues associated with each Epic should nest under the "Epic" tile within each pipeline.

## Planning Sprints

You can set up sprints within ZenHub so that you can easily assign each issue to the current or an upcoming sprints during your sprint planning meetings. To turn on sprints in ZenHub:

1. Click "Create on the left-hand navigation pane.
2. Select "Set up Sprints for your team" from the dropdown.
3. Leave the default selections on the left ("Move unfinished Issues to the next Sprint" should be turned on; "Automatically build new Sprints from the backlog" should be turned off).
4. Select the start and end date of the first sprint. This establishes the pattern that ZenHub will carry forward. For instance, if you select one week for the first sprint, ZenHub will create a weekly cycle. If you select two weeks for the first sprint, ZenHub will create a bi-weekly cycle.
5. Click "Create Sprints."
6. Open each issue that has already been assigned to the current sprint in your planning and formally assign it to the current sprint by selecting the sprint.

## Monitoring Progress

If you and your team are diligent in establishing time estimates for each issue that you create, you will be able to track your overall progress on this roadmap view. ZenHub calls those time estimates "story points," but it is easier to just think of them as rough working hours. Here is an example where one Epic is 47% complete and the Epic that follows is not yet begun:
___________________________IMAGE 

## Tips and Tricks

Issues created in GitHub automatically appear in ZenHub. Issues created in ZenHub automatically appear in GitHub. They are interconnected.
Follow the lab's GitHub etiquette by moving issues into the appropriate pipeline when they are 