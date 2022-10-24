---
layout: post
title: 'File Transfers: Part 1'
date: '2022-10-22 17:57:48 +0100'
categories: [Tutorial, OSCP]
tags: [linux, oscp, python, file-transfer, pentesting, code, tutorial, ctf]
---

This is part of a series of tutorials on file transfer methods for pentesting and CTF scenarios.

# Linux to Linux File Transfer

## Scenario

We have two Linux systems connected to the same local network

KALI             - 192.168.56.103
EXPLOIT-LAB      - 192.168.56.102

We have a file `exploit.py` that we want to transfer from KALI to EXPLOIT-LAB.

The file starts off on our Kali machine in `/tmp/transfers`.
As we can see, the `/tmp/transfers` directory on Exploit-lab is currently empty.

![ft1.png](/assets/img/ft1.png)
<br>
![ft2.png](/assets/img/ft2.png)

In order to transfer a file FROM a Linux machine, we need to make it accessible to a remote machine. 
There are a number of ways we can do this. However, for this tutorial we will be using the **Python HTTP Server**.

## Serving Files with Python HTTP Server

The setup is a very simple one-liner. The HTTP Server will serve all the files in the directory from 
which we execute the command. So the first step is to `cd` to the directory where the file(s) you want
to share reside.

**To start the HTTP server:**

### Python 3.x

`python3 -m http.server`

![http1](/assets/img/http1.png)

### Python 2.x

`python2 -m SimpleHTTPServer`

![http2](/assets/img/http2.png) 
<br>
As we can see from the screenshots above, the default port for the server is 8000. 
We can change that to a port of our choosing by adding it to the end of the command.

`python3 -m http.server 80`

Now we are ready to transfer our `exploit.py` file.

## Transferring Files

On our KALI system we start the HTTP server from the directory containing `exploit.py`.

![http1](/assets/img/http1.png)

From our UBUNTU system, we have a number of ways to transfer the file.

### 1. Web Browser

We browse to the file in a web-browser, making sure to include the right port in the URL, click on the file we want, and it will download to our system.

![browse-file](/assets/img/browsefile.png)




### 2. Wget

While there is no guarantee, it is common to find Linux systems will this tool installed. A GET request is a simple one-liner.
Here we have used the `-O` option, to output a file to a specified location.

`wget http://192.168.56.103:8000/exploit.py -O /tmp/transfers/exploit.py`

![wget](/assets/img/wget.png)
<br>
Looking back at our KALI system, we can see the GET request made by **wget**
![request1](/assets/img/request1.png)

### 3. Curl

Again, there is no guarantee that this tool will be present on a Linux system, but it is widely used, and if present on a system it also provides an easy method of performing a GET request. Here we have used the `-o` option to output the file to a specified location.

`curl http://192.168.56.130:8000/exploit.py -o /tmp/transfers/exploit.py`

![curl](/assets/img/curl.png)
<br>
Again, looking back at our KALI system, we can see the second GET request, this time made by **curl**
![request2](/assets/img/request2.png)

## Explore Your Tools

Both **wget** and **curl** have a large number of options and can be used to perform complex tasks.
It is well worth getting to know both of these tools better. The best way to do this is to check out
their **man pages** on Linux, and search for more info online.

Some good places to start would be finding out how to:

- Transfer multiple files with one command
- Perform POST requests

## Conclusion

I hope you found this tutorial helpful, thanks for reading!
