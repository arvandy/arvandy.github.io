---
layout: post
title: OSCP Seventh Week (Exam)
tags: [oscp]
---


**Date: 12 August - 18 August 2018**
<br><br>
<p style="text-align: justify;">
Amazing Week! My exam scheduled on Wednesday, 15 August 2018 15:00 (Asia/Jakarta). One day before the exam, I take a rest from exploiting any machines and just making sure all the scripts, tools, notes and provisions are ready to use. I also prepare the contingency plan such as second internet connection and machine that ready to use in case some issues occurred in the middle of the exam.
</p>
<br>
<p style="text-align: justify;">
I simplified my enum script just to run the Nmap and OneTwoPunch tools. Nmap used to run a quick scan using -sV and -sC flag while the OneTwoPunch will run full TCP and UDP port scanning. I tried the script on the lab machines and its working fine. Single host scan took around 15-20 minutes to finish. There are five machines in the exam network with two 25 point machines, two 20 point machines, and one 10 point machine. The minimal points to pass is 70.
</p>
<br>

<b>This is the exam plan:</b><br>
15:00 - 15:15 = Check VPN connection, read exam instructions carefully and making note <br>
15:15 - 17:00 = Exploiting Machine 1 (25 Points) <br>
17:10 - 19:00 = Exploiting Machine 2 (10 Points) <br>
19:00 - 20:00 = Break <br>
20:00 - 23:00 = Exploiting Machine 3 (20 Points) <br>
23:00 - 04:30 = Sleep <br>
04:30 - 07:00 = Exploiting Machine 4 (20 Points) <br>
07:00 - 08:00 = Break <br>
08:00 - 11:00 = Exploiting Machine 5 (25 Points) <br>
11:00 - 12:00 = Break <br>
12:00 - 14:30 = Final check and gather necessary documentation 
<br>

<b>This is the actual:</b><br>
15:00 - 15:10 = Check VPN connection, read exam instructions carefully and making note <br>
<span style="color:blue">15:10 - 15:45 = Successfully exploiting machine 1 (25 Points)</span> <br>
15:45 - 15:55 = Ten minutes short break <br>
<span style="color:blue">15:55 - 16:10 = Successfully exploiting machine 2 (10 Points)</span> <br>
16:10 - 16:20 = Ten minutes short break <br>
16:20 - 17:00 = Working on machine 3 (20 points, stuck) <br>
<span style="color:blue">17:00 - 18:00 = Successfully exploiting machine 4 (25 Points)</span> <br>
18:00 - 18:10 = Collect necessary screenshots for machine 4 <br>
18:10 - 18:20 = Another ten minutes short break <br>
18:20 - 19:00 = Back working on machine 3 (Got access to certain service but no shell) <br>
19:00 - 20:00 = One hour break for dinner <br>
<span style="color:blue">20:00 - 20:42 = Successfully exploiting machine 5 (20 Points)</span> <br>
20:42 - 21:00 = Collect necessary screenshots for machine 5 <br>
21:00 - 21:10 = Another ten minutes short break<br>
21:10 - 23:00 = Working on machine 3 (Found another hidden service and privilege escalation vector but still no shell)<br>
23:00 - 04:30 = Sleep <br>
04:30 - 07:00 = Keep working on machine 3 (Nightmare, lead to nowhere) <br>
07:00 - 08:00 = One hour break for breakfast <br>
08:00 - 09:30 = Decided to skip the last machine and focus on triple checks the exam guidelines and gather necessary documentation screenshots <br>
09:30 - 12:00 = Going to college to finish some administration stuff <br>
12:00 - 14:45 = Start doing the exam reports <br>
<br>
<p style="text-align: justify;">
Overall the exam machines are not too hard but a little bit tricky with a few rabbit holes. Keep calm and stay focus. The exam did not require any advanced techniques or exploitation. All that you learned from the course and lab will get you through it. Don't get stuck too long on one machine when you still have other machines to exploits.
</p> <br>
<p style="text-align: justify;">
Before the exam, I read a lot of exams write up that a bit intimidating where some students fail the exam even after finish all the machines in the lab. Personally, I think the intimidating one is the exam rules itself, not the exam machines. The exam rules are very very strict and even if you success exploiting all the machines in the exam, you still will fail if you didn't follow the exam guidelines. That's one of the reasons I choose to skip the last machine and focusing on the documentation report.
</p> <br>
<p style="text-align: justify;">
I sent the exam and lab reports around 22:30 and get the receipt confirmation on 00:25 which states that the exams results will be received within 3 business days. This waiting time slowly killing me. I keep asking myself "did I break any exam rules? did my documentation report good enough? did I make any typing mistakes?". The anxiety on waiting for the exam results far worse than doing the actual exam. I feel ready and on-fire when doing the exam. 
</p> <br>
<p style="text-align: justify;">
Finally, at 18 August 2018 01:29, the email results arrived. It's faster than I expected. I passed the exam and officially obtained the Offensive Security Certified Professional (OSCP) certification. My first professional certification! OffSec did not provide the soft copy of the certificate and the hard copy will be delivered via DHL courier to my address. They tell me to expect the delivery within 60 days (Way too long but I hope it will be faster than that).
</p> <br>
<p align="center">
  <img src="https://raw.githubusercontent.com/arvandy/arvandy.github.io/master/img/oscp/results.png">
