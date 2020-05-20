---
layout: post
title: Developer Experience
description: Developer experience matters more than we believe. An easy to setup development environment makes people more productive and happy.
categories:
- developers
- opinion
tags:
- developers
- opinion
status: publish
type: post
published: true
---

This post is about how one can help their colleagues being more productive and avoiding unnecessary
work battling the source code they are trying to run.

## User experience

User Experience (UX) should be part of our mindset as software developers, UX has the potential to be
what makes a user continue to use a given product or not.

Good UX is about making the usage of a given product as easy as it can be, the user should never
battle the product in order to get what they want.

## Developer Experience

Developers on the other hand are smart people. Developers can go down a bumpy road and not even notice it.

Complicated development environment and hidden configuration files? Not an issue for a developer.

That's why products focused on developers are usually unpolished, full of sharp edges and sometimes even
enigmatic. This is to be sure that the real developers will keep the common folks away from those black
screens and complicated commands.

Developers will even complicate a simple text editor to make it harder to use, all effort is valid to keep
our world as peasant free as possible.

Right?

**WRONG!**

Developers need good experience as much as "regular users" do.

Being able to work on a project with guardrails and safe nets can make a big impact on one's productivity
and engagement.

This is where **Developer Experience** gets on the spotlight.

The products for developers are getting easier to use, see how easier it is to setup a cloud based
queueing system vs running and maintaining your own solutions.

Frameworks and IDEs are going the extra mile to make building software easier, or at least making the start
less scary and more welcoming.

We can and should have the same mindset on our own software. But how?

## How to help

Here is a list of what you can do from today on to help your colleagues, your community and yourself:

### Local development environment

* Having a local environment to test changes is a MUST, so be sure to make the local environment work
  perfectly with Docker or other solution for portable environment
  * Perfectly means: Clone the repo and run `docker-compose build`. The development environment should
    then be ready
  * No extra steps, no changing only one file
* Everything is automated and replicable
  * Need access to other services? Docker-compose is there for you, clone and build the images you need
* Sensible defaults
  * Be sure to provide a configuration file (or files) with working parameters
  * Like Sandbox/Testing database access out of the box
* Did you introduce a new parameter? Add default development value on the distributed config file
* Tests should run all the time
  * Tests should not run only on CI/CD
* README file should always be there with instructions and general explanation of what the software does
* Empowerment:
  * Always empower your colleagues to do their job as hassle free as possible
  * Developers should be able to run your code with no issues
  * QAs should be able to run testing environments as they need
  * Operations should be able to replicate your application and scale it as needed
  
Happy coding!

InFog
