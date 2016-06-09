---
title: Skeddly API Reference

language_tabs:
  - http
  - shell: curl

toc_footers:
  - <a href='https://app.skeddly.com/Account/Register'>Sign-up for a Skeddly account</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - actionExecutions
  - actions
  - regions
  - timeZones
  - models
  - apiClients
  - errors

search: true
---

# Introduction

Welcome to the Skeddly API.

This API is organized as a [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)ful API:

* URLs are organized into "resources", and
* Appropriate HTTP methods, such as GET, POST, PUT, and DELETE are used.

[Cross-origin resource sharing](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing), or CORS, is fully supported.

POST and PUT requests support [JSON](http://www.json.org/) in the body of the request.

All responses, successes and failures, return [JSON](http://www.json.org/).

# Making Requests

All API requests must be made to the following endpoint:

`https://api.skeddly.com/api/`

All requests must use HTTPS.

By default, some properties of some response models may be omitted from responses. This is for performance reasons. To include those properties, specify them in the request's `include` query parameter.

# Authentication

> To authorize, use this code:

```http
GET /api/resource HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: AccessKey <api key>"
```

> Make sure to replace `<api key>` with your API key.

In order to use the Skeddly API, you require an API key. API keys can be obtained by doing the following:

1. Sign-in to your Skeddly account.
2. Click your username on the top-right of the page, then click "Account Settings".
3. Scroll down to the "API Key Management" section, and click "Manage API Keys".
4. Click the "Create API Key" button to create an API key.

When making HTTP requests, all requests must include the "Authorization:" header in the following format:

`Authorization: AccessKey <api key>`

<aside class="notice">
You must replace <code>&lt;api key&gt;</code> with your personal API key.
</aside>

