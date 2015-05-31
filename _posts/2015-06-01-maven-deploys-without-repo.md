---
layout: post
title: How can we deploy public Maven artifacts without a repository?
summary: To deploy nicely in the cloud we need publicly available artifacts, but how can we do that without having to run our own repository?
author: Simon Casey <a href="https://github.com/simoncasey"><i class="fa fa-github-square"></i></a> <a href="https://twitter.com/simoncasey1982"><i class="fa fa-twitter-square"></i></a>
comments: true
---

## Some background ...
[DashboardHub](http://dashboardhub.io) is moving to a microservice architecture to provide hooks into all the APIs we will use (GitHub, Travis, etc). Many of these microservices will be implemented in Java and deployed into a 'mini Heroku' environment called '[Dokku](http://progrium.com/blog/2013/06/19/dokku-the-smallest-paas-implementation-youve-ever-seen/)'. Dokku uses [Heroku](https://devcenter.heroku.com/categories/java) build packs so for our purposes it works in the same way at deploy time - we use Java, therefore [Apache Maven](https://maven.apache.org/) is our build tool.

## On to the issue
We have a shared library that is used by many of these Java microservices. Since Maven is handling our dependencies, it makes sense for this shared library to be made available to Dokku/Heroku during deployment/build as the appropriate Maven artifact. Here lies the problem - this artifact needs to be publically available.
Typically, maven artifacts are made available in this way by:

1. Signing up to Maven Central repository and then deploying there
2. Running your own publicly accessible repository and serving the artifacts (eg [Nexus](http://www.sonatype.org/nexus/), [Artifactory](http://www.jfrog.com/artifactory/))
3. Using some funky awkwardness to serve the artifact from github pages or some other host

So what did we choose? **None of them**.

- Option 1 involves signing up with Sonatype for access (something that is possible in the future once we become more stable and established)
- Option 2 is too complicated and too much of an admin/cost/time sync.
- Option 3 is just a pain and pretty inflexible - it's not how maven is meant to be used

## Tell us what you actually did damnit!
What I really wanted was for there to be a way of using GitHub as the artifact repository (like [Composer](https://getcomposer.org/) does for PHP for instance). Sadly this doesn't quite fit with Maven - you need a jar file, not source.

**Enter [JitPack.io](https://jitpack.io/)**

This excellent project will automatically build and publish a maven artifact from a GitHub repository!! All you need to do is to add their repository to your maven pom.xml, and then name your dependency appropiately. Upon the first request by anything of the dependency, it is pulled from GitHub, built and then returned. Cached for later whenever need too.
JiPack.io uses the GitHub 'releases' functionality to drive the artifact naming which makes it flexible, at the cost of potentially dirtying your project's releases history. Just mark them all as 'pre-release' for dev/snapshot equivalent versions. Alternatively, you can specifiy a commit id instead of a release.

It's a great project, and a useful way for smaller teams or open source projects to make their maven artifacts available. You can also use [Gradle](https://gradle.org/) with JitPack.io if that is your thing and they support private repos too. If you need help, the team is super-friendly and available on their [Gitter channel](https://gitter.im/jitpack/jitpack.io).

---

- [JitPack.io](https:jitpack.io)
- [JitPack.io GitHub](https://github.com/jitpack/jitpack.io)

---

To keep up-to-date please follow us on [Twitter](https://twitter.com/dashboardhub)

And feedback and/or suggestions please log on [Github Issues](https://github.com/DashboardHub/PipelineDashboard/issues)
