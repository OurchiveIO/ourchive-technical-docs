---
title: "Basic Principles"
date: 2020-11-12T13:26:54+01:00
lastmod: 2020-11-12T13:26:54+01:00
draft: false
resources:
  - name: stop-programming-computers
    src: "stop_programming_computers.jpeg"
    title: Stop programming computers
    params:
      credits: "The Internet"
menu:
  docs:
    parent: "usage"
weight: 610
toc: true
---

If you're considering developing against the Ourchive codebase, either as a project contributor or by forking the project, **we are delighted to have you**. The below information functions as a set of guidelines we apply when scoping and building features, and is meant to help prospective developers understand what we're all about.

<!--more-->



## Technical Principles

### Settings

Ourchive is built with the goal of **maximum configurability**. We want users to have settings to control their experiences, and we want admins to be able to enable/disable features as they see fit. 

Our own scoped features will always include information about the expected level of configurability. If you want to PR a feature that's not on our roadmap, please do! If it's a feature that's brand new to the archive, please ensure its behavior can be controlled by settings as much as feasible.

### Django Admin

Ourchive has made the conscious decision to leverage the admin site as much as possible. We want our admins to have ownership over their app, and using the admin site allows us to mitigate the need for external dependencies. If someone wants to run Ourchive without email, they can, thanks to the admin site. 

### Django Rest Framework

Currently, Ourchive uses Django Rest Framework for ease of headless development. For Ourchive API v2.0, that might change; if we run into performance issues with our vanilla DRF setup, that might change sooner than 2.0. (When is 2.0, you ask? Great question! Years away from MVP.) 

If you have tips, tricks, or optimizations for DRF or its supported plugins, please feel free to let us know or PR your fix! As we scale, we'll be scrutinizing performance more and more.

## Design Principles

### User Safety

On the internet no one knows you're a dog but they do know what buttons to press to fuck your life up. Any feature we spec will have associated trust & safety acceptance criteria.

If you PR a new-to-us feature that lets users collaborate, be that something obvious like direct messaging or something tangential like profile badging, please ensure you've thought through how the feature might be misused and built in settings to handle for common abuse vectors.

### Dependency Management

There are so many cool tools online and all of them have versions.

![A meme: stop programming computers! Sand wasn't meant to think.](/images/stop_programming_computers.jpeg)

We're always trying to walk the fine line of "don't roll your own" vs "a manageable dependency chain". Wherever possible, our specced features will specify what dependencies and level of complexity we expect. If you're PR'ing something new, you guessed it, please try to limit dependencies or allow admins to disable the functionality that depends on third-party applications or installations. 

## Have Fun With It: The Principle

Having said all that, ultimately, we are here to have fun. If you want to contribute but you're only gravitating towards the "fun stuff" like word wars or badging, that's totally fine! We want to give our users shit they enjoy in addition to a stable, scalable platform. We will welcome anything that improves the user's experience with open arms.