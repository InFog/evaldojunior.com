---
layout: post
title: Are micro-frameworks for beginners?
categories:
- WebDev
- Microframeworks
- Discussion
tags:
- WebDev
- PHP
- Python
- Microframeworks
status: publish
type: post
published: true
---

In my [last post about micro-frameworks](http://blog.evaldojunior.com/webdev/microframeworks/discussion/2015/01/08/are-micro-frameworks-suitable-only-for-small-projects.html)
a new question came to the table: Are micro-frameworks a good choice for
beginners?

What some of the options out there claim is that they are super simple to use
and no matter if you are a novice or an experienced developer, they are a good
option for you.

Well, maybe this is not true. I mean, if you just want to prototype something,
ok, a micro-framework will be a good option, even if you are a beginner, but, if
you want to build something that should grow and probably will be used for some
time, then a micro-framework could not be exactly the best choice for you.

After all, a micro-framework is like just the engine and basic parts of a car.

**TODO: Draw of an engine...**

My point is not about the technology you choose being better or worse than
another one, my points are aimed on these topics:

- Team productivity
- Good practices
- Patterns
- External tools

Sometimes we, developers, have a feeling that everything is wrong and if we
move to a new framework, a new language, a new database or a new something else
everything will be ok and there will be no problems anymore. Well, most of the
time we are wrong about it, and with a little bit of patience and love to the
project, things can be fixed. So let's talk about the topics I mentioned.

## The good on full-stack frameworks

In my point of view a full-stack framework is a tool developers can use for
almost everything, and the best thing is that they usually come with batteries
included. If you need a database abstraction layer, framework will have it, if
you need a template parsing library, frameworks will have it, and you get it.
Most of the things that most of the projects need, a full-stack framework will
somehow have it.

So, the full stack is like the complete car.

**TODO: Draw a car**

And this is good for almost all the projects out there. When a framework ship
something is like it's recommending it as a good, or maybe the best, option.

When working in teams, thing can get ugly when it comes to choosing options for
libraries and tools. Usually each member of the team will try to push her/his
prefered options.

But, if the team is using a full-stack framework, it can just use the default
options and avoid discussions. With ORM is better for PHP? Well, I don't know,
but we are using Symfony, so, let's go with Doctrine.

And the same goes for **Good Practices** and **Patterns**. To avoid fights and
keep consistency in the project, just go with the default your framework uses.
It's easier ;)

If you have a team with too much juniors or maybe no seniors to push things,
then a full-stack is definitely a good option. The team can follow what the
framework dictates and learn a lot in the process.

Well, sometimes the team will add pieces to replace the bad partes of the full
stack.

**TODO: a modified car**

## The good thing on micro-frameworks

And where, in my opinion, is the place for micro-frameworks?

Well, of, course, for small REST APIs a micro-framework is a really good option,
but this is not the only case where a micro-framework can be used.

If you are building a big application, with tons of pages, database abstraction,
pdf generation, email sending, reports and everything else in the most wild
users' dreams, a micro-framework can also be a good option.

But now the problem is that you will need to make choices and you have a whole
world of options out there. And, of course, always remember:

    With great powers comes great responsibility

When using a micro-framework you are the owner of your ground and you need to
choose on which bases you want to build your race car, sorry, application.

**TODO: a racing car**

And here is where I say that micro-frameworks are not good options for beginners,
since a beginner is still learning and cannot make good choices for long term
applications. I mean, it's hard for seniors to choose something to use and be
sure it will still be a good option in the future!

**TODO: a funny race car**

And there are more points, like application architecture, design patterns, best
practices, etc. Beginners will have a hard time building everything. It's
almost like going back when web applications were just a bunch of scripts
loading each other (Well, I guess it is still something like this, in the end).

In my point of view is too much responsibility for a begginer to deal with
all these choices.

And what about you? Do you use full-stack frameworks? Have you ever tryied a
micro-framework? What you think about it? Leave your comment bellow.
