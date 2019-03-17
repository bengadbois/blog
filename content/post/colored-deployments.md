---
author: "Ben Gadbois"
date: 2019-03-17
title: "Colored Deployments"
weight: 10
---

<!--more-->

---

Many people are familiar with blue/green deployments. The basic idea is to have two production environments, one which is "green" and receives all traffic. A new version of an application is deployed to the idle "blue" environment. Traffic is slowly shifted over from the green environment until blue takes all traffic and green is now idle. If there is an issue with blue, traffic can quickly be shifted back to green, rolling back the change.

A variant is red/black deployments, where all the traffic is shifted at once, instead of gradually.

While these are valuable terms, they fail to encompass all types of deployments. I would like to propose the adoption a few new terms:

 * Green/Pitch Black - A network bug in the new version takes everything offline.
 * Silver/Gold - A feature in the new version causes third party services providers to charge more due to extra resources consumed.
 * Green/Slightly Darker Green - The new version has a corner case bug which goes unnoticed for months.
 * Green/Red/Blue - A bugfix is deployed, but there is a worse bug introduced in the new version. But the new version is no longer backwards compatible, so it requires a third version with another fix just to get things working again.
 * #blackandblue/#whiteandgold - An experimental user testing deployment, where some users see one thing, but other users who hit the exact same address see something else.
 * Rainbow - At an early stage startup where corners are cut for perceived velocity, and anybody can deploy anything anytime any way.
