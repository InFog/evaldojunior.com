---
layout: post
title: Do not change the default framework's architecture
categories:
- frameworks
- architecture
- software
tags:
- frameworks
- architecture
- software
status: publish
type: post
published: true
mainimage: "architecture.jpg"
---

A development framework will usually guide the development of web applications,
from back office systems to e-commerce and websites.

A framework contains basic functionalities and guidance that help the
development team starting a project faster and later on having a more maintainable
code base. It also makes it easier to add new members to the team by reducing
the entry barrier for developers with experience in the base framework. In this
scenario a new developer in the team would be able to focus on learning the
business details, not the foundation basics of the software. Even developers
with no experience on the base framework could benefit from it's documentation
and even books about it.

We can even say that the correct framework for a project would cover all it's
needs. We still may find some situations where the basic framework would not
provide a given functionality or the provided one is not exactly what you need.
With access to the framework's source code it is possible to simply change it
to provide the needed functionality and solve the issue in hand.

This is not a good idea because it breaks the framework's internals and makes it
harder for the team to keep it updated.

Well, I believe this issue is quite small nowadays (2017) with Composer being
used to control the dependencies of a project (even the framework). Composer
puts the dependencies in a separated directory, called `vendor`, that is not
even kept under version control, so changes to this directory are removed often.

Another possible way to extend a framework's functionality is to simply extend
one of the framework's classes and adding what you need there. This will cause
some other issues in the future, like making it harder to keep the framework
up to date, since now your application knows too much about the framework's
internal behaviour. This also breaks encapsulation in OOP.

I would say the best way to do that is implementing some kind of adapter to use
the framework's behaviour and your needs on top. It would make future changes
less harder, since you would need to care only about the public APIs of the
classes you are using.

Still it is possible to change things like the file `web/app.php` in Symfony
applications. This file is kept under version control, but it is part of the
framework, so it is a gray area. Still, changes there can cause problems for
updates and when developers would not expect a different behaviour implemented
there.

In the end my opinion on this topic is: To not change the behaviour of a
framework because it will cause you more trouble in the future than solutions in
the present.

PS: Another really good way to do that is to add the new functionality into the
framework's core and to submit it to the community building the framework.

Happy hacking!

Credits to the cover image: [Flickr](https://www.flickr.com/photos/joeshlabotnik/3707230247/).
