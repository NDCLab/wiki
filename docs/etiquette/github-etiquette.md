---
layout: default
title: GitHub Etiquette
parent: Etiquette
nav_order: 3
---

### Contents
1. Overview
2. Tools
3. Terminology
4. Project Lifecycle
5. Opening a New Project
6. Communication

## Overview

Having an agreed-upon set of standards for how team members coordinate and collaborate on work leads to more efficient and more enjoyable workflows that yield better results with less effort. In business and software development, there is a long history of research into best practices for how teams should collaborate and coordinate their work, often collectively referred to as “project management.” There is an upfront cost to learning a new system of working together and coordinating work; however, this initial work pays enormous dividends, ultimately translating into more publications and faster deployment of code that is more widely adopted by the community.

The NDCLab uses a modified [agile methodology](https://en.wikipedia.org/wiki/Agile_software_development) to organize our workflows and maximize our productivity. The core idea is that we break larger projects into smaller, iterative pieces and set ourselves time limitations on completing each of the smaller pieces. You do not need to fully understand the tenets of agile beyond the information provided on this page. If you do decide to do extracurricular reading, please be aware that we have modified some of the typical agile terminology to better meet the needs of an academic research lab.

A key purpose of using this agile methodology, including the tools and processes outlined below, is to reduce the amount of time needed for meetings while keeping all team members apprised of project status. Initiative and self-assignment of tasks is highly encouraged, along with active collaboration to solve problems and share new knowledge.

## Tools

### GitHub
All lab projects live on [GitHub](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html) and make use of native features of the platform, such as issues and pull requests. If you haven't already, [get yourself onboarded](https://ndclab.github.io/wiki/docs/Onboarding/get-with-git.html). 

### ZenHub
ZenHub (link coming soon!) is a plug-in to GitHub. Issues within a GitHub repository connect automatically to the ZenHub Kanban board of associated workspaces. In general, each repository is connected to one workspace, but it is possible to connect multiple repositories in special circumstances where this would be beneficial to project management.

## Terminology

[**Agile**](https://en.wikipedia.org/wiki/Agile_software_development): a philosophy for flexible, iterative, team-centric project management<br/>
[**Scrum**](https://en.wikipedia.org/wiki/Scrum_(software_development)): a framework for deploying an agile system for project management by breaking larger projects down into manageable chunks<br/>
[**Kanban Board**](https://en.wikipedia.org/wiki/Kanban_board): a visual depiction of project progress<br/>
**Project**: a big idea that may comprise multiple research publications or the distribution of cool, open-source software<br/>
[**Epic**](https://help.zenhub.com/support/solutions/articles/43000010341-an-intro-to-zenhub-epics): a large narrative that is smaller than the whole project but bigger than an individual task, for example, a specific poster presentation or the release of v1 of a software tool<br/>
[**Issue**](https://guides.github.com/features/issues/): a feature in GitHub that is a single, well-defined, cohesive task that is accomplished on the road to completing a full-scale project<br/>
[**Sprint**](https://en.wikipedia.org/wiki/Scrum_Sprint): a fixed, short period of time into which tasks are batched and completed

(There are many other terms used in agile project management. We are focusing here on those that best describe the process used here in the lab.)

## Project Lifecycle

Within the NDCLab, projects are conceptualized and organized across three timescales:
* Project
* Epic/Release
* Sprint

### Project (1-3 years)

Each project has a goal; this goal is what will ultimately be achieved after completing all work and releasing all papers and posters envisaged for the project.  For standard projects that do not require new data collection, this timeline is typically 1-2 years. For standard projects that require the lab to collect new data, the timeline is typically 2-3 years.

The project goal should be explicitly stated in the `readme` file on the project's GitHub repository.

Each active project has its own GitHub repository and ZenHub workspace.

### Epic/Release (4-6 months)

Projects are broken down into intermediate chunks, referred to as "releases" or, in ZenHub terminology, "epics." (ZenHub also has something called a "release." Pretend you didn't see that. Remember what we said above about modifying terminology? :wink:) Within the timeframe of an epic, some significant change or improvement should be accomplished. For a research project, this might be the publication of a poster. For a new tool, this might be an upgrade that includes a new feature.

Almost all projects will involve more than one release. This is to provide psychological milestones, as well as to yield somewhat self-contained products that can be deployed, presented, published, or otherwise shared with the world. The work completed during each release is integrally tied to the releases that precede it and the releases that come after; in this way, each release helps to achieve the larger project goal. However, each release should also reflect a conceptual advance upon the prior release, and reflect a change that is significant enough to:
* warrant a novel conference submission (in the case of a research project) or
* encourage users to download the new release (in the case of tool development).

All release goals for a project should be explicitly stated in the `readme` file on the project's GitHub repository. Each planned release should be established as a time-blocked "epic" within ZenHub.

------------------QUESTION
Should project/release goals be on the MAIN readme even before anything else is posted to MAIN?
------------------QUESTION

------------------QUESTION
What parameters should be in place for PR review and merge with main?
------------------QUESTION

A release is considered complete when the improvement (be that a new version of a tool or a publication of some type) is pushed to the `main` branch of the project repository on GitHub.

### Issues (1-3 weeks)

On a day-to-day basis, these big-picture projects and their iterative releases are broken down into bite-sized chunks called "issues." Issues are the primary unit of work and can be broken down into a series of sub-tasks.

Issues are created as GitHub issues within the project’s GitHub repository. Sub-tasks, if helpful or required, can be listed as a simple list within the issue description.

At the start of any new project, an effort is made to identify and define all the issues that need to be completed to achieve all project goals and complete all releases. The issues that comprise the first release are placed in the Release Backlog pipeline on ZenHub and assigned to the associated Epic. All other issues are placed in the Project Backlog pipeline on ZenHub.

Issues inside the Project Backlog can be relatively large and abstract (e.g., listing a release goal inside the project backlog is appropriate). However, these issues must be refined and/or broken down further prior to moving them into the Release Backlog. Completing all the work inside the Release Backlog will achieve the release goal.

### Sprints

A sprint is a collection of issues that the team for a given project has decided to work on within a specified 1-3 week period. Each issue should not take longer than one sprint to complete (ideally much less than that, and multiple issues will be completed during each sprint). 

A sprint meeting occurs at the beginning of each sprint and involves reviewing work from the prior sprint, reflecting on what did/did not work, and planning what issues will be completed during the upcoming sprint.

Before being assigned to the sprint backlog, issues must:

* be fully defined (specifically, what does "Done" look like?)
* have completion time estimated (don't get bogged down in precision, just provide a reasonable estimate of task complexity and effort required)
* have all subtasks defined (only if subtasks are applicable)

#### Before the Sprint Meeting

* All work for the current sprint should be completed >1 day before the next sprint meeting (**not** within four hours of the next meeting).
* Team members should review items in the Release Backlog and add "Add to sprint?" labels to promote discussion. Only well-defined issues are added to a sprint, so issues being proposed at the next sprint meeting should be updated with adequate definitions if those are lacking.
* An "upcoming sprint" issue is created, which remains in the New pipeline on ZenHub. All team members add their comments (>1 day prior to the meeting) to this issue to promote discussion, including:
    * what we tried and worked really well
    * what we tried and really didn't work
    * what we didn't give a fair try to
    * work that will not be completed in time
    * outstanding roadblocks
    * unexpected developments

#### During the Sprint Meeting

The sprint meeting is broken down into three parts:

1. Retrospective (<15 min: reflect on processes that did or did not work

The retrospective is an opportunity to share tips and tricks so that all members of the team can learn from the experience of others.

2. Sprint Review (15 min: review what remains incomplete)

There is no need to discuss completed work as this information is easily viewable to all team members on the ZenHub project workspace.

3. Planning (60 min: plan work for the next sprint)

The Sprint Backlog in ZenHub is stocked with the issues that will be accomplished during the sprint. By the end of the meeting, all issues should have a time estimate and 75% of the issues should be assigned to specific team members (the remaining 25% can be handled by self-assignment during the sprint). All high-priority items must be assigned; lower-priority items can be self-assigned during the sprint.

As part of this planning process, the time estimates should be added together to ensure that a reasonable amount of work has been tagged for the sprint.

Once issues are added to the Sprint Backlog, remove the "Add to sprint?" label to remove unnecessary visual noise on ZenHub during the sprint.

#### After the Sprint Meeting

Team members tackle the issues to which they have been assigned, moving the issues into the In Progress pipeline on ZenHub. Ad hoc meetings, impromptu discussions, and the labeling of issues with "Help Wanted" labels are all highly encouraged to ensure team members don't get caught up in roadblocks that slows progress. It is normal to hit roadblocks and it is therefore important to communicate these openly so that more minds can be involved in finding an elegant solution.

When an individual completes an issue, they move it into the Review/QA pipeline on ZenHub and a review is requested. Once all of an individual's tasks for the sprint are completed, they are expected to check out the ZenHub workspace and:
* self-assign any unassigned tasks in the current sprint
* reach out to any teammates who have posted a "Help Wanted" label

Following review and approval, issues are closed. This automatically moves them to the Closed pipeline on ZenHub.

------------------QUESTION
What parameters do we want to specify for pull requests to merge with dev?
------------------QUESTION

### Presentation and Feedback

For each release, plan on putting together a work-in-progress presentation, to be given at a lab meeting or similar event, in order to organize thinking regarding the status of the release and larger project. This is also a chance to receive feedback on the release/project.

Typically, this presentation will occur in the second half of the release, and most often, near the end (or just after completion) of a release. 

Pending the venue, project status, and other particulars, this may be a very informal presentation with minimal slides, or a formal presentation.


## Opening a New Project

1. Start with [brainBox](https://github.com/NDCLab/brainBox)
This is where all great ideas get incubated. After your idea completes the brainBox journey, you will get the green-light from the PI to launch your project. If you believe that the brainBox process is not appropriate for your idea, talk to the lab manager before creating any new repository on GitHub.

2. Create a new repo
------------------ADD LINKS
Use template-tool or template-project
------------------ADD LINKS

------------------QUESTION
At the start of any new project, after the project lead forks the appropriate [project template](https://ndclab.github.io/wiki/docs/etiquette/github-templates.html)
------------------QUESTION

3. Create ZenHub workspace.
4. Plan all project releases and create ZenHub Epics.
5. Plan all project issues (which may be large and abstract at this stage), assigning to the appropriate Epic.
6. Launch the first Epic by moving the "Epic" issue and all associated issues to the Release Backlog in ZenHub.
7. Plan your first sprint meeting with your team!

## Communication

respond to your notifications when someone @mentions you or asks you to review a pull request
when assigning someone to an issue, include an explanatory comment (with @mention) to explain why you think the person is a good fit for the task -- don't just randomly assign people issues without dialogue


A sprint meeting occurs at the beginning of each sprint and involves reviewing work from the prior sprint, reflecting on what did/did not work, and planning what issues and subtasks will be completed during the upcoming sprint. 



- Every repository should have a succinct `readme.md` file that guides development and points to relevant data.