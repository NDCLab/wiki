---
layout: default
title: Data Encryption
parent: Technical Documentation
nav_order: 1
---

### Contents
1. [Overview](#overview)
2. [Study Passwords](#study-passwords)
3. [Download GPG](#download-gpg)
4. [Encryption](#encryption)
5. [Decryption](#decryption)

## Overview

Data encryption is an essential aspect of data security. It is the process of converting data into a code to prevent unauthorized access. GPG (GNU Privacy Guard) is a free and open-source encryption software that provides a secure way to encrypt and decrypt files. It is a popular tool used by individuals and organizations to protect sensitive data from unauthorized access. GPG uses a combination of symmetric-key encryption and public-key encryption to provide a secure way to encrypt and decrypt files. By using GPG, we can ensure that our data is protected from unauthorized access.


## Study Passwords

The NDCLab manager maintains a list of study passwords. All files encrypted for a particular data collection study should be encrypted with a password provided directly from the lab manager.


## Download GPG 

### MacOS
To download GPG on MacOS, visit [this link](https://gpgtools.org/). After downloading, install it on your Mac. The install procedure is a standard Mac package install.

### Windows
To download GPG on Windows, visit [this link](https://www.gpg4win.org/get-gpg4win.html). You can submit $0 for Paypal donation and then start downloading. After downloading, install it on your Windows machine. The installation process is similar to other regular Windows software. After installing, the software name is "Kleopatra." (Note: Kleopatra is already installed on the lab PCs in DM.)


## Encryption

### MacOS

1. To encrypt a file, right-click it, navigate to the “Services” sub-menu and click “OpenPGP: Encrypt File”.

![how_encrypt](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/how_encrypt.png)

2. Click on "Encrypt with password". Enter your encryption password and confirm it by re-entering it. Then, click on "Encrypt".

![how_encrypt2](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/how_encrypt2.png)

3. Test you have encrypted the file correctly, make a temporary copy of the encrypted in another folder. Try to decrypt (see below). After making sure that you have done it correctly, you can delete the original, un-encrypted file, as well as the encrypted and unencrypted versions of your temporary copy. 

### Windows

(Soon!)

### Linux (HPC)

It is generally preferable to encrypt files locally and then upload to the HPC. However, if you must encrypt on the HPC directly, follow the instructions below:

1. On the HPC virtual desktop, go to the directory that the file you need to encrypt exist. Right click inside the folder (right click on white space, not on a specific file) and then select “Open Terminal Here.”

![hpc_enc1](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/hpc_enc1.png)

2. This will open a black terminal window which will allow you to encrypt the files by typing commands into it.

3. First, copy the name of the file in the folder by right clicking on the file and selecting “Copy.”

![hpc_enc2](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/hpc_enc2.png)

4. Now go to the terminal window and type `gpg -c`, then click the spacebar once, and then right click and select paste. Press Enter.

5. You will be prompted to enter the encryption password. Type the password for this study. You will be asked to re-enter the password a second time to ensure it is entered correctly. Be very careful to enter the password correctly; if you encrypt the file with the wrong password, then we will be unable to open the file later for data coding and analysis.

![hpc_enc3](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/hpc_enc3.png)

6. After entering the password twice, an encrypted copy of the file will appear inside the downloads folder. The encrypted copy ends with “.gpg”.

7. Test decryption (see below). After making sure that you have done it correctly, you can delete the un-encrypted file. 


## Decryption

### MacOS

To decrypt a file, right-click it, navigate to the “Services” sub-menu and click “OpenPGP: Decrypt File”. Enter the password. If it does not work, it means that you are either trying to decrypt with the wrong password or you have used the wrong password to encrypt the file in the first place. You need to make sure that you are using the correct study password to encrypt/decrypt your files.

### Windows

(Soon!)

### Linux (HPC)

To decrypt a file on the HPC, simply double-click it. The decryption dialogue box will appear. Enter the password. If the decryption is successful, be careful to immediately remove the unencrypted file from the HPC (by right-clicking and selecting "Delete").  If decryption is unsuccessful, it means that you are either trying to decrypt with the wrong password or you have used the wrong password to encrypt the file in the first place. You need to make sure that you are using the correct study password to encrypt/decrypt your files.
