---
layout: post
title: Using Composer for global libraries
categories:
- PHP
- Composer
tags:
- php
- composer
status: publish
type: post
published: true
---

A few time ago PHP developers could have global libraries installed via PEAR.
Ok, we still can still some things via PEAR, but this distribution method is
being replaced by Composer.

Usually Composer is used to install local dependencies for each project, but I
guess not everyone knows it can also be used to install global dependencies,
commands and libraries.

I usually keep global installations for commands, like PHPUnit and PHPCPD.

PHPCPD is a tool used to find duplicated code and you usualy don't need to have
it in the dependencies for each project.

So, here is my recipe on how to use composer to install global commands.

First of all, I have a directory **~/bin** in my home. In this directory I keep
my local commands. This directory is also in my **$PATH**:

  # .bashrc, .zshrc or your favorite shell config file
  PATH=$PATH:~/bin

In my home dir I also have a **.composer** dir, where I created a **composer.json**
with this content:

  {
    "config": {
      "bin-dir": "/home/myuser/bin"
    }
  }

This file will tell composer to install the binaries of the packages in my
**~/bin** dir. Ans since this dir is in my **$PATH**, I'll be able to execute
php commands simply calling the command name.

For example, to install PHPCPD, use this (assuming **composer** is also in your
PATH):

  composer global require "sebastian/phpcpd:*"

Wait for the installation and done, you have PHPCPD to run whenever you need:

  phpcpd src/
  phpcpd 2.0.1 by Sebastian Bergmann.
  0.00% duplicated lines out of 5107 total lines of code.

Wow, good! No duplication in a real project :)

You can also setup something like this to install binaries (executables) into
**/usr/local/bin** or something like this. But it would be more for shared envs.

Any tips on composer usage for global dependencies? Comment below :)

InFog
