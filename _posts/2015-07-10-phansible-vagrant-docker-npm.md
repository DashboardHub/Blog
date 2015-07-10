---
layout: post
title: Phansible provisionings for PHP-based projects and more
summary: Phansible with vagrant, ansible, docker and npm
author: Eddie Jaoude <a href="https://github.com/eddiejaoude"><i class="fa fa-github-square"></i></a> <a href="https://twitter.com/eddiejaoude"><i class="fa fa-twitter-square"></i></a>
comments: true
alert: DRAFT  / WORK IN PROGRESS
---

I have used quite a few provisionings tools in the past from Puppet, Chef, Saltstack etc and more recently Docker. Each one has its pros and cons. Docker was working great until I upgrade my boot2docker vm and all kept failing even after a re-initialise each time. This made me realise that I should provision my own Docker VM for my Mac.

I heard lots of good things about Ansible from the PHP community and this is one I had not tried. Knowing of Phansible, I thought it would be a good starting point. And it was a great starting point! I got a development environment VM up and running very quickly with the basics: PHP, MySQL, Apache2 (or Nginx).

But for me (and probably most) that was not enough. I needed Docker & npm. After a quick search, Ansible has modules for these.

## NPM dependencies

For **npm**, it is as simple as:

```yaml
- name: install npm
  apt:  pkg=npm state=present

- name: install global node packages
  npm: name={{item}} global=yes
  with_items:
    - bower
    - grunt-cli
    - express
    - socket.io
```

## Docker containers

And for **Docker**, it is:

```yaml
- name: redis container
  docker:
    name: redis
    image: redis
    state: started
    ports:
      - "6379:6379"
```
