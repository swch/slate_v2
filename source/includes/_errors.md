# Errors

<aside class="notice">
Strivve adheres to a standard set of error codes.  In general, formatting/data errors should return 400 responses.  500 errors should be reported to developers@strivve.com.
</aside>

The Strivve API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The request is hidden for administrators only.
404 | Not Found -- The specified entity could not be found.
405 | Method Not Allowed -- You tried to access an entity with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
429 | Too Many Requests -- You're requesting too many entities! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
