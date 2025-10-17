---
categories:
- Writeup
image:
  path: forgotten.png
  media_subpath: /assets/posts/2025-10-17-htb-forgotten-writeup
layout: post
media_subpath: /assets/posts/2025-10-17-htb-forgotten-writeup
tags:
- Writeup
- CTF
title: HTB Forgotten writeup
---
Forgotten is an Easy Linux machine from VulnLab, recently added to Hackthebox. It involves exploiting an incomplete LimeSurvey installation to gain admin access (RCE) and then using a shared folder between the container and the host to transfer a bash script and escalate to root.

# Reconnaissance / Scanning

Nmap scan results:

```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 28:c7:f1:96:f9:53:64:11:f8:70:55:68:0b:e5:3c:22 (ECDSA)
|_  256 02:43:d2:ba:4e:87:de:77:72:ce:5a:fa:86:5c:0d:f4 (ED25519)
80/tcp open  http    Apache httpd 2.4.56
|_http-server-header: Apache/2.4.56 (Debian)
|_http-title: 403 Forbidden
| http-methods: 
|_  Supported Methods: POST OPTIONS HEAD GET
```
An initial HTTP request to the webserver returned a 403 Forbidden response (HTTP/1.1 403), indicating access to the requested resource is denied.

![Forbidden](forbidden.png)
