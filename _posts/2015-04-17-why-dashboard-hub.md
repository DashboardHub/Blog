---
layout: post
title: Why was the DashboardHub created?
comments: true
---

[DashboardHub](http://dashboardhub.io) was created to fill a gap in a **Developer's** workflow. As **Developers** we have a lot of great tools at our disposal to help us to do our job and to do it well. However in our fast paced environment, we do not always have the time to log into different sites, until someone points a problem out, such as:

  > The **Build** is failing...The **Client** says the website is slow since the last deploy...and so on...
  
Following the above feedback, we then log into **CI** or in the **Metics** Application to see has the Server ran out of resource or is it a slow running script... and so the journey begins.  This journey may not only lead us down a rabbit hole, but it will almost certainly disrupts our daily work. Furthermore, working in this way is **Reactive**.  Would it not be better to be **Proactive** and solve issues before anyone noticed them? There is also an advantage in dealing with a particular issue at the time when we are working on that part of the project (rather than later) as it will be fresh in our mind.

**DashboardHub** was born. Initially with **PipelineDashboard** for public repositories, integrating with **Github**, **Travic CI** and **Scrutinizer**. In the Pipeline (pardon the pun), are Service like: VersionEye, Jira, Packagist, Pingdom...more ideas welcome and discussed on [Github Issue](https://github.com/DashboardHub/PipelineDashboard/issues/11).

---

## Initially a Proof of Concept was put together

The Pipeline Dashboard Proof of Concept was done in a couple of days and launched to get feedback from the *community*. Below is a screenshot of what it looked like:

![Proof of Concept Dashboard](/assets/screenshots/proof-of-concept.png)

---

## Dashboard Hub (aka Pipeline Dashboard) current State

Now this has moved onto a **Prototype** with more functionality, *Github OAuth login* to allow one to choose a **Dashboard Theme** and save, then share their **Dashboard**(s) while monitoring their statistics, search,

![Prototype of Concept Dashboard](/assets/screenshots/prototype.png)

---

To keep up-to-date please follow us on [Twitter](https://twitter.com/dashboardhub)

And feedback and/or suggestions please log on [Github Issues](https://github.com/DashboardHub/PipelineDashboard/issues)
