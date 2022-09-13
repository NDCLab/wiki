---
layout: default
title: Get with Git
parent: Onboarding
nav_order: 7
---

# Get with Git

## Overview
A large portion of NDCLab collaboration happens on GitHub. If you've never used GitHub before, never fear! This page walks you through a miniature training program to jumpstart your Git skills.  Here is an overview of what we'll be doing:
* Installing Git on your computer (for free).
* Setting up your free GitHub account.
* Learning the ropes of Git and GitHub.
* Putting your new skills to use to update your entry on the NDCLab wiki ["Who's Who" page](https://ndclab.github.io/wiki/docs/welcome/whos-who.html).

## How to Get with Git
Follow the steps below to become a Git ninja! We will set up your computer so you can use the Git language and tools locally (offline). We will also set up your identity on GitHub. GitHub is a web platform that is a "hub" for "Git" activities. After we have Git installed and you have a GitHub account, you can make your computer and GitHub talk to one another!

1. Find your [shell](https://ndclab.github.io/wiki/docs/technical-docs/shell.html). The shell enables you to interact quickly and easily with GitHub.

2. Install Git on your local machine. [This page](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html) includes instructions for macOS, Windows, and Linux/Unix installations, as well as a lot of other useful information about working with Git and GitHub. Even though you won't understand it all now, read through the full page so you know that you have this helpful resource for the future.

3. [Sign up](https://github.com) for a free GitHub account.

4. Set up your identity by typing two commands into your shell: <br/>
`git config --global user.name "John Doe"` <br/>
`git config --global user.email johndoe@example.com` <br/>
(Obviously, replace John Doe and johndoe@example.com with your actual name and your actual e-mail. If you're not sure whether you've done this before, check with the command `git config --list`.)

5. Authenticate yourself to GitHub by setting up a [personal access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token). (Be aware that other authentication methods are possible; personal access tokens are recommended because they are the simplest to set up for GitHub.) A personal access token is an alternative to using a login and password each time you connect to GitHub.  Once you set up the token, GitHub will recognize your computer and know that you are YOU each time you connect to it from the shell.

6. Notify the lab manager so that you are now ready to be added to the NDCLab organization on GitHub. Continue with the next step while you wait. (Note: when you receive the invitation to join the organization, please make your membership `public`. If you accidentally set your membership to `private,` don't stress: simply navigate to the People tab from the main NDCLab page, then change the dropdown next to your own name from `private` to `public`.)

7. Start with [this video](https://www.youtube.com/watch?v=DVRQoVRzMIY) by Tech With Tim, which offers a broad overview of Git and GitHub while showing you both the command line interface and the GitHub interface. Do not worry about digesting *everything* that he shows in this video, but rather focus on learning the big picture lessons: key terminology, core concepts, and the commands he uses most frequently.

8. Take the [quiz](https://forms.gle/B83WY7q1wWkpZtKV6).

9. Work through two hands-on tutorials by following the instructions in the readmes, then head back over here and continue to #10 below.
    - [Introduction to GitHub](https://github.com/skills/introduction-to-github)
    - [Communicate Using Markdown](https://github.com/skills/communicate-using-markdown)

10. Watch [this video](https://youtu.be/4nEAxtKvrQE) where the lab manager gives you a tour of the NDCLab wiki and takes you through the steps to update your entry on the who's-who page.

11. Time to put it all together! Update your entry on the wiki's who's-who page using the new commands you've just learned:<br/>
`git clone <link>`  <br/>
`git branch whos-who-[yourname]`  <br/>
`git checkout whos-who-[yourname]`  <br/>
`git add docs/welcome/whos-who.md` <br/>
`git add docs/_assets/whos-who/[yourname].jpg` <br/>
`git status`  <br/>
`git commit -m "Add [yourname] to who's-who"`  <br/>
`git push origin whos-who-[yourname]`

    Don't forget to:

    * Create your own branch, off the main branch, entitled "whos-who-[yourname]" (without the brackets).
    * Switch to your branch before you start making any changes!
    * Resize your photo to 100 x 100 pixels and copy it into the "whos-who" folder within "_assets". (If you cannot find your Home folder on Mac, type cmd+shift+H inside Finder.)
    * Name your photo simply as your last name. This way, you can reference it with<br/>
    `![name](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/whos-who/name.jpg)`
    * Nest your entry under your lab title, alphabetically by last name.
    * Push all your changes back to the remote.
    * Create a pull request and tag the lab manager (you can find the lab manager's GitHub handle on the page you just updated!) to review your changes and merge them into the live wiki!

12. After the lab manager has merged your changes, you have one more important mission. Review the wiki and identify (at least) one improvement, in a different section of the wiki, that you think would help a future lab member.

* Within your wiki folder, switch back to the main branch: `git checkout main`
* Update your main branch with any new changes from other lab members: `git pull`
* Create a new branch off the main branch and name it in accordance with the lab's [naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#github): `git branch feature-[improvement]-[yourname]`
* Switch to your new branch: `git checkout feature-[improvement]-[yourname]`
* Navigate within the wiki folders, using `cd` and `ls`, to open the file(s) where you will implement your suggestion.
* Add your modified file(s) to your staging area: `git add [filename]`.
* Commit your changes, push to the remote, and submit a new pull request to the lab manager!

13. Some final thoughts to maximize your use of GitHub:
* **DO** be careful in customizing your notifications. You want to see every time someone @mentions you or assigns an issue to you, and you don't want those messages to be lost in a sea of other, less important notifications. Think of GitHub as being another inbox to monitor or, alternately, treat the automatic GitHub notifications that hit your e-mail inbox as actionable messages.
* **DON'T** worry about breaking something. You can always clone a repository, make suggested changes, and tag someone on a pull request. The worst that can happen is that they disagree!
* But **DON'T** forget to create and checkout to a *new* branch. Never make your changes directly on main.
* **DO** think about who should review your work before it is integrated into the main branch. Feel free to start a conversation with a pull request, even if you aren't ready for a final merge.
