---
layout: post
title: Using Fedora for a week
categories:
- Distros
- Linux
- Fedora
tags:
- fedora
- linux
- distros
status: publish
type: post
published: true
---

A week ago I decided to try a different GNU/Linux distro for my desktop. I use
[Debian](http://debian.org) for many years and I like to try a new distro now
and then, you know, just to leave my comfort zone for a while.

The distro for the week should be different from what I'm used to, so the many
Debian flavors were not an option (Like Ubuntu, Linux Mint, etc).

![Fedora Project](/assets/images/fedora-logo.png)

So I made a quick research and ended up choosing [Fedora](http://fedoraproject.org).
Actually it would be [CentOS](http://centos.org), but Fedora is basically the
same RedHat flavor with more up to date packages.

### Installation

The installation process was pretty simple and I was able to keep my home
partition with all my data.

The installer is easy to use and I had just a small problem to set up the
keyboard map to Brazilian. The problem was that after the installation the
default keyboard map was automatically set up to English again (I think that's
because I installed the system in English).

### First boot

I really like the [XFCE](http://xfce.org) desktop environment, so for the week
I chose the XFCE Fedora's version. Unfortunately I had problems in the first
boot.

For some reason the installer changed the user permissions of my home dir and
I could not login using the login manager. I tried to login and it push me back
to the login screen with no alerts of what was going on.

Then I used the root user to investigate and fix the problem. After that I was
able to login to XFCE.

### Softwares

Package installation was very easy using **yum**. Yum is simple to use via cli
and I had no problem using it since I'm used to manage packages using **aptitude**.

Of course I had no problem using the default Fedora packages. But things were
not so easy when I needed some packages that were not in the official repositories.

An example is the Chromium browser. I added an extra repository and I could
install it, but it crashed every time I typed an @. Google Chrome had the same
problem. Firefox worked perfectly, but it's in the official repository.

Skype was pretty easy to install. I used the Fedora 16 32 bits' version and the
installation was simple using a GUI. I didn't even need to solve the 32 bits
dependencies.

The development environment was also simple to install, I just had to get used
to the location of the config files that were different from Debian's. I
installed a basic LEMP environment, package by package, with no help from tools
like Ansible.

Flash player didn't work, and that's all. I was not in the mood to try to make
it work.

### Conclusion

I think Fedora is pretty good for the Desktop and also for a development
environment. I had some problems with a small number of packages but I liked
the distro.

Of course that was not enough to make me switch to a new distro, and that's why
I stuck to the original plan of using it for only one week. Now I'm back to
Debian :)

The experience was very nice and I recommend to all GNU/Linux users to try it
to. If you use Fedora, try Debian for a week, or maybe OpenSuSE, or Slackware...

And what about you? Did you ever tried to use a different distro for a while?
Do you have some tips for people who wants to try it? Just leave a comment.
