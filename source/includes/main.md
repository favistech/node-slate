# Introduction

> API Endpoint: https://app.mertzcrew.com/api/

Welcome to the Mertzcrew API! You can use our API to access Mertzcrew API endpoints, which allow you to manage all aspects of your projects along with their assigments.

The Mertzcrew API is organized around REST. Our API has predictable, resource-oriented URLs, and uses a combination of HTTP response codes to indicate API errors along with a JSON payload for more specific error messages. 

We use built-in HTTP features, like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients. We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application using your username and password combination. JSON is returned by all API responses, including errors.

# Authentication

> To authorize, use this code:

```bash
# Make sure to replace `myUsername` with your username and `myPassword` with your password.
curl -X POST -F "username=myUsername" -F "password=myPassword" "https://app.mertzcrew.com/api/login"
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "message": "Login successful",
  "token": "xxxxxxxxxxxx"
}
```

Authenticate your account by using your username and password combination to the /login endpoint. Upon successful login, the JSON response will contain the attribute **token**. This **token** is required and is expected to be included in all API requests to the server in the header that looks like the following:

`Authorization: xxxxxxxxxxxx`

<aside class="notice">
You must replace <code>xxxxxxxxxxxx</code> with the token retrieved from the /login endpoint.
</aside>

# Projects

## Get All Projects

```bash
# With shell, you can just pass the authorization header with each request
curl "https://app.mertzcrew.com/api/projects"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "2",
    "type": "Corporate",
    "job_number": "AC-12345",
    "name": "Acme",
    "status": "Future Project",
    "end_date": "2018-06-15T22:00:50.296Z",
    "modified_by": "57ab828fd9f336f86f3b1be8",
    "modified_on": "2018-05-29T15:09:32.877Z",
    "start_date": "2018-06-11T12:00:50.290Z",
    ...
  }
]
```

This endpoint retrieves all projects.

### HTTP Request

`GET https://app.mertzcrew.com/api/projects`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
criteria |  | If specified, only projects that have a case insensitive match in their name or job number are returned.

<aside class="warning">
Only projects you have access to are returned by this endpoint.
</aside>

## Get a Specific Project

```bash
curl "https://app.mertzcrew.com/api/project/1"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "2",
  "type": "Corporate",
  "job_number": "AC-12345",
  "name": "Acme",
  "status": "Future Project",
  "end_date": "2018-06-15T22:00:50.296Z",
  "modified_by": "57ab828fd9f336f86f3b1be8",
  "modified_on": "2018-05-29T15:09:32.877Z",
  "start_date": "2018-06-11T12:00:50.290Z",
  ...
}
```

This endpoint retrieves a specific project.

<aside class="warning">
Only projects you have access to are returned by this endpoint.
</aside>

### HTTP Request

`GET https://app.mertzcrew.com/api/project/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project to retrieve
