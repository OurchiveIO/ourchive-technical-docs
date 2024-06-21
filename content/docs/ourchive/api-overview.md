---
title: "API"
weight: 4
toc: true
---

Ourchive uses Django Rest Framework and auto-generated API documentation. Despite the package name, our API is not pure REST, but it is meant to function as a headless API that others can build clients for. 

<!--more-->


## Docs

You can access API docs on our <a href="https://ourchive.io/api/redoc/" target="_blank" title="API docs">beta site</a>.

## Permissions

Ourchive has a number of custom permissions, including permissions based on admin settings like Registration Permitted. All permissions are centralized in `permissions.py` and follow the DRF documentation's examples.

## CRUD Customization

Business logic relevant to the archive is encapsulated at the serializer layer wherever possible. This includes clearing/adding tags on work or bookmark save, validating permissions to comment, and other mission-critical logic. 

As a rule, authorization will always have checks at the API layer. 

We have done our best to document areas where the API will update related objects. If you encounter any unexpected behavior, [let us know]({{< relref "developer_community" >}}).

## Notes & Roadmap

One of our top priorities after MVP launch is integration with OAUTH for true headless functionality. We welcome PRs for other auth schemes as well.

If you are developing a client and running into issues or simply have questions about the API's structure or functionality, feel free to [contact us]({{< relref "developer_community" >}}).