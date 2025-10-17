---
categories:
- Writeups
image:
  path: forgotten.png
  media_subpath: assets/posts/2025-10-17-htb-forgtten-writeup
layout: post
media_subpath: assets/posts/2025-10-17-htb-forgtten-writeup
tags:
- CTF
- Writeup
title: HTB - Forgotten writeup.
---
Forgotten is a Easy difficulty Linux machine from VulnLab that showcases several real-world techniques. It involves exploring a non finished LimeSurvey instalation and getting access to the admin panel, which is vulnerable to remote code execution. In order to escalate privileges, we must use a common folder between the container and the host user to transfer the bash file and become root.

## What is "FullHouse" about?
FullHouse is a simulated environment of an online casino. Our initial step is to perform a penetration test on its main website and identify multiple vulnerabilities. It consists of 7 different flags spread across 4 different machines that we need to hack into using various techniques. It personally took me much longer than anything else I’ve tried, mainly because it involved areas I wasn’t very familiar with yet — specifically, pentesting blockchain and AI bypass techniques.

## Difficulty and areas covered.

![fullhousestatus](fullhousestatus.png)

The lab is rated as Intermediate, though in my opinion, it feels more like "Intermediate to Advanced." The unusual scenario and the variety of advanced techniques might require you to spend a significant amount of time mapping things out and trying different approaches along the way. Be aware that this lab also requires a good understanding of programming languages and the ability to edit scripts, which made me struggle a bit at the beginning.

### These are:
1. Good knowledge of the main tools used when performing a pentest.
2. Familiarity with both windows and linux operating systems.
3. Webhacking techniques.
4. Programming.
5. Active Directory.
6. Pivoting.
7. Windows Powershell usage.
8. Bloodhound.

# Should you try it?
As I mentioned earlier, FullHouse is a very different experience and can definitely be a great opportunity to get into blockchain hacking, machine learning and AI bypass, as well as sharpen your programming skills. For me, it was certainly a great ProLab and totally worth trying, even though it took me quite a while to finish. And here’s the best part: it’s completely free! Not only can you test your skills, but you’ll also earn a very cool certificate upon completion. :)

![fullhousecert](fullhousecert.png)

Thank you so much for reading and best of luck! :)

## Useful links.
- [HacktheBox Penetration Tester Path](https://academy.hackthebox.com/path/preview/penetration-tester)
- [ProLabs Access](https://app.hackthebox.com/prolabs)
