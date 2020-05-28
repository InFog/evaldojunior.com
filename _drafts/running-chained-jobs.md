---
layout: post
title: Running chained jobs
description: Ever got yoursenf in a situation where you had to run jobs in a sequence in a given schedule? This is an interesting case I found while maintaing a chain of commands that depend on the previous one to finish before running.
categories:
- dev
- discussion
- commands
- cronjobs
tags:
- dev
- discussion
- commands
- cronjobs
status: publish
type: post
published: true
mainimage: ""
image_url: ""
image_author: ""
---

Recently I found myself maintaing an interesting piece of code.

It is a sequence of Symfony Commands to do some calculation and publish the results.
It was a sequence of around 8 commands doing each one its part of the process, all independent
of each other but also dependent of the previous command's output. Almost like chaining commands
on Unix using the pipe operator.

Putting it on a more visual way, it looked like this:

Command1 -> Command2 -> Command3 -> ...

This implementation was using a `trait` in PHP to make the commands `Chainable`, so to speak.
After each command finished running the trait was checking if the `$nextCommand` was set for then
starting a new `Symfony Process` calling it. Each subsequent command was doing the same until there
was no more `$nextCommand` defined. Yes, this sounds a lot like a `Chain of Responsibility` pattern,
but it was not.

This is not a bad solution and it works nicely.

There is one problem however. It is not possible to run each command in isolation, making it harder
to test.

There is another problem. This one is more about software architecture: As described by **Ken Pugh** in
his book **Interface-Oriented Design**:

*An interface's implementation shall do what its methods says it does*

This is the first law of interfaces.

Let's say the first command on that chain is called "calculate-overpriced-products". When using this
command one would expect to have a list of over priced products. Instead the next command would run,
then next and the next and the next... Until the whole chain is finished and the output is a list of
best priced products. You call the command expecting A and it gives you Z.

Anyway, I was working on making those commands auto-retry-able, like, if it fails it should try itself
again and again. After some time trying to extend the `Chainable` concept and apply it into something
like `Retryable` I realised I was going in the wrong direction.

Why? Again, thanks to **Ken Pugh's** and his third **Law of Interfaces**:

*If an implementation is unable to perform its responsibilities, it shall notify its caller*.

This is what made me realise the whole concept was wrong.

I removed all the code related to make the commands `Chainable`, because one command should do one thing
and one thing alone.

I added then a kind of Front Controller that is responsible for calling all the commands on sequence
and to retry them in case of failure.

The new structure is now like this:

Front Controller:
* Command1
* Command2
* ...
