# Introduction

> API Endpoint: https://app.mertzcrew.com/api/

Welcome to the Mertzcrew API! You can use our API to access Mertzcrew API endpoints, which allow you to manage all aspects of your projects along with their assignments.

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

# General

## Get Country List

This endpoint retrieves a list of countries. You will need to specify a valid country ID when creating projects.

```bash
curl "https://app.mertzcrew.com/api/countries"
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": 230,
    "abbreviation": "GB",
    "name": "United Kingdom"
  },
  {
    "_id": 1,
    "abbreviation": "US",
    "name": "United States"
  },
  {
    "_id": 231,
    "abbreviation": "UM",
    "name": "United States Minor Outlying Islands"
  }
]
```

### HTTP Request

`GET https://app.mertzcrew.com/api/countries`

## Get State/Province List

This endpoint retrieves a list of states/provinces. You will need to specify a valid state/province ID and country combination when creating projects.

```bash
curl "https://app.mertzcrew.com/api/state_provinces"
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": 1,
    "name": "Alabama",
    "abbreviation": "AL",
    "country": 1,
    "taxes": []
  },
  {
    "_id": 2,
    "name": "Alaska",
    "abbreviation": "AK",
    "country": 1,
    "taxes": []
  },
  {
    "_id": 4,
    "name": "Arizona ",
    "abbreviation": "AZ",
    "country": 1,
    "taxes": []
  }
]
```

### HTTP Request

`GET https://app.mertzcrew.com/api/state_provinces`

# Projects

## Get Project Types/Classifications

This endpoint retrieves a list of your project types/classifications.

```bash
curl "https://app.mertzcrew.com/api/project_classifications" -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns JSON structured like this:

```json
[
  {
    "type": "Corporate"
  },
  {
    "type": "Integration"
  },
  {
    "type": "Touring"
  },
  {
    "type": "Other"
  }
]
```

### HTTP Request

`GET https://app.mertzcrew.com/api/project_classifications`

## Create Project

This endpoint creates a new project.

```bash
curl -d "@data.json" -H "Content-Type: application/json" -X POST "https://app.mertzcrew.com/api/project"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command requires data.json to have the following format:

```json
{
  "name": "Testing",
  "type": "Corporate",
  "country": 1,
  "state_province": 12,
  "city": "Orlando"
  ...
}
```

> For a complete list refer to the section POST parameters.

### HTTP Request

`POST https://app.mertzcrew.com/api/project`

### POST Parameters

Parameter | Description
--------- | -----------
name | The name of the project
type | The project type/classification
country | The country where this project is located
state_province | The state/province in the country specified
city | The city of the state/province specified

## Edit a Specific Project

This endpoint edits a specific project.

```bash
curl -d "@data.json" -H "Content-Type: application/json" -X PUT "https://app.mertzcrew.com/api/project/1"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command requires data.json to have the following format:

```json
{
  "_id": "569702a6026b03086fa378c8",
  "name": "Testing API",
  "country": 1,
  "state_province": 12,
  "city": "Orlando"
  ...
}
```

> For a complete list refer to the section PUT parameters.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`PUT https://app.mertzcrew.com/api/project/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project you are editing 

### PUT Parameters

Parameter | Description
--------- | -----------
_id | The ID of the project
name | The name of the project
country | The country where this project is located
state_province | The state/province in the country specified
city | The city of the state/province specified

## Delete a Specific Project

This endpoint deletes a specific project.

```bash
curl -X DELETE "https://app.mertzcrew.com/api/project/1"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns an HTTP status code of 200 if successful. Refer to the Error section for error codes.

<aside class="warning">
Only projects you have access to are usable with this endpoint.
</aside>

### HTTP Request

`DELETE https://app.mertzcrew.com/api/project/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project to delete

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

## Generate Services - Internal Report Excel Spreadsheet

This endpoint generates an internal services report excel spreadsheet for a specific project supplied by ID.

<aside class="notice">
Upcoming release - check back soon.
</aside>

## Generate Services - Client Report Excel Spreadsheet

This endpoint generates an client services report excel spreadsheet for a specific project supplied by ID.

<aside class="notice">
Upcoming release - check back soon.
</aside>

## Generate Expense Report Excel Spreadsheet

This endpoint generates an expense report excel spreadsheet for a specific project supplied by ID.

<aside class="notice">
Upcoming release - check back soon.
</aside>

## Generate Per Diem Report Excel Spreadsheet

