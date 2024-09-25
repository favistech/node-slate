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

## Get Pay Models/Rules List

This endpoint retrieves a list of pay modes/rules. You will need to specify a valid pay model/rule ID when creating assignments.

```bash
curl "https://app.mertzcrew.com/api/pay_rules"
```

> The above command returns JSON structured like this:

```json
[
  {
      "_id": "5e59549c4e7ae3001342024d",
      "name": "Test Name",
      "is_default": false,
      "is_default_field_office": false,
      "is_hourly": true,
      "is_day_rate": false,
      "minimum_full_day_hours": 10,
      "enable_minimum_full_day_hours": false,
      "holiday_rate": "Premium",
      "enable_holiday_rate": true,
      "premium_pay_after_xhours": 10,
      "enable_premium_rate": true,
      "prime_pay_after_xhours": 16,
      "enable_prime_rate": false,
      "is_deleted": false,
      "weekly_ot_rate_after_xhours": 40,
      "same_day_if_less_then": 8,
      "late_night_start": "00:00",
      "late_night_end": "04:00",
      "late_night_rate": "Premium",
      "enable_late_night_rate": true
  }
]
```

### HTTP Request

`GET https://app.mertzcrew.com/api/pay_rules`

## Get Roles List

This endpoint retrieves a list of roles in the system.

```bash
curl "https://app.mertzcrew.com/api/contractor_roles"
```

> The above command returns JSON structured like this:

```json
[
  ...
  {
		"_id": 29,
		"department": {
			"_id": 2,
			"name": "Video"
		},
		"name": "ARS Technician",
		"responsibilities": "The Role of the Audience Response System (ARS) Technician involves:\nSetting up, configuring & instructing presenters on incorporating an ARS into the presentation.  Additionally, the technician will be able to deliver the tabulated results in real-time to the appropriate technician/presenter so that the audience response can be seamlessly incorporated into the show."
	},
	{
		"_id": 85,
		"department": {
			"_id": 1,
			"name": "Production"
		},
		"name": "Actor/Actress",
		"responsibilities": "Responsible for portraying a character in a performance or production. EDIT"
	},
  ...
]
```

### HTTP Request

`GET https://app.mertzcrew.com/api/contractor_roles`

## Get Role Departments List

This endpoint retrieves a list of department roles in the system.

```bash
curl "https://app.mertzcrew.com/api/contractor_role_departments"
```

> The above command returns JSON structured like this:

```json
[
  ...
	{
		"_id": 7,
		"name": "General",
		"contractor_roles": []
	},
	{
		"_id": 9,
		"name": "Integration",
		"contractor_roles": []
	},
  ...
]
```

### HTTP Request

`GET https://app.mertzcrew.com/api/contractor_role_departments`


## Get Skills List

This endpoint retrieves a list of skills in the system.

```bash
curl "https://app.mertzcrew.com/api/skills/all"
```

> The above command returns JSON structured like this:

```json
[
	...
  {
		"_id": "55a144cb95fec5358003ea00",
		"name": "Digico",
		"department": {
			"_id": "55a1401f95fec5358003e9c1",
			"name": "Audio"
		},
		"is_cert_validation_required": false,
		"is_cert_required": false,
		"is_system": true
	},
	{
		"_id": "55a144cb95fec5358003e9fc",
		"name": "Kara",
		"department": {
			"_id": "55a1401f95fec5358003e9c1",
			"name": "Audio"
		},
		"is_cert_validation_required": false,
		"is_cert_required": false,
		"is_system": true
	},
    ...
]
```

### HTTP Request

`GET https://app.mertzcrew.com/api/skills/all`

## Get Skill Departments List

This endpoint retrieves a list of skill departments in the system.

```bash
curl "https://app.mertzcrew.com/api/skill_departments"
```

> The above command returns JSON structured like this:

```json
[
	...
	{
		"_id": "55a1401f95fec5358003e9c3",
		"name": "General"
	},
	{
		"_id": "55a1401f95fec5358003e9c5",
		"name": "Integration"
	},
  ...
]
```

### HTTP Request

`GET https://app.mertzcrew.com/api/skill_departments`

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

## Final Approve a Specific Project

This endpoint final approves a specific project.

```bash
curl -H "Content-Type: application/json" -X POST "https://app.mertzcrew.com/api/project/1/approve_final"
  -H "Authorization: xxxxxxxxxxxx"
```

> For a complete list refer to the section POST parameters.

<aside class="warning">
Only projects you have access to are usable with this endpoint.
</aside>

### HTTP Request

`POST https://app.mertzcrew.com/api/project/<ID>/approve_final`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 

## Generate Services - Internal Report Excel Spreadsheet

This endpoint generates an internal services report excel spreadsheet for a specific project supplied by ID.

