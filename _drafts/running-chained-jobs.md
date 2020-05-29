---
layout: post
title: Running chained jobs
description: Ever got yourself in a situation where you had to run jobs in a sequence in a given schedule? This is an interesting case I found while maintaining a chain of commands that depend on the previous one's output to run.
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
mainimage: "the_chain.jpg"
image_url: "https://www.flickr.com/photos/58134/4510594507"
image_author: "thierry ben abed"
---

Recently I found myself maintaining an interesting piece of code.

It is a sequence of Symfony Commands to do some calculation and publish the results.
It was a sequence of around 8 commands doing each one its part of the process, all independent
of each other but also dependent of the previous command's output. Almost like chaining commands
on Unix using the pipe operator.

Putting it on a more visual way, it looked like this:

![Classes depending on each other to run chained commands](/assets/images/chained_commands.png)

This implementation was using a `trait` in PHP to make the commands `Chainable`, so to speak, kind
of an interface like this:

![The Chainable Interface](/assets/images/interaface_chainable.png)

After each command finished running the trait was checking if the `$nextCommand` was set for then
starting a new `Symfony Process` calling it. Each subsequent command was doing the same until there
was no more `$nextCommand` defined. Yes, this sounds a lot like a `Chain of Responsibility` pattern,
but it is not.

This is not a bad solution and it works nicely.

There is one problem however. It is not possible to run each command in isolation, making it harder
to test.

There is another problem. This one is more about software architecture: As described by **Ken Pugh** in
his book **Interface-Oriented Design**:

*An interface's implementation shall do what its methods says it does*

This is the first law of interfaces.

Let's say the first command on that chain is called "calculate-overpriced-products". When using this
command one would expect to have a list of over priced products. Instead the next command would run,
then next, and the next, and the next... Until the whole chain is finished and the output would be a list of
best priced products. You call the command expecting A and it gives you Z.

Anyway, I was working on making those commands auto-retry-able, like, if it fails it should try itself
again and again. After some time trying to extend the `Chainable` concept and applying it into something
like `Retryable` I realised I was going in the wrong direction.

Why? Again, thanks to **Ken Pugh's** and his third **Law of Interfaces**:

*If an implementation is unable to perform its responsibilities, it shall notify its caller*.

This is what made me realise the whole concept was wrong.

I removed all the code related to make the commands `Chainable`, because one command should do one thing
and one thing alone.

I added then a kind of Front Controller or Orchestrator that is responsible for calling all the commands
in the correct sequence and to retry them in case of failure.

The new structure is now like this:

![One main controller calling the commands](/assets/images/controlled_commands.png)

Now, when a command fails it will notify the caller, in this case, the `Controller`, that will retry the
command until completion. In PHP using `Symfony Process` a simple implementation of the `Controller` looks
like this:

{% highlight php %}
<?php

namespace Commands\MainCommand;

use Symfony\Component\Console\Command\Command;
use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Output\OutputInterface;
use Symfony\Component\Process\Process;

class MainCommand extends Command
{
    protected function configure()
    {
        $this
            ->setName('commands:main')
        ;
    }

    protected function execute(InputInterface $input, OutputInterface $output)
    {
        $commandsToRun = [
            'commands:command1',
            'commands:command2',
            'commands:command3',
            'commands:command4',
        ];

        foreach ($commandsToRun as $command) {
            $didItWork = false;

            while (! $didItWork) {
                $didItWork = $this->runCommand($command);
            }
        }
    }

    private function runCommand($command) {
        $commandline = sprintf(
            'php bin/console %s',
            $command
        );

        $process = new Process($commandline);
        $process->disableOutput();
        $process->setTimeout(null);
        $process->run();

        return $process->isSuccessful();
    }
}
{% endhighlight %}

Now the main controller can retry the failed commands and the commands do not know they are
part of a chain anymore. The commands now the have an input and they generate some output, an
that is it, one responsibility per command.

Happy hacking.
