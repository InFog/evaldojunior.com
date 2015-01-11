---
layout: post
title: Are micro-frameworks suitable only for small projects?
categories:
- WebDev
- Microframeworks
- Discussion
tags:
- WebDev
- PHP
- Python
status: publish
type: post
published: true
---

When I first heard about micro-frameworks I thought they were suitable only for
small projects, prototyping and small REST Apis (or other types of Apis).

Well this kind of thinking wasn't my fault. That's how some micro-frameworks
were presented to the world. And still, nowadays, some of them have descriptions
that make us think they are really super simple and supposed to be used only for
small or simple projects.

Let's take a look into some of them (Based on a search on [DuckDuckGo](http://ddg.gg)
for **php micro framework**).

- [Slim Framework's](http://www.slimframework.com/) page says the framework
    helps you building **simple** yet powerful applications.
- [Limonade's](https://limonade-php.github.io/) page says it's aimed for rapid
    web development and **prototyping**.
- [Fat-Free Framework's](http://fatfreeframework.com/home) page says it's
    **easy** to use.

Another interesting note is that most of micro-framework's pages uses the words
**simple** and **easy** to describe the framework. Ok, they want to bring in new
developers, but maybe **simple** and **easy** are not the right choice of words.

Now, to the big question: Are micro-frameworks really easy to use and aimed
mainly to small projects?

Well, I don't think so.

A lot of people misunderstands what the **micro** means for micro-frameworks. It
doesn't mean that your projects should be micro or small, it means that the
framework will not provide you with almost everything a software project needs.
Micro-frameworks are a response for the big full-stack frameworks, that usually
ships a lot of libraries, helpers, patterns and structure to help you focus on
your problem, not on defining which patterns, libraries, best practices or
whatever a project usually needs to be good and maintainable.

So, if you think about it, micro-frameworks are actually **harder** to use than
**full-stacks**!

And this leads to another question: Are micro-frameworks good choices for
beginners? Ok, maybe this topic will turn into a new post :)

Now, going back to projects' size...

Well, for really, really small apps, with no database connection, no Apis
consuming and basically no need for more than a few lines of code for each route
(or prototyping with mock data), micro-frameworks will be really easier to use
and will not require tons of config files and other services running like some
full-stack ones require.

But it doesn't mean that micro-frameworks should be used only for these cases.

If you are a seasoned web developer, you should have used some full-stack
frameworks already. Actually they were kinda the first experience with frameworks
a lot of us had. One of my first experiences with frameworks was CodeIgniter.
It's fast, easy to learn, has a nice documentation and has a lot of nice stuff
to help you getting things done.

Don't know how to organize your code? Use default directories organization from
CodeIgniter and done.

Don't really understand MVC? Just create controllers, models and views following
the documentation and done. And it's ok if you have a lot of business logic in
your controllers and super slim models used just for data persistence and
database's searches and basically no real OOP at all (that was my case).

Want to send e-mails? Framework has a library for you.

Want to log stuff? Framework is here for you.

Need a cache layer? Framework!

Template engine? Framework!!! (Ok, not CodeIgniter...)

Well, you get it.

And maybe you don't need all these things. Maybe you need just a router for your
small Api. And I think this is where the problem lies. If full-stack frameworks
have a lot of helpful things, they are useful only for big projects, that will
really make use of everything in the framework, or most part of it. And, of
course, micro-frameworks will be the opposite of full-stack and be suitable only
for small projects where you need just a few libs.

... This is not true!

Actually, my old CodeIgniter projects are now so glued to the framework that it
became really hard to use something new or to add simple stuff like... Tests! So
if I really want or need to move away, I'll have some hard times ahead. And the
problem is not just moving away. If the default template engine of the framework
is not suitable for the project anymore, it will not be easy to get rid of it.

When you choose a full-stack framework, you are kind of choosing to couple your
project to the framework. Ok, you can build a project decoupled from the
framework, but this is not the usual way to go and is surely not easy.

If you use a micro-framework, you will also have a lot of hard decisions to make
as your project grows and needs new features. Yet, it will be easier to decouple
your project from the framework.

It's not hard to find ZF1 projects using Doctrine for database management or
twig for templates (or ZF2 :) ... )

So, if you think about it, maybe micro-frameworks should be targeted at small
and big/huge projects, because the standard libs of a full-stack will not be
always the best choices and the project will be really glued to it.

If you are a experienced developer and know you can build a better stack out of
decoupled components and keep them up to date, go for micro-frameworks. It will
surely not be easy in the beginning, yet it should pay off as the project grows
and having a better understanding of the stack and how to mold and control it
is necessary.

What about you? have any thoughts on this topic? Where are you using
micro-frameworks? Leave your comment below :]

Happy coding!

InFog