```bash
curl -H "Content-Type: application/json" -X GET "https://app.mertzcrew.com/api/project/<ID>/reports/services"
  -H "Authorization: xxxxxxxxxxxx"
```

<aside class="warning">
Only projects you have access to are usable with this endpoint.
</aside>

### HTTP Request

`POST https://app.mertzcrew.com/api/project/<ID>/reports/services`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project the report will be generated for.


## Generate Services - Client Report Excel Spreadsheet

This endpoint generates a client services report excel spreadsheet for a specific project supplied by ID.

```bash
curl -H "Content-Type: application/json" -X GET "https://app.mertzcrew.com/api/project/<ID>/reports/services_client"
  -H "Authorization: xxxxxxxxxxxx"
```

### HTTP Request

`GET https://app.mertzcrew.com/api/project/<ID>/reports/services_client`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project the report will be generated for.


## Generate Expense Report Excel Spreadsheet

This endpoint generates an expense report excel spreadsheet for a specific project supplied by ID.

```bash
curl -H "Content-Type: application/json" -X GET "https://app.mertzcrew.com/api/project/<ID>/reports/expense"
  -H "Authorization: xxxxxxxxxxxx"
```


### HTTP Request

`GET https://app.mertzcrew.com/api/project/<ID>/reports/expense`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project the report will be generated for.


## Generate Per Diem Report Excel Spreadsheet

This endpoint generates a per diem report excel spreadsheet for a specific project supplied by ID.

```bash
curl -H "Content-Type: application/json" -X GET "https://app.mertzcrew.com/api/project/<ID>/reports/per_diem"
  -H "Authorization: xxxxxxxxxxxx"
```


### HTTP Request

`GET https://app.mertzcrew.com/api/project/<ID>/reports/per_diem`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project the report will be generated for.


## Generate Crew List Report Excel Spreadsheet

This endpoint generates a client list report excel spreadsheet for a specific project supplied by ID.

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
contractor | The email address (or ID if known) of the contractor if this assignment is for a contractor
employee | The email address (or ID if known) of the employee if this assignment is for an employee
contractor_role | The ID of the role for this assignment
daily_rate | The rate amount for this assignment
pay_model | The ID of the pay rule/model 
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
<!--  -->

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
contractor | The email address (or ID if known) of the contractor if this assignment is for a contractor
employee | The email address (or ID if known) of the employee if this assignment is for an employee
contractor_role | The ID of the role for this assignment
daily_rate | The rate amount for this assignment
pay_model | The ID of the pay rule/model 
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

## Approve a Timesheet Entry for a Specific Project Assignment
This endpoint approves a specific timesheet entry assignment for a specific project.

```bash
curl -H "Content-Type: application/json" -X POST "https://app.mertzcrew.com/api/project/1/contractor/2/approve/3"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command requires data.json to have the following format:

```json
{
	"date": "2021-03-08T00:00:00" 
}
```

> For a complete list refer to the section POST parameters.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`POST https://app.mertzcrew.com/api/project/<ID>/contractor/<CONTRACTOR_ID>/approve/<TIMESHEET_ENTRY_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 
CONTRACTOR_ID | The ID of the contractor of the timesheet you want to edit
TIMESHEET_ENTRY_ID | The ID of the timehseet entry you want to edit

### POST Parameters

Parameter | Description
--------- | -----------
date | The date of the timesheet entry you would like to reject.

## Approve all Assignments for a Specific Project

This endpoint approves all assignments for a specific project.

```bash
curl -H "Content-Type: application/json" -X POST "https://app.mertzcrew.com/api/project/1/approve_all"
  -H "Authorization: xxxxxxxxxxxx"
```

> For a complete list refer to the section POST parameters.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`POST https://app.mertzcrew.com/api/project/<ID>/approve_all`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 

## Reject a Specific Project Assignment
This endpoint rejects a specifice assignment for a specific project.

```bash
curl -H "Content-Type: application/json" -X POST "https://app.mertzcrew.com/api/project/1/contractor/2/reject"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command requires data.json to have the following format:

```json
{
	"reason": "Please clarify your hours for this day", 
}
```

> For a complete list refer to the section POST parameters.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`POST https://app.mertzcrew.com/api/project/<ID>/contractor/<CONTRACTOR_ID>/reject`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 
CONTRACTOR_ID | The ID of the contractor of the timesheet you want to edit
TIMESHEET_ENTRY_ID | The ID of the timehseet entry you want to edit

### POST Parameters

Parameter | Description
--------- | -----------
reason | The message to the contractor for the rejection.

## Reject a Timesheet Entry for a Specific Project Assignment
This endpoint rejects a specific timesheet entry assignment for a specific project.

```bash
curl -H "Content-Type: application/json" -X POST "https://app.mertzcrew.com/api/project/1/contractor/2/reject/3"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command requires data.json to have the following format:

```json
{
	"reason": "Please clarify your hours for this day", 
	"date": "2021-03-08T00:00:00" 
}
```

> For a complete list refer to the section POST parameters.

<aside class="warning">
Only project assignments you have access to are usable with this endpoint.
</aside>

### HTTP Request

`POST https://app.mertzcrew.com/api/project/<ID>/contractor/<CONTRACTOR_ID>/reject/<TIMESHEET_ENTRY_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project of the assignment 
CONTRACTOR_ID | The ID of the contractor of the timesheet you want to edit
TIMESHEET_ENTRY_ID | The ID of the timehseet entry you want to edit

### POST Parameters

Parameter | Description
--------- | -----------
reason | The message to the contractor for the rejection of the timesheet entry.
date | The date of the timesheet entry you would like to reject.

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

## Get All Timesheets

This endpoint allows you to get all timesheet periods along with all timesheet entries.

```bash
curl -X GET "https://app.mertzcrew.com/api/employees/1/timesheets"
  -H "Authorization: xxxxxxxxxxxx"
```

> The above command returns JSON structured like this:

```json
{
    "results": [
        {
            "start_date": "2024-09-11T07:00:00.000Z",
            "end_date": "2024-09-17T07:00:00.000Z",
            "employees": [
                {
                    "_id": "57681dbfaf67a09d1f15bf1f",
                    "first_name": "Jeffery",
                    "last_name": "Atkisson",
                    "main_office": "ETP",
                    "main_office_id": "549630aa4f7b88bb3c8ed42d",
                    "employee_type": "",
                    "timesheet_id": "66e2f25d554b3fde54df1cb6",
                    "hours": 0,
                    "pto_hours": 0,
                    "low_rate_hours": 0,
                    "expenses": 0,
                    "per_diem": 0,
                    "status": "Awaiting Submittal"
                }
            ]
        }, 
```
<aside class="warning">
Only timesheets you have access to are returned by this endpoint.
</aside>

### HTTP Request

`GET https://app.mertzcrew.com/api/employees/<ID>/timesheets`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Client (client)


## Get a Specific Employee Timesheet

This endpoint retreives a specific employees timesheet.

```bash
curl -X GET "https://app.mertzcrew.com/api/employee/1/?timesheet_details=2"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command returns JSON structured like this:

```json
{
	"_id": "5e8ce8f10e28c20013236b7c",
	"user": {
		"_id": "5e8ce8f10e28c20013236b7b",
		"postal_code": "12345",
		"address": "123 Main Street",
		"last_name": "Iverson",
		"first_name": "Allen",
		"city": "Seattle",
		"state_province": {
			...
		},
		"username": "ai@aol.com",
		"country": {
			...
		},

```
<aside class="warning">
Only timesheets you have access to are returned by this endpoint.
</aside>


### HTTP Request

`https://app.mertzcrew.com/api/employee/<ID>/?timesheet_details=<timesheet_id>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee whose timesheet you want to approve
timesheet_id | The ID of the timesheet you want to approve


## Force Submit a Specific Employee Timesheet

This endpoint forces the submit of a specific employees timesheet.

```bash
curl -X POST "https://app.mertzcrew.com/api/employee/1/forcesubmit_timesheet"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command returns JSON structured like this:

```json
{
    "status": "success",
    "message": "Timesheet entries submitted successfully.",
    "data": {
        "forced_submit_by": "65132a2f6556fc001c84de9e",
        "forced_submit_on": "2024-09-22T19:55:40.896Z",
        "is_forced_submit": true,
        "submitted_on": "2024-09-22T19:55:40.896Z",
        "start_date": "2024-09-04T07:00:00.000Z",
        "end_date": "2024-09-10T07:00:00.000Z",
        "start_date_string": "20240904",
        "end_date_string": "20240910",
        "status": "Pending Approval",
        "_id": "66d87a33d15c1200159eff18",
    }
}
```
<aside class="warning">
Only timesheets you have access to can be submitted by this endpoint.
</aside>


### HTTP Request

`https://app.mertzcrew.com/api/employee/<ID>/forcesubmit_timesheet`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee you want to submit 

Body      | Description
--------- | -----------
timesheet_id | the ID of the timesheet you want to submit


## Clarify Employee Timesheet

This endpoint rejects/requests clarification for an employees timesheet. 

```bash
curl -X POST "https://app.mertzcrew.com/api/employee/1/reject_timesheet/2"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command returns JSON structured like this:

```json
{
	"status": "success",
	"message": "Timesheet entries submitted successfully.",
	"data": {
		"start_date": "2024-07-10T07:00:00.000Z",
		"end_date": "2024-07-16T07:00:00.000Z",
		"start_date_string": "20240710",
		"end_date_string": "20240716",
		"status": "Clarify",
		"_id": "66b14e2384e25463faf76b16",
		"hours": 0,
		"pto_hours": 0,
		"rate_hours": 0,

```
<aside class="warning">
Only timesheets you have access to can be clarified by this endpoint.
</aside>


### HTTP Request

`https://app.mertzcrew.com/api/employee/<ID>/reject_timesheet/<timesheet_id>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee you want to clarify 
timesheet_id | the ID of the timesheet you want to clarify




## Approve Employee Timesheet

This endpoint approves a specific employee timesheet. 

```bash
curl -X POST "https://app.mertzcrew.com/api/employee/1/approve_timesheet/2"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command returns JSON structured like this:

```json
{
	"status": "success",
	"message": "Timesheet entries submitted successfully.",
	"data": {
		"submitted_on": "2024-09-23T19:42:20.007Z",
		"is_forced_submit": true,
		"forced_submit_on": "2024-09-23T19:42:20.007Z",
		"forced_submit_by": "65132a2f6556fc001c84de9e",
		"rate_low_hours": 0,
		"rate_hours": 0,
		"pto_hours": 0,
		"hours": 0,
		"_id": "66c37950e64a8167aa419e48",
		"status": "Approved",
		"end_date_string": "20240813",
		"start_date_string": "20240807",
		"end_date": "2024-08-13T07:00:00.000Z",
		"start_date": "2024-08-07T07:00:00.000Z",
```


<aside class="warning">
Only timesheets you have access to can be approved by this endpoint.
</aside>


### HTTP Request

`https://app.mertzcrew.com/api/employee/<ID>/approve_timesheet/<timesheet_id>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee you want to approve 
timesheet_id | The ID of the timesheet you want to approve 


## Get Timesheet Details

This endpoint retrieves the details of a specific timesheet. 

```bash
curl -X GET "https://app.mertzcrew.com/api/employee/1?timesheet_details=2"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command returns JSON structured like this:

```json
{
	"_id": "5e8ce8f10e28c20013236b7c",
	"user": {
		"_id": "5e8ce8f10e28c20013236b7b",
		"postal_code": "12345",
		"address": "123 Main Street",
		"last_name": "Iverson",
		"first_name": "Allen",
		"city": "Seattle",
		"state_province": {
			...

```


<aside class="warning">
Only timesheets you have access to can be retrieved by this endpoint.
</aside>


### HTTP Request

`https://app.mertzcrew.com/api/employee/<ID>?timesheet_details=<timesheet_id>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee you want to retrieve 
timesheet_id | The ID of the timesheet you want to retrieve 


## Download Timesheets By Employee 

This endpoint retrieves the timesheets of a specific employee as an excel document. 

```bash
curl -X GET "https://app.mertzcrew.com/api/employee/1?timesheet_details=2&generate_report=application/vnd.ms-excel"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command returns an excel file (.xlsx) where content-type/mime-type is application/vnd.ms-excel


<aside class="warning">
Only timesheets you have access to can be retrieved by this endpoint.
</aside>


### HTTP Request

`https://app.mertzcrew.com/api/employee/<ID>?timesheet_details=<timesheet_id>&generate_report=application/vnd.ms-excel`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee whose timesheets you want to download 
timesheet_id | The ID of the timesheet you want to retrieve


## Download Timesheets By Client 

This endpoint retrieves the timesheets from a specific client. 

```bash
curl -X GET "https://app.mertzcrew.com/api/employees/reports/payroll/1/2?main_office=3&field_office=4"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command returns an excel file (.xlsx) where content-type/mime-type is application/vnd.ms-excel 


<aside class="warning">
Only timesheets you have access to can be retrieved by this endpoint.
</aside>


### HTTP Request

`https://app.mertzcrew.com/api/employees/reports/payroll/<start_date>/<end_date>?main_office=<main_office_id>&field_office=<field_office_id>`

### URL Parameters

Parameter | Description
--------- | -----------
start_date | as a timestamp
end_date | as a timestamp
main_office_id | ID of the client's main office. Can be found in the "Get All Timesheets" response
field_office_id | ID of the field office. Can be found in the "Get All Timesheets" response (optional)



## Download Timesheets By Start/End Date 

This endpoint retrieves the timesheets from a specific date range. 

```bash
curl -X GET "https://app.mertzcrew.com/api/employees/reports/payroll/1/2"
  -H "Authorization: xxxxxxxxxxxx"
```
> The above command returns an excel file (.xlsx) where content-type/mime-type is application/vnd.ms-excel


<aside class="warning">
Only timesheets you have access to can be retrieved by this endpoint.
</aside>


### HTTP Request

`https://app.mertzcrew.com/api/employees/reports/payroll/<start_date>/<end_date>`

### URL Parameters

Parameter | Description
--------- | -----------
start_date | as a timestamp
end_date | as a timestamp



