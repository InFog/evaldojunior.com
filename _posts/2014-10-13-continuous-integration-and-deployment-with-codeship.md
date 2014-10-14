---
layout: post
title: Continuous Integration and Deployment with Codeship
categories:
- DevOps
tags:
- devops
- codeship
status: publish
type: post
published: true
---

If you were sleeping for the past two years you may be surprised by a movement
called DevOps.

DevOps tries to bring together development and operations teams, since those
teams have different points of view from the product they keep running.

Usually the Dev team want to update the code base and deliver more and more
features. The Ops team want stability. The problem is that the product must not
stop, it should grow and get better, so the teams must play together. The DevOps
movement try to solve these communication problems using a lot of automation
and cultural changes.

When Dev and Ops don't play along changes to the code base are slow. Tell me the
truth, how many deploys your team do every month? How many problems like "it
works on my computer" you ever faced? Bad stuff, right?

There are two important thing in DevOps: CI and CD.

CI stands for Continuous Integration. That's when a bunch of test are run
against the code base on every push to the code repository. That guarantees that
the code quality will not fall and the test are not broken.

CD stands for Continuous Deployment. That's when the code is packed and delivered
in production, usually after a push to the code repository. Everything is automated.

Once more, tell me the truth, is it difficult for your team to deliver new code
in production? Which are the steps? If the steps start with something like
"connect to the FTP server", you are doing if wrong (maybe not wrong, but really
not a good practice).

There are some ways to do CI and then CD. Yep, you will need CI first, since you
don't want to deliver broken code.

A way to start with CI and CD is creating scripts that run the tests and,
if everything is ok, deploy to production. This way is not so simple to keep,
since scripts are hard to update.

Another well known way is using [Jenkins](http://jenkins-ci.org/), a task
automator. Jenkins can do anything you want for task automation and is used for
CI and CD. The bad part is to setup and host a Jenkins installation. Also, the
Jenkins' interface is not very user friendly. Jenkins has some issues but it is
an amazing tool that everyone doing automation and DevOps must have in their
toolboxes.

Another very cool and easy to use tool is [Codeship](https://www.codeship.io).
I came to know Codeship when I was looking for some hosted Jenkins service. Then
I made some tests and liked if a lot.

![Codeship Logo](/assets/images/codeship/logo.png)

I did the automation of the tests and deployment for a PHP project. That's what
I had:

- A PHP project
- Composer installed dependencies.
- PHPUnit tests (no database connection)
- Packing and deployment using Ant (over SSH)

The steps to create and setup the project on Codeship were pretty simple. The
first one is to choose the repository:

![Repository choose](/assets/images/codeship/1_source.png)

In the next page you are asked about the technology you are using, this way
Codeship can fill the fields with default options. I chose PHP, so Codeship
used Composer for dependencies and PHPUnit for tests.

![Setup and tests](/assets/images/codeship/2_tests.png)

Of course you can change these fields to aim your needs. The are run as shell
scripts and changes are easily made.

Next step is to add the hook on Bitbucket (if your project is there). Then you
need to do a commit and a push in order to run the tests for the first time.
Codeship suggests to add their badge in the readme:

![Hook and badge](/assets/images/codeship/3_push.png)

After running the tests for the first time (and have them passing), you'll need
to setup  how the deploy is done. Codeship has a lot of options:

![Deploy options](/assets/images/codeship/4_deploy.png)

I chose **$script**, since I already had a script to pack and deploy using
**Apache Ant**. So my setup was something like that:

```bash
ant deploy
```

Then I just made a new push and magic happened.

There was some other steps, like adding the Codeship's SSH key to my server, but
it was easy.

Oh, and I must not forget to tell about Codeship's user support. It's amazing!
If you need anything, just ping them on twitter ([@codeship](https://twitter.com/codeship))
and they answer in no time. They also have a support form in their site.

And what about the pricing? It's free for 5 projects or less and 100 builds/month.
That's a pretty nice way to start automating your personal projects and also the
ones at the company.

Do you know any nice CI and CD tools? Let me know in the comments bellow ;)
