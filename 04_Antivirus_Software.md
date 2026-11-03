## 1. Startup and file protection

First, antivirus software works in kernel mode, on the same level as anti-cheat software and the operating system. What you see is only its interface. It can hide from Task Manager or even change Task Manager. Rather than a piece of software, it is more like "xxx."

Most importantly, antivirus software should start with the operating system, before all other software. It then scans new files, analyzes them, and marks them. It also filters programs when they start. The operating system's APIs are actually intercepted by the antivirus, so programs without permission cannot run. A program that has just arrived on the disk and has not been scanned cannot run either. This is real-time file protection.

## 2. File and behavior analysis

The methods of identifying threats are complex and differ between companies. They mainly examine file structure and patterns. A pattern can be a hash, which works well for viruses that are already widespread. They can also check certain bytes, such as a section of highly matching binary code.

Next comes file analysis, including the Windows PE structure. It becomes more complex from there. For example, the software checks whether a file is packed, encrypted, compressed, or hiding things in other ways.

Dynamic analysis has a high chance of false alarms. It judges a program by its live behavior, such as downloading files, changing the registry, creating tasks, or injecting into processes. It also examines the startup chain and how the software was installed, such as from a website or a USB drive.

## 3. System and runtime protection

Antivirus software also needs memory scanning. This is similar to real-time file protection, but checks code in memory. It can make games and other programs stutter.

Signatures are also very important, because they directly determine reputation. The issuing company can affect the trust level. I must be clear: in many cases, antivirus software can stop you from using a program even after you have explicitly allowed it and given it administrator rights. This seems to be a problem with the antivirus built into Windows.

Even when antivirus software is turned off, the system still has basic protection. You also do not need to worry too much about a virus changing operating system files so that a fake system starts next time. The motherboard has protection and checks the operating system's signatures. The operating system also verifies things as it loads.

Other API protection covers startup options, the registry and other sensitive settings, and protection against DNS changes. Some functions are more dynamic and need an internet connection, such as live protection against vulnerabilities. If a program is reported to have a vulnerability and may be attacked, the antivirus gives it special attention. It blocks attempts to use the vulnerability.
