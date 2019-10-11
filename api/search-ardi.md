(2b) The url of the search API may be something like this
https://ardi-dev.medra.org/ardi-ra/api/search-ardi
It will accept  a HTTP GET Request with one or more of following parameters:
ardi
creationIdentifierType
creationIdentifierValue
creationType
creationName
asserterName
startAsserterDate
endAsserterDate
rightsNoticeName
rightsNoticeYear
rightsNoticeExtension
 
(2c) The response will be a json array of objects, each one with only one key (“ardi”) and a value of type string:
[
{“ardi”:”{ardi1}”},
{“ardi”:”{ardi2}”},
…
]
The array will be empty if no ardi matches the query parameters.
I’ve choosen an array of object and not an array of strings because in this way we can easily add others keys to each object, if needed.
 
The endpoint of the search API will be public (no authentication will be required).
