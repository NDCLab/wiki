---
layout: default
title: FileZilla
parent: Technical Documentation
nav_order: 3
---

### Contents
1. [Overview](#overview)
2. [Downloading FileZilla](#Downloading-FileZilla)
3. [Installing FileZilla](#Installing-FileZilla)
4. [Connecting to an FTP server](#Connecting-to-an-FTP-server)

## Overview

FileZilla is a free and open-source FTP client that allows you to transfer files between your local machine and a remote server. It is available for Windows, Mac, and Linux, and provides a user-friendly interface for managing your FTP connections. With FileZilla, you can upload and download files, manage your remote files, and edit files directly on the server. We can use it to download or upload files in bulk, either to or from the HPC. 

## Downloading FileZilla
To download FileZilla, go to the [official website](https://filezilla-project.org/) and click on the "Download FileZilla Client" button. This will take you to a page where you can choose your operating system (Windows, macOS, or Linux) and download the appropriate version of FileZilla.

## Installing FileZilla
Once you have downloaded FileZilla, run the installer and follow the on-screen instructions to install it on your computer. The installation process should be straightforward and only takes a few minutes to complete.

## Connecting to an FTP server
Now that you have installed FileZilla, you can use it to connect to an FTP server. To do this, follow these steps:

1. Launch FileZilla.
2. Click on the "File" menu and select "Site Manager".
3. In the Site Manager window, click on the "New Site" button.
4. Enter the following information:

    * Host: The hostname or IP address of the FTP server you want to connect to. In our case (as we want to connect to the HPC), use `hpclogin01.fiu.edu`.
    * Port: The port number of the FTP server. Use `22` for HPC. 
    * Protocol: Choose "FTP - File Transfer Protocol".
    * Encryption: Choose "Use explicit FTP over TLS if available".
    * Logon Type: Choose "Normal".
    * User: Your FTP username. (If you use your FIU student email to login to the HPC, this is your fiu email name without @fiu.edu; e.g., "khoss005").
    * Password: Use your FIU password.

5. Click on the "Connect" button.

If everything is entered correctly, FileZilla should connect to the FTP server (HPC) and display a list of files and folders on the server. You can now transfer files between your computer and the server by dragging and dropping them between the local and remote panes in FileZilla.

![filezilla](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/filezilla.png)

If you have any questions or run into any problems, don't hesitate to seek help from the 'tech' channel on the Slack.

