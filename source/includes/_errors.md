# Errors

Mertzcrew uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, etc.). Codes in the 5xx range indicate an error with our servers.

Some 4xx errors that could be handled programmatically (e.g., add a required parameter). We include an error message that briefly explains the error reported.

Error Code | Meaning
---------- | -------
400 | Bad Request -- The request was unacceptable, often due to missing a required parameter.
401 | Unauthorized -- No valid API token provided.
402 | Request Failed -- The parameters were valid but the request failed.
403 | Forbidden -- The enpoint requested is hidden for administrators only.
404 | Not Found -- The requested resource doesn't exist.
405 | Method Not Allowed -- You tried to access an endpoint with an invalid HTTP verb.
409 | Conflict -- The request conflicts with another request (perhaps due to using the same idempotent key).
429 | Too Many Requests	-- Too many requests hit the API too quickly. We recommend an exponential backoff of your requests.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
