## ROOTCON 15 Capture The Flag

I’m back to ROOTCON CTF! This time with a new team which we called Squid Gamers. Yes, we joined the hype! Special thanks to my teammates, Cyber3n, and Zem3ck1s for doing their best during their free time solving the challenges. Though we didn’t win CTF we still get to enjoy the game and learn a lot which is for me is still a win. Plus a bonus real win for getting the top score in Hacker Jeopardy which gives us our first Black Badge. Not bad for first time in Rootcon HJ. And we also made the goons drink so much!

Before I totally lost focus, let me go back on the CTF Web challenge — 200 points. Just like with my previous writeup from last year's event, during Rootcon Recovery Mode, I’ll walk through the steps I did to solve the challenge, which turns out to be the first blood of the game.

-------------------------------------------------------
#### Web
- [Web 200: You can't see me!](#web200)



------------------------------------------------------

## Web200
![](1.png)

Let's Go!!

Challenge Writeups

Category: Web

Challenge: You can’t see me!

Points: 200

![](2.png)

The IP address above directed me to the PHP code below.

![](3.png)

### Analysis
LINE 7 is the inclusion of the file flag.phpbut we can't see the source code.
LINE 11 is to GET request accepting 2 parameters. If you look closely the font used for the letter C in rootcon is different in the 2nd get request. The condition tells us that these 2 parameters should not be equal.


