---
categories:
- Writeup
image:
  path: forgotten.png
  media_subpath: /assets/posts/2025-04-05-htb-forgotten-writeup
layout: post
media_subpath: /assets/posts/2025-04-05-htb-forgotten-writeup
tags:
- Writeup
- CTF
title: HTB Forgotten writeup
---
Forgotten is an Easy Linux machine from VulnLab, recently added to Hackthebox. It involves exploiting an incomplete LimeSurvey installation to gain admin access (RCE) and then using a shared folder between the container and the host to transfer a bash script and escalate to root.
