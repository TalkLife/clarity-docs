# Errors

The Clarity API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- There was something wrong with the parameters in your request.
401 | Unauthorized -- Your API key is invalid or has expired.
403 | Forbidden -- You tried making a request to an endpoint with an unsuitable key type.
404 | Not Found -- The specified endpoint was incorrect.
405 | Method Not Allowed -- You tried to access a valid endpoint with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
429 | Too Many Requests -- You're making too many classification requests at once, please get in touch.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
