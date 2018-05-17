# Introduction

Welcome to the Mertzcrew API! You can use our API to access Mertzcrew API endpoints, which allow you to manage all aspects of your projects along with their assigments.

We have language examples in Shell, and Javascript! Although these are REST Endpoints so this should work with any REST client/library. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```bash
# With shell, you can just pass the correct header with each request
curl "/login?output=json"
  -H "Authorization: xxxxxxxxxxxx"
```

```javascript
const mertzcrew = require('mertzcrew');

let api = mertzcrew.authorize('xxxxxxxxxxxx');
```

> Make sure to replace `xxxxxxxxxxxx` with your API key.

Mertzcrew uses API keys to allow access to the API. You can register a new Mertzcrew API key at our [app portal](http://app.mertzcrew.com/signup).

Mertzcrew expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: xxxxxxxxxxxx`

<aside class="notice">
You must replace <code>xxxxxxxxxxxx</code> with your personal API key.
</aside>

# Projects

## Get All Projects

```bash
curl "https://app.mertzcrew.com/api/projects"
  -H "Authorization: xxxxxxxxxxxx"
```

```javascript
const mertzcrew = require('mertzcrew');

let api = mertzcrew.authorize('xxxxxxxxxxxx');
let projects = api.projects.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all projects.

### HTTP Request

`GET https://app.mertzcrew.com/api/projects`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
available | true | If set to false, the result will include projects that have open positions.

<aside class="success">
Remember — a happy project is an authenticated project!
</aside>

## Get a Specific Project

```bash
curl "https://app.mertzcrew.com/api/projects/2"
  -H "Authorization: xxxxxxxxxxxx"
```

```javascript
const mertzcrew = require('mertzcrew');

let api = mertzcrew.authorize('xxxxxxxxxxxx');
let max = api.projects.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific project.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://app.mertzcrew.com/projects/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project to retrieve
