Search ARDI API
===============
This API allows to retrieve a list of ARDIs given one or more search parameters.

Endpoint
--------
The endpoints of the API are:

* staging environment: https://ardi-dev.medra.org/ardi-ra/api/search-ardi
* production environment: https://ardi.medra.org/ardi-ra/api/search-ardi

The endpoints are public (no authentication is required).

HTTP Request
------------
The API accepts an HTTP GET request with one or more of the following parameters, where:

* **HTTP PARAMETER**: key of the HTTP parameter;
* **CASE SENSITIVE**: if the search will be case sensitive or not;
* **SEARCH MODE**: how the search on that field will be done;
* **NOTES**: additional notes;
* **DRS ELEMENT**: the DRS element.

| HTTP PARAMETER |	CASE SENSITIVE	| SEARCH MODE |	NOTES |DRS ELEMENT|
| ----------- | ----------- | ------------| ---------- |------------|
|ardi|NO|LIKE||DigitalRightsholderStatement/Right/RightIdentifier|
|creationIdentifierType|NO|EXACT||DigitalRightsholderStatement/Right/ControlledCreation/Identifier/@IdentifierType|
|creationIdentifierValue|YES|EXACT||DigitalRightsholderStatement/Right/ControlledCreation/Identifier/IdentifierValue|
|creationType|NO|EXACT||DigitalRightsholderStatement/Right/ControlledCreation/CreationType|
|creationName|NO|LIKE||DigitalRightsholderStatement/Right/ControlledCreation/Name|
|asserterName|NO|LIKE||DigitalRightsholderStatement/Asserter/Name|
|startAssertionDate|-|EQUAL OR AFTER|in the form dd/MM/yyyy|DigitalRightsholderStatement/AssertionDateTime|
|endAssertionDate|-|EQUAL OR BEFORE|in the form dd/MM/yyyy|DigitalRightsholderStatement/AssertionDateTime|
|rightsNoticeName|NO|LIKE||DigitalRightsholderStatement/Right/RightsNotice/Name|
|rightsNoticeYear|-|EXACT|in the form yyyy|DigitalRightsholderStatement/Right/RightsNotice/Year|
|rightsNoticeExtension|NO|LIKE||DigitalRightsholderStatement/Right/RightsNotice/Extension|

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

The array will be empty if no ARDI matches the query parameters.

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

Examples
------------
### 1. No HTTP parameter sent to the endpoint
#### HTTP REQUEST
    https://ardi-dev.medra.org/ardi-ra/api/search-ardi
#### HTTP RESPONSE 
Status code:

    400

Body:
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
#### HTTP RESPONSE
Status code:

    200

Body:

    [
     {"ardi":"10.29414/ardi:1528986002482"}
    ]
    
### 3. Retrieve all ARDIs assigned to a creation with a given DOI
#### HTTP REQUEST
    https://ardi-dev.medra.org/ardi-ra/api/search-ardi?creationIdentifierType=lcc:DOI&creationIdentifierValue=10.978.88910/0000134
#### HTTP RESPONSE
Status code:

    200

Body:

    [
     {"ardi":"10.29414/ardi:15271569600022"},
     {"ardi":"10.29414/ardi:1533290488854"},
     {"ardi":"10.29414/ardi:1533290434780"}
    ]
