---
layout: default
title: Git on HPC
parent: HPC
nav_order: 8
---

### Contents
1. [Setting Up](#setting-up)
2. [Guidance](#guidance)


## Setting Up
1. [Log on](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node) to the HPC.
2. Set your user name as your real name:
```
git config --global user.name "Mona Lisa"
```
3. Set your user e-mail as the address you use to access the HPC (usually your student account):
```
git config --global user.email "mlisa001@fiu.edu"
```
4. Add your SSH key to GitHub
    1. Use the code below to print your public key:
        `cat ~/.ssh/id_rsa.pub`
        **NOTE**: If you see this error (`cat: ~/.ssh/id_rsa.pub: No such file or directory`), that means that you don't have an RSA key set up yet. Follow the instructions [here](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to generate one. When it asks for the file to save the key to, just hit `Enter`. When it asks for a passphrase, just hit `Enter` (so there will be no passphrase).
    2. Copy the key to your Clipboard, then paste it to your GitHub account settings (on the website: Settings > SSH and GPG Keys > New SSH key).  Name it "fiuhpc".
5. Modify your SSH configuration file
    1. `nano ~/.ssh/config`
        - **NOTE**: If you do not have a config file (or if it is empty), then copy [the example one from this repository](https://github.com/FIU-Neuro/Onboarding/blob/master/templates/.ssh/config) into your .ssh folder.
    2. Add the following lines:  
        - > UserKnownHostsFile ~/.ssh/known_hosts   
          > Host github.com  
          > Hostname ssh.github.com  
          > Port 443<br/>

    3. You may see the following line somewhere in the file:
        `UserKnownHostsFile /dev/null`
        - If you see it, remove that line. We are replacing it with the first line that you pasted into the file.
    4. To save the file and exit nano, do the following:
        1. ctrl+x (this is control on both Mac and PC)
        2. y
        3. enter/return
6. Test by using `cd` to navigate into a folder where you have access.  Run `git status`.


## Guidance
You will want to treat the HPC as if it were simply another computer where your folder lives. Imagine the GitHub remote as the lynchpin and each of your computers (including your personal computer and the HPC) as residing on the end of a different spoke.  Whenever you interact with your files on any computer:
1. First use `git pull` to make sure you have the latest copy from the remote.
2. After you make changes, use `git push` to update the remote.
3. If you create branches other than `main` within your repo, ensure that you always leave the HPC on main (`git checkout main`) before you log off.  Checking out a branch on the HPC actually checks it out for all users, so by consistently returning to `main`, everybody has a shared baseline expectations for all project folders.