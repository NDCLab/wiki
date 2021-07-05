---
layout: default
title: GitHub Etiquette
parent: Etiquette
nav_order: 3
---

### Contents
1. [Overview](#overview)
2. [Tools](#tools)
3. [Terminology](#terminology)
4. [Project Lifecycle](#project-lifecycle)
5. [Opening a New Project](#opening-a-new-project)
6. [Publishing a Release](#publishing-a-release)
7. [Communication](#communication)

## Overview

Having an agreed-upon set of standards for how team members coordinate and collaborate on work leads to more efficient and more enjoyable workflows that yield better results with less effort. In business and software development, there is a long history of research into best practices for how teams should collaborate and coordinate their work, often collectively referred to as “project management.” There is an upfront cost to learning a new system of working together and coordinating work; however, this initial work pays enormous dividends, ultimately translating into more publications and faster deployment of code that is more widely adopted by the community.

The NDCLab uses a modified [agile methodology](https://en.wikipedia.org/wiki/Agile_software_development) to organize our workflows and maximize our productivity. The core idea is that we break larger projects into smaller, iterative pieces and set ourselves time limitations on completing each of the smaller pieces. You do not need to fully understand the tenets of agile beyond the information provided on this page. If you do decide to do extracurricular reading, please be aware that we have modified some of the typical agile terminology to better meet the needs of an academic research lab.

A key purpose of using this agile methodology, including the tools and processes outlined below, is to reduce the amount of time needed for meetings while keeping all team members apprised of a project's status. Initiative and self-assignment of tasks is highly encouraged, along with active collaboration to solve problems and share knowledge.

## Tools

### GitHub
All lab projects live on [GitHub](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html) and make use of native features of the platform, such as issues and pull requests. If you haven't already, [get yourself onboarded](https://ndclab.github.io/wiki/docs/Onboarding/get-with-git.html). 

### ZenHub
[ZenHub](https://ndclab.github.io/wiki/docs/technical-docs/zenhub.html) is a plug-in to GitHub. Issues within a GitHub repository connect automatically to the ZenHub Kanban board associated with the GitHub repository. In general, each repository is connected to one workspace, but it is possible to connect multiple repositories to a single workspace in special circumstances where this would be beneficial to project management.

## Terminology

[**Agile**](https://en.wikipedia.org/wiki/Agile_software_development): a philosophy for flexible, iterative, team-centric project management<br/>
[**Scrum**](https://en.wikipedia.org/wiki/Scrum_(software_development)): a framework for deploying an agile system for project management by breaking larger projects down into manageable chunks<br/>
[**Kanban Board**](https://en.wikipedia.org/wiki/Kanban_board): a visual depiction of project priorities and progress<br/>
**Project**: a big idea that may comprise multiple research publications or the distribution of cool, open-source software<br/>
[**Epic/Release**](https://help.zenhub.com/support/solutions/articles/43000010341-an-intro-to-zenhub-epics): a large narrative that is smaller than the whole project but bigger than an individual task; for example, a specific poster presentation or the beta release of a software tool<br/>
[**Issue**](https://guides.github.com/features/issues/): a feature in GitHub that is a single, well-defined, cohesive task that is accomplished on the road to completing the current epic/release<br/>
[**Sprint**](https://en.wikipedia.org/wiki/Scrum_Sprint): a fixed, short period of time (~1-3 weeks) into which tasks are batched and completed
**Level 1 Review**: a good-faith attempt to catch any errors when reviewing a pull request from a labmate; the reviewer is not equally responsible for the accuracy/quality of the content being merged
**Level 2 Review**: a thorough review of accuracy/quality of the content being merged in a pull request; the reviewer is equally responsible with the individual initiating the pull request


(There are many other terms used in agile project management. We are focusing here on those that best describe the process used here in the lab.)

## Project Lifecycle

Within the NDCLab, projects are conceptualized and organized across three timescales:
* Project
* Epic/Release
* Sprint

### Project (1-3 years)

Each project has a goal; this goal is what will ultimately be achieved after completing all work and releasing all papers and posters envisaged for the project.  For standard projects that do not require new data collection, this timeline is typically 1-2 years. For standard projects that require the lab to collect new data, the timeline is typically 2-3 years.

The project goal should be explicitly stated in the `readme` file on the project's GitHub repository.

Each active project has its own GitHub repository, ZenHub workspace, folder on the HPC, and at least one assigned project lead.

### Epic/Release (4-6 months)

Projects are broken down into smaller chunks, referred to as "releases" or, in ZenHub terminology, "epics." (ZenHub also has something called a "release." Pretend you didn't see that. Remember what we said above about modifying terminology? :wink:) Within the timeframe of an epic/release, some significant change or improvement should be accomplished. For a research project, this might be the publication of a poster. For a new tool, this might be an upgrade that includes a new feature.

Almost all projects will involve more than one epic/release. This is to provide psychological milestones, as well as to yield somewhat self-contained products that can be deployed, presented, published, or otherwise shared with the world (and help build CVs). The work completed during each epic/release is integrally tied to the epics/releases that precede it and the epics/releases that come after; in this way, each epic/release helps to achieve the larger project goal. However, each epic/release should also reflect a conceptual advance upon the prior epic/release, and reflect a change that is significant enough to:
* warrant a novel conference submission (in the case of a research project) or
* encourage users to download the new software release (in the case of tool development).

At the start of a project, all planned epic/release goals for a project should be explicitly stated in the `readme` file on the project's GitHub repository. Each planned epic/release should be established as a time-blocked "Epic" within ZenHub.

An epic/release is considered complete when the improvement (be that a new version of a tool or a publication of some type) is pushed to the `main` branch of the project repository on GitHub.

### Issues (1-3 weeks)

On a day-to-day basis, epics/releases are broken down into bite-sized chunks called "issues." Issues are the primary unit of work and can be broken down into a series of sub-tasks as needed.

Issues are created within the project’s GitHub repository. Sub-tasks, if helpful or required, can be listed as a simple list within the issue description.

At the start of any new project, an effort is made to identify and define a majority of the issues that need to be completed to achieve the first epic/release. The issues that comprise the first release are placed in the Release Backlog pipeline on ZenHub and assigned to the associated ZenHub Epic. All other issues are placed in the Project Backlog pipeline on ZenHub (where they can optionally be assigned to an upcoming epic/release or be left unassigned).

Issues inside the Project Backlog can be relatively large and abstract. However, these issues must be refined and/or broken down further prior to moving them into the Release Backlog. Completing all the work inside the Release Backlog will achieve the epic/release goal.

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
* An "upcoming sprint" issue is created, which remains in the New pipeline on ZenHub and serves as the agenda for the sprint meeting. All team members add their comments (>1 day prior to the meeting) to this issue to promote discussion, including:
    * what we tried and worked really well
    * what we tried and really didn't work
    * what we didn't give a fair try to
    * work that will not be completed in time
    * outstanding roadblocks
    * unexpected developments

#### During the Sprint Meeting

The sprint meeting is broken down into three parts:

1. **Retrospective** (<15 min: reflect on processes that did or did not work<br/>
The retrospective is an opportunity to share tips and tricks so that all members of the team can learn from the experience of others.

2. **Sprint Review** (15 min: review what was completed and what remains incomplete)<br/>
All items in the Done pipeline are move to the Closed pipeline in Zenhub and discussed as needed. There is no need to discuss everything that was completed, as this information is easily viewable to all team members on the ZenHub project workspace. However, particular issues may benefit from reporting on additional details. 

3. **Planning** (60 min: plan work for the next sprint)<br/>
The Sprint Backlog in ZenHub is stocked with the issues that will be accomplished during the next sprint. By the end of the meeting, all issues should have a time estimate and 75% of the issues should be assigned to specific team members (the remaining 25% can be handled by self-assignment during the sprint). All high-priority items must be assigned; lower-priority items can be self-assigned during the sprint. As part of the planning process, the time estimates should be added together to ensure that a reasonable amount of work has been tagged for the sprint.

Once issues are added to the Sprint Backlog, remove the "Add to sprint?" label to remove unnecessary visual noise on ZenHub during the sprint.

#### After the Sprint Meeting

Team members tackle the issues to which they have been assigned, moving the issues into the In Progress pipeline on ZenHub. Ad hoc meetings, impromptu discussions, and the labeling of issues with "Help Wanted" labels are all highly encouraged to ensure team members don't get caught up in roadblocks that slow progress. It is normal to hit roadblocks and it is therefore important to communicate these openly so that more minds can be involved in finding an elegant solution.

When an individual completes an issue, they move it into the Review/QA pipeline on ZenHub and request a review. In most cases, the process of reviewing and approving work on issues involves the preparation of content to be merged with an upstream branch (such as `dev` or `dev-[feature]`). Therefore, the individual who has completed work on the issue initiates a pull request for their working branch, tagging one of the project leads to review the suggested content prior to merging it with the upstream branch. A level 1 review is required; a level 2 review is encouraged whenever possible.

Following review and approval, an issue should be moved to the Done pipeline on ZenHub (but not closed until the next sprint meeting).

Once all of an individual's tasks for the sprint are completed, they are expected to review the ZenHub workspace and:
* Self-assign any unassigned tasks in the current sprint.
* Reach out to any teammates who have posted a "Help Wanted" label.

### Presentation and Feedback

For each epic/release, plan on putting together a work-in-progress presentation, to be given at a lab meeting or similar event. These presentations serve as a way to organize thinking regarding the status of the release and the larger project. This is also a chance to receive feedback.

Typically, the presentation will occur in the second half of the epic/release, and most often, near the end (or just after completion) of the epic/release. 

Pending the venue, project status, and other particulars, this may be a very informal presentation with minimal slides or a formal presentation.


## Opening a New Project

New projects should be based on the NDCLab templates. Visit [this page](https://ndclab.github.io/wiki/docs/etiquette/github-templates.html) for details.

The `main` branch is reserved for "published" information, such as pre-registrations, posters, publications, and official releases of validated software tools.

The `dev` branch reflects the most up-to-date version of the current release.

Since all work will eventually be merged onto `dev` (before an ultimate merge onto `main`), all new branches should be created by branching off `dev`. More information is available on the [naming conventions page](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#github).


## Publishing a Release

At certain stages of each project, information will be ready for public consumption. Since the NDCLab is an open lab, all of our work-in-progress is publicly available. However, we make a clear distinction to show visitors from outside our lab what we consider "done" by pushing this content to the `main` branch.

To "publish" a release on GitHub:

1. The project lead(s) should ensure that the `dev` branch is fully ready to deploy. This means that all content that is being "published" is well-organized and independently verified. (It is ok that some parts of future releases may still be in-progress.)

2. The project lead(s) initiate a pull request, tagging the lab director for a level 2 review. He may review personally or delegate the review.

Once `dev` is merged to `main`, this completes the current epic/release. The ZenHub Release Backlog, Sprint Backlog, In Progress, Review/QA, and Done pipelines should all be empty. The next epic/release is initiated by moving the Epic tile for the next planned epic/release and its associated issues into the Release Backlog.


## Communication

* Watch your notifications so that you respond in a timely manner when someone e@mentions you or asks you to review a pull request.
* When assigning someone to an issue, include an explanatory comment (with @mention) to explain why you think the person is a good fit for the task -- don't just randomly assign people issues without dialogue.
* Use the "question" and "help wanted" labels to communicate to the broader team that you are stuck and need assistance.