</p>
<br>
<p style="text-align: justify;">
I didn't write much about the technical things since there are a lot of very good resources out there. You need to learn to do your own research. Google-fu is one of the must-have skills when doing PWK course. By simply typing "OSCP cheat sheet" on Google, you will find a lot of good resources. Since this is once in a lifetime experiences, I decide to record my exam process in timelapse.
</p>
<br>
<div align="center" width="800" height="600">
  <a href="https://www.youtube.com/watch?v=wj6c4gbl6u4"><img src="https://img.youtube.com/vi/wj6c4gbl6u4/0.jpg" alt="IMAGE ALT TEXT"></a>
</div>
<br>
<p style="text-align: justify;">
I see a lot of people preparing for OSCP by learning about the operating system, programming, networking, etc and forgetting to actually learn to exploit vulnerable machines. It’s not wrong (I also did that at first), But for me, all of that not good enough if you did not know the techniques or the attack vectors. You can learn those stuff along the way when exploiting the vulnerable machines. The best thing to prepare is by actually start exploiting vulnerable machines, get comfortable enough and equip yourself with a lot of different attack vectors. The programming stuff required also only the basic one, you just need to able to read and modify the exploit code slightly. 
</p> <br>
<p style="text-align: justify;">
How to get such things? If you have a lot of time you can try exploiting vulnerable machines in VulnHub and HTB.  At first, it surely will be hard and frustrating since you will encounter a lot of new things. But if you really like this field, you will keep going and working on it, persevere, be committed and consistent! Everyone starts somewhere, don’t be ashamed of asking for a hint but make sure not to rely too much on it. Every master was once a beginner. Every pro was once an amateur. There’s no magic button. We just need to keep striving!
</p> <br>
<p style="text-align: justify;">
For people that don’t have much time to dedicate on it, simply watch IppSec videos and read the VulnHub write-up on your free time. You will have a lot of attack vectors in your pocket that will be applicable in PWK lab and exam. 
</p> <br>
<p style="text-align: justify;">
The other important things are the mindset and methodology. If we already set our mind to tackle this course, dedicate our time, commit and consistent about it, I am sure it’s achievable even if we didn’t have any pen-testing experiences. I also new in this field, didn’t have any certification and professional pen-testing experiences. For the methodology and tips, I post some of them on the weekly update in this blog including my OSCP preparation. I will try to wrap it up (preparation, lab and exam) into a single post in another one or two weeks, and at last, happy hacking!
</p> <br> <br>


