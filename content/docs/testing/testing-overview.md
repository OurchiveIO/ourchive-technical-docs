---
title: "Testing Overview"
draft: false
weight: 8
toc: true
---

Ourchive is working with a pretty standard [Django setup](https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/unit-tests/) for testing: apps have one or more files that the test runner finds by naming convention. 

## Philosophy

Like many projects, we do not have as many tests as we should. However, we do try to leverage tests to validate the package prior to release. Having said that, a few guiding principles: 

* Unit tests should test as small a unit of code as feasible. 
* Happy path and sad path testing should be used.
* External services should be mocked.
* Wherever possible, unit tests should not rely on fixtures or other static data.
* Test complexity should drive code improvements: if a test requires a baroque arrangement of data to ensure a single specific response, and using mocks and other existing tools isn't feasible, that's a strong indicator that refactoring should be prioritized. 

## Existing Tests

* [Unit Testing]({{<ref "unit-testing.md">}})
* [Integration Testing]({{<ref "integration-testing.md">}})

## Known Issues

Some tests are skipped, either because they are broken or because they are flaky. You are welcome to debug and fix these. Speaking of which...

## We always welcome more tests.

Seriously.