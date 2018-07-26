Table of contents
=================

   * [Table of contents](#table-of-contents)
   * [ARDI service overview](#ardi-service-overview)
      * [High level workflow description](#high-level-workflow-description)
   * [ARDITO registration tools](#ardito-registration-tools)
      * [Registration via the API for B2B registrations](#registration-via-the-api-for-b2b-registrations)
      	* [Authorization](#authorization)
      	* [Description of the Response body](#description-of-the-response-body)
        * [DRS submission with correct parameters](#drs-submission-with-correct-parameters)
      	* [DRS submission with wrong username](#drs-submission-with-wrong-username)
        * [DRS submission with wrong password](#drs-submission-with-wrong-password)
        * [DRS submission with wrong content type in the header](#drs-submission-with-wrong-content-type-in-the-header)
        * [DRS submission with empty root element](#drs-submission-with-empty-root-element)
        * [DRS submission with empty request body](#drs-submission-with-empty-request-body)
        * [DRS submission with wrong element or wrong attribute value of an identifier](#drs-submission-with-wrong-element-or-wrong-attribute-value-of-an-identifier)
      * [XML upload interface for manual registration](#xml-upload-interface-for-manual-registration)


ARDI service overview
======================
The ARDI service provides persistent and web resolvable identification of copyright deposits. The service features a new web resolvable identifier driven by DOI (ARDI), an interoperable standard format to express and communicate rights declarations (DRS - Digital Rightsholder Statement, based on LCC framework), resolvable links to the content identifiers, a new landing page making accessible to any users the chain of declarations for a given identified content asset and integration with the Copyright Hub.
   
   High level workflow description
   ===============================
Here follows a summary of the high level workflow of ARDI web app:
  1. receives a DRS record in input
  2. validation of DRS against the schema
     
     a) failure: error – feedback and stop the workflow
     
     b)	success: proceed with the workflow
  3. ARDI generation
     
     a) if the DRS does not contain an ARDI: creates a unique ARDI, assigns it to the DRS and proceeds with the workflow as a create
     
     b)	if the DRS already contains an ARDI: proceeds with the workflow as an update
  4. onboards data with the Copyright Hub
  5. following onboarding, ARDI and content identifiers are indexed in the Copyright Hub index, for query purposes and used by Copyright Hub front-end tools
  6. stores and maintains DRS metadata
  7. builds and exposes the landing page for DRS information upon resolution of an ARDI directly or via resolution of the associated content identifier
  8. mints the ARDI in the DOI Handle System, providing persistence and resolution driven by DOI
  9. stores results of the above operations (accounting data) and provides feedback
  
ARDITO registration tools
=========================

The entry point is the ARDI registration service REST API that allows a user to submit a DRS (Digital Rightsholder Statement) record expressing a rights notice on an individual content asset (creation in LCC terms) in a simplified but fully compliant version of the LCC DRS Schema, that is a DRS Profile for ARDI registration (lcc:DrsProfile_ARDI). Each XML file validated against this schema profile is valid also against the LCC DRS Schema. This first release of the ARDI service allows for the deposit of one DRS at the time.

To download the xsd of DRS profile for ARDI registration in production environment click [here](https://ardi.medra.org/ardi-ra/schema/drs/1.0/medra-drs.xsd).

To download the xsd of DRS profile for ARDI registration in staging environment click [here](https://ardi-dev.medra.org/ardi-ra/schema/drs/1.0/medra-drs.xsd).

The registration of an ARDI is handled in two ways: Registration via the API for B2B registrations and XML upload interface for manual registration
    
   Registration via the API for B2B registrations
   ==============================================
   
   To register an ARDI  via the API for B2B registrations, the following endpoints are available:
   
   Production environment endpoint: https://ardi.medra.org/statement
   
   Staging environment endpoint: https://ardi-dev.medra.org/statement
   
   A valid DRS (application/xml) according to the LCC DRS schema must be sent in the request body.
   
   The ARDI registration service REST API returns a JSON response to the user submitting the DRS which includes:
    
   * The assigned ARDI, to be stored and reused by the registrant for following updates of the same DRS or to make it available to let users resolve to the landing page
    
   * The full DRS metadata as submitted, that can be re-used to communicate with other systems in B2B mode
    
   * The accounting data, providing results (success/failure) for each operation (creation/update) for each service (Handle System service/Hub service/Metadata service)

   ## Authorization
   
   This API requires a basic authentication, the user must be registered (username and password) on mEDRA in order to achieve the
   registration. Request valid DRS (Digital Rightsholder Statement) from request body ({application/xml; charset=utf-8})
   
   ### Required data for ARDI registration

   | Property        | Description                                | Type                  | Mandatory |
   | :-------        | :----------                                | :---                  | :-------- |
   | Authentication  | Basic Authentication                       | string                | yes       |
   | request body    | valid DRS (Digital Rightsholder Statement) | application/xml       | yes       |
   
   <!--
   To obtain the encoded string, perform the following steps:
   <!--
   Open a Rest API client like chrome://restclient/content/restclient.html on Mozzilla Forefox browser and choose the basic 
   authentication:
   <!--
   ![basic-authentication](https://user-images.githubusercontent.com/39902417/42159008-9377df60-7df2-11e8-88c3-9df8843bb53a.png)
   <!--
   Then enter the user and the password as on the figure below (authentication on mEDRA application as DRS register):
   <!--
   ![basic-authorization](https://user-images.githubusercontent.com/39902417/42159024-9f91cc7a-7df2-11e8-91cf-61c33a380b6d.png)
    -->

## DRS submission with correct parameters

   + Request Method
 
         [POST]
  
   + Request Headers
      
         * Content-Type: [application/xml]
         * Http request with basic authentication
   + Request body: 
     
   For examples of DRS to be pasted as content in the request body see [here](https://github.com/Ediser/ARDI-service/blob/master/sample-drs-xml.md)
   
  + Response 200 (application/json; charset=UTF-8):

    * Body
               
               {
                  "user": "DEMO",
                  "statement": {
                    "ardi": "10.29414/ardi:1510841716516",
                    "asserterName": "Italian Publisher Association",
                    "asserterDateTime": "2017-09-10T13:44:01",
                    "creation": {
                      "type": "lcc:LexicalWork",
                      "name": "Il mercato delle riviste scientifiche italiane: una ricerca",
                          "identifiers": [
                                            {
                                              "type": "lcc:ISBN",
                                              "value": "9788899630096",
                                              "subtype": ""
                                            }, {
                                              "type": "lcc:DOI",
                                              "value": "10.978.8899630/096",
                                              "subtype": ""
                                            }, {
                                              "type": "lcc:ISBNA",
                                              "value": "10.978.8899630/096",
                                              "subtype": ""
                                            }
                                         ]
                     },
                    "rightsNotice": {
                      "names": [
                        "Anna Lionetti", "Pierfrancesco Attanasio"
                      ],
                      "years": [
                        "2016"
                      ],
                      "extensions": [
                          {
                            "value": "This article is published online with Open Access and distributed under the terms
                            of the Creative Commons Attribution Non-Commercial License (CC BY-NC 4.0).",
                            "language": "eng"
                          }, {
                            "value": "Il testo di questo articolo è rilasciato dagli autori in licenza Creative Commons
                            Attribuzione - Non commerciale (CC-BY-NC 4.0)",
                            "language": "ita"
                          }
                      ]
                    },
                    "furtherRightsInformation": {
                        "assignmentTypes": [
                          "lcc:CC_License_BY_NC"
                        ],
                        "rightAssignments": [
                          "https://creativecommons.org/licenses/by-nc/4.0/"
                        ],
                        "rightsInformationTypes": [
                          "lcc:ApplicableLicense"
                        ]
                    },
                    "drs": "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"no\"?>\r\n<!--Sample XML file generated by
                  XMLSpy v2015 sp2 (x64) (http://www.altova.com)-->\r\n<DigitalRightsholderStatement
                  xmlns=\"http://www.rightscom.com/2011/drs#\" xmlns:drs=\"http://www.rightscom.com/2011/drs#\"
                  xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xsi:schemaLocation=\"http://www.rightscom.com/2011/drs#
                  https://ardi-dev.medra.org/schema/drs/1.0/medradrs.xsd\">\r\n\t<DrsProfileType>lcc:DrsProfile_ARDI</DrsProfileType>
                  \r\n\t<Right>\r\n\t\t<RightIdentifier

                  IdentifierType=\"lcc:ARDI\">\r\n\t\t<IdentifierValue>10.29414/ardi:1510841716516</IdentifierValue>\r\n\t</RightIdentifi
                  er>\r\n\t\t<RightStatus>lcc:EffectiveRight</RightStatus>\r\n\t\t<Rightsholder>\r\n\t\t\t<Identifier
                  IdentifierType=\"lcc:ORCID\">\r\n\t\t\t\t<IdentifierValue>orcid.org/0000-0001-6157-
                  8808</IdentifierValue>\r\n\t\t\t</Identifier>\r\n\t\t\t<Name>\r\n\t\t\t\t<NameValue>Anna
                  Lionetti</NameValue>\r\n\t\t\t\t<NamePart NamePartType=\"lcc:KeyName\">Lionetti</NamePart>\r\n\t\t\t\t<NamePart
                  NamePartType=\"lcc:NamesBeforeKeyName\">Anna</NamePart>\r\n\t\t\t</Name>\r\n\t\t</Rightsholder>\r\n\t\t<Rightsholder>\r
                  \n\t\t\t<Identifier IdentifierType=\"lcc:ORCID\">\r\n\t\t\t\t<IdentifierValue>orcid.org/0000-0001-7410-
                  6682</IdentifierValue>\r\n\t\t\t</Identifier>\r\n\t\t\t<Name>\r\n\t\t\t\t<NameValue>Pierfrancesco
                  Attanasio</NameValue>\r\n\t\t\t\t<NamePart NamePartType=\"lcc:KeyName\">Attanasio</NamePart>\r\n\t\t\t\t<NamePart
                  NamePartType=\"lcc:NamesBeforeKeyName\">Pierfrancesco</NamePart>\r\n\t\t\t</Name>\r\n\t\t</Rightsholder>\r\n\t\t<Contro
                  lledCreation>\r\n\t\t\t<Identifier
                  IdentifierType=\"lcc:ISBN\">\r\n\t\t\t\t<IdentifierValue>9788899630096</IdentifierValue>\r\n\t\t\t</Identifier>\r\n\t\t
                  \t<Identifier 
                  IdentifierType=\"lcc:DOI\">\r\n\t\t\t\t<IdentifierValue>10.978.8899630/096</IdentifierValue>\r\n\t\t\t</Identifier>\r\n
                  \t\t\t<Identifier
                  IdentifierType=\"lcc:ISBNA\">\r\n\t\t\t\t<IdentifierValue>10.978.8899630/096</IdentifierValue>\r\n\t\t\t</Identifier>\r
                  \n\t\t\t<Name>Il mercato delle riviste scientifiche italiane: una
                  ricerca</Name>\r\n\t\t\t<CreationType>lcc:LexicalWork</CreationType>\r\n\t\t<!--
                  \t<URL>http://www.giornaledellalibreria.it/presentazione-tra-editoria-e-universita-i-risultati-del-gruppo-di-  
                  lavorouniversita-di-verona-cineca-e-aie-2585.html</URL>--
                  >\r\n\t\t</ControlledCreation>\r\n\t\t<UseType>lcc:All</UseType>\r\n\t\t<ControlType>lcc:All</ControlType>\r\n\t\t<Righ
                  tsNotice>\r\n\t\t\t<Name>Anna Lionetti</Name>\r\n\t\t\t<Name>Pierfrancesco
                  Attanasio</Name>\r\n\t\t\t<Year>2016</Year>\r\n\t\t\t<Extension Language=\"eng\">This article is published online with
                  Open Access and distributed under the terms of the Creative Commons Attribution Non-Commercial License (CC BY-NC
                  4.0).</Extension>\r\n\t\t\t<Extension Language=\"ita\">Il testo di questo articolo è rilasciato dagli autori in licenza
                  Creative Commons Attribuzione - Non commerciale (CC-BY-NC
                  4.0)</Extension>\r\n\t\t</RightsNotice>\r\n\t\t<FurtherRightsInformation>\r\n\t\t\t<!-- relates to RightsPolicyType =
                  lcc:CC_License_BY_NC--
                  >\r\n\t\t\t<RightsAssignmentType>lcc:CC_License_BY_NC</RightsAssignmentType>\t\t\r\n\t\t<RelatedRightAssignment
                  IdentifierType=\"lcc:URI\">\r\n\t\t\t\t<IdentifierValue>https://creativecommons.org/licenses/bync/4.0/</IdentifierValue>
                  \r\n\t\t\t</RelatedRightAssignment>\r\n\r\n\t\t\t<FurtherRightsInformationType>lcc:ApplicableL
                  icense</FurtherRightsInformationType>\r\n\t\t</FurtherRightsInformation>\r\n\t\t<Territory>lcc:World</Territory>\r\n\t\
                  t<StartTime>2016-01-01</StartTime>\r\n\t\t<!-- <EndTime>2017-12-31</EndTime>--
                  >\r\n\t\t<PercentageShare>100</PercentageShare>\r\n\t\t<IsExclusive>lcc:True</IsExclusive>\r\n\t</Right>\r\n\t<!--
                  <Asserter><Name>Italian Publisher Association</Name></Asserter>-->\r\n\t<Asserter>\r\n\t\t<Identifier
                  IdentifierType=\"lcc:ISNI\">\r\n\t\t\t<IdentifierValue>1234-5678-9876-
                  4444</IdentifierValue>\r\n\t\t</Identifier>\r\n\t\t<Name>Italian Publisher
                  Association</Name>\r\n\t</Asserter>\r\n\t<AssertionDateTime>2017-09-
                  10T13:44:01</AssertionDateTime>\r\n</DigitalRightsholderStatement>\r\n"
                  },
                    "accounting": [
                      {
                        "ardi": "10.29414/ardi:1510841716516",
                        "service": "HANDLE",
                        "operation": "UPDATE",
                        "result": "SUCCESS",
                        "resultDescription": null,
                        "timestamp": "24-11-2017 13:00:23"
                      }, {
                          "ardi": "10.29414/ardi:1510841716516",
                           "service": "HUB",
                           "operation": "UPDATE",
                          "result": "SUCCESS",
                          "resultDescription": null,
                          "timestamp": "24-11-2017 13:00:25"
                        }, {
                          "ardi": "10.29414/ardi:1510841716516",
                          "service": "METADATA",
                          "operation": "UPDATE",
                          "result": "SUCCESS",
                          "resultDescription": null,
                          "timestamp": "24-11-2017 13:00:25"
                        }
                      ],
                  "startTimestamp": "24-11-2017 13:00:22",
                  "endTimestamp": "24-11-2017 13:00:25"
              }
  
  Description of the Response body
  ================================
  
  The following table describes the JSON fields in the response body:

   | Field           | Description                                |
   | :-------        | :----------                                |
   | user            | The user that perform the DRS submission   |
   | statement       | The whole DRS submitted in XML format transforms in JSON format except the field "drs"|
   | Subfield "drs" in statement|The whole original DRS submitted in XML format. Noticed that, if the original DRS in XML format doesn't contain the ARDI identifier, after the submission, in case of **SUCCESS**, the field will contain the ARDI identifier generated by the web application|
   |accounting| The accounting data, providing results for operations and for services as describe in the next table|
   
   | Field             | Description |
   | :--------         | :----------
   | ardi              | The ARDI identifier provided during submission or the ARDI generated by the web application|
   | service           | The three services involved in the submission process (HANDLE, COPYRIGHT HUB, METADATA)|
   | operation         | The two allowed operations (CREATION and UPDATE)|
   | result            | The result type, could be either SUCCESS or FAILURE)|
   | resulDescription  | In case of **SUCCESS**, the field contains value *null*, instead (**FAILURE**), a nearly human readable message that describes what wrong during the submission process|
   | timestamp         | The process time of each service in format DD-MM-YYYY HH:mi:ss|
  
  The response body provided through the REST API in the form of a JSON includes:
  * The assigned ARDI
  * The full DRS metadata in the LCC compliant format.
  * The accounting data, providing results (success/failure) for each operation (creation/update) for each service (Handle System/Hub service/Metadata service).
      
  To be sure that the submission has been successfully achieved, in the JSON response body the following array must contain **SUCCESS** result for all the operations
  
        { ...
          "accounting": [
                        {
                          "ardi": "10.29414/ardi:1510841716516",
                          "service": "HANDLE",
                          "operation": "UPDATE",
                          "result": "SUCCESS",
                          "resultDescription": null,
                          "timestamp": "24-11-2017 13:00:23"
                        }, {
                            "ardi": "10.29414/ardi:1510841716516",
                             "service": "HUB",
                             "operation": "UPDATE",
                            "result": "SUCCESS",
                            "resultDescription": null,
                            "timestamp": "24-11-2017 13:00:25"
                          }, {
                            "ardi": "10.29414/ardi:1510841716516",
                            "service": "METADATA",
                            "operation": "UPDATE",
                            "result": "SUCCESS",
                            "resultDescription": null,
                            "timestamp": "24-11-2017 13:00:25"
                          }
                      ]
           ...
        }
        
   In case one or more operation fail, the JSON response contains **FAILURE**, as in the following example
   
        {
           ...
           "accounting": [
                        {
                          "ardi": "10.29414/ardi:1530787684558",
                          "service": "HANDLE",
                          "operation": "CREATE",
                          "result": "SUCCESS",
                          "resultDescription": null,
                          "timestamp": "05-07-2018 12:48:04"
                        },
                        {
                          "ardi": "10.29414/ardi:1530787684558",
                          "service": "HUB",
                          "operation": "CREATE",
                          "result": "FAILURE",
                          "resultDescription": "503 Service Unavailable",
                          "timestamp": "05-07-2018 12:48:06"
                        },
                        {
                          "ardi": "10.29414/ardi:1530787684558",
                          "service": "METADATA",
                          "operation": "CREATE",
                          "result": "SUCCESS",
                          "resultDescription": null,
                          "timestamp": "05-07-2018 12:48:06"
                        }
                      ]
           ...
        }
   
   ## DRS submission with wrong username
   
  + Response 401 Unauthorized (application/json; charset=UTF-8):

    * Body
               
               {
                  "timestamp": 1530791989024,
                  "status": 401,
                  "error": "Unauthorized",
                  "message": "UserDetailsService returned null, which is an interface contract violation",
                  "path": "/ardi-ra/statement"
               
               }
   
   ## DRS submission with wrong password
   
  + Response 401 Unauthorized (application/json; charset=UTF-8):

    * Body
               
               {
               "timestamp": 1530791951195,
                "status": 401,
                "error": "Unauthorized",
                "message": "Bad credentials",
                "path": "/ardi-ra/statement"
               
               }
   
   ## DRS submission with wrong content type in the header
   
   + Request Headers
      
         * Content-Type: [application/json]
         * Http request with basic authentication
   
  + Response 415 Unsupported Media Type (application/json; charset=UTF-8):

    * Body
               
               {
                "timestamp": 1530792178198,
                "status": 415,
                "error": "Unsupported Media Type",
                "exception": "org.springframework.web.HttpMediaTypeNotSupportedException",
                "message": "Content type 'application/json' not supported",
                "path": "/ardi-ra/statement"
               
               }
   
   
   ## DRS submission with empty root element
   
   + Request body: 
     
	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<DigitalRightsholderStatement xmlns="http://www.rightscom.com/2011/drs#" 
	    xmlns:drs="http://www.rightscom.com/2011/drs#" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
	    xsi:schemaLocation="http://www.rightscom.com/2011/drs# https://ardi.medra.org/schema/drs/1.0/medra-drs.xsd">

	</DigitalRightsholderStatement>
          
  + Response 400 Bad Request (application/json; charset=UTF-8):

    * Body
               
           {
                "status": 400,
	              "timestamp": "05-07-2018 14:04:10",
	              "message": "org.xml.sax.SAXParseException; lineNumber: 1; columnNumber: 456; cvc-complex-type.2.4.b: The content of 
                element 'DigitalRightsholderStatement' is not complete. One of '{\"http://www.rightscom.com/2011/drs#\":DrsProfileType, 
                \"http://www.rightscom.com/2011/drs#\":Right}' is expected.",
	              "path": "/statement",
	              "error": "Bad Request"
               
           }
   
   ## DRS submission with empty request body
   
   
  + Request body: 
        
   
  + Response 400 Bad Request (application/json; charset=UTF-8):

    * Body
    
     	  No body returned for response
               
   
   ## DRS submission with wrong element or wrong attribute value of an identifier
   
   + Request body: 
     
         <?xml version="1.0" encoding="UTF-8" standalone="no"?>
         <DigitalRightsholderStatement xmlns="http://www.rightscom.com/2011/drs#" xmlns:drs="http://www.rightscom.com/2011/drs#"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.rightscom.com/2011/drs# 
	      https://ardidev.medra.org/schema/drs/1.0/medra-drs.xsd">
	     <DrsProfileType>lcc:DrsProfile_ARDI</DrsProfileType>
			<Right>
			  <RightStatus>lcc:EffectiveRight</RightStatus>
			  <Rightsholder>
			    <Identifier IdentifierType="lxx:ORCID">
			      <IdentifierValue>orcid.org/0000-0001-6157-8808</IdentifierValue>
			    </Identifier>
			  <Name>
			    <NameValue>Anna Lionetti</NameValue>
			    <NamePart NamePartType="lcc:KeyName">Lionetti</NamePart>
			    <NamePart NamePartType="lcc:NamesBeforeKeyName">Anna</NamePart>
			  </Name>
			  </Rightsholder>
			  <Rightsholder>
			    <Identifier IdentifierType="lcc:ORCID">
			      <IdentifierValue>orcid.org/0000-0001-7410-6682</IdentifierValue>
			    </Identifier>
			    <Name>
			      <NameValue>Pierfrancesco Attanasio</NameValue>
			      <NamePart NamePartType="lcc:KeyName">Attanasio</NamePart>
			      <NamePart NamePartType="lcc:NamesBeforeKeyName">Pierfrancesco</NamePart>
			    </Name>
			  </Rightsholder>
			  <ControlledCreation>
			    <Identifier IdentifierType="lcc:ISBN">
			      <IdentifierValue>9788899630096</IdentifierValue>
			    </Identifier>
			    <Identifier IdentifierType="lcc:DOI">
			      <IdentifierValue>10.978.8899630/096</IdentifierValue>
			    </Identifier>
			    <Identifier IdentifierType="lcc:ISBNA">
			      <IdentifierValue>10.978.8899630/096</IdentifierValue>
			    </Identifier>
			      <Name>Il mercato delle riviste scientifiche italiane: una ricerca</Name>
			      <CreationType>lcc:LexicalWork</CreationType>
			      <URL>http://www.giornaledellalibreria.it/presentazione-tra-editoria-e-universita-i-risultati-del-gruppo-dilavoro-universita-di-verona-cineca-e-aie-2585.html</URL>
			    </ControlledCreation>
			    <UseType>lcc:All</UseType>
			    <ControlType>lcc:All</ControlType>
			    <RightsNotice>
			    <Name>Anna Lionetti</Name>
			    <Name>Pierfrancesco Attanasio</Name>
			    <Year>2016</Year>
			    <Extension Language="eng">This article is published online with Open Access and distributed under the
			      terms of the Creative Commons Attribution Non-Commercial License (CC BY-NC 4.0).
			    </Extension>
			    <Extension Language="ita">Il testo è rilasciato dagli autori in licenza Creative Commons Attribuzione -
			      Non commerciale (CC-BY-NC 4.0)
			    </Extension>
			    </RightsNotice>
			    <FurtherRightsInformation>
			      <RelatedRightAssignment IdentifierType="lcc:URI">
				<IdentifierValue>https://creativecommons.org/licenses/by-nc/4.0/</IdentifierValue>
			      </RelatedRightAssignment>
			      <RightsAssignmentType>lcc:CC_License_BY_NC</RightsAssignmentType>
			      <FurtherRightsInformationType>lcc:ApplicableLicense</FurtherRightsInformationType>
			    </FurtherRightsInformation>
			    <Territory>lcc:World</Territory>
			    <StartTime>2016-01-01</StartTime>
			    <PercentageShare>100</PercentageShare>
			    <IsExclusive>lcc:True</IsExclusive>
			  </Right>
			    <Asserter>
			      <Identifier IdentifierType="lcc:ISNI">
			      <IdentifierValue>1234-5678-9876-4444</IdentifierValue>
			      </Identifier>
			      <Name>Italian Publisher Association</Name>
			    </Asserter>
			    <AssertionDateTime>2017-09-10T13:44:01</AssertionDateTime>
			</DigitalRightsholderStatement>
        
        
  + Response 400 Bad Request (application/json; charset=UTF-8):

    * Body
               
               {
                
                "status": 400,
	              "timestamp": "05-07-2018 14:21:32",
	              "message": "org.xml.sax.SAXParseException; lineNumber: 1; columnNumber: 1038; cvc-enumeration-valid: Value 'lxx:ORCID' 
                is not facet-valid with respect to enumeration '[lcc:ISNI, lcc:IPICode, lcc:ORCID, lcc:LCC_Term]'. It must be a value 
                from the enumeration.",
	              "path": "/statement",
	              "error": "Bad Request"
               
               }
   
   
   
   
   XML upload interface for manual registration
   ============================================
   Using the XML upload interface allows to register an ARDI by manually uploading the DRS XML file to the API
   
   Access point in production environment: https://ardi.medra.org/ardi-ra/ardi/logon-page.html
   
   ![logon-page-ardi-prod](https://user-images.githubusercontent.com/39902417/43138435-2307685e-8f4f-11e8-8ce6-6fb7a5f39828.PNG)
   
   Access point in staging environment: https://ardi-dev.medra.org/ardi-ra/ardi/logon-page.html
   
   ![login-page](https://user-images.githubusercontent.com/39902417/41343402-ca92bd7e-6efe-11e8-8985-083fa8b8ee57.PNG)
   
   ## Authorization
 The user must enter his login credential (username and password) on mEDRA in order to achieve the submission.

### How to reach the upload page?
The following screenshot displays the link to reach the upload page.

![link-upload-page-ardi](https://user-images.githubusercontent.com/39902417/43138453-3343555c-8f4f-11e8-857e-e0944c0a5583.png)

 By clicking the link in screenshot above the user gets to the page where to select and upload an XML file containing a valid DRS to be submitted.
 
 XML upload page in production enviroment: https://ardi.medra.org/ardi-ra/ardi/reserved/upload-page.html
 
 XML upload page in staging environment: https://ardi-dev.medra.org/ardi-ra/ardi/reserved/upload-page.html
 
![upload-page-ardi](https://user-images.githubusercontent.com/39902417/43138424-17cd8a36-8f4f-11e8-914b-587dde17f00e.png)

The JSON response body is the same as in the Result of registration via the API for B2B registrations.
