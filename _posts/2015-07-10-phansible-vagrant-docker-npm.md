---
layout: post
title: Phansible provisionings for PHP-based projects and more
summary: Phansible with vagrant, ansible, docker and npm
author: Eddie Jaoude <a href="https://github.com/eddiejaoude"><i class="fa fa-github-square"></i></a> <a href="https://twitter.com/eddiejaoude"><i class="fa fa-twitter-square"></i></a>
comments: true
alert: DRAFT  / WORK IN PROGRESS
---

I have used quite a few provisionings tools in the past from Puppet, Chef, SaltStack etc. But more recently using containers with Docker. Each one has its pros and cons. Docker was working great until I upgraded my boot2docker VM and kept failing even after a re-initialise each time to do with keys - many others had the same issue. In my search for a solution that worked, it was recommended not to use boot2docker and provision a VM oneself; makes sense. This made me realise that I should provision my own Docker VM for my Mac, that I can recreate if anything goes wrong.

I heard lots of good things about Ansible (and Phansible) from the PHP community and this is one I had not tried. Knowing of Phansible from the community, I thought it would be a good starting point. And it was a great starting point! I got a development environment VM up and running very quickly with the basics: PHP, MySQL, Apache2 (or Nginx). With access to the webserver on `http://192.168.33.99/` and mysql on `192.168.33.99:3306`, elasticsearch on `192.168.33.99:9200` etc. [Dashboard for Phansible](http://pipeline.dashboardhub.io/d/5597eefd804c29.11877860).

But for me (and probably most) that was not enough. I needed Docker & npm. After a quick search, Ansible has modules for these too.

## npm dependencies

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

*Now we are cooking on gas!*

Phansible allowed me to install **xdebug** and **blackfire** with ease, so now I can step through my code for debugging and profile my application for performance improvements.

## Custimising system wide apt packages

Edit `ansible/vars/all.yml` and add to collect on line 4, looks like packages: [vim, htop, iotop]

## Customise what roles are installed

eg. Swap from Apache2 to Nginx (or vice versa)

Edit `ansible/playbook.yml` comment/uncomment roles collection.

## Profiling with Blackfire

Add your credentials to `ansible/vars/all.yml` and install the **Blackfire** chrome extension.

![Profiling with Blackfire](/assets/2015-07-10-phansible-vagrant-docker-npm/blackfire-profiling.mov.gif)

---

Full code can be found on [Github repo](https://github.com/eddiejaoude/vagrant-ansible-docker)

Suggestions / contributions etc all welcome.
