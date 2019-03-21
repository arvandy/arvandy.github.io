---
layout: post
title: OSCP Preparation
tags: [oscp]
---

<p style="text-align: justify;">
Reading OSCP journey and write-up always motivates me to take the PWK course and obtains OSCP certification. By writing my own journey I hope it can motivate and encourages other people that share the same enthusiasm. Tuesday 5 June 2018, I completed PWK course registration with 60 days lab access that starts on 1 July 2018.
<br><br>
<b>My background</b>
<br>
As of now, I pursuing my master degree in information security and just finish up my second semester. Before continue my study on master degree, I have three years of IT professional experiences mostly in ERP, programming, and data management stuff. I have zero experiences on pen-testing, never exploit any vulnerable machines and rarely use Linux.
<br><br>
<b>Preparation Journey</b>
<br>
My preparation for OSCP started around September 2017. I started from the bottom, the only sort of "hacking" or exploit things I ever did was using Armitage on BackTrack for my college task, back in 2011. I never use Kali Linux before, didn't know what is bind/reverse shell, LFI, RFI, RCE and only know the theory of SQL injection but never really doing it. I do have basic knowledge on networking and programming, but If it comes to pen-testing I am totally blind.
<br><br>
<b>September 2017 - Finding resources</b>
<br>
At first, like any other newbies on this field, I am so clueless on where and how to start. I started with download bunch of e-books and hacking videos from YouTube. Although the e-book contains a lot of good information, I found it bored and hard to grasp the concept without actually practicing it. On the other hand, the videos I found only showing the straight way to exploits a machine without explaining how and why. I spend a lot of time trying to find right places that suit me.
<br><br>
<b>October to November 2017 - VulnHub and OverTheWire</b>
<br>
I joined Facebook group <a href="https://www.facebook.com/groups/oscpsg/" target="_blank">"OSCP Study Group"</a> and this group helps me find the right places to start. I found two great Pen-test platform from this group which is <a href="https://www.vulnhub.com/" target="_blank">VulnHub</a> and <a href="https://www.hackthebox.eu/" target="_blank">HackTheBox</a>. On 16 October 2017, I joined HackTheBox with the help of "google" to find the entry point for getting the invite code. After getting in, I didn't know what to do, all I can do at that time was just running Nmap scan. I have no idea what to do with the information from the Nmap since I never exploit any machines before. I decided it too soon for me to start there and shifting myself to VulnHub machine to learn the methodology from the write-up.

I download these VulnHub machines: Kioptrix series, Simple, Stapler, SickOs 1.2 and Quaoar, follow the write-up and trying to understand the methodology on exploiting a vulnerable machine. I didn't and can't exploit any of them on my own. After learning the methodology, I brush up my Linux and web security basic by doing OverTheWire challenges. I did OverTheWire Bandit (1-27) and OverTheWire Natas (1-10).
<br><br>
<b>November 2017 to Present - HackTheBox</b>
<br>
<b>19 November 2017</b>, After feel confident enough on the basic and methodology, I went back to HackTheBox and successfully exploit "Blue" machine. The first vulnerable machine that I exploit on my own. Even though its just as simple as firing the Metasploit, the feeling is amazing and made me addicted. From that time, I spent most of my free time practicing on the HackTheBox machines.
<br><br> </p>
<p align="center">
  <img src="https://raw.githubusercontent.com/arvandy/arvandy.github.io/master/img/oscp/owned_machine.png">
</p>
<br><br>
<p style="text-align: justify;">
In less than a month, I am able to exploits 12 of 20 active machines on HackTheBox. Overall I am happy with my progress, but there's one thing that keeps bothering me. I didn't exploit it all by myself, I got help/hint/pointer from my friends that I meet there. That thought keeps bothering me, I start questioning myself is this the right way to learn, is it okay to ask for a hint and if I continue this way is this gonna make me lazy to try harder. So far my methodology on exploiting those machines was jumping straight into the machines, reading the forum post, and a LOT of googling/research whenever I am stuck. If I still can't find the answer then I will be asking for hint/pointer, usually its some attack vectors/techniques/concepts that I am not even aware if its exist. Its a month of an exciting and sleepless night but I really enjoy the process and happy with the progress I made. I really learn a lot from each machine that I exploited.
<br><br>
<b>January 2018</b>, one month of college holidays, I went back to my hometown and take breaks from HackTheBox for almost a month. Spent this month reading learning resources from OSCP write-up and thinking whether I should continue learning this way or should I take a break from exploiting any machines and brush-up my basic so I don't rely too much on others to exploit the machine.
<br><br>
<b>February 2018</b>, I decided that the best learning method that suits me is learning by doing it. I convince myself its okay to ask for a hint as long as I made sure I have tried hard enough using everything I knew before asking for it. I take it as part of learning process. It's better to ask for hints rather than stuck for weeks without progress. Hints will make me proceed further and gains more knowledges. I still need to brush up some of my basic before went back to HackTheBox. I spent around one week doing this before went back:
<br><br>
<b>Linux</b>: <a href="https://linuxjourney.com/" target="_blank">Linux journey</a> (Grasshopper, Journeyman, Networking Nomad) and <a href="https://cmdchallenge.com/" target="_blank">CMD Challenges</a>.<br>
<b>PowerShell</b>: <a href="http://www.underthewire.tech/wargames.htm" target="_blank">UnderTheWire</a> (Century and Cyborg).<br>
<b>Linux Privilege Escalation</b>: <a href="https://exploit-exercises.com/nebula/" target="_blank">Exploit-exercise Nebula</a> (Level 01-11).<br>
<b>Python</b>: <a href="https://www.cybrary.it/course/python/" target="_blank">Cybrary: Python for Security Professional</a>.
<br><br>
<b>March 2018</b>, From reading a lot of OSCP write-ups, I know there's a machine on the OSCP exam that vulnerable to buffer overflow with the highest point. I have learned some basic Linux buffer overflow from exploiting HackTheBox machines but not yet touching Windows buffer overflow. I learn simple Windows buffer overflow using <a href="http://www.pentesteracademy.com/course?id=13" target="_blank">PentesterAcademy: Exploiting Simple Buffer Overflows on Win32 Course</a>. This course is amazing, it will guide you from the very basic and give you some exercises to actually practicing it. I highly recommend this course to learn basic overflow on win32, even though I don't know for sure if this course relevant with OSCP buffer overflow.
<br><br>
<b>April to May 2018</a>, I am near the end of the college semester. A lot of my time spent on college tasks. I still spare times practicing in HackTheBox and VulnHub machines that similar to OSCP: Kioptrix series, Stapler, PwnLab: Init, Fristileaks 1.3, SickOs 1.2, PwnOS, Quaoar, MR. Robot and Vulnix.
<br><br>
<b>June 2018</b>: Finish up my second semester and got almost three months holidays! The next semester will begin on 20 August. I spent this month on PWK registration and final preparations.



