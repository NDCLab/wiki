---
layout: default
title: Pavlovia + GitLab
parent: Technical Documentation
nav_order: 4
---

# Pavlovia + GitLab Tutorial

An overview on how to get started with Git, GitLab, and Pavlovia in order to run PsychoPy projects on the browser.

#### TABLE OF CONTENTS
1. [Setting up SSH Keys](https://ndclab.github.io/wiki/docs/pavlovia.html#setting-up-ssh-keys)
2. [Adding an SSH Key to Pavlovia](https://ndclab.github.io/wiki/docs/pavlovia.html#adding-an-ssh-key-to-pavlovia)
3. [Creating a Repository on GitLab](https://ndclab.github.io/wiki/docs/pavlovia.html#creating-a-repository-on-gitlab)
4. [Setting Up the Local Repository](https://ndclab.github.io/wiki/docs/pavlovia.html#setting-up-the-local-repository)
5. [GitLab Workflow](https://ndclab.github.io/wiki/docs/pavlovia.html#gitlab-workflow)
6. [PsychoJS Workflow](https://ndclab.github.io/wiki/docs/pavlovia.html#psychojs-workflow)


## Opening a Shell and Installing Git
Please reference the setup instructions for Git [here](https://ndclab.github.io/wiki/docs/technical-docs/git_and-github.html).

## Adding an SSH key to Pavlovia

### Overview

Now that you have an SSH key pair (the private and public key), you will need to add the public key to Pavlovia.

[GitLab Guide](https://docs.gitlab.com/ee/ssh/README.html#generating-a-new-ssh-key-pair)

### Steps

Login into [Pavlovia](https://gitlab.pavlovia.org/users/sign_in) using your username and password.

![](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/pavlovia_md/sshk_signin.png)

At the top-right hand corner, click the drop down and select **Settings**.

![](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/pavlovia_md/sshk_settings.png)

On the left side, you will see **User Settings** and a list of categories. Select **SSH Keys**

![](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/pavlovia_md/sshk_settings_category.png)

With a text editor open up the ssh key file that ends with `.pub` and inside you will see a `ssh-ed25519` and a long alpha-numeric sequence and an email or username at the end. Copy the entire line.

Paste it into the **Key** text box in the page that you are on.

Give the key a **Title**, this can be anything as it is a name to help you remember where the key is when you have multiple keys.

Press **Add key**.

![](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/pavlovia_md/sshk_input.png)

Refresh and you will see the new key in **Your SSH keys (1)**.

![](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/pavlovia_md/sshk_newkey.png)

### Resources

[Gitlab in-depth guide](https://docs.gitlab.com/ee/ssh/README.html#adding-an-ssh-key-to-your-gitlab-account)

## Creating a Repository on Gitlab

### Overview

To create a repository, you will need to create an empty repository on the NDC Lab organization or your personal Gitlab on the Pavlovia Gitlab instance. The NDC Lab organization or group will be where we put the PsychoPy and PsychoJS projects. Your personal projects can be used for things like experimenting with changes that you may not necessarily want to push to the main repository.

**Note:** Group and Organization can be used interchangeably. And repository and project can be used interchangeably.

### Accessing the NDC Lab group

By default, you will be able to see the NDC Lab projects when you are logged in on the main page when you access `https://gitlab.pavlovia.org`. If not these are different ways to access the projects:

- Open the **Groups** drop-down at the top of the page
- Select **Your groups**
- Select NDCLab

Or

- click this [link](https://gitlab.pavlovia.org/ndclab)

### Creating a Gitlab Project

Once you are inside the group page:

Press **New project**.

![](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/pavlovia_md/nproj_new.png)

Name the project.

Make sure that **ndclab** is selected in the **Project URL**.

Write out a **Project Slug**, substitute spaces with a hyphen (-).

Set to **Public**.

Press **Create project**.

![](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/pavlovia_md/nproj_create.png)

\* Note: A "[Slug](https://en.wikipedia.org/wiki/Clean_URL#Slug)" is generally the part of a URL that comes after the domain bits. It is a nicer way to link to something instead of a long alpha-numeric string or a long directory and file combo.

### Resources

[GitLab In-depth guide](https://docs.gitlab.com/ee/gitlab-basics/create-project.html)


## Setting Up the Local Repository

### Overview

Setting up a local repository in our case means that we will be cloning the Gitlab repository. The repository can be empty or have a lot of work already incorporated. The process for "setting it up locally" is exactly the same.

### Steps

- `git clone` the repository that was created. For example: 
	`git clone git@gitlab.pavlovia.org:furcb/temp.git`
- `cd repo-name` where repo-name is the name of the repository.

## Gitlab Workflow

At this point, you will have a repository that is correctly configured. To begin adding changes, you must create a new branch. To create a new branch follow theses steps:

- `git checkout -b fix_a` to create a new branch with the name "fix\_a", change the name to match the changes you will be making.

Once the new branch is created, open the PsychoPy project and start making changes to the project. After adding all the new changes, do the following:

- Add all the new changes using the `add` command
- Commit those changes using the `commit` command
- `git push origin fix_a` to push the new branch to the remote repository under the new branch name

Once you have something you want to merge with the main branch, confirm with other team members by having them pull the new branch and testing the new changes. Once the branch with the changes has been reviewed, we can add the new branch to the main branch.

- Checkout the main branch by using `git checkout main`

> Any uncommitted changes will be transferred into the main branch, this might make the next steps
> difficult in some cases. If you would like to PERMANENTLY discard/delete those changes use `git
> reset --hard HEAD`

If the main branch has not been changed since the point when the new branch was created follow these steps:

- Merge the new branch by using `git merge fix_a`
- Do `push` to push the updated main branch to the remote repository

If the main branch has been changed since the point when the new branch was created, in this case fix\_a, follow these steps:

- Use the `pull` command to pull the newest changes for the main branch
- `git merge fix_a` to merge the changes from the new branch

At this point if there where no conflicting changes, git will have completed the merge as if the main branch was not different from the point when you created the new branch. If there are conflicting changes, or changes that are in the same area as changes that were added to the main branch after creating the new branch, you will have to manually fix those conflicts.

- Fix those conflicts
- Use `add` to add those changes
- Use `commit` to commit those changes
- Use `push` to upload the new main branch to the remote repository

**A word of warning:** most files will be simple to fix merge conflicts. The python project file for PsychoPy may be harder since it is auto-generated python code. Although as long as changes do not overlap i.e. merging changes for same components, merge conflicts should not happen and if they do they are easy to incorporate.

Example merge conflict:

```sh
# Contents of "some_file.txt"
<<<<<<< HEAD
This was added after fix_a and conflicts with fix_a
=======
This is a change in fix_a
>>>>>>> fix_a
```

Example resolved merge conflict:

```sh
# Contents of the fixed "some_file.txt"
This is a change in fix_a
```

## PsychoJS Workflow
 
### Overview

Pavlovia allows us to add the html files to the root of the project directory or to create an html directory and add those files created on export there. It is suggested to use the latter method since it is cleaner and more organized.

### Export PsychoJS project

With the builder open go to "File > Export HTML" and the PsychoPy builder will export the html files.

Using your file manager of choice, Explorer on Windows and Navigator on Mac OS, move those new files to `html/` in the project directory.

Add any assets like pictures, csv's, and any other files needed for the project to run to `html/` as well. It is recommended to use `resources/` as the directory for those files. If you use a `resources/` directory in `html/` you must also use it in the root of the project.

Example:

```
# Think of the html directory as a mini PsychoJS project

└── psychopy_proj
   ├── html
   │  └── resources
   └── resources
```


### `push`

This command will push all changes that have been add to the Pavlovia Gitlab repository.

Example:

```sh
# Local repository is ahead of Pavlovia Gitlab repository
git push
# Changes are uploaded
```

### `pull`

This command will "pull" changes from the remote repository, in this case the Pavlovia Gitlab repository you cloned. Pull will try to fetch any new changes and merge them. Generally, as long as you have not diverged from the remote repository this will work fine.

Example:

```sh
# Local repository is behind of Pavlovia Gitlab repository but has not diverged
git pull
# Git will download new changes and merge them automatically
```
