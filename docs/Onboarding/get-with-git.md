---
layout: default
title: Get with Git
parent: Onboarding
nav_order: 8
---

# Get with Git

## Overview
A large portion of NDCLab collaboration happens on GitHub. If you've never used GitHub before, never fear! This page walks you through a miniature training program to jumpstart your Git skills.  Here is an overview of what we'll be doing:
* Installing Git on your computer (for free).
* Setting up your free GitHub account.
* Learning the ropes of Git and GitHub.
* Putting your new skills to use to update your entry on the NDCLab wiki ["Who's Who" page](https://ndclab.github.io/wiki/docs/welcome/whos-who.html).

## How to Get with Git

1. Find your [shell](https://ndclab.github.io/wiki/docs/technical-docs/shell.html).

2. Install git on your local machine. [This page](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html) includes instructions for macOS, Windows, and Linux/Unix installations. Work through the instructions until you have completed setting up your SSH keys. Read the rest of the page to get an idea of what it contains; you won't understand it all now, but it will be a helpful resource for you in the future!

3. [Sign up](https://github.com) for a free GitHub account.

4. Set up your identity by typing two commands into your shell: </br>
`$ git config --global user.name "John Doe"` </br>
`$ git config --global user.email johndoe@example.com` </br>
(Obviously, replace John Doe and johndoe@example.com with your actual name and your actual e-mail. If you're not sure whether you've done this before, check with the command `git config --list`.)

--------QUESTION (asked wiki #36, 5/12)
5. Authenticate yourself to GitHub (ASKED ON GH)
--------QUESTION

6. Start with [this video](https://www.youtube.com/watch?v=DVRQoVRzMIY) by Tech With Tim, which offers a broad overview of Git and GitHub while showing you both the command line interface and the GitHub interface. Do not worry about digesting *everything* that he shows in this video, but rather focus on learning the big picture lessons: key terminology, core concepts, and the commands he uses most frequently.

7. Take the [quiz](https://forms.gle/Lw5uQAvGC5XQGUum6).

8. Work through [this hands-on tutorial](https://lab.github.com/lmachens/git-and-github-first-timers) inside GitHub. Once you are signed into GitHub and connected, click "Start free course."

--------STILL TO DO
9. Watch this video where the lab manager gives you a tour of the NDCLab wiki and takes you through the steps to update your entry on the who's-who page.
--------STILL TO DO

9. Time to put it all together! Update your entry on the wiki's who's-who page using the new commands you've just learned:</br>
`git clone <link>`  </br>
`git branch whos-who-[yourname]`  </br>
`git checkout whos-who-[yourname]`  </br>
`git add whos-who.md` </br>
`git status`  </br>
`git commit -m "Added [yourname] to who's-who"`  </br>
`git push origin whos-who-[yourname]`

Don't forget to:
* Create your own branch, off the main branch, entitled "whos-who-[yourname]" (without the brackets).
* Switch to your branch before you start making any changes!
* Resize your photo to 100 x 100 pixels and copy it into the "whos-who" folder within "_assets".
* Name your photo simply as your last name. This way, you can reference it with</br>
`![name](https://raw.githubusercontent.com/NDCLab/wiki/docs/_assets/whos-who/name.jpg)`
* Nest your entry under your lab title, alphabetically by last name.
* Push all your changes back to the remote.
* Create a pull request and tag the lab manager (you can find the lab manager's GitHub handle on the page you just updated!) to review your changes and merge them into the live wiki!

10. After the lab manager has merged your changes, you have one more important mission. Review the wiki and identify (at least) one improvement that you think would help a future lab member. Create a new branch off the main branch (name it "dev-[improvement]-[yourname]"). Implement your suggestion and submit a pull request to the lab manager!