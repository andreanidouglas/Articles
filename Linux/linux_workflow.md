---
title: Moving your workflow to Linux
published: true
description: How to move your workflow to Linux and be free from Windows/Mac
tags: Linux, Workflow, Beginners, Ubuntu
---

Since forever, I've been a Windows user with almost zero knowledge of other Operational Systems. But I always found to develop inside Windows environments to be a little tricky since and if you are out of the Visual Studio environment things are even more complicated.

After a period considering a change to a MacOSX environment, I decided to try Linux, since it's free and work on (most) any hardware that works with Windows.


![Linux TUX](https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/TUX_G2.svg/2000px-TUX_G2.svg.png)

__HOW__:

First, you will need to choose a distribution (flavor) of Linux that will suit your needs. I like to recommend [Ubuntu Mate](https://ubuntu-mate.org/download/) to new users for a couple of reasons:

* It has the support and features of one of the most used distributions on the Linux world plus a great UI (Mate) that have a lot in common with other OS.

Just use [Etcher](https://etcher.io/) to burn the image into a USB stick and plug into the PC before booting it. Your BIOS/UEFI must be set to read from the USB. Follow the instructions on the screen to install the OS (Backup any relevant data first, because this will erase your HD).

__LANGUAGE SUPPORT__:

Most Linux distributions have a large support for programming languages, from C to GO, you will only need to find the correct package for your distribution. To start just run the command `sudo apt install build-essential` to have the most common toolchain for C/C++ compiling that will help to install a lot of other development software like:

* Python: `sudo apt install python2 python3 python3-pip`
* Java: `sudo apt install jdk8-openjdk`
* Javascript/Node: `sudo apt install nodejs npm`

*PS: `apt` is a command line tool to help install packages into the system, like brew for MacOSX or choco for Windows, used by Debian like systems (Debian, Ubuntu, Mint). You can learn more at [`man apt`](http://manpages.ubuntu.com/manpages/zesty/man8/apt.8.html)*




__TEXT EDIT__:

Most common text editors will work without any sweat, like Atom, Visual Studio Code, Sublime. Even some exclusive editors can make your life easier like Kate, Gedit, Geany and KDevelop.

__GIVE IT A TRY__:

If you are not comfortable to move an entire system to a Linux environment, you can still try it using some Virtual Machine environment, like VMWare Workstation or Oracle VirtualBox. You can see for yourself if it suits you and what you can learn from it.

__CONCLUSION__:

Linux systems are very powerful and fully feature to be your next development environment, just remember is not the same thing as Windows or MacOSX and you should approach it with an open mind. 

**And Remember** Google is your friend. Do not be afraid to search for dumb things such: *How to move a file from directory* or *How to install sublime on Linux*. You are learning everything again and some easy things should not stop you.  