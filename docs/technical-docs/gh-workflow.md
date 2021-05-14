---
layout: default
title: General Issues Workflow
parent: Technical Documentation
nav_order: 6
---

# General Overview

GitHub issues work flow. GitHub issues are similar to requests for actions by anyone who interacts
with the project. They can be unstructured or structured with templates depending on the
project. And can cover any aspect of the project.

## Issues

The issues will be the place we will be adding the Scrum backlog to, in other words the user
stories. Feature requests or enhancements that can be made to the project. And any bug or problem
that is found with the project.

Each type of issue will have a specific template to aid the contributor with the general structure
and formatting, and what kind of information is expected.

## Opening an Issue

Here are the following steps on how to create an issue:

- Go to the Issues tab on GitHub for the repository you wish to submit an issue for.

![issues tab](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/general_issues_workflow/issues_tab.png)

- First make sure that the issue does not exist already and/or has been solved.
  - A simple way to check is to delete `is:open` and search for the issue in question.

![delete open](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/general_issues_workflow/delete_open.png)

- If none exists, click on "New Issue"

![new issue](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/general_issues_workflow/new_issue.png)

- You will be prompted to select from a list of templates which in our case will be "Bug Report",
	"Feature Request", "User Story", or "Open a blank issue" if the issue does not currently have a
	category.

![select template](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/general_issues_workflow/select_template.png)

- Select the correct category by pressing "Get Started"
- Fill out the template with the relevant information
  - You can select the "Preview" tab to preview the submission before doing the final submission
- Click "Submit new issue" to publish the issue

![fill out the form](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/general_issues_workflow/fill_out_form.png)

> Note: Before submitting you can use a label to make the submission easier to find. If the problem
> requires a specific persons help assign them to "Assignees"

![assignee selection](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/general_issues_workflow/assignee_selection.png)

> Note: Which labels to use? The nine default labels are useful and can be used to make an issue
> more visible. For certain types of projects like the Wiki or PsychoPy, there will be more specific
> labels to help make issues more visible.

## Working on an Issue

In this step it might become relevant to add code that may solve the issue. To do this:

- First make a pull requests with changes
- On the Issue page on the right hand side you will see "Linked pull requests"

![link pull request](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/general_issues_workflow/link_pull_request.png)

- Select the cog wheel which will bring up a list of available pull requests
- Select the pull request for this issue
  - This allows for easy tracking that changes have fixes are on that pull request

![select pull request](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/general_issues_workflow/select_pull_request.png)

- When the merge is being done by the reviewer, add "fixes #1" or substituting the "1" with the
	issue number in the merge commit message to automatically close the issue.

> Note: using "@" can notify additional people who might be needed to continue to work on the issue
> if they were note initially assigned to the issue.

## Closing an Issue

If the issue has been resolved and was not automatically closed by reviewer using special commit
word:

- Go to the Issue
- If relevant provide a comment on why you are closing the issue
- Then click either "Close issue" or "Close with comment"

![close issue manually](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/general_issues_workflow/close_issue.png)

> Note: Project boards can be accessed through the issue page, and if automatic management is not
> set for the Project board you can move the Issue to "Done" at this step or a category that would
> make sense depending on how the issue was resolved.

> Note: Issue can be re-opened if changes that would have fixed any problem or implemented a feature
> did not work.

## Who Will Resolve Issues

Anyone can post issues and post resolutions to those issues since our projects are open source.
Although anyone can do this, when it comes to merging those resolutions only the project maintainers
or the group owner are allowed to merge them. This is covered in more details under [Pull
Requests](#).

## Templates

The default templates for each project will be available from a template/skeleton repository that
will also include other files that will be useful for creating the base of a project.

- [Bug Template](#)
- [User Story Template](#)
- [Feature Request Template](#)

## Additional Resources

- [Issues Guide](https://guides.github.com/features/issues/)
- [Templates](https://github.com/stevemao/github-issue-templates)
- [Linking a pull request to
	an](https://docs.github.com/en/free-pro-team@latest/github/managing-your-work-on-github/linking-a-pull-request-to-an-issue)
- [Words for Issue
	Commits](https://docs.github.com/en/free-pro-team@latest/github/managing-your-work-on-github/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword)
