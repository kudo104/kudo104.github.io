---
title: Owa Bakcdoor on Microsoft Exchange
slug: OwaBackdoor_ENG
date: 2024-6-11 00:00:00+0000
image: image.png
categories:
    - Malware
tags:
    - malware
    - C#
    - backdoor
---

## Overview
We can see that this is a C# file, using .NET Reactor for obfuscation to avoid analysis and detection by antivirus software.

![Picture 1](1.png)

## Unpack
I used .NETReactorSlayer to unpack, and you can see the difference before and after unpacking.

![Picture 2](2.png)

## Analysis 

### Stolen
The malware captures the `username` and `password` at `owa/auth` when login on Mail Exchange. The credentials are stored in C:\windows\temp\~ex.dat, XORed with 183, and then saved in base64 format.

![Picture 3](3.png)
![Picture 4](4.png)

~ex.dat file of the malware stores the following information:
- Timestamp
- Remote IP address
- Username and Password upon login

```
9/6/2024 3:39:01 PM	192.168.204.166	username pasword	Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36	302
```

### Connect

Attacker uses a special sessionid field to connect to the server, allowing them to execute commands and download anything.

![Picture 5](6.png)

![Picture 6](5.png)

## IOCs

> MD5: `A13E534F18967AF816FBE0EF83CC2AB8`

> File: `~ex.dat`