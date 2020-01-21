---
author: "Ben Gadbois"
date: 2020-01-20
title: "The Internet Is Not Yet Ready For Long TLDs"
weight: 10
---

<!--more-->

---
For a while, I tried using a .email domain name for my email address. The new world of TLD's continues to grow and diversify, and this was a perfect application.

As I started migrating online accounts to the new address, a number of website forms would reject it as an invalid email. Most used one of the following verifications  1) regex based TLD length requirement (.email being five would fail) 2) a whitelist of valid domains (of which did not include .email). About half the websites would only do a javascript based verification, which I could bypass with some clever `curl`ing, but the server-side verifications were a problem. Until websites drop these antiquated verifications, using a domain name that ends in .email will be a nuisance.

The non-Internet is also not ready. When answering questions in real life like "and what's your email?", I'd find skeptics think it wasn't a real address. I also came across people mishearing "dot gmail" instead of "dot email". With roughly half the people I told, there would be some issue.

I have since switched back to a traditional, boring .com domain name. Basic, but hassle free.
