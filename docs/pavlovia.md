---
layout: default
title: Pavlovia Documentation Draft
nav_exclude: true
search_exclude: true
---

## Installing Git

Installing the Git command line tool:

**Mac**

- [Download](https://git-scm.com/download/mac)
- Recommended methods for install: Binary or [Homebrew](https://brew.sh/)
  - Download [dmg](https://sourceforge.net/projects/git-osx-installer/files/latest/download) file
  - `brew install git`

[How to](https://www.ofzenandcomputing.com/how-to-install-dmg-files-mac/) install a binary file on
Mac OS.

**Windows**

- [Download](https://git-scm.com/download/win)
- Recommended method: portable version or "thumbdrive edition"
  - [64bit version](https://github.com/git-for-windows/git/releases/download/v2.29.2.windows.2/PortableGit-2.29.2.2-64-bit.7z.exe)

## Opening a Shell

**Mac**

On Catalina and Mojave, the default shell provided is [Zsh](https://en.wikipedia.org/wiki/Z_shell)
which is very similar to [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) because both are
[POSIX](https://en.wikipedia.org/wiki/POSIX) compliant. This is good because shell scripts written
in either scripting language will be usable on either Mac OS or Windows without tweaks.

To access Zsh, [open up a normal terminal](https://www.wikihow.com/Open-a-Terminal-Window-in-Mac).

**Windows**

Navigate to the portable git folder and double click on `git-bash.exe` and that will launch a shell
instance for Bash.

There is a different option, `git-cmd.exe` which uses the [Command
Prompt](https://en.wikipedia.org/wiki/Cmd.exe). Using the Command Prompt is not recommended since it
uses a different tool set which is not covered in this guide.

## Setting Up SSH Keys

SSH keys are a form of authentication like username and passwords that simplify the process of
working with git repositories.

If you have ssh keys already please make sure to check the names before hand to avoid overriding
them.

To create an SSH key pair; a private key and a public key you will need to do the following steps:

- Open up a Terminal with a Shell; Bash on Windows, Zsh on Mac
- Copy-paste the following commands:

```sh
# The "comment" should either be an email "username@email.com" or user@hostname "username@mycomputer"
ssh-keygen -t ed25519 -C "comment"
```

- At this point you will be prompted for two things:
  - Where to save the private/public key, the default location is displayed
  - A passphrase for the key

\* Note on the key type: the current (as of 2020) recommendation is ED25519 over RSA.
\* Note on the passphrase: The passphrase can be excluded but it is recommended that you use one for
improved security.

### Resources

[Github
Guide](https://docs.github.com/en/github-ae@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

[Gitlab Guide](https://docs.gitlab.com/ee/ssh/README.html#generating-a-new-ssh-key-pair)

## Adding an SSH key to Pavlovia

### Overview

Now that you have an SSH key pair, the private and public key, you will need to add the public key
to Pavlovia.

### Steps

Login into [Pavlovia](https://gitlab.pavlovia.org/users/sign_in) using your username and password.

![](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/pavlovia_md/sshk_signin.png)

At the top-right hand corner click the drop down and select "Settings".

![](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/pavlovia_md/sshk_settings.png)

On the left side you will see "User Settings" and a list of categories. Select "SSH Keys"

![](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/pavlovia_md/sshk_settings_category.png)

With a text editor open up the ssh key file that ends with `.pub` and inside you will see a
`ssh-ed25519` and a long alpha-numeric sequence and an email or username at the end. Copy the entire
line.

Paste it into the "Key" text box in the page that you are on.

Give the key a "Title", this can be anything as it is a name to help you remember where the key is
when you have multiple keys.

Press "Add key"

![](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/pavlovia_md/sshk_input.png)

Refresh and you will see the new key in "Your SSH keys (1)"

![](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/pavlovia_md/sshk_newkey.png)

### Resources

[Gitlab in-depth
guide](https://docs.gitlab.com/ee/ssh/README.html#adding-an-ssh-key-to-your-gitlab-account)

## Creating a Repository on Gitlab

### Overview

To create a repository you will need to create an empty repository on the NDC Lab organization or
your personal Gitlab on the Pavlovia Gitlab instance. The NDC Lab organization or group will be
where we put the PsychoPy and PsychoJS projects. Your personal projects can be used for things like
experimenting with changes that you may not necessarily want to push to the main repository.

Note: Group and Organization can be used interchangeably. And repository and project can be used
interchangeably.

### Accessing the NDC Lab group

By default you will be able to see the NDC Lab projects when you are logged in on the main page when
you access `https://gitlab.pavlovia.org`. If not these are different ways to access the projects:

- Open the "Groups" drop-down at the top of the page
- Select "Your groups"
- Select NDCLab

Or

- click this [link](https://gitlab.pavlovia.org/ndclab)

### Creating a Gitlab Project

Once you are inside the group page:

Press "New project"

![](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/pavlovia_md/nproj_new.png)

Name the project

Make sure that "ndclab" is selected in the "Project URL"

Write out a "Project Slug", substitute spaces with a hyphen "-"

Set to "Public"

Press "Create project"

![](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/pavlovia_md/nproj_create.png)

\* Note: A "[Slug](https://en.wikipedia.org/wiki/Clean_URL#Slug)" is generally the part of a URL
that comes after the domain bits. It is a nicer way to link to something instead of a long
alpha-numeric string or a long directory and file combo.

### Resources

[Gitlab In-depth guide](https://docs.gitlab.com/ee/gitlab-basics/create-project.html)

## Shell Tips

### Overview

This section will cover some basic commands for moving around, and displaying the current location
in a Terminal running a Bash or Zsh shell.

Some of the terminology used:

- directory: another name for a folder
- option: an option that the program will allow you to change using special formatting, generally
	denoted with a "--" in front of the option name. For example "--option value".
- flag: an option that can be on or off, generally denoted with a "-" in front of the name. For
	example "-t".

### Important Commands

#### ls

`ls` or list directory contents will list the files and directories in the directory that you are
in. This is useful to know what is in the current directory, but it can show any contents of any
directory as long as you provide a valid path to that directory and you have permission to view that
directory.

Example:

```sh
# ls without options
ls
#> Download Desktop stories.txt ... etc
# ls with the flag option l
ls -l
#> drwxr-xr-x    - username 31 May 10:35 Desktop
#> drwxr-xr-x    - username  9 Oct 14:52 Downloads
#> drwxr-xr-x    - username 25 Aug 17:00 stories.txt
```

#### cd

`cd` or change directory is a shell command that allows you to move from one directory to another.
This is useful to move around in the shell, like `ls` it will accept any valid path to any
directory.

There are two kinds of paths:

Relative paths, which are paths relative to your current directory. This paths can start with either
`.` for the "current directory or `..` for "the directory above this directory".

And absolute paths or paths that start from the root of the file-system `/` in Mac OS or `c:/` in
Windows.

Example:

```sh
# Example with a relative path
# Current directory: /home/user/proj_folder/
cd ./some_folder/
# Current directory: /home/user/proj_dir/some_folder/

# Example with an absolute path
# Current directory: /c/Users/username/Desktop/
cd /c/Users/
# Current directory: /c/Users
```

Since we will be using Bash on Windows, a small quirk that we will need to consider is the one that
can be seen in the example above. Anytime you would write `c:\` you would need to replace it with
`/c/`. And swap all `\` with `/`. Mac OS uses `/` like Linux so write paths as you would normally.

### Resources

Some cheat sheets, with useful commands. On Windows not all this commands will work due to the fact
that some of the tools listed won't be installed. Similarly, on Mac some commands will work but some
will not.

[Linux Commands](https://www.guru99.com/linux-commands-cheat-sheet.html)

[Linux Tutorials](https://ryanstutorials.net/linuxtutorial/cheatsheet.php)

For more in-depth information you can read the manual page for all these commands.

[Manual page](https://linux.die.net/man/)

## Git Usage

### Overview

Git has several commands that will be necessary to properly work with the Pavlovia Gitlab
repositories. Those are `status`, `add`, `commit`, `push`, `pull`, and `checkout`.

### Commands and their Usage

#### Status

This command will list files and there state within git.

Files can either be ignored, untracked, unstaged, and staged. Ignored means that the files satisfies
a rule in the `.gitignore` file.  Untracked refers to files that git is not ignoring but have never
been committed, this is normal for newly created files. Unstaged files are files that currently have
changes and have been committed before but are not currently staged. Staged files are files that
have been committed before and have been added to the staging area so they can be committed.

#### Add

This command will add any file that you want whether it is tracked or not.

Example:

```sh
git add some_file.txt
```

### Commit

This command will commit your changes to the repository. There are two important options for commit
`-m` and `-a`. `-m` is for the commit message, and `-a` means that git will automatically add any
tracked files that have not been added and add them to staging and committing those changes.

Example:

```sh
# Staged files: s.txt
# Unstaged files: u.txt
# Untracked and unstaged files: uu.txt

# first example
git commit -m "Update s file"
# Commits only changes for s.txt

# Reset
# Second example
git commit -am "Update s and u file"
# Adds u.txt to staging area
# Commits changes for s.txt and u.txt
```

#### Push

This command will push all changes that have been add to the Pavlovia Gitlab repository.

Example:

```sh
# Local repository is ahead of Pavlovia Gitlab repository
git push
# Changes are uploaded
```

#### Pull

This command will "pull" changes from the remote repository, in this case the Pavlovia Gitlab
repository you cloned. Pull will try to fetch any new changes and merge them. Generally, as long as
you have not diverged from the remote repository this will work fine.

Example:

```sh
# Local repository is behind of Pavlovia Gitlab repository but has not diverged
git pull
# Git will download new changes and merge them automatically
```

#### Checkout

This command changes the contents of the local repository to match the branch that you "checkout".
It will leave changed files untouched so that you can commit them to the branch you are checking
out. This is useful when you accidentally made changes to "branch\_b" thinking you were on
"branch\_a".

Example:

```sh
# on branch_b
git checkout branch_a
# on branch_a
# changes were brought over
```

## Setting Up the Local Repository

### Overview

Setting up a local repository in our case means that we will be cloning the Gitlab repository. The
repository can be empty or have a lot of work already incorporated. The process for "setting it up
locally" is exactly the same.

### Steps

- `git clone` the repository that was created. For example: 
	`git clone git@gitlab.pavlovia.org:furcb/temp.git`
- `cd repo-name` where repo-name is the name of the repository.

## Gitlab Work-Flow

At this point you will have a repository that is correctly configured. To begin adding changes we
must create a new branch. To create a new branch follow theses steps:

- `git checkout -b fix_a` to create a new branch with the name "fix\_a", change the name
	to match the changes you will be making.

Once the new branch is created open the PsychoPy project and start making changes to the project.
After adding all the new changes, do the following:

- Add all the new changes using the `add` command
- Commit those changes using the `commit` command
- `git push origin fix_a` to push the new branch to the remote repository under the new branch
	name

Once you have something you want to merge with the main branch, confirm with other team members by
having them pull the new branch and testing the new changes. Once the branch with the changes has
been reviewed, we can add the new branch to the main branch.

- Checkout the main branch by using `git checkout main`

> Any uncommitted changes will be transferred into the main branch, this might make the next steps
> difficult in some cases. If you would like to PERMANENTLY discard/delete those changes use `git
> reset --hard HEAD`

If the main branch has not been changed since the point when the new branch was created follow these
steps:

- Merge the new branch by using `git merge fix_a`
- Do `push` to push the updated main branch to the remote repository

If the main branch has been changed since the point when the new branch was created, in this case
fix\_a, follow these steps:

- Use the `pull` command to pull the newest changes for the main branch
- `git merge fix_a` to merge the changes from the new branch

At this point if there where no conflicting changes, git will have completed the merge as if the
main branch was not different from the point when you created the new branch. If there are
conflicting changes, or changes that are in the same area as changes that were added to the main
branch after creating the new branch, you will have to manually fix those conflicts.

- Fix those conflicts
- Use `add` to add those changes
- Use `commit` to commit those changes
- Use `push` to upload the new main branch to the remote repository

A word of warning, most files will be simple to fix merge conflicts. The python project file for
PsychoPy may be harder since it is auto-generated python code. Although as long as changes do not
overlap i.e. merging changes for same components, merge conflicts should not happen and if they do
they are easy to incorporate.

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

Pavlovia allows us to add the html files to the root of the project directory or to create an html
directory and add those files created on export there. We will be using the latter method since it
is cleaner and more organized.

### Export PsychoJS project

With the builder open go to "File > Export HTML" and the PsychoPy builder will export the html
files.

Using your file manager of choice, Explorer on Windows and Navigator on Mac OS, move those new files
to `html/` in the project directory.

Add any assets like pictures, csv's, and any other files needed for the project to run to `html/` as
well. It is recommended to use `resources/` as the directory for those files. If you use a
`resources/` directory in `html/` you must also use it in the root of the project.

Example:

```
# Think of the html directory as a mini PsychoJS project

└── psychopy_proj
   ├── html
   │  └── resources
   └── resources
```
