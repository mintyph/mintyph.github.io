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

Time to keep enumerating, now fuzzing for subdirectories:

```
➜  Forgotten ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.129.234.81/FUZZ -fs 278

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.129.234.81/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 278
________________________________________________

survey                  [Status: 301, Size: 315, Words: 20, Lines: 10, Duration: 265ms]
```

Accessing the /survey directory exposed a partially completed LimeSurvey installation, indicating setup steps were incomplete and left the instance in a misconfigured state.

![LimeSurvey](limesurvey.png)

### Exploitation

The LimeSurvey installer requires a MySQL database, so we must run a local MySQL service before proceeding with the installation.

```
sudo docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mysql:latest
```

![Installed](installed.png)

Once the LimeSurvey installation is finished, we can access the admin interface by authenticating with the credentials defined during the setup process.

![Admin](admin.png)

Upon logging in, the admin interface indicates LimeSurvey **6.3.7+231127** is running. Public advisories report that this version is susceptible to an **authenticated remote code execution (RCE)** vulnerability.







