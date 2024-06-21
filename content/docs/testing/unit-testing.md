---
title: "Unit Testing"
draft: false
weight: 9
---

## Setup

Unit tests run against your default database. Some of them rely on fixtures. To run unit tests, simply run:

`python manage.py test`

If you are using PyCharm, you'll need to update your run configuration. Set **Custom Settings** to the `base.py` file in `ourchive_app.settings`.

## Considerations

1. Use mocks for external services
2. Wherever possible, move API data processing outside of the API-dependent views; test inputs and outputs independently of the actual Django Rest Framework functionality.
3. Wherever possible, use object instantiation and calls to __dict__ or JSON over hardcoded JSON; this ensures tests adapt when data contracts change (or fail because, as intended, they caught a bug).

## For PRs

As described in our [contributor documentation]({{<ref "drive_by_pr.md">}}), we do prefer high unit test coverage for PRs. But, this is not a standard we ourselves currently meet. Please do your best, and if the architecture of the codebase is preventing effective testing, call this out in your PR. Refactoring is a fact of life - feedback from other developers helps us decide what to prioritize!