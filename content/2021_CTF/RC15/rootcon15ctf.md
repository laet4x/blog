## ROOTCON 15 Capture The Flag

I’m back to ROOTCON CTF! This time with a new team which we called Squid Gamers. Yes, we joined the hype! Special thanks to my teammates, Cyber3n, and Zem3ck1s for doing their best during their free time solving the challenges. Though we didn’t win CTF we still get to enjoy the game and learn a lot which is for me is still a win. Plus a bonus real win for getting the top score in Hacker Jeopardy which gives us our first Black Badge. Not bad for first time in Rootcon HJ. And we also made the goons drink so much!

-------------------------------------------------------
#### Exploitation
- [Exploitation 4](#exploitation4)
- [Exploitation 6](#exploitation6)

#### Web
- [Web 200: You can't see me!](#web200)




------------------------------------------------------
## Exploitation4
![](exploitation4/exploitation4.png)

This challenge need to read the /flag.txt file

During our enumeration we found the **Elasticsearch Directory Traversal (CVE-2015-5531)** vulnerabilities

Description:
Directory traversal vulnerability in Elasticsearch before 1.6.1 allows remote attackers to read arbitrary files via unspecified vectors related to snapshot API calls.

![](exploitation4/exploitation4_1.png)

We change the path to /flag.txt to read the file. But we got encoded data.

![](exploitation4/exploitation4_2.png)

We used some online decoding tools to decode the data from decimal into ascii.

![](exploitation4/exploitation4_3.png)

![](exploitation4/exploitation4_4.png)

Flag: **RC15{J5ekuUdMY7BLZmktYCXzWZhZZ4J3W8pv}**

------------------------------------------------------
## Exploitation6
![](exploitation6/exploitation6.png)

This challenge requires us to get shell access to the server.

Based on our enumeration using Ridgebot, one of the vulnerablities of the server is **Shellshock Remote Code Execution (CVE-2014-6271).**

Description: GNU Bash through 4.3 processes trailing strings after function definitions in the values of environment variables, which allows remote attackers to execute arbitrary code via a crafted environment, as demonstrated by vectors involving the ForceCommand feature in OpenSSH sshd, the mod_cgi and mod_cgid modules in the Apache HTTP Server, scripts executed by unspecified DHCP clients, and other situations in which setting the environment occurs across a privilege boundary from Bash execution, aka 'ShellShock.'

I use ngrok since i dont have any VPS to create a tunnel to my kali machine

![](exploitation6/exploitation6_1.png)

I replace the payload with one-liner reverse shell

![](exploitation6/exploitation6_2.png)

I prepare my netcat listener, then i hit enter  then i got a reverse shell connection

![](exploitation6/exploitation6_3.png)

Inside the server, i found the image which contains the flag

![](exploitation6/exploitation6_4.png)

Flag: **RC15{sXpbTeFkvtXALSTpT2Fd866774kA5kzp}**

------------------------------------------------------

## Web200
![](web200/1.png)

Let's Go!!

Challenge Writeups

Category: Web

Challenge: You can’t see me!

Points: 200

![](web200/2.png)

The IP address above directed me to the PHP code below.

![](web200/3.png)

### Analysis
LINE 7 is the inclusion of the file flag.phpbut we can't see the source code.

LINE 11 is to GET request accepting 2 parameters. If you look closely the font used for the letter C in rootcon is different in the 2nd get request. The condition tells us that these 2 parameters should not be equal.

![](web200/4.png)

I manually copied the word and verified it using URL decoding.

![](web200/5.png)

Now we have our URL without a value:

http://149.28.134.167/?rootcon=&root%D1%81on=

Let’s analyze the next line, which is LINE 12, which indicates that the 2 md5hash must be equal.

![](web200/6.png)

It reminds me of my previous writeup for Rootcon Recovery Mode last year about magic hash. You may check it from this link below [https://laet4x.medium.com/rootcon-recovery-mode-ctf-final-web-wizardry-1419d664eedf](https://laet4x.medium.com/rootcon-recovery-mode-ctf-final-web-wizardry-1419d664eedf).

So I decided to reuse the script. Basically, this script will find word/s to combine with the word ‘pwndemanila’, which in return will results in “0e” + 30 digits MD5 hash.

![](web200/7.png)

After several minutes I got the results:

![](web200/8.png)

Solution:

pwndemanilaaffyjL = 0e154876879366669632612315475677

pwndemanilaa1MGTc = 0e660685420749161809595800684366

Anything that starts with “0e”, followed strictly by only digits will return TRUE, which makes LINE 12 TRUE.

This is also what we need in LINE 11 since we remove the ‘pwndemanila’ we got pffyjL and a1MGtc and make LINE 11 TRUE.

I crafted our final URL and we Got the flag:

http://149.28.134.167/?rootcon=ffyjL&root%D1%81on=a1MGTc

![](web200/9.png)

Flag: **RC15{tqfXZWoEvj4ukK5WJGAPqTfBRs7iTN}**

Special Thanks!

I would like to thanks pwndemanila and rootcon for the exciting challenges in this year’s Capture The Flag. Shoutout to our another team, SOCTEAM CTF for the support. See you next year!!!

[https://www.rootcon.org/](https://www.rootcon.org/)

[https://twitter.com/rootconph](https://twitter.com/rootconph)

[https://www.facebook.com/rootcon/](https://www.facebook.com/rootcon/)