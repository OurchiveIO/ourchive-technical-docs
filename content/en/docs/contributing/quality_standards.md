---
title: "Quality Standards"
date: 2020-11-12T13:26:54+01:00
lastmod: 2020-11-12T13:26:54+01:00
draft: false
images: []
menu:
  docs:
    parent: "contributing"
weight: 610
toc: true
---

We try to keep it short and sweet:

* We follow slightly modified PEP8 standards and strongly recommend a linter for this. Our max line length is 88 and our sole backend dev (hi) has the following PEP8 ignore rules configured in Sublime: "E203", "E231", "E309", "E501", "W503", "W191".
* We ask for 90% test coverage on PRs. Test coverage is an imperfect metric so this is not enforced as a code gate, but if 90% coverage isn't met, please let us know why.
* Please use exception handling and log warnings/errors.
* Stay [DRY](https://en.wikipedia.org/wiki/Don't_repeat_yourself).