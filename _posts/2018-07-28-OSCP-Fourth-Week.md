---
layout: post
title: OSCP Fourth Week
tags: [oscp]
---

<p style="text-align: justify;">
**Date:** 22 July - 28 July 2018 <br>
**PDF:** 380/380 <br>
**Videos:** 149/149 <br>
**Exercises:** 42/42 <br>
**Exploited Machines:** 53 <br>
(Alice, Alpha, Barry, Beta, Bethany, Bob, Brett, Carol, Carrie, Core, Cory, DJ, Dotty, FC4, Gamma, Gh0st, Helpdesk, Hotline, Humble, Internal, JD, Jack, James, Jeff, Joe, John, Kevin, Kraken, Leftturn, Luigi, Mail, Mario, Master, Mike, Niky, Nina, Observer, Oracle, Pain, Payday, Pedro, Phoenix, Pi, Punchout, Ralph, Sean, Sherlock, Slave, Sufferance, Susie, Timeclock, Tophat, Tricia) <br>
**Unlocked Networks:** 4 of 4 <br>
(Public, IT, Development and Admin)</p><br><br>

**Day 22**<br>
**Exploited Machines (1): Jack**<br><br>

**Day 23**<br>
**working on Internal**<br><br>

**Day 24**<br>
**Exploited Machines (2): Internal and Humble**<br>

<p align="center">
  <img src="https://raw.githubusercontent.com/arvandy/arvandy.github.io/master/img/oscp/HUMBLE.png">
</p>
<br>
**Day 25 - Day 28**<br>
**Doing Lab Report and Remaining Exercises**<br><br>
<p style="text-align: justify;">
I just realized the "Big Four" term is not from OffSec, its the term created by the students due to the difficulty of the machines. I found there are several machines that more difficult for me to exploits than the Big Four. My version of Big Four will be Jack, Humble, Sufferance and Observer. Those machines required a lot of enumerations, troubleshooting and fuzzing to gains the low privilege shell. It required more works and patience compared to other machines in the lab. The privilege escalation on those machines is easier compared to the effort to gain the low privilege shell.</p>
<br>
<p style="text-align: justify;">
My lab report has the total of 145 pages with the first 74 pages are the pen-test report for 10 machines in the lab and the remaining pages for the PWK Course exercises. I am following the template provided by OffSec with this structure:</p>
<br>
1.0 High-Level Summary<br>
     1.1 Recommendations<br>
2.0 Methodologies<br>
     2.1 Machine 1<br>
           2.1.1 Service Enumeration<br>
           2.1.2 Penetration<br>
           2.1.3 House Cleaning<br>
     2.2 Machine 2<br>
     ......<br>
     2.10 Machine 10<br>
3.0 PWK Course Exercises<br>
<br>
<p style="text-align: justify;">
Until now, I didn't use or create any scripts for automating enumeration in the lab. I just did it manually using built-in tools like NMAP, Nikto, NC, Gobuster, Enum4linux, etc. Since time factor is important in the exam, I will try to make a script to run simple enumeration such as saving Nmap output to file, run Nikto and Gobuster if web service exists, run Enum4linux if samba service exists, etc. It will save a lot of times to run it in the background while spending time exploiting another machine.</p>
<br><br>
**TIPS:**
<br>
<ul>
  <li align="justify">"All Roads Lead to Rome". If you exploiting the machine and for some reasons it cannot talked back to your machine, understand how the PWK lab network works and find another route to reach the target.</li>
  <li align="justify">A certain machine in the lab "hates" automated tools. If your Nmap, Nikto, Gobuster or any automated tools failed to run, don't waste your revert on the machine. Instead, do manual enumeration on the service. </li>
  <li align="justify">It's obvious public exploits rarely work without modifications. Try fuzzing and troubleshoot the public exploit to get simple command works first rather than directly trying to get the shell.</li>
  <li align="justify">Some exercises in the PWK course asking to do exploit using automated tools and then replicate the exploit manually. The verbose options on the automated tools can help you find the correct payload to replicate it manually.</li>
</ul>
<br><br>
