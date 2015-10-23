---
layout: post
title: Make it testable
categories:
- development
- unittests
- cleancode
tags:
- development
- unittests
- cleancode
- php
status: publish
type: post
published: true
mainimage: "general/tests.png"
---

I really like the way Symfony is changing the PHP community and in general
leading us to a better place.  It's really nice to see people using good
practices in their daily work and pet projects.

But I still have one concern with Symfony2 projects: The heavy dependency on
the **container**. I mean, don't get me wrong, Dependency Injection Containers
are great, but the way they are usually used is where the problem lies. Look
at this example:

```php
<?php

use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Response;

class StuffController extends Controler
{
    /**
     * @access public
     * @return Response
     */
    public function addStuffAction()
    {
        $request = $this->container->get('request');

        if ('POST' == $request->getMethod()) {
            $stuff = $this->buildStuffFromRequest($request);

            $stuffRepository = $this
                ->container
                ->get('doctrine')
                ->getEntityManager()
                ->getRepository('StuffBundle:Stuff');

            $stuffRepository->add($stuff);

            return new Response('Ok', 200);
        }

        return new Response('Bad request', 400);
    }
}
```

It does not look bad, right? It is just a simple action receiving some data
and persisting it to the database via a repository method.

Now, try to unit test it.

By the way, I'm not going to discuss whether or not Controllers should be tested. The
thing is trying to test this controller that heavily depends on the Container.

In order to test it you will have to mock the container and inject it, which is
not that hard, since there is already a method **setContainer()** in the
**ContainerAware** class. But things get more complicated when you try to build
a container to mock Doctrine, EntityManager and then the repository.

But the real problem here is that the dependencies for this controller to properly work
are not clear, one must read the code in order to find out all **container->get()**
calls and then go after the services or objects embedded in the container.

One way to make it better and have your dependencies explicit is adding the actual
dependencies as properties of the class and injecting them in the constructor.
Here is an example:

```php
<?php

use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Response;
use StuffInc\StuffBundle\Entity\StuffRepository;

class StuffController extends Controler
{
    /**
     * @var StuffRepository
     * @access private
     */
    private $stuffRepository;

    /**
     * @param StuffRepository $stuffRepository
     * @access public
     */
    public function __construct(StuffRepository $stuffRepository)
    {
        $this->stuffRepository = $stuffRepository;
    }

    /**
     * @access public
     * @return Response
     */
    public function addStuffAction()
    {
        $request = $this->container->get('request');

        if ('POST' == $request->getMethod()) {
            $stuff = $this->buildStuffFromRequest($request);

            $this->stuffRepository->add($stuff);

            return new Response('Ok', 200);
        }

        return new Response('Bad request', 400);
    }
}
```

Now it is easier do inject a StuffRepository to the testing. But there is still
one wild dependency to cover, the **Request**:

```php
<?php

use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
use StuffInc\StuffBundle\Entity\StuffRepository;

class StuffController extends Controler
{
    /**
     * @var StuffRepository
     * @access private
     */
    private $stuffRepository;

    /**
     * @param StuffRepository $stuffRepository
     * @access public
     */
    public function __construct(StuffRepository $stuffRepository)
    {
        $this->stuffRepository = $stuffRepository;
    }

    /**
     * @param Request $request
     * @access public
     * @return Response
     */
    public function addStuffAction(Request $request)
    {
        if ('POST' == $request->getMethod()) {
            $stuff = $this->buildStuffFromRequest($request);

            $this->stuffRepository->add($stuff);

            return new Response('Ok', 200);
        }

        return new Response('Bad request', 400);
    }
}
```

This one was easier, since the request is a dependency only for the method, not
for the whole class. Now it is possible to easily mock the Repository and the
Request and test this controller and what is even better the dependencies are as
clear as the day light.
