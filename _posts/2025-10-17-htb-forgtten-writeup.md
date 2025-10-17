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
Forgotten is an Easy Linux VM from VulnLab that was recently added to Hack the box. It involves exploiting an incomplete LimeSurvey installation to gain admin access (RCE) and then using a shared folder between the container and the host to transfer a bash script and escalate to root.


