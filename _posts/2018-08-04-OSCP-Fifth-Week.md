---
layout: post
title: OSCP Fifth Week
tags: [oscp]
---

<p style="text-align: justify;">
<b>Date:</b> 29 July - 04 August 2018
<b>PDF:</b> 380/380
<b>Videos:</b> 149/149
<b>Exercises:</b> 42/42
<b>Exploited Machines:</b> 53
(Alice, Alpha, Barry, Beta, Bethany, Bob, Brett, Carol, Carrie, Core, Cory, DJ, Dotty, FC4, Gamma, Gh0st, Helpdesk, Hotline, Humble, Internal, JD, Jack, James, Jeff, Joe, John, Kevin, Kraken, Leftturn, Luigi, Mail, Mario, Master, Mike, Niky, Nina, Observer, Oracle, Pain, Payday, Pedro, Phoenix, Pi, Punchout, Ralph, Sean, Sherlock, Slave, Sufferance, Susie, Timeclock, Tophat, Tricia)
<b>Unlocked Networks:</b> 4 of 4
(Public, IT, Development and Admin)</p>
<br>
<p style="text-align: justify;">
This week activity consists of reading my own write-up for machines in the lab, compiling frequently use commands into a single note, creating enumeration script, and start re-exploiting machines in the lab. The enumeration script only does Nmap, Enum4linux, Nikto and Gobuster scan and save the output into a file. These tools took more times to run, especially Nmap and Nikto so it will be wise to run it as soon as possible. </p>

<p style="text-align: justify;">
After start re-exploiting machines in the lab, I found an issue with my enum4linux tool. I remember these tool revealed important information to exploit the machine before, but now it keeps saying "null session not allowed". Turn out this issue occurred because I update my smbclient when attacking certain machine before. I tried downgrading the smbclient but keep getting dependency and repository issue, so I decide to revert the VM to the original state. Before doing revert, I back up all the necessary files on current VM and take the snapshot. </p>

<p style="text-align: justify;">
I suggest not to upgrade or update any tools in the VM since It will cause the unnecessary issue later. If you need to use certain updated tools, use it on another Kali VM.
</p>
