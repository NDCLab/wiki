---
layout: default
title: Shell
parent: Technical Documentation
nav_order: 2
---

### Contents
1. [Overview](#overview)
2. [Opening a Shell](#opening-a-shell)
3. [Shell Tips](#shell-tips)
   1. [Key Terms](#key-terms)
   2. [Important Commands](#important-commands)
   3. [Additional Resources](#additional-resources)

# Overview

It's very useful to know how to use a [command-line interface (CLI)](https://en.wikipedia.org/wiki/Command-line_interface) inside a [shell](https://en.wikipedia.org/wiki/Shell_(computing)).  At the NDCLab, you will need this knowledge to work with [GitHub](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html) and the [FIU HPC](https://ndclab.github.io/wiki/docs/technical-docs/hpc-doc.html), among other applications.

# Opening a Shell

**Mac**

On OS releases starting from Catalina, the default shell provided is [Zsh](https://en.wikipedia.org/wiki/Z_shell) which is very similar to [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) because both are [POSIX](https://en.wikipedia.org/wiki/POSIX) compliant. This is good because shell scripts written in either scripting language will be usable on either macOS or Windows without tweaks.

To access Zsh, open up a normal terminal simply by clicking on the Terminal application on your Mac.

**Windows**

Install Git first. Check out [these instructions](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html).

Navigate to any location on your machine (although one suggests selecting a location where you will do all your NDCLab work), right-click, and select "Git Bash Here" from the menu. This opens a Bash shell where you can input shell and git commands.

![git-bash](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/git-bash.png)

(There is a different option that uses the [Command Prompt](https://en.wikipedia.org/wiki/Cmd.exe). Using the Command Prompt is not recommended since it uses a different tool set which is not covered in this guide.)

**Linux**

There are many ways to open a shell on Linux. One example: right-click your desktop and select "Open Terminal" from the menu.


# Shell Tips

## Key Terms

Here is some of the key terminology used in working with a shell:

- **command**: an instruction from you (the user) to your computer.
- **directory**: another name for a folder. When you navigate around your files using the shell, you're always "sitting" in a directory (called your "current directory").
- **option**: an option that the program will allow you to change using special formatting, generally	denoted with a "--" in front of the option name. For example "--option value".
- **flag**: an option that can be on or off, generally denoted with a "-" in front of the name. For example "-t".

## Important Commands

### ls

`ls` will list the files and directories that live within the directory that you are currently "in." This is useful to see what is in your current directory, but it can also show you the contents of any directory as long as you provide a valid path to that directory and you have permission to view that directory.

Example:

```sh
# ls without options (outputs results on one line)
ls
#> Downloads Desktop stories.txt ...

# ls with the flag option -l (outputs one result per line)
ls -l
#> drwxr-xr-x    - username 31 May 10:35 Desktop
#> drwxr-xr-x    - username  9 Oct 14:52 Downloads
#> drwxr-xr-x    - username 25 Aug 17:00 stories.txt
```

### cd

`cd` (change directory) is a shell command that allows you to move from one directory to another. This is useful to move around in the shell and, like `ls`, it will accept any valid path to any directory.

There are two kinds of paths:

**Relative paths**, which are path names relative to your current directory. This path can start with either `.` for the "current directory or `..` for "the directory above this directory".

**Absolute paths** are paths that start from the root of the file-system (`/` in macOS or `c:/` in Windows).

Example:

```sh
# Example with a relative path
# Current directory: /home/user/proj_dir/
cd ./sub_folder/
# Current directory: /home/user/proj_dir/sub_folder/

# Example with an absolute path
# Current directory: /c/Users/username/Desktop/
cd /c/Users/
# Current directory: /c/Users

# Shortcut to go up one level
# Current directory: /home/user/proj_dir/sub_folder/
cd ..
# Current directory: /home/user/proj_dir/

# Shortcut to return home
# Current directory: /home/user/proj_dir/sub_folder/
cd ~
# Current directory: /home/
```

## Additional Resources

Here are several Linux cheat sheets with useful commands. Not all of these commands will work on Windows and macOS, but most of the core commands are the same with Linux and will therefore work.

[Linux Commands](https://www.guru99.com/linux-commands-cheat-sheet.html)<br/>
[Linux Tutorials](https://ryanstutorials.net/linuxtutorial/cheatsheet.php)
