---
layout: post
title: Symfony Controller not extending FOSRest Bundle
summary: Symfony Controller Best Practice by not extending a Base Controller but injecting dependencies
author: Eddie Jaoude <a href="https://github.com/eddiejaoude"><i class="fa fa-github-square"></i></a> <a href="https://twitter.com/eddiejaoude"><i class="fa fa-twitter-square"></i></a>
comments: true
tags: symfony, controller, best practices, dependency injection
alert: DRAFT  / WORK IN PROGRESS
---

Most examples of a **Symfony Controller** extend `FOSRestController`. This is not ideal, it is better to have **Controllers** as a **Service**, just like any other **Service**. This is much easier to **Unit Test** with tools like **PHPUnit** and **PHPSpec** and then forces the **Controllers** to do less and have less dependencies - we all like *Thin Controllers*.

Below is a *standard* example of a **Controller**.

```php
<?php

namespace Your\Namespace

use FOS\RestBundle\Controller\FOSRestController;

class UsersController extends FOSRestController
{
    public function getUsersAction()
    {
        $data = ...; // get data, in this case list of users.

        return $this->handleView(
            $this->view($data, 200)
        );
    }
}
```

To run it as a **Service** is quite easy and **Decouples** it from **Symfony FOSRest Bundle**, which will look like below.

```php
<?php

namespace Your\Namespace

class UsersController
{
    /** @var Controller */
    private $controller;

    /**
     * @param Controller $controller
     */
    public function __construct(Controller $controller)
    {
        $this->controller = $controller;
    }

    public function getUsersAction()
    {
        $data = ...; // get data, in this case list of users.

        return $this->controller->handleView(
            $this->controller->view($data, 200)
        );
    }
}
```

I introduced a new class here called **Controller**, this will *proxy* through to the **Symfony FOSRestController** - it too will have **Unit Tests**.

```php
<?php

namespace Your\Namespace

use FOS\RestBundle\View\View;
use FOS\RestBundle\View\ViewHandler;

/**
 * Class Controller
 */
class Controller
{

    /** @var ViewHandler */
    private $viewHandler;

    /** @var View */
    private $view;

    /**
     * @param ViewHandler $viewHandler
     * @param View $view
     */
    public function __construct(ViewHandler $viewHandler, View $view)
    {
        $this->viewHandler = $viewHandler;
        $this->view        = $view;
    }

    /**
     * @param View $view
     *
     * @return \Symfony\Component\HttpFoundation\Response
     */
    public function handle(View $view)
    {
        return $this->viewHandler
            ->handle($view);
    }

    /**
     * @param  array $data
     * @return View
     */
    public function setData(array $data)
    {
        return $this->view
            ->setData($data);
    }
}
```

The `services.yml` will look something like this

```yaml
services:
    your_app.fos_rest.view.view:
        class: FOS\RestBundle\View\View
        factory: [FOS\RestBundle\View\View, create]

    your_app.controller:
        class: Your\Namespace\Controller\Controller
        arguments: [@fos_rest.view_handler, @your_app.fos_rest.view.view]

    your_app.controller.users:
        class: Your\Namespace\Controller\UsersController
        arguments: [@your_app.controller]
```

I hope that helps. Feedback welcome.
