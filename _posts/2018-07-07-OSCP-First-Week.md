---
layout: post
title: OSCP First Week
tags: [oscp]
---
<p style="text-align: justify;">
<b>Date:</b> 01 July - 07 July 2018 <br>
<b>PDF:</b> 380/380 <br>
<b>Videos:</b> 149/149 <br>
<b>Exercises:</b> 37/42 <br>
<b>Exploited Machines:</b> 14 <br>
(Alice, Barry, Bob, FC4, Gh0st, Helpdesk, Kraken, Mike, Pain, Payday, Phoenix, Ralph, Sherlock, Sufferance) <br>
<b>Unlocked Networks:</b> 1 of 4 </p>
<br>
**Day 1 - 4**
<br>
<p style="text-align: justify;">
The PDF contains 380 pages that spread over 18 chapters. The video's length is around 7 and half hours spread over 149 Videos. I spent around 30 hours doing the materials and exercises. There are five exercises that I decided to do it later since it requires to do it on the correct machines in the lab. The video and PDF fit together but the videos seem outdated and have some differences with the PDF. If you encounter any issues while following the syntax on course materials, use the syntax on the PDF one.</p>
<br>
**Day 4** <br>
**Exploited Machines (5): Phoenix, Alice, Helpdesk, Mike, Bob**
<br>
<p style="text-align: justify;">
I finish the course materials at 11:00 AM and start attacking lab machines in the afternoon. Phoenix was my first machine. I exploited five machines that day and all of them without using Metasploit. Modifying the manual script is not a big deal, you just need to pay attention to the comment section in the script and made necessary changes. One of the chapters in course materials also covers this topic. Bob privilege escalation technique is fun and the first time I encountered. </p>

<p style="text-align: justify;">
My impression after the first day on the OSCP lab is its simulates real-world scenario. So far all the exploit is known exploit and no puzzle or random guessing needed. All you need is proper enumeration to spot the vulnerability. </p>
<br>
**Day 5** <br>
**Exploited Machines (5): PAIN, Barry, Payday, Ralph, Sherlock**
<br>
<p style="text-align: justify;">
There are four hardest machines in the OSCP lab that known as The Big Four. Those machines are Pain, Sufferance, Gh0st and Humble. Feeling confident after exploiting five machines yesterday, this day I start with PAIN machine. I spent around 3 hours to fully exploited this machine. The low privilege shell is easy to spot and explained clearly in the course materials. The privilege escalation teach you to fully understand the exploit before using it. </p>
<br>
<p align="center">
  <img src="https://raw.githubusercontent.com/arvandy/arvandy.github.io/master/img/oscp/PAIN.png">
</p>
<br>
<p style="text-align: justify;">For Ralph, its required to think outside the box and Sherlock was a fun and unique machine. This day I also successfully exploited five machines.</p>
<br>
**Day 6** <br>
**Exploited Machines (2): SUFFERANCE and Kraken** <br>
**Low Privilege Shell (1): GH0ST** <br>
<p style="text-align: justify;">
This is where the suffering start. I start attacking SUFFERANCE on 04:30 for 10 hours straight! I take two regular breaks for breakfast and lunch about 2 hours with my mind keep thinking on how to tame this beast. The hardest part was getting a low privilege shell. The low privilege shell required us to know the old famous vulnerability. I am lucky I have read about this kind of vulnerability before from my OSCP preparation. The privilege escalation is straightforward and I have encountered this kind of privesc before. </p> <br>
<p align="center">
  <img src="https://raw.githubusercontent.com/arvandy/arvandy.github.io/master/img/oscp/SUFFERANCE.png">
</p> <br>
<p style="text-align: justify;">
At the night I start attacking GH0ST around 19:30 and got low privilege shell around 23:30. Right when I want to take sleep, an idea punch out then I power on my VM and got my low privilege shell! I spent one more hour trying to escalate the privilege but I am too tired to think clearly. I decided to take sleep and continue tomorrow. The low privilege shell for GH0ST is CTF-like one. The things about CTF-like machines is its force you to think creatively, outside the box and to TRY HARDER. </p>
<br>
**Day 7** <br>
**Exploited Machines (2): GH0ST and FC4** <br>
<p style="text-align: justify;">
After getting enough sleep, I successfully gain root access in 1 hour. Same as PAIN, understanding exploits playing an important role to exploit this machine.  In the afternoon, I exploited one more machine which is FC4. This machine is hard, fun and mind-blowing for me. </p> <br>
<p align="center">
  <img src="https://raw.githubusercontent.com/arvandy/arvandy.github.io/master/img/oscp/GHOST.png">
</p>
<br>
<br>
**TIPS:**
<ul>
  <li align="justify">You MUST do the course materials and exercises, it's a GEM. Even when you already familiar with most of the topics, it will become a refresher. When you attacking machines in the lab it will help you spot the “vulnerability” faster. I think it took around 30-50 hours to complete it. Sparing your time at the beginning for this can save your day later in the lab. </li>
  <li align="justify">In course materials and exercises, some of the tools are outdated and have version issues with Offsec Kali VM. If you encounter any issues, search the problem on the Offsec forum. Most of them are known issues and there are solutions available there.</li>
  <li align="justify">Don't just do nothing waiting for Nmap scan finish. Make some guess like checking if web service opens using the browser, checking if FTP, SSH or any other common services open using NC and do some manual enumeration while waiting.</li>
  <li align="justify">NMAP Scripts are powerful tools to check for vulnerability. Get familiar with it and play with the scripts. All of the scripts located in /usr/share/nmap/scripts/ directory.</li>
  <li align="justify">Most of the public exploits won't work without modifying it. It usually has hardcoded IP address and Path. Make sure you understand the exploit and change it as necessary.</li>
  <li align="justify">When compiling exploit, compile it on the environment (OS/kernel) that as close as possible with the target machine. If the target machine didn't have the compiler, the workaround could be downloading the same OS as target machine, install and compile it there, but it takes a lot of times. I found out that some of Vulnhub VM Machines that similar to OSCP can be used to compile the exploit too. I am using Kioptrix machines to compile the old exploit and it works so far. Saving time on downloading and installing new OS.</li>
<li align="justify">MSF is a powerful tool even though its restricted in the exam. Use MSF for post-exploitation, it makes your life easier to upload and download the file using Meterpreter shell. It also has many post-exploitation modules that really helpful.</li>
<li align="justify">For some of the straightforward machines, the methodology is simple: NMAP -> check service or software version for known vulnerability (searchsploit or google) -> read and understand the public exploit code -> make the necessary changes -> exploit.</li>
  <li align="justify">Google anything that you find suspicious or anything that you don't know at all.</li>
    <li align="justify">Spare your time to make write up after you exploit a machine. It will make you understand better your current methodology and how to improve it. Someday you may also encounter similar machines and it will help you.</li>
</ul>
<br><br>
