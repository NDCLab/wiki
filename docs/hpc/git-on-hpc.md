---
layout: default
title: Git on HPC
parent: HPC
nav_order: 8
---

### Contents
1. [Setting Up](#setting-up)
2. [How to Use](#how-to-use)


## Setting Up
1. [Log on](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node) to the HPC and access the terminal (Clusters > Panther Shell Access).
2. Run two separate commands in the terminal:
    1. Update your user name as your real name: `git config --global user.name "Mona Lisa"`.
    2. Set your user e-mail as the address you use to access the HPC (usually your student account): `git config --global user.email "mlisa001@fiu.edu"`.
3. Add your SSH key to GitHub. This involves extracting information from the HPC and inputting it to your GitHub settings.
    1. Use the code below to print your public key, if one already exists:
        `cat ~/.ssh/id_rsa.pub`
        **NOTE**: If you see this error (`cat: ~/.ssh/id_rsa.pub: No such file or directory`), that means that you don't have an RSA key set up yet, so simply continue to the instruction below.
    2. Generate a new key using the command: `ssh-keygen -t ed25519 -C "your_email@example.com"`. When it asks which file to save the key to, just hit `Enter`. When it asks for a passphrase, just hit `Enter` again (so there will be no passphrase). Details of this process are available [here](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).      
    3. This will print some information to the console, including the location of a `.pub` file.  Open this file using this command:
      `nano /home/<your-user-name>/.ssh/id_e25519.pub`
    4. This opens a file that shows you the key. It will look like: `ssh-ed25519 SUPERLONGSTRINGOFSYMBOLS`. Copy the key to your clipboard.
    5. Navigate to GitHub on a browser and log in.  Go to Settings > SSH and GPG Keys > New SSH key.
    6. Name your new key "fiuhpc" and paste in the key (from "ssh-ed" to the end of the very long string of symbols), then save.
4. Modify your SSH configuration file on the HPC.
    1. Input the command: `nano ~/.ssh/config`. **NOTE**: You probably will not have a configuration file, or it will be empty. In this case, copy and paste all 12 lines below ("Config File Contents") into the file.
    2. If you do already have a configuration file, make sure that the last four lines of the code below are included and that you do not have any line that reads: `UserKnownHostsFile /dev/null`. If you see it, remove that line. We are replacing it with the first line that you pasted into the file.
    3. To save the file and exit nano, do the following:
        1. ctrl+o (this is control on both Mac and PC)
        2. enter/return
        3. ctrl+x
6. Test by using `cd` to navigate into a folder where you have access.  Run `git status`.

**Config File Contents**
```
ForwardX11 yes
StrictHostKeyChecking no
FallBackToRsh no
ConnectionAttempts 5
UsePrivilegedPort no
Compression no
Cipher blowfish
UserKnownHostsFile ~/.ssh/known_hosts
CheckHostIP no
Host github.com
Hostname ssh.github.com
Port 443
```


## How to Use
You will want to treat the HPC as if it were simply another computer where your folder lives. Imagine the GitHub remote as the lynchpin and each of your computers (including your personal computer and the HPC) as residing on the end of a different spoke. Your goal is to make sure you always keep that lynchpin up-to-date, so that you can "refresh" your working copy before you make any changes each time you log in.

1. Before you do anything that adds, modifies, or deletes a file within the repository (either on the HPC or on your personal computer), do `git pull` to ensure you have the latest copy from the remote. (The only exception to this rule is the uploading of data to sourcedata/raw on the HPC, which is explicitly untracked by GitHub, and therefore does not care about any `git pull` procedure.)
2. After you make changes (for example, tweaks to a preprocessing or analysis script), use `git push` to update the GitHub remote. Again, this is true whether you are making those changes on your personal computer or directly to the copy on the HPC.
3. If you create branches other than `main` within your repo, ensure that you always leave the HPC on main (`git checkout main`) before you log off.  Checking out a branch on the HPC actually checks it out for all users, so by consistently returning to `main`, everybody has a shared baseline expectations for all project folders.