This endpoint generates an per diem report excel spreadsheet for a specific project supplied by ID.

<aside class="notice">
Upcoming release - check back soon.
</aside>

## Generate Crew List Report Excel Spreadsheet

This endpoint generates an client list report excel spreadsheet for a specific project supplied by ID.

<aside class="notice">
Upcoming release - check back soon.
</aside>

# Assignments

## Get All Project Assignments

This endpoint retrieves all assignments for a specific project.

```bash
curl "https://app.mertzcrew.com/api/project/1/contractors"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns JSON structured like this:

```json
[{
  "_id": "2",
  "department": "Audio",
  "status": "Accepted",
  "modified_by": "57ab828fd9f336f86f3b1be8",
  "modified_on": "2018-05-29T15:09:32.877Z",
  "daily_rate": 350,
  "start_date": "2018-06-11T12:00:50.290Z",
  ...
}]
```
<aside class="warning">
Only project assignments you have access to are returned by this endpoint.
</aside>

### HTTP Request

`GET https://app.mertzcrew.com/api/project/<ID>/contractors`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project to retrieve all assignments

## Get a Specific Project Assignment

This endpoint retrieves a specific assignment for a specific project.

```bash
curl "https://app.mertzcrew.com/api/project/1/contractor/2"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "2",
  "department": "Audio",
  "status": "Accepted",
  "modified_by": "57ab828fd9f336f86f3b1be8",
  "modified_on": "2018-05-29T15:09:32.877Z",
  "daily_rate": 350,
  "start_date": "2018-06-11T12:00:50.290Z",
  ...
}
```
<aside class="warning">
Only a project assignment you have access to are returned by this endpoint.
</aside>

### HTTP Request

`GET https://app.mertzcrew.com/api/project/<PROJECT_ID>/contractors/<ASSIGNMENT_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The ID of the project to retrieve the assignment from
ASSIGNMENT_ID | The ID of the assignment to retrieve

## Create Project Assignment

This endpoint creates a new assignment for a specific project.

```bash
curl -d "@data.json" -H "Content-Type: application/json" -X POST "https://app.mertzcrew.com/api/project/1/contractor"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command requires data.json to have the following format:

```json
{
  "contractor": "569702a6026b03086fa378c9",
  "contractor_role": "4",
  "daily_rate": 350,
  "pay_model": "564fda3fc4b109fc4a1726d4",
  "timesheets": [[{"start_date_time":"2018-08-19","end_date_time":"2018-08-19","break":null,"is_half_day":false,"is_travel":false,"no_time_entries":true},{"start_date_time":"2018-08-20","end_date_time":"2018-08-20","break":null,"is_half_day":false,"is_travel":false,"no_time_entries":true}]]
  ...
}
```

> For a complete list refer to the section POST parameters.

<aside class="warning">
Only project you have access to are usable with this endpoint.
</aside>

### HTTP Request

`POST https://app.mertzcrew.com/api/project/<ID>/contractor`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project to retrieve all assignments

### POST Parameters

Parameter | Description
--------- | -----------
contractor | The ID of the contractor if this assignment is for a contractor
employee | The ID of the employee if this assignment is for an employee
contractor_role | The ID of the role for this assignment
daily_rate | The rate amount for this assignment
pay_model | The ID of the employee 
timesheets | The schedule of the assignment - this is a JSON object with a start_date_time, end_date_time, break, is_half_day, is_travel, no_time_entries


## Edit a Specific Project Assignment

This endpoint edits a specific assignment for a specific project.

```bash
curl -d "@data.json" -H "Content-Type: application/json" -X PUT "https://app.mertzcrew.com/api/project/1/contractor/2"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command requires data.json to have the following format:

```json
{
  "_id": "569702a6026b03086fa378c8",
  "contractor": "569702a6026b03086fa378c9",
  "contractor_role": "4",
  "daily_rate": 350,
  "pay_model": "564fda3fc4b109fc4a1726d4",
  "timesheets": [[{"start_date_time":"2018-08-19","end_date_time":"2018-08-19","break":null,"is_half_day":false,"is_travel":false,"no_time_entries":true},{"start_date_time":"2018-08-20","end_date_time":"2018-08-20","break":null,"is_half_day":false,"is_travel":false,"no_time_entries":true}]]
  ...
}
```

> For a complete list refer to the section PUT parameters.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`PUT https://app.mertzcrew.com/api/project/<ID>/contractor/<ASSIGNMENT_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 
ASSIGNMENT_ID | The ID of the assignment you want to edit

