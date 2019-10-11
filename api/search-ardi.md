Search Ardi API
===============
This API allow you to retrieve a list of ARDI given one or more 

Endpoint
--------
The endpoints of the API are:
* staging environment: https://ardi-dev.medra.org/ardi-ra/api/search-ardi
* production environment: https://ardi.medra.org/ardi-ra/api/search-ardi
The endpoint are public (no authentication is required).

HTTP Request
------------
The API accept an HTTP GET request with one or more of the following parameters:

| HTTP PARAMETER |	CASE SENSITIVE	| SEARCH MODE |	NOTES |
| ----------- | ----------- | ------------| ---------- |
|ardi|NO|LIKE||
|creationIdentifierType|NO|EXACT||
|creationIdentifierValue|YES|EXACT||
|creationType|NO|EXACT||
|creationName|NO|LIKE||
|asserterName|NO|LIKE||
|startAsserterDate|-|EQUAL OR AFTER|in the form dd/MM/yyyy|
|endAsserterDate|-|EQUAL OR BEFORE|in the form dd/MM/yyyy|
|rightsNoticeName|NO|LIKE||
|rightsNoticeYear|-|EXACT|in the form yyyy|
|rightsNoticeExtension|NO|LIKE||

HTTP Response
------------
### SUCCESS
In case of success, an HTTP response will be returned with status code `200` and as body a json (`Content-Type="application/json;charset=UTF-8"`) array of objects, each one with only one key (`ardi`) and a value of type string:
```
[
 {"ardi":"{ardi1}"},
 {"ardi":"{ardi2}"},
 …
]
```

The array will be empty if no ardi matches the query parameters.

An array of objects was chosen (and not, for example, an array of strings) because it can be easily extended with other keys.

### FAILURE
If an error occurs, an HTTP response will be returned with status code other than `200` and as body a json (`Content-Type="application/json;charset=UTF-8"`) object with the following structure

|KEY|DESCRIPTION|
|---|-----------|
|timestamp|when the response was sent (in UNIX time)|
|status|the HTTP status code|
|error|the HTTP status description|
|message|the description of the error occurred|
|path|the URL path of the endpoint|

For example, *if no HTTP parameter is sent to the endpoint*, the HTTP response will be have a status code `400` and the following json as body:

 
Examples
------------
### 1. No HTTP parameter sent to the endpoint
#### HTTP REQUEST
    https://ardi-dev.medra.org/ardi-ra/api/search-ardi
#### HTTP RESPONSE (400)
```
{
 "timestamp": 1530791951195,
 "status": 400,
 "error": "Bad Request",
 "message": "missing parameter",
 "path": "/ardi-ra/api/search-ardi"              
}
 ```
### 2. Check if an ARDI exists
#### HTTP REQUEST
    https://ardi-dev.medra.org/ardi-ra/api/search-ardi?ardi=10.29414/ardi:1528986002482
#### HTTP RESPONSE (200)
    [{"ardi":"10.29414/ardi:1528986002482"}]
    
### 3. Retrieve all ARDIs assigned to a creation with a given DOI
#### HTTP REQUEST
    https://ardi-dev.medra.org/ardi-ra/api/search-ardi?creationIdentifierType=lcc:DOI&creationIdentifierValue=10.978.88910/0000134
#### HTTP RESPONSE (200)
    [{"ardi":"10.29414/ardi:15271569600022"},{"ardi":"10.29414/ardi:1533290488854"},{"ardi":"10.29414/ardi:1533290434780"}]
