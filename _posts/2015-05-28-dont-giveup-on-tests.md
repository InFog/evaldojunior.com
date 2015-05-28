---
layout: post
title: Don't give up on your tests
categories:
- tests
- unittest
tags:
- development
- programming
- tests
- unittest
status: publish
type: post
published: true
---

It's a new day and you are about to start a new project. It's not a public/open
source project, it's a private one, for the company you are working for.

You sit together with your team and everyone is excited about the possibility to
use new technologies and play with all the new tools everyone is talking about
in conferences, blog posts, twitter and wherever else.

And another important thing: Everyone in the team agrees that the project should
definitely have automated tests. You should start small, with some unit tests,
maybe some [behavior tests with Behat](http://behat.org) and so on.

As time goes by people start not to pay so much attention to tests anymore. It's
just one or two not tested methods, or classes, or packages... You know, it's just
for one feature that we need to deliver as soon as possible, or it's just because this one is
hard to test because it requires some dependencies, or maybe this other one is
so simple that is kind of useless to test it. The reasons don't matter, the thing
is that little by little the team is leaving tests behind and when someone tries
to run the test suite he/she will get some errors, or a lot of errors and then
tests will become real dead code, because no one wants to fix them and no one
is brave enough to just delete them.

Without tests the project starts to get harder to maintain. Small changes can
explode things in unexpected places and the team's motivation drops down and
then everyone will again just want for the new project, the fresh start, the
chance to make things right.

I know sometimes it's hard to maintain the tests and keep them running and useful, but trust me, good tests will
pay off well. Good tests will prevent sending issues to production.

Good tests can also help newcomers to the project, because they can read code
and tests in order to understand a given behavior and, of course, tests will fail if something is wrong, and that is
usually the case when making your first changes in a project :)

My message here is: Don't give up on your tests. Please! Tests will help keep
your project healthy, keep your team not afraid of changes and keep devs happy
(or, at least, not sad or afraid).
