---
layout: post
title: Great Open Source tools DashboardHub use
summary: We use a lot of Open Source tools and we want to say 'Thank You'
author: Eddie Jaoude <a href="https://github.com/eddiejaoude"><i class="fa fa-github-square"></i></a> <a href="https://twitter.com/eddiejaoude"><i class="fa fa-twitter-square"></i></a>, Simon Casey <a href="https://github.com/simoncasey"><i class="fa fa-github-square"></i></a> <a href="https://twitter.com/simoncasey1982"><i class="fa fa-twitter-square"></i></a>
comments: true
alert: DRAFT  / WORK IN PROGRESS
---

Here at **DashboardHub** we use a lot of **Open Source** tools and libraries! Thats why we not only contribute back to these tools in various ways ([ways to support Open Source tools](/2015/06/08/supporting-open-source-projects/)) but also give our Applications & Tools back to the community as **Open Source**.

Lets break this down into sections:

### Communication

Our team works fully remotely, therefore communications and collaboration are key! These tools are vital to **DashboardHub**:

* [Gitter.im](gitter.im) - chat room via the browser
* [Appear.in](appear.in) - video conferencing, includes desktop sharing, all via the browser

---

### Static Code (blog, website etc)

Not all websites need to be written in PHP or Java etc. Static informational websites (eg. blogs) are best suited to keeping things simple. Jekyll and GitHub pages are perfect for this. Write pages in Markdown and host on GitHub - continuous delivery for free.

* [GitHub pages](https://pages.github.com) - hosting static pages
* [Jekyll](http://jekyllrb.com) - markdown to html blogging platform

---

### Services we use

There is no point reinventing the wheel. We could host our own Git repo, manage emails, build user feedback etc, but there is no point, this is already done well for us and very easy to setup.

* [GitHub](https://github.com) (no explanation needed here, just pure awesomeness)
* [Zoho](https://www.zoho.com) - email hosting
* [Doorbell](https://doorbell.io/home) - user feedback

---

### Our Micro Service and Friends (main part of DashboardHub)

The DashboardHub architecture is split into **micro services**, this allows for high flexibility.

#### PHP

* [PHPStorm](https://doorbell.io/home) - PHP IDE
* [Composer](https://getcomposer.org) - Dependency Manager for PHP
* [Doctrine](http://www.doctrine-project.org) - ORM
* [Symfony2](http://symfony.com) - MVC Framework

#### Java

* [Spring Boot](http://projects.spring.io/spring-boot/) - all the features of the Spring platform, without all the config hassle
* [JitPack.io](https://jitpack.io/) - A novel way to use GitHub as your maven/gradle repository
* [IntelliJ IDEA](https://www.jetbrains.com/idea/) - without doubt the best IDE for just about any language
* [JSONServer / jsonplaceholder](https://github.com/typicode/json-server) - handy tool to fake an API for prototyping

#### Clientside

* [AngularJS](https://angularjs.org)
* [Twitter Bootstrap](http://getbootstrap.com)
* [FontAwesome](http://fontawesome.io/)

#### Friends

* [MySQL](http://www.mysql.com)- database
* [ElasticSearch](https://www.elastic.co) - search and analytics

---

### DevOPs (a current buzz word, I am still waiting for *DevTestOps* or *DevTest* to take off)

* [Digital Ocean](https://www.digitalocean.com) - simple & fast hosting
* [Dokku](http://progrium.viewdocs.io/dokku/) - private Heroku using Docker (baby brother of DEIS)
* [Git](https://git-scm.com) - version control and deployment
