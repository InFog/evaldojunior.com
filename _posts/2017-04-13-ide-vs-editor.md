---
layout: post
title: IDEs vs Text Editors
categories:
- IDEs
- Text Editors
- Vim
- Development
tags:
- IDEs
- Text Editors
- Vim
- Development
status: publish
type: post
published: true
mainimage: "general/vs.jpg"
---

IDEs are out there and they are a natural evolution for developers. IDEs can
help with several tasks, from simple code formating to code generation and
advanced refactoring techniques.

Still, simple text editors with features like code highlighting and word
completion are still there. [Sublime Text](http://www.sublimetext.com/),
[Atom](https://atom.io/), [GNU Emacs](https://www.gnu.org/software/emacs/) and
[Vim](http://www.vim.org/) are some good example of text editors that are not
hard to find if you walk into a software development team.

The thing is, with so many good options for IDEs, why do people still use simple
text editors?

Well, I cannot speak for everyone else out there, but here are some of my points
on why I prefer to work with a text editor rather than an IDE.

I'm using Vim for the past 5+ years and I even have a nice configuration for it
that I like to share around. Check the project out on
[GitHub](https://github.com/infog/meuvim).

It all started when my laptop broke and I had to spend a few weeks coding on an
[10" Asus Eee PC](https://en.wikipedia.org/wiki/Asus_Eee_PC). Back then I was
using a local LAMP stack, no VMs or Containers, and
[Netbeans](https://netbeans.org/) was my best friend.

Instaling a LAMP stack was the easy part, but actually running Netbeans was kind
of a pain, not only because of the memory usage, but also because of the space
on the screen, even hiding most of the menus, I was still having just a small
space left to code on.

So, this was my perfect excuse to actually try Vim a bit more than the usual
messing around and trying a couple of colorschemes that every developer does at
some point.

And here is the first reason to use a Text Editor instead of an IDE: Machine
Resources. One may say that this is not the case anymore, specially using modern
hardware, but for me, reducing the resources' usage is kind of a life style now.

And then I started adding plugins and more plugins to Vim. The idea was to
replace all the features I liked about Netbeans, like code completion for
classes and methods, displaying the documentation and some kind of macros
to generate pieces of code.

Of course I could not find all the pieces, but I got used to do some stuff
manually, after some time.

After some weeks I had my laptop back and I decided to keep on using Vim and
something really nice happened: I could migrate all my configs to the other
machine by simply cloning the repo. Wow! No more going into several config
windows and trying to remember every shortcut I made on another machine. Simply
clone the repo under **~/.vim**, link the **vimrc** file and you are done.
Just like magic, right?

And this is the second reason to use a text editor (such as Vim and Emacs), you
can usually have your configuration migrated into other systems in no time and
usually not depending on other software (Ok, I do depend on Git here, but this
is ok). Again, one may say that you can copy the config dir from IDEs, but, you
know, it is not the same ;)

I spent then some months learning Vim one command at a time and a couple of
tricks here and there. Of course it does not take months to learn the basics to
be actually productive with Vim, but I was trying to learn not more than one or
two commands per day and trying not to forget some of them. In the end it did
not work and now I think I have a core set of commands on my fingertips and I
usually go with them for everything.

And there you go, yet another reason: Once you learn how to use an editor like
Vim or Emacs you will be able to use it the same way anywhere, even in different
operatin systems.

Ok, now, back to the main topic, what is better, an IDE or a Text Editor?

Well, it depends a lot on your needs, but in my opinion everyone should try to
use a simple text editor for a while at least once. You may not stick to it but
you will have some learnings to take with you.

By using a text editor you will have to better understand the architecture of
the application you are working on. If you have to manually create directories
and files and classes and everything else you will have a better overview of
the whole software and why things are the way they are.

Another thing is that you will have to better understant the languages you work
with. Without autocompletion and some magic from IDEs you will see yourself
forced to learn some basics by heart and to look more into the manual pages.
And I'm from the opinion that if a language is too hard to program with without
the assistence of an IDE, it is because such language failed beign for humans
to write and read.

Since most of the text editors do not have "project like" features, you will
not be able to run searches on your entire codebase from within the text editor,
actually in such situations you will have to use other tools like the good and
old **grep** or some modern flavour like [ack](http://beyondgrep.com/).

And if you have to replace several occurences of a string you will use something
like **awk** or **sed**.

You will have to use **git** or other versioning tools on the command line and
learn it's basics.

After trying a regular text editor for a while and doing things manually you will
better understand what the IDE is doing for you and will even be able to solve
problems when the IDE fails to help.

As I said, I think every software developer should have this experience at least
once, and then decide the path to follow.

So, what do you think? What about playing around with Vim for a while? If you
don't like it you can just walk away with some new knowledge ;-)
