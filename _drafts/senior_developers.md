---
layout: post
title: What a senior PHP developer should know in 2017
categories:
- PHP
- Developers
tags:
- PHP
- Developers
status: publish
type: post
published: true
mainimage: ""
---

This post is my opinion about what I think a senior PHP developer should know
in 2017. The main reason for me to write this post is to help developers better
understand their own knowledge and if they are missing something.

Of course the number one requirement is a good understanding about the PHP
language. You don't need to know the deepest details about the language, but
you should know it well to feel comfortable reading source files and you should
know here to find documentation and help when you need.

PHP 7 is out there for quite a while now and even 7.1 is available as a stable
release, so you should know what the new 7 family brings to the table. Speed is
the number one item tat every PHP developer knows, but things like
the [null coalesce operator](http://php.net/manual/de/migration70.new-features.php#migration70.new-features.null-coalesce-op),
the [scalar type declarations](http://php.net/manual/de/migration70.new-features.php#migration70.new-features.scalar-type-declarations)
and the usage of exceptions in place of the errors are super useful and can make
your code more secure and reliable.

Using [composer](https://getcomposer.org/) to manage the dependencies of your
application should be the default way to manage dependencies for you and simple
tricks like adding custom scripts to composer should also not be a mystery.

You also need to know  the main frameworks out there and the differences between
them. Should I use Symfony to build a landing page that will be discarded in a
few weeks? Or is CakePHP a better option for that? Maybe it is Yii or Laravel?
The important thing here is not to be locked inside one framework's tool set
and capabilities. The reason we have so many frameworks in the wild is because
people and projects have different needs. And here we can apply that saying:
If all you have is a hammer, all your problems will look like nails.

Recognizing and implementing design patterns is also a must. A senior developer
knows one should not exactly start a project saying "I will use a Strategy
pattern here", one should rather recognize where the patterns are the solution
for the task in hand. Of course, at some point developers are able to recognise
such situations earlier in the process, but a rule of thumb, in my opinion, is
that patterns emerge from the design, they are not pushed into the design.

Development is cool, but you also have to deploy your code to production so
people can actually use it. Although it is possible to deploy code using FTP
this should not be the only option you know. Specialized deployment tools are
not hard to find and you can always get some experience with some SaaS
deployment pipeline tool. [Capistrano](http://capistranorb.com/) is a Ruby tool
mostly used to deploy [Ruby on Rails](http://rubyonrails.org/) applications, but
you can also use it for PHP and there are even some plugins for frameworks like
Symfony. [Ant](http://ant.apache.org/) is a long time favorite of mine to
automate tasks, including deployment scripts. [Fabric](http://www.fabfile.org/)
is a Python tool that can also be used to deploy PHP applications and there is
also [Deployer](https://deployer.org/) for the ones who want to keep everything
in the PHP world.

After deployment you should be able to understand how your applications behave
in production, so you need monitoring tools like [NewRelic](https://newrelic.com/),
[Datadog](https://www.datadoghq.com/) and [Sentry](https://sentry.io/welcome/)
are SaaS tools that can be easily integrated into your servers and applications.
There are also self-hosted free options like the excellent [ELK](https://www.elastic.co/products)
stack.

Do you think I missed something in this post? Help me expand this post by adding
your thoughts in the comments bellow.

InFog.
