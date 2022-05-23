## HackTheBox Cyber Apocalypse 2022 Intergalactic Chase

I’m back to HTB! This time with a new team which we called HackinKaNalang. Despite of our busy schedule we play this year Cyber Apocalypse CTF

-------------------------------------------------------
#### Web
- [Web 300 : Kryptos Support ](#kryptos_support)
- [Web 300 : BlinkerFluids ](#web2)

------------------------------------------------------
## Kryptos_Support
![](web1/1.png)

During my enumeration we got a field which you can submit via form then another page which is login portal

I submit a test content and we got this:

![](web1/2.png)

This a message  that give me a hint of possible XSS attack to get an Admin Cookies, and yes I send a crafted xss payload to get the admin cookies. Gotcha!

![](web1/3.png)

I install a cookie editor to use the session came from the results of my XSS attack.

![](web1/4.png)

Then I redirected to the admin panel and I dont see any field or upload files, just the ticket that I submitted, then I check the links and I found a change password field.

![](web1/5.png)

I notice that the account that I compromised is a moderator, Im thinking that there is an Admin account for this application.
I enable the inspect element functions of browser to check a hidden fields, then I found a UID.

![](web1/6.png)

I decided to edit the value to 1 and supplied my chosen password and click submit, then I  got this message

![](web1/7.png)

I login using admin and my chosen password and automatically redirected to Home Page with a Flag

![](web1/flag.png)

Conclusion: We able to get the flag since the application are vulnerable to Persistent XSS and IDOR or known as Insicure Direct Object Reference
------------------------------------------------------