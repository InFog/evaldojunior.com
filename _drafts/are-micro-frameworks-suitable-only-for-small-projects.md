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

When I first heard about micro-frameworks I thought they were suitable only for small projects,
prototyping and small REST Apis (or other types of Apis).

Well this kind of thinking wasn't my fault. That's how some micro-frameworks were presented to the world.
And still, nowadays, some of them have descriptions that make us think they are really super simple and supposed to
be used only for small or simple projects.

Let's take a look into some of them (Based on a search on [DuckDuckGo](http://ddg.gg) for **php micro framework**).

- [Slim Framework's](http://www.slimframework.com/) page says the framework helps you building **simple** yet powerful applications.
- [Limonade's](https://limonade-php.github.io/) page says it's aimed for rapid web development and **prototyping**.
- [Fat-Free Framework's](http://fatfreeframework.com/home) page says it's **easy** easy to use.

Another interesting note is that most of framework's pages uses the words **simple** and **easy** to describe
the framework. Ok, they want to bring in new developers, but maybe **simple** and **easy** are not the right
choice of words.

Now, to the big question: Are micro-frameworks really easy to use and aimed mainly to small projects?

Well, I don't think so.

A lot of people misunderstands what the **micro** means for micro-frameworks. It doesn't mean that your
projects should me micro or small, it means that the framework will not provide you with almost everything
a software project needs. Micro-frameworks are a response for the big full-stack frameworks, that usually
ships a lot of libraries, helpers, patterns and structure to help you focus on your problem, not on
defining which patterns, libraries, best practices or whatever a project usually needs to be good
and maintainable.

So, if you think about it, micro-frameworks are actually **harder** to use than **full-stacks**!

But, how can they be harder if they claim that you can simply add some routes and have everything working in no time?

Well, for really, really small apps, with no database connection, no api consuming and basically no need for
more than a few lines of code for each route (or prototyping with mock data), micro-frameworks will be really
easier to use. Now if you need more sophisticated archtecture for your application, things will not be so easy.

I know some people will say you can build your archtecture with only the things you need and using libraries
you trust and like. But another important thing that micro-frameworks claim is that they are suitable for all
level of developers.

Are you an expert developer with some years of experience and a reasonable knowledge about software archtecture,
design patterns and good practices? Micro-frameworks are for you!

Are you a begginer with no experience and no idea of what archtecture means in the software world? Micro-frameworks
are for you too!
