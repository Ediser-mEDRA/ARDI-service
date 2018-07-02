Table of contents
=================

   * [Table of contents](#table-of-contents)
   * [Right-aware DOI suite overview](#right-aware-doi-suite-overview)
   * [ARDITO registration tool](#ardito-registration-tool)
      * [Directly via the API for B2B registrations](#directly-via-the-api-for-b2b-registrations)
           * [application xml](#application-xml)
      * [Using the XML upload interface for manual registration](#using-the-xml-upload-interface-for-manual-registration)


Right-aware DOI suite overview
==============================
This service describes the technical features of the new tool that achieves the registration of a Digital Rightsholder Statement (DRS). The
tool is a new web App for ARDITO taking care of the registration process of an ARDI identifier to be assigned to rights declarations,
and includes a new registration schema based on the LCC DRS format and a new landing page making accessible to any users the chain of 
declarations for a given identified content asset and interfaces for registrants. From technical point of view, the registration of a DRS 
involves at least two infrastructures: 
 - The handle system that receive the ARDI identifier created, and persisted it for management purpose, resolution URL, etc.
 - The Open Permissions Platform Onboarding Service that receive the identifiers (isbn, doi, ardi, etc.) and onboard them to a repository
 within the Hub.

ARDITO registration tool
========================

The point of entry is the ARDI registration service REST API that allows a user to submit a DRS (Digital Rightsholder Statement) 
expressing a rights notice on an individual content asset (creation in LCC terms) according to the LCC DRS schema.

The registration of an ARDI is handled in two ways:
    
   Directly via the API for B2B registrations
   ==========================================
   Directly via the API that hold the DRS as request body, for B2B registrations.
   
   HOST: https://ardi-dev.medra.org
   
   ENDPOINT: https://ardi-dev.medra.org/statement
   
   ## Authorization
   
   This API requires a basic authentication, the user must be registered (username and password) on mEDRA in order to achieve the
   registration. Request valid DRS (Digital Rightsholder Statement) from request body ({application/xml; charset=utf-8})
   
   ### Required data for ARDI registration

   | Property        | Description                                | Type      | Mandatory |
   | :-------        | :----------                                | :---      | :-------- |
   | Authentication  | Basic Authentication (username:password)   | string    | yes       |
   | request body    | valid DRS (Digital Rightsholder Statement) | xml       | yes       |

   + Request Method
 
         [POST]
  
   + Request Headers
      
         * Accept: [application/xml]
         * The authorization method and a space (e.g. "Authorization: Basic ") is then prepended to the encoded string. For example, use
         Aladdin as the username and OpenSesame as the password, then the field's value is the base64-encoding of 
         Aladdin:OpenSesame, or QWxhZGRpbjpPcGVuU2VzYW1l. Then the Authorization header will appear as:
         Authorization: Basic QWxhZGRpbjpPcGVuU2VzYW1l
         
   + Request body: valid DRS (Digital Rightsholder Statement) (application/xml) according to the LCC DRS schema. In order to allow the 
   deposit of simple statement, the ARDI registration format contains a subset of group of elements taken from the DRS schema. In
   mEDRA application, we have decided to simplify the structure of a Right, starting from two basic use cases:
     * an (self-published) author wishing to declare his/her copyright ownership on a content
     * a publisher wishing to indicate some basic copyright info and licence info (especially related to Open Access) on a content
     Thus in mEDRA application a DRS is described by the following [link](https://ardi-dev.medra.org/ardi-ra/schema/drs/1.0/medra-drs.xsd):
     
        application xml
        ---------------
        Look for the xml sample [here](https://github.com/Ediser/ARDI-service/blob/master/sample-drs-xml.md)
   
   + Response body
      Finally the ARDI registration service REST API returns a JSON response to the user submitting the DRS which includes:
      * The assigned ARDI, to be stored and reused by the registrant for following updates of the same DRS or to make available the ARDI 
      resolving to the landing page along the value chain
      * The full DRS metadata as submitted, that can be re-used to communicate with other systems in B2B mode. This is especially relevant 
      once GUIs for registrants will be developed on top of existing services, as users will be able to exploit DRS in the LCC format 
      although they might have no proficiency with it
      * The accounting data, providing results (success/failure) for each operation (creation/update)for each service (Handle System 
      service/Hub service/Metadata service).  Example of a JSON response for a DRS update, assigned with an ARDI:
      
              {
                "status": 200,
                
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
   
   Using the XML upload interface for manual registration
   ======================================================
   Using the XML upload interface sending the file containing the DRS to the API, for manual registration
   
   Access point: https://ardi-dev.medra.org/ardi-ra/ardi/logon-page.html
   
   ![login-page](https://user-images.githubusercontent.com/39902417/41343402-ca92bd7e-6efe-11e8-8985-083fa8b8ee57.PNG)
   
   ## Authorization
 The user must enter his login credential (username and password) on mEDRA in order to achieve the submission.

### Required data for ARDI registration as result of DRS (Digital Rightsholder Statement) submission

| Property        | Description                                     | Type      | Mandatory |
| :-------        | :----------                                     | :---      | :-------- |
| Authentication  | Basic Authentication (username:password)        | string    | yes       |
| request body    | valid DRS (Digital Rightsholder Statement) file | file      | yes       |

 After the user has successfully logged in, the following page is display to allow the user to select the file containing the valid DRS 
 to be submitted.
 
 https://ardi-dev.medra.org/ardi-ra/ardi/reserved/upload-page.html
 
![upload-page](https://user-images.githubusercontent.com/39902417/41341832-fdf47f12-6efa-11e8-932e-e2c986a6836a.png)

The json response body is the same as in the Result of registration via the API that hold the DRS as request body, for B2B registrations
