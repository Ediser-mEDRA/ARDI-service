Table of contents
=================

<!--ts-->
   * [Table of contents](#table-of-contents)
   * [Useful links](#useful-links)
   * [Right-aware DOI suite overview](#right-aware-doi-suite-overview)
   * [ARDITO registration tool](#ardito-registration-tool)
      * [Directly via the API for B2B registrations](#directly-via-the-api-for-b2b-registrations)
           * [application/xml](#application-xml)
           * [application/json](#application-json)
      * [Using the XML upload interface for manual registration](#using-the-xml-upload-interface-for-manual-registration)
   * [Dependency](#dependency)
<!--te-->

Useful links
============
* [Low level design](https://github.com/Ediser/ARDI-service/blob/master/low-level-design.md)

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
The point of entry is the ARDI registration service REST API that allows a user to submit a DRS (Digital Rightsholder Statement) expressing 
a rights notice on an individual content asset (creation in LCC terms) according to the LCC DRS schema.
The registration of an ARDI is handled in two ways:
    
   Directly via the API for B2B registrations
   ==========================================
   Directly via the API that hold the DRS as request body, for B2B registrations.
   HOST: https://ardi-dev.medra.org/statement
   ## Authorization
   This API requires a basic authentication, the user must be registered (username and password) on mEDRA in order to achieve the
   registration. Request Registers valid DRS (Digital Rightsholder Statement) from request body ({application/xml; charset=utf-8, 
   application/json; charset=utf-8})
   ### Required data for ARDI registration as result of DRS (Digital Rightsholder Statement) submission

   | Property        | Description                                | Type      | Mandatory |
   | :-------        | :----------                                | :---      | :-------- |
   | Authentication  | Basic Authentication (username:password)   | string    | yes       |
   | request body    | valid DRS (Digital Rightsholder Statement) | xml/json  | yes       |

   + Request Method
 
         [POST]
  
   + Request Headers
      
         Accept: [application/json, application/xml]
         Authorization: Basic [username:password]
         
   + Request body: valid DRS (Digital Rightsholder Statement) ({application/xml; charset=utf-8, application/json; charset=utf-8}) according 
   to the LCC DRS schema.
        
        application/xml
        ===============
        Look for the xml sample [here](https://github.com/Ediser/ARDI-service/blob/master/low-level-design.md)
   
        application/json
        ================
        (To be provided)
        Look for the json sample [here]()
   
   + Response body
      
          {
            "status": 200,
            Content-Type: application/json;charset=UTF-8,
            {
                    "user": "DEMO",
                    "statement": {
                      "ardi": "10.29414/ardi:1528878585467",
                      "subtype": "",
                      "asserterName": "PM (for test)",
                      "asserterDateTime": 1526284981000,
                      "hubKey": "https://openpermissions.org/s1/hub1/a409c790edfd4b6c89c4ddf989ee7d25/asset/10de8d7526ec497093c669ca6b2c9095",
                      "rightsHolders": [
                        {
                          "id": 264,
                          "holderIdentifiers": [
                            {
                              "type": "lcc:ISNI",
                              "value": "1234-5678-9876-0000"
                            },
                            {
                              "type": "lcc:ORCID",
                              "value": "1234-5678-9876-0023"
                            }
                          ],
                          "holderName": {
                            "nameValue": "Paola Pluto",
                            "holderNameParts": [
                              {
                                "namePartType": "lcc:KeyName",
                                "value": "Mazzucchi"
                              },
                              {
                                "namePartType": "lcc:NamesBeforeKeyName",
                                "value": "Paola"
                              }
                            ]
                          },
                          "holderContacts": [
                            {
                              "emailAddress": "paola.pippo@email.it",
                              "phoneNumber": "02555555555",
                              "contactName": "Paola Pluto",
                              "postalAddress": "Corso di Porta Romana, 108 Milano 20132",
                              "url": "www.medra-dev.medra.org"
                            },
                            {
                              "emailAddress": "test-drs@email.it",
                              "phoneNumber": "0255222555",
                              "contactName": "Jehu Paperino",
                              "postalAddress": "Corso di Porta Romana, 108 Milano 20132",
                              "url": "www.ardi-dev.medra.org"
                            }
                          ]
                        },
                        {
                          "id": 265,
                          "holderIdentifiers": [
                            {
                              "type": "lcc:ORCID",
                              "value": "1234-5678-9876-0023"
                            },
                            {
                              "type": "lcc:ISNI",
                              "value": "1234-5678-9876-2323"
                            }
                          ],
                          "holderName": {
                            "nameValue": "mEDRA",
                            "holderNameParts": null
                          },
                          "holderContacts": [
                            {
                              "emailAddress": "ivana.medra@medra.com",
                              "phoneNumber": "025522255521",
                              "contactName": "Pippo Pluto Paperino",
                              "postalAddress": "Corso di Porta Romana, 108 Milano 20132",
                              "url": "www.ardi-dev.medra.org"
                            }
                          ]
                        },
                        {
                          "id": 266,
                          "holderIdentifiers": [
                            {
                              "type": "lcc:ISNI",
                              "value": "1234-5678-9876-2323"
                            }
                          ],
                          "holderName": {
                            "nameValue": "mEDRA staff support",
                            "holderNameParts": [
                              {
                                "namePartType": "lcc:KeyName",
                                "value": "mEDRA tech"
                              },
                              {
                                "namePartType": "lcc:NamesBeforeKeyName",
                                "value": "staff support"
                              }
                            ]
                          },
                          "holderContacts": [
                            {
                              "emailAddress": "my.email@mail.it",
                              "phoneNumber": "021122255521",
                              "contactName": "Contact Pippo (for test)",
                              "postalAddress": "Corso di Porta Romana, 108 Milano 20132",
                              "url": "www.ardi-dev.medra.org"
                            }
                          ]
                        }
                      ],
                      "creation": {
                        "type": "lcc:LexicalWork",
                        "name": "DRS name",
                        "identifiers": [
                          {
                            "type": "lcc:ISBN",
                            "value": "99X09100000134",
                            "subtype": ""
                          },
                          {
                            "type": "lcc:DOI",
                            "value": "10.081.77910/000013447",
                            "subtype": ""
                          },
                          {
                            "type": "lcc:ISBNA",
                            "value": "2018.910.229101343",
                            "subtype": ""
                          }
                        ]
                      },
                      "rightsNotice": {
                        "names": [
                          "Paola Pippo (as a sample)",
                          "mEDRA",
                          "ARDITO"
                        ],
                        "years": [
                          "2016",
                          "2017"
                        ],
                        "extensions": [
                          {
                            "value": "Extension di test in lingua italiana",
                            "language": "ita"
                          },
                          {
                            "value": "All rights reserved. (test for english language)",
                            "language": "eng"
                          }
                        ]
                      },
                      "furtherRightsInformation": {
                        "assignmentTypes": [
                          "lcc:CC_License_BY_NC"
                        ],
                        "rightAssignments": [
                          "https://test.org/licenses/by-medra-staff/006/"
                        ],
                        "rightsInformationTypes": [
                          "lcc:ApplicableLicense"
                        ]
                      },
                      "drs": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<DigitalRightsholderStatement xmlns:drs=\"http://www.rightscom.com/2011/drs#\"\n                              xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\"\n                              xsi:schemaLocation=\"http://www.rightscom.com/2011/drs# medra-drs.xsd\">\n              <DrsProfileType>lcc:DrsProfile_ARDI</DrsProfileType>\n\t            <Right>\t\n\t\t            <RightIdentifier IdentifierType=\"lcc:ARDI\">\n         <IdentifierValue>10.29414/ardi:1528878585467</IdentifierValue>\n      </RightIdentifier>\n      <RightStatus>lcc:EffectiveRight</RightStatus>\n\t\t            <Rightsholder>\n                  <Identifier IdentifierType=\"lcc:ISNI\">\n                    <IdentifierValue>1234-5678-9876-0000</IdentifierValue>\n                  </Identifier>\n                  <Identifier IdentifierType=\"lcc:ORCID\">\n                    <IdentifierValue>1234-5678-9876-0023</IdentifierValue>\n                  </Identifier>\n                  <Name>\n                    <NameValue>Paola Pluto</NameValue>\n                    <NamePart NamePartType=\"lcc:KeyName\">Mazzucchi</NamePart>\n                    <NamePart NamePartType=\"lcc:NamesBeforeKeyName\">Paola</NamePart>\n                  </Name>\n                  <Contact>\n                    <Name>Paola Pluto</Name>\n                    <EmailAddress>paola.pippo@email.it</EmailAddress>\n                    <PhoneNumber>02555555555</PhoneNumber>\n                    <PostalAddress>Corso di Porta Romana, 108 Milano 20132</PostalAddress>\n                    <URL>www.medra-dev.medra.org</URL>\n                  </Contact>\n                  <Contact>\n                    <Name>Jehu Paperino</Name>\n                    <EmailAddress>test-drs@email.it</EmailAddress>\n                    <PhoneNumber>0255222555</PhoneNumber>\n                    <PostalAddress>Corso di Porta Romana, 108 Milano 20132</PostalAddress>\n                    <URL>www.ardi-dev.medra.org</URL>\n                  </Contact>\n\t\t            </Rightsholder>\n                <Rightsholder>\n                  <Identifier IdentifierType=\"lcc:ORCID\">\n                    <IdentifierValue>1234-5678-9876-0023</IdentifierValue>\n                  </Identifier>\n                  <Identifier IdentifierType=\"lcc:ISNI\">\n                    <IdentifierValue>1234-5678-9876-2323</IdentifierValue>\n                  </Identifier>\n                  <Name>\n                    <NameValue>mEDRA</NameValue>\n                  </Name>\n                  <Contact>\n                      <Name>Pippo Pluto Paperino</Name>\n                      <EmailAddress>ivana.medra@medra.com</EmailAddress>\n                      <PhoneNumber>025522255521</PhoneNumber>\n                      <PostalAddress>Corso di Porta Romana, 108 Milano 20132</PostalAddress>\n                      <URL>www.ardi-dev.medra.org</URL>\n                    </Contact>\n                </Rightsholder>\n                <Rightsholder>\n                  <Identifier IdentifierType=\"lcc:ISNI\">\n                    <IdentifierValue>1234-5678-9876-2323</IdentifierValue>\n                  </Identifier>\n                  <Name>\n                    <NameValue>mEDRA staff support</NameValue>\n                    <NamePart NamePartType=\"lcc:KeyName\">mEDRA tech</NamePart>\n                    <NamePart NamePartType=\"lcc:NamesBeforeKeyName\">staff support</NamePart>\n                  </Name>\n                  <Contact>\n                    <Name>Contact Pippo (for test)</Name>\n                    <EmailAddress>my.email@mail.it</EmailAddress>\n                    <PhoneNumber>021122255521</PhoneNumber>\n                    <PostalAddress>Corso di Porta Romana, 108 Milano 20132</PostalAddress>\n                    <URL>www.ardi-dev.medra.org</URL>\n                  </Contact>\n                </Rightsholder>\n                <ControlledCreation>\n                  <Identifier IdentifierType=\"lcc:ISBN\">\n                    <IdentifierValue>99X09100000134</IdentifierValue>\n                  </Identifier>\n                  <Identifier IdentifierType=\"lcc:DOI\">\n                    <IdentifierValue>10.081.77910/000013447</IdentifierValue>\n                  </Identifier>\n                  <Identifier IdentifierType=\"lcc:ISBNA\">\n                    <IdentifierValue>2018.910.229101343</IdentifierValue>\n                  </Identifier>\n                  <Name>DRS name</Name>\n                  <CreationType>lcc:LexicalWork</CreationType>\n                </ControlledCreation>\n              <UseType>lcc:All</UseType>\n              <ControlType>lcc:All</ControlType>\n              <RightsNotice>\n                <Name>Paola Pippo (as a sample)</Name>\n                <Name>mEDRA</Name>\n                <Name>ARDITO</Name>\n                <Year>2016</Year>\n                <Year>2017</Year>\n                <Extension Language=\"ita\">Extension di test in lingua italiana</Extension>\n                <Extension Language=\"eng\">All rights reserved. (test for english language)</Extension>\n              </RightsNotice>\n              <FurtherRightsInformation> <!-- relates to RightsPolicyType = lcc:CC_License_BY_NC-->\n                <RightsAssignmentType>lcc:CC_License_BY_NC</RightsAssignmentType> \n                <RelatedRightAssignment IdentifierType=\"lcc:URI\"> \n                  <IdentifierValue>https://test.org/licenses/by-medra-staff/006/</IdentifierValue>  \n                </RelatedRightAssignment>                            \n                <FurtherRightsInformationType>lcc:ApplicableLicense</FurtherRightsInformationType> \n              </FurtherRightsInformation>\n              <Territory>lcc:World</Territory>\n              <StartTime>2018-06-13</StartTime>\n              <EndTime>2018-12-31</EndTime>\n              <PercentageShare>100</PercentageShare>\n              <IsExclusive>lcc:True</IsExclusive>\n\t            </Right>\n            <Asserter>\n              <Identifier IdentifierType=\"lcc:ISNI\">\n                <IdentifierValue>1234-5678-9876-4444</IdentifierValue>\n              </Identifier>\n              <Name>PM (for test)</Name>\n            </Asserter>\n            <AssertionDateTime>2018-05-14T10:03:01</AssertionDateTime>\n           </DigitalRightsholderStatement>"
                    },
                    "accounting": [
                      {
                        "ardi": "10.29414/ardi:1528878585467",
                        "service": "HANDLE",
                        "operation": "CREATE",
                        "result": "SUCCESS",
                        "resultDescription": null,
                        "timestamp": "13-06-2018 10:29:46"
                      },
                      {
                        "ardi": "10.29414/ardi:1528878585467",
                        "service": "HUB",
                        "operation": "CREATE",
                        "result": "SUCCESS",
                        "resultDescription": null,
                        "timestamp": "13-06-2018 10:29:50"
                      },
                      {
                        "ardi": "10.29414/ardi:1528878585467",
                        "service": "METADATA",
                        "operation": "CREATE",
                        "result": "SUCCESS",
                        "resultDescription": null,
                        "timestamp": "13-06-2018 10:29:50"
                      }
                    ],
                    "startTimestamp": "13-06-2018 10:29:45",
                    "endTimestamp": "13-06-2018 10:29:50"
                  }
          }
   
   Using the XML upload interface for manual registration
   ======================================================
   Using the XML upload interface sending the file containing the DRS to the API, for manual registration
   HOST: https://ardi-dev.medra.org/ardi-ra/ardi/logon-page.html
   ![login-page](https://user-images.githubusercontent.com/39902417/41343402-ca92bd7e-6efe-11e8-8985-083fa8b8ee57.PNG)
   ## Authorization
 This interface requires a basic authentication, the user must be registered (username and password) on mEDRA in order to achieve the 
 registration. Request Registers valid DRS (Digital Rightsholder Statement) from request body ({application/xml; charset=utf-8, 
 application/json; charset=utf-8})

### Required data for ARDI registration as result of DRS (Digital Rightsholder Statement) submission

| Property        | Description                                     | Type      | Mandatory |
| :-------        | :----------                                     | :---      | :-------- |
| Authentication  | Basic Authentication (username:password)        | string    | yes       |
| request body    | valid DRS (Digital Rightsholder Statement) file | file      | yes       |

 After the user has successfully logged in, the following page is display to allow the user to select the file containing the valid DRS to 
 be submitted.
 https://ardi-dev.medra.org/ardi-ra/ardi/reserved/upload-page.html
 
![upload-page](https://user-images.githubusercontent.com/39902417/41341832-fdf47f12-6efa-11e8-932e-e2c986a6836a.png)

Finally the ARDI registration service REST API returns a JSON response to the user submitting the DRS which includes:
- The assigned ARDI, to be stored and reused by the registrant for following updates of the same DRS or to make available the ARDI resolving to the landing page along the value chain
- The full DRS metadata as submitted, that can be re-used to communicate with other systems in B2B mode. This is especially relevant once GUIs for registrants will be developed on top of existing services, as users will be able to exploit DRS in the LCC format although they might have no proficiency with it
- The accounting data, providing results (success/failure) for each operation (creation/update) for each service (Handle System service/Hub service/Metadata service). This solution is scalable to other services that might make use of the DRS and assigned ARDI in the future, such as for example export to other third party systems.

The json response body is the same as in the Result of registration via the API that hold the DRS as request body, for B2B registrations
