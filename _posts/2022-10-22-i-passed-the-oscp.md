---
layout: post
title: Resources I Used to Pass the OSCP on my First Attempt
date: '2022-10-22 16:14:27 +0100'
categories: [Pentesting, OSCP]
tags: [oscp, pentesting, hacking, linux]
---

I recently passed the OSCP exam by [Offensive Security](https://www.offensive-security.com/) on my first attempt. This was a big moment for me, as it was something I had wanted for quite some time, and I had put a **lot** into preparing for it. It was a long and winding journey, spent almost exclusively in a chair, bathed in the light of a computer screen, often neglecting the needs of the flesh. It was also an exciting journey of learning, meeting great like-minded individuals, and realising that each failure can mean a future success if you learn its lesson. Needless to say, earning the certification was an extremely gratifying culmination of a lot of hard work.

Throughout my OSCP journey, I came across a lot of great resources that really helped me to build and refine my skill-set. In this post, I talk a little bit about my preparation for the exam, and have compiled some of the best resources I came across. The fact is that the PEN-200 course really does give you everything you need to pass the exam. However, these extra resources will flesh out your understanding, and provide alternate ways to approach things which can really give you an edge. I certainly haven't covered everything here, but it's my hope that this can serve as a useful reference for anyone who wants to tackle this certification.

### Labs worth practicing on

I primarily stuck to the machines on the [publicly available list](https://docs.google.com/spreadsheets/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/edit#gid=0) put together by [TJ_Null](https://twitter.com/tj_null).
This list was compiled with 'similarity to OSCP' in mind, by someone who works at Offensive Security, so it's worth focusing your efforts here.
It contains vulnerable machines from [HackTheBox](https://www.hackthebox.com/) and Offensive Security's own [Proving Grounds](https://portal.offensive-security.com/library/labs), where you can get practice exploiting scenarios that can approximate those you will face in the OSCP exam.

Before starting the PEN-200 course, I was pretty exclusively hacking on HTB, where I completed ~50 boxes. Basically all the HTB boxes on the 'TJ_Null list' are **retired machines**, which you need a subscription to access, so I highly recommend a VIP subscription(~$12/pm at time of writing). 

I then started the PEN-200 course. As an aside, before touching the lab machines, I completed nearly all the exercises in the course. I didn't watch any of the videos, I stuck to the PDF for learning, as I preferred it. How you go about doing things in the course is just personal preference, but make sure you leave yourself time for everything you need to do. Going through the courseware before the labs made sense for me. 

Going through the labs in the PEN-200 course itself, I completed around 65 boxes in total, this included several Active Directory sets. The more you can do the better, but make sure to do at least 30 to qualify for the 10 bonus points (You must also complete all Topic-Exercises).

When my lab time ended, I wanted to take a couple of weeks to do the **Proving Grounds Practice** boxes on TJ_Null's list, 
as I felt they would be a particularly good preparation for the OSCP machines.
On **PG Practice**, I completed nearly all of the 'TJ_Null list' machines, and shortly thereafter took the exam. **Proving Grounds** has two tiers. The free tier, **Play**, consists of only Linux machines. The paid tier, **Practice**, has both Windows and Linux (Plus all the **Play** machines). I would highly recommend subscribing(~$19/pm at time of writing), even for just one month, to tackle the TJ_Null **Practice** machines.

Practicing on the **Proving Grounds** boxes directly before taking the exam was helpful to me. Some people don't like to (or don't have time to) take a break between the end of their PEN-200 labs and the exam, but I found it worked well.

Another site that I haven't used personally, but have heard mention of quite a bit is [Virtual Hacking Labs](https://www.virtualhackinglabs.com/). It may be worth a look, but is by far the most expensive option.


### How to get better at Buffer Overflows

The course covers BOFs pretty extensively, but I found when it came to streamlining my approach, **Tib3rius**, author of the well-known [AutoRecon](https://github.com/Tib3rius/AutoRecon) tool, has provided a very concise and well documented methodology. You'll be overflowing buffers much more quickly if you study his BOF cheatsheet, and check out the links on the page too. If you get a chance, do the labs he has set up on **TryHackMe**, also linked below.

[Tib3rius Buffer Overflows Cheatsheet](https://github.com/Tib3rius/Pentest-Cheatsheets/blob/master/exploits/buffer-overflows.rst)<br>
[Tib3rius Buffer Overflow Practice lab](https://www.tryhackme.com/room/bufferoverflowprep)

### Learning Privilege Escalation

Apart from the course materials, I found some courses online that really helped me understand privilege escalation
for both Windows and Linux. I know it means extra cost, but if it's an option, I can't recommend these highly enough.

**Tib3rius**, that helpful fellow who created the BOF resources above, has also created two courses on Privilege Escalation,
one for Windows and one for Linux. They are both quite concise and to the point.

[Tib3rius Privilege Escalation Udemy courses](https://www.udemy.com/user/tib3rius/?src=sac&kw=tib3)

**TheCyberMentor** (aka Heath Adams) of TCMSecurity has also created Windows and Linux Privilege Escalation courses.
I think they are a bit longer than the Tib3rius offerings, but they are very worth the time.

[TCMSecurity](https://academy.tcm-sec.com/)

**Automated Enumeration**

Here are a couple of great enumeration scripts you'll want to be familiar with for the exam. Always know what your tools do, as any form of auto-exploitation is restricted in the OSCP. As of time of writing the following tools are allowed, but don't use them unless **you** are sure.

Windows & Linux - [PEASS-ng](https://github.com/carlospolop/PEASS-ng)<br>
Windows - [PrivescCheck.ps1](https://github.com/itm4n/PrivescCheck)<br>

**Enumeration Cheatsheets**

There are also plenty of Windows and Linux enumeration cheatsheets out there that are great. Here are a few

[Windows Enum - sushant747](https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html)<br>
[Windows Enum - FuzzySecurity](https://fuzzysecurity.com/tutorials/16.html)<br>
<br>
[Linux Enum - g0tmi1k](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)

### How to get better at pentesting Active Directory

Again, the course covers pretty much all you need to know about Active Directory in the context of the exam.
However, going the extra mile is always a good idea if you have the time. I could recommend the following 
resources.

[ippsec videos](https://ippsec.rocks/?#) - ippsec's youtube channel is a must watch for anyone tackling the OSCP. This special search
engine allows you to search for particular topics. The search results are links to the exact points in his videos where he deals with the topic. Try a search for 'Active Directory' and watch as much as you can! This goes for any topic too.

[TheCyberMentor](https://www.youtube.com/c/TheCyberMentor) - Search for his videos on Active Directory attacks. You can learn to build
your own attack lab, which will come in especially useful if you still have time for study after your PEN-200 lab time ends.

[adsecurity.org](https://adsecurity.org/) - This site contains a wealth of information about AD exploitation. Some of the articles can get pretty technical, but it's absolutely worth exploring.


### How to take notes

For me, how I take notes is tightly coupled with my methodology. I have a personal template that I use for every machine. This means I always know where to look for key pieces of information as and when I need them. It also makes it less likely I will overlook enumerating something, as it's easier for me to see when something is missing. On top of that, it makes me less likely to forget to consider previous findings I have already put in my notes, since it's been done in a structured way from the start, and I'm not looking at a mess of data that's hard to digest.

This is obviously a highly personal thing, but if you don't have a structured, consistent way of recording all your findings, I would recommend you get that down as soon as possible. It will save you a lot of energy down the line.

**Note-taking applications**

This is very down to the individual.
My preference for note-taking is [Cherrytree](https://www.giuspen.net/cherrytree/). I just like the interface, and the organisation
of all my notes into trees of 'nodes'.

Others I've talked to use [Obsidian](https://obsidian.md/), which seems to be a good option too. There are many applications you could use.
It's really just a matter of trying them out and finding what's best for you. In this sense, there isn't a 'best' option.

**Taking Screenshots**

For taking screenshots, I use [flameshot](https://flameshot.org/)<br>
I know there are other options out there, but **flameshot** does everything you need it to, and it's available
for both Linux and Windows.


### Youtube channels worth checking out

Here are just a few that are really worth your time.

[ippsec](https://www.youtube.com/c/ippsec) - Lots and lots of HTB Walkthroughs. Really a must watch, you will pick up so many tips and tricks that will not just help you in the labs, but in your career. An invaluable resource.<br>
[ippsec.rocks](https://ippsec.rocks/?#) - Not a Youtube channel, but a special search engine for ippsecs videos. You can search for almost any topic(Ex: Bloodhound) and are returned a list of links to all videos where he deals with that topic. Each link is cued right to relevant part of the video. <br>
[TheCyberMentor](https://www.youtube.com/c/TheCyberMentor) - Great videos on all aspects of penetration testing. I particularly found his videos on Active Directory very helpful - He has full instructional videos on building out your own AD lab for setting up and practicing enumeration and attacks.

### General Pentesting resources that really help
**Hack Tricks by Carlos Polop**<br>
[https://book.hacktrickz.xyz](https://book.hacktricks.xyz/welcome/readme)

This site is like the Wikipedia for pentesting. It covers pretty much every topic you could need for the OSCP. It shouldn't replace your notes, but it probably could!
<br>
<br>
**GFTObins**<br>
[GTFObins](https://gtfobins.github.io/)

"GTFOBins is a curated list of Unix binaries that can be used to bypass local security restrictions in misconfigured systems."
You need this site in your life. If you ever find an SUID binary, make sure to check for it here.
<br>
<br>

**The Pen-200 PDF!**

Seems like an obvious one. However, when you first get the course PDF, the sheer amount of information in there can feel overwhelming.
It takes quite a while to get through, and by the time you've reached the end, it's unlikely you've retained all that data. Remember that if you get stuck on something, it's always worth doing a Ctrl-F on the PDF as the vast majority of the information you need is in there in good detail. 

### Conclusion

The OSCP is hard, and even with the best preparation, the exam is sure to present a real challenge. But with a consistent, well practiced methodology you give yourself the best chance to pass. The more machines you exploit in labs, the more experiences you will have to add to your notes. Remeber, each failure is just a future success, if you use it to learn a lesson. All the best on your journey!