### PUT Parameters

Parameter | Description
--------- | -----------
_id | The ID of the assignment
contractor | The ID of the contractor if this assignment is for a contractor
employee | The ID of the employee if this assignment is for an employee
contractor_role | The ID of the role for this assignment
daily_rate | The rate amount for this assignment
pay_model | The ID of the employee 
timesheets | The schedule of the assignment - this is a JSON object with a start_date_time, end_date_time, break, is_half_day, is_travel, no_time_entries

## Approve a Specific Project Assignment

This endpoint approves a specific assignment for a specific project.

```bash
curl -H "Content-Type: application/json" -X POST "https://app.mertzcrew.com/api/project/1/contractor/2/approve"
  -H "Authorization: xxxxxxxxxxxx"
```

> For a complete list refer to the section POST parameters.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`PUT https://app.mertzcrew.com/api/project/<ID>/contractor/<ASSIGNMENT_ID>/approve`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 
ASSIGNMENT_ID | The ID of the assignment you want to edit


## Delete a Specific Project Assignment

This endpoint deletes a specific assignment for a specific project.

```bash
curl -X DELETE "https://app.mertzcrew.com/api/project/1/contractor/2"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns an HTTP status code of 200 if successful. Refer to the Error section for error codes.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`DELETE https://app.mertzcrew.com/api/project/<ID>/contractor/<ASSIGNMENT_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 
ASSIGNMENT_ID | The ID of the assignment you want to edit

## Publish a Specific Project Assignment

This endpoint publishes a specific assignment for a specific project. This generates a contract or notification and sends it to the technician assigned.

```bash
curl -X POST "https://app.mertzcrew.com/api/project/1/publish/2"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns an HTTP status code of 200 if successful. Refer to the Error section for error codes.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`POST https://app.mertzcrew.com/api/project/<ID>/publish/<ASSIGNMENT_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 
ASSIGNMENT_ID | The ID of the assignment you want to edit

## Publish all Project Assignments

This endpoint publishes all assignments for a specific project. This generates any contracts and/or notifications for the assigned technician.

```bash
curl -X POST "https://app.mertzcrew.com/api/project/1/publish"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns an HTTP status code of 200 if successful. Refer to the Error section for error codes.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`POST https://app.mertzcrew.com/api/project/<ID>/publish`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 
ASSIGNMENT_ID | The ID of the assignment you want to edit

# Contractors

## Search for Contractors

This endpoint allows you to search our database of contractors.

```bash
curl -X GET "https://app.mertzcrew.com/api/contractor/search/stagehand"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns an HTTP status code of 200 if successful. Refer to the Error section for error codes.

### HTTP Request

`GET https://app.mertzcrew.com/api/contractor/search/<CRITERIA>`

### URL Parameters

Parameter | Description
--------- | -----------
CRITERIA | The text you want to use as your search criteria

## Get a Specific Contractor

This endpoint retreives a specific contractor.

```bash
curl -X GET "https://app.mertzcrew.com/api/contractor/1"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns an HTTP status code of 200 if successful. Refer to the Error section for error codes.

### HTTP Request

`GET https://app.mertzcrew.com/api/contractor/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the contractor you want to retrieve

# Employees

## Search for Employees

This endpoint allows you to search your employee database in Mertzcrew.

```bash
curl -X GET "https://app.mertzcrew.com/api/employee/search/stagehand"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns an HTTP status code of 200 if successful. Refer to the Error section for error codes.

### HTTP Request

`GET https://app.mertzcrew.com/api/employee/search/<CRITERIA>`

### URL Parameters

Parameter | Description
--------- | -----------
CRITERIA | The text you want to use as your search criteria

## Get a Specific Employee

This endpoint retreives a specific employee in Mertzcrew.

```bash
curl -X GET "https://app.mertzcrew.com/api/employee/1"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns an HTTP status code of 200 if successful. Refer to the Error section for error codes.

### HTTP Request

`GET https://app.mertzcrew.com/api/employee/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee you want to retrieve

# Timesheets

## Get all timesheets

This endpoint allows you to get all timesheet periods along with all timesheet entries.

<aside class="notice">
Upcoming release - check back soon.
</aside>

## Get a specific employee timesheet

This endpoint retreives a specific employee timesheet.

<aside class="notice">
Upcoming release - check back soon.
</aside>