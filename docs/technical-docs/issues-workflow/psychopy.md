---
layout: default
title: Custom Workflows
parent: General Issues Workflow
---

# Custom Workflows

## Overview

Custom Issues workflow for specific projects in the lab where the issues are used for more than just
posting bugs and feature requests.

Reference the [General Issues Workflow](./index.md) document to get a more in-depth description about the
workflow, and view additional resources.

Sections:

Labels that will signal the kind of issue to make it easier for contributors to find issues that
they can help with more easily.

Templates:

Template forms for the issues that will provide context to what information is needed to submit an
issue.

## PsychoPy Knowledge Share

The PsychoPy Knowledge Share will use a custom Issues workflow to utilize GitHub Issues for sharing
information about getting around PsychoPy, PsychoJS, and Pavlovia issues.

### Labels


- psychopy: An issue relating to psychopy in general when it runs on the desktop
- builder: An issue relating to the builder, for example "The Text Box[beta] is crashing my project"
- psychojs: An issue relating to psychojs but not necessarily Pavlovia dependent, for example "This
	python code is not being converted to javascript correctly"
- pavlovia: An issue relating to the Pavlovia platform, for example "My experiment does not show
	under the "Experiment" tab"
- question: A general question about PsychoPy, can use the other tags to make this tag more
	specific.

### Templates

- Error: This can be used for any form of error that crashes crashes the experiment on desktop or
	pavlovia, or when the builder crashes or provides an error message.
- General: Unexpected behaviour that is hard to classify, can be an error in disguise or something
	else.
- Blank issue: Blank template, still use labels, assignees if it is relevant.

### Workflow

- Go to the PsychoPy Knowledge Share repository
- Go to the "Issues" tab
- Search for the issue to see if it exists, make sure to delete "is:open" to make sure you search
	for resolved issues.

In the case where the issue does not exist:

- Create a new issue with a template that matches the issue the best, the templates will have a
	title and short description to give you an idea before selecting one.
- Fill out the information in the form
- Try to resolve the issue or wait for help
- Once the issue is resolved, write a comment stating the issue has been resolved and close the
	issue.

If the issue exists, review what the current state of the issue is.

- Provide any additional information that you see is missing from the issue that may give others a
	better idea of how to resolve the issue.


