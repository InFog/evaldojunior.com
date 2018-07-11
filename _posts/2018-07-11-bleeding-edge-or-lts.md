---
layout: post
title: Bleeding edge or LTS - Which framework version to choose?
categories:
- framework
- development
- discussion
tags:
- framework
- development
- discussion
status: publish
type: post
published: true
mainimage: "architecture.jpg"
---

Starting a new software project is nice and the mythical green field project is
usually able to bring joy to any developer. After planning what the application
will do it is time to select the libraries and frameworks that will compose the
stack of the new application. This task is usually done using the mindset of
"what do I like better?" or "what am I comfortable with?" or even "what do I
want to learn?". Of course some options will be selected according to the type
of software to be built.

We need one type of mindset when selecting the tools to develop an
enterprise application that will live for years to come and another one for a
promotional website that will live for a couple weeks or months. This post
focuses more on the first case, when the application to be built will have to
live for years to come and has to be reliable, maintainable and upgradable
avoiding full rewrites using newer versions of the framework used.

In some way or another stacks get chosen and applications get built. But what
happens down the line when the software is already build and has to be supported?
If the code is coupled to the underlying framework it can get harder to upgrade
to newer versions, specially when the newer versions break the compatibility.
And let's all be honest here, writing web applications completely decoupled from
the framework is a hard task that most of us will fail at some point or another.

Another problem for applications that have to live longer is to keep the pace with
the releases of the libraries/frameworks being used. Talking about PHP, for example,
running a *composer update* may break things in unexpected ways, and depending on
the level of stability needed, upgrading a library will spawn a full set of
regression tests, being those tests automated or not.

Some libraries will release newer versions so fast that you could get one version
in the morning and another one in the afternoon (I'm looking at you Javascript
community). This is not bad, super bad, but it can generate a lot of work to
simply try to stay on the latest version of all the libraries the application
needs.

What I'm trying to say here is that at some point you may spend more time keeping
your stack up to date than building new features or fixing bugs. Your customer
does not care if you are running the latest version of your stack, the customer
cares about new features and less bugs.

To try to solve this issue some frameworks release Long Term Support (LTS) versions
that are maintained for a longer time than the regular releases. Symfony for
example is supported for 8 months after each regular release and for 3 years for
the LTS versions, Laravel is doing the same releasing LTS versions with 2 years
support and 3 years security fixes.

Using an LTS version has its pros and cons. On the pros side the team will have
more time to focus on a stable product and to build features and fix bugs. Keeping
everything up to date will be easier because the minor versions released on the
LTS version will not introduce backward compatibility breaks. The team can get
experienced with that given version and extract the most out it.

But not everything is shiny and nice on LTS. Updating to a newer version when
the support time is gone can be complicated. That's when the team will have to
deal with backwards compatibility breaks and adoption of new ways to do things
on an environment that used to be well known. Other problem is to stay behind
the new features present on the regular releases.

I usually prefer LTS versions for software that will least for years
but this is not a rule and it depends a lot on the team and its vision. A team
of four developers who need to deliver new features and fix bugs constantly will
probably have no time to upgrade to newer versions every couple months. On the
other side a team with people dedicated to keep the stack up to date, clean and
stable will be able to adopt new features more easily.

Sometimes we also see those small proof of concept projects that for some reason
succeed and hit production. In such cases a major refactor/rewrite is recommended,
but when it is not possible then I recommend following the regular releases until
an LTS is out. Then it is possible to stay on the LTS if that is better for your
team.

What about you? What do you usually prefer or what do you recommend for
applications that will live a long time, LTS or regular releases?

Happy coding.
