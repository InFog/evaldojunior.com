---
layout: post
title: What a senior PHP developer should know in 2017
categories:
- PHP
- Developers
- Carrier
tags:
- PHP
- Developers
- Carrier
status: publish
type: post
published: true
mainimage: "developer_magic.png"
---

This post is my opinion about what I think a senior PHP developer should know
in 2017. The main reason for me to write this post is to help developers better
understand their own knowledge and if they are missing something to hit the
next level in their carriers.

An important note is that this post is not the universal truth about what a
senior PHP developer should know. Keep this in mind and enjoy the reading.

Of course the number one requirement is a good understanding about the PHP
language. You don't need to know the deepest details about the language, but
you should know it well to feel comfortable reading source files and you should
know where to find documentation and help when you need. Yes, senior developers
also look for usage example and learn from them, so do not be afraid to search
for answers online, just be sure to be able to tell apart the good sources of
information from the not good ones. When in doubt go for the
[official manual](http://php.net/docs.php) and take a look on
[PHP the Right Way](http://www.phptherightway.com/) from time to time.

PHP 7 is out there for quite a while now and even 7.1 is available as a stable
release, so you should know what the new 7.x family brings to the table. Speed
is the number one item that every PHP developer knows, but things like
the [null coalesce operator](http://php.net/manual/de/migration70.new-features.php#migration70.new-features.null-coalesce-op),
the [scalar type declarations](http://php.net/manual/de/migration70.new-features.php#migration70.new-features.scalar-type-declarations)
and the usage of exceptions in place of the errors are super useful and can make
your code more secure and reliable.

Using [composer](https://getcomposer.org/) to manage the dependencies of your
application should be the default way to manage dependencies for you and simple
tricks like adding custom scripts to composer should also not be a mystery.
It is also important to know the difference between the commands `install` and
`update` and why it is important to commit the `composer.lock` file to your
version control. I won't give you the answer here ;-)

And by the way, it is 2017, a developer should be able to use versioning tools
like [Git](https://git-scm.com/), [Mercurial](https://www.mercurial-scm.org/) and
others. Branching, merging and solving conflicts should be natural actions for
a senior developer.

You also need to know  the main frameworks out there and the differences between
them. Should I use Symfony to build a landing page that will be discarded in a
few weeks? Or is CakePHP a better option for that? Maybe it is Yii or Laravel?
The important thing here is not to be locked inside one framework's toolset
and capabilities. The reason we have so many frameworks in the wild is because
people and projects have different needs. And here we can apply that saying:
If all you have is a hammer, all your problems will look like nails.

Recognizing and implementing design patterns is also a must. A senior developer
knows one should not exactly start a project saying something like "I will use
a Strategy pattern here", one should rather recognize where the patterns are the
solution for the task in hand. Of course, at some point developers are able to
recognise such situations earlier in the process, but a rule of thumb, in my
opinion, is that patterns emerge from the design, they are not pushed into the
design.

A senior PHP developer should be able to write unit tests for untested code and
refactor it. Our industry is in constant change and tools and libraries are
constantly evolving. Being able to remove an unmaintained library from a code
base and replace it with another one is a really nice skill to have. A hard one
because it requires investigation and patience usually, but it is still a skill
that not all devs have because we as developers usually want to replace code
with what is new and better (and will become old and worse in some months/years,
but no one remembers this part usually).

And talking about tests, a senior developer should be able to write tests and
also to practice techniques like Test Driven Development. Mocking other systems
and APIs should not be a mysterious thing.

Development is cool, but you also have to deploy your code to production so
people can actually use it. Although it is possible to deploy code using FTP
this should not be the only option you know. Specialized deployment tools are
not hard to find and you can always get some experience with some SaaS
deployment pipeline tools. [Capistrano](http://capistranorb.com/) is a Ruby tool
mostly used to deploy [Ruby on Rails](http://rubyonrails.org/) applications, but
you can also use it for PHP and there are even some plugins for frameworks like
Symfony. [Ant](http://ant.apache.org/) is a long time favorite of mine to
automate tasks, including deployment scripts. [Fabric](http://www.fabfile.org/)
is a Python tool that can also be used to deploy PHP applications and there is
also [Deployer](https://deployer.org/) for the ones who want to keep everything
in the PHP world.

After deployment you should be able to understand how your applications behave
in production, so you need monitoring tools like [NewRelic](https://newrelic.com/),
[Datadog](https://www.datadoghq.com/) and [Sentry](https://sentry.io/welcome/),
that are SaaS tools that can be easily integrated into your servers and applications.
There are also self-hosted free options like the excellent [ELK](https://www.elastic.co/products)
stack.

Caching is another important skill. Understanding where to apply a caching
technique may be the difference between having a nice and fast user experience
or a slow one where the servers are always on fire while the customer is waiting
for the page to load. And users will not wait for the page to load, they will look
for something else. Remember caching exists in different flavours and it is
important do know what, when and where to use cache, from code the cdn.

**Important**: Do not depend on the company you are working for to learn new things.
If you don't have the chance to learn unit tests in your current position, you can
do it at home, building some personal project. The same applies for everything else.
Nowadays it is super easy to setup a GNU/Linux virtual machine where you can play
around and practice new skills that may be useful for your current work or to get
a new one. You can always get a [$10 credit on Digital Ocean](https://m.do.co/c/1059a87d7c47)
to deploy your applications and setup deployment pipelines using tools like GitHub,
BitBucket and [Codeship](https://codeship.com/).

Senior developers should also have good communication skills and be able to
understand the business of the companies they work for. Let's be realistic, a
really small number of us are working for Google, GitHub, Atlassian, Oracle and
other software centered companies. We are working for online shops, banks,
web agencies and other lots of companies that are doing businesses online and
depend on a solid platform to stay alive but not exactly will put loads of
money into that rewriting you want to do to get rid of the legacy system you
hate with a passion. So, try to understand the business and align the technical
needs with the business to create a win-win situation, because bad code can
also destroy a company.

An important note: You don't have to be perfect and know all the things I listed
here from the top of your mind, but you should be able to understand all the
concepts and to look for help in the right places.

Do you think I missed something in this post? The PHP community is a really
large one and senior developers will come in all shapes and sizes, so help me
expand this post by adding your thoughts in the comments bellow.

InFog.
