---
title: Frontend Overview
weight: -20
---

Ourchive has a standard Django frontend. Currently, we don't use class-based views; this may change as the project matures.

## Admin Site

Ourchive utilizes the admin site to allow administrators to control site features, manage users and user reports, and configure tags and attributes. 

## Internationalization and Translation

As Ourchive matured towards MVP, we began adding translation tags. I18n is a work in progress we expect to be complete with the 1.0 release. 

## Tests

Ourchive has a basic set of frontend unit tests, meant to validate data transformations/abstractions and provide a baseline level of smoke testing. You can find those in the `tests` folder.