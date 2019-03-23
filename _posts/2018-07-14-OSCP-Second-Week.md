---
layout: post
title: OSCP Second Week
tags: [oscp]
---
<p style="text-align: justify;">
<b>Date:</b> 08 July - 14 July 2018 <br>
<b>PDF:</b> 380/380 <br>
<b>Videos:</b> 149/149 <br>
<b>Exercises:</b> 37/42 <br>
<b>Exploited Machines:</b> 34 <br>
(Alice, Alpha, Barry, Beta, Bob, Core, DJ, Dotty, FC4, Gamma, Gh0st, Helpdesk, Hotline, JD, Joe, Kevin, Kraken, Leftturn, Mail, Mike, Observer, Oracle, Pain, Payday, Pedro, Phoenix, Punchout, Ralph, Sean, Sherlock, Slave, Sufferance, Susie, Tophat) <br>
<b>Unlocked Networks:</b> 2 of 4 <br>
(Public, IT) </p>
<br>

**Day 8**<br>
**Exploited Machines (3): Tophat, Dotty, Leftturn**<br><br>

**Day 9**<br>
**Exploited Machines (3): DJ, Susie, Oracle**<br><br>

**Day 10**<br>
**Exploited Machines (3): Hotline, Alpha, Beta**<br><br>

**Day 11**<br>
**Exploited Machines (3): Gamma, Core, Kevin**<br><br>

**Day 12**<br>
**Exploited Machines (3): Mail, JD, Punchout**<br><br>

**Day 13**<br>
**Exploited Machines (3): Pedro, Sean, Joe**<br><br>

**Day 14**<br>
**Exploited Machines (2): Slave and Observer**<br><br>
<p style="text-align: justify;">
This week I exploited 20 machines and unlock IT Network. Pivoting required to exploits the machines in IT network, personally I use Proxychains with socks4. The lab getting harder and interesting, some of the machines cannot be exploited directly. To exploit them the relationship between machines must be find out first. Some of the machines have easy or unintended way to exploit but it always better to do the intended way, it teach a lot. </p>
<br>
<p style="text-align: justify;">
For the last couple of days, I keep checking the exam slot availability. The slot has been filled till 20 August, but today I check and found the slot on 14 and 15 August. It could be some of the students rescheduled their exams date. I decide to scheduled my exam on 15 August, 15:00. </p>
<br>
**TIPS:**
<ul>
  <li align="justify">POST Enumeration is really important. Make sure you do and document it or you gonna need to return to all of the machines you have been exploited.</li>
  <li align="justify">Some binaries/executables on the machine not located in the default PATH. If your rev-shell/RCE didn't work, enumerate more.</li>
  <li align="justify">Client-side exploit require more times to be executed. Be patient.</li>
  <li align="justify">If you encounter login page of certain software, first things you need to do is looking for its default login credentials on google.</li>
  <li align="justify">Developer guide manual of certain software can be a good resource if you unfamiliar with the software.</li>
  <li align="justify">If you see a lot of ports open from NMAP result, go for the low hanging fruit first such as Samba and FTP.</li>
  <li align="justify">After you get low privilege shell, make sure you spawn TTY shell. Some exploits won't work without TTY shell.</li>
</ul>
<br><br>
