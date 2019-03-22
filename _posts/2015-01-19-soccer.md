---
layout: post
title: OSCP Third Week
tags: [oscp]
---

**Date:** 15 July - 21 July 2018 <br>
**PDF:** 380/380 <br>
**Videos:** 149/149 <br>
**Exercises:** 37/42 <br>
**Exploited Machines:** 50 <br>
(Alice, Alpha, Barry, Beta, Bethany, Bob, Brett, Carol, Carrie, Core, Cory, DJ, Dotty, FC4, Gamma, Gh0st, Helpdesk, Hotline, JD, James, Jeff, Joe, John, Kevin, Kraken, Leftturn, Luigi, Mail, Mario, Master, Mike, Niky, Nina, Observer, Oracle, Pain, Payday, Pedro, Phoenix, Pi, Punchout, Ralph, Sean, Sherlock, Slave, Sufferance, Susie, Timeclock, Tophat, Tricia) <br>
**Unlocked Networks:** 4 of 4 <br>
(Public, IT, Development and Admin)<br>
<br>

**Day 15**<br>
**Exploited Machines (2): Master and Bethany**<br><br>

**Day 16**<br>
**Exploited Machines (3): Nina, Niky and Jeff**<br><br>

**Day 17**<br>
**Exploited Machines (3): Carrie, Cory and Brett**<br><br>

**Day 18**<br>
**Exploited Machines (2): James and Timeclock**<br><br>

**Day 19**<br>
**Exploited Machines (2): Carol and John**<br><br>

**Day 20**<br>
**Exploited Machines (2): Mario and Luigi**<br><br>

**Day 21**<br>
**Exploited Machines (2): Pi (314159265) and Tricia**<br><br>

<p style="text-align: justify;">
Exploiting Master machine using the intended way indeed a long journey but its worthy. I think that's the way OffSec want us to learn, by doing proper post-enumeration and try figure out how the machine related with the others. This week I exploited 16 machines and unlock Development and Admin Network. This means I have successfully unlocked all of the networks in the lab. I am getting closer to achieve my personal challenges. </p>

<p align="center">
  <img src="https://raw.githubusercontent.com/arvandy/arvandy.github.io/master/img/oscp/control_panel.png">
</p>
<br>
<p style="text-align: justify;">
So far my opinion about the lab is the Public and Admin network more dominant on the kernel exploit and misconfiguration, the IT and Dev networks more about how well you do the post-exploitation, figuring relationship between the machines and client-side exploit. </p>
<br><br>
**TIPS:** <br>
<ul>
  <li align="justify">Dedicate yourself, refuse to give up! All the pain and sufferance will be gone when you finally did the root dance!</li>
  <li align="justify">If things start getting complicated and you think you are deep in rabbit holes, take a break. Check again your enumeration note and ask yourself if there are any steps you missed or some obvious/simple things you forget to do.</li>
  <li align="justify">Running NMAP with Proxychains is slow, especially on double pivoting. As an alternative, you can upload NMAP to the "pivot" machine and scan it from there or scan using NC.</li>
  <li align="justify">For double pivoting, I found this website explained it well and applicable.
https://pentest.blog/explore-hidden-networks-with-double-pivoting/</li>
</ul>
<br><br>
