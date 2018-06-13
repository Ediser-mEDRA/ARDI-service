Access to rights data via identification technologies optimisation - Right-aware DOI suite 
# Right-aware DOI suite overview
This service describes the technical features of the new tool that achieves the registration of a Digital Rightsholder Statement (DRS). The tool is a new web App for ARDITO taking care of the registration process of an ARDI identifier to be assigned to rights declarations,
and includes a new registration schema based on the LCC DRS format and a new landing page making accessible to any users the chain of declarations for a given identified content asset and interfaces for registrants. From technical point of view, the registration of a DRS involves at least two infrastructures: 
 * The handle system that receive the ARDI identifier created, and persisted it for management purpose, resolution URL, etc.
 * The Open Permissions Platform Onboarding Service that receive the identifiers (isbn, doi, ardi, etc.) and onboard them to a repository within the Hub.
# ARDITO registration tool
The point of entry is the ARDI registration service REST API that allows a user to submit a DRS (Digital Rightsholder Statement) expressing a rights notice on an individual content asset (creation in LCC terms) according to the LCC DRS schema.
The registration of an ARDI is handled in two ways:

# 1. Directly via the API that hold the DRS as request body, for B2B registrations
 HOST: https://ardi-dev.medra.org/statement
 ## Authorization
 This API requires a basic authentication, the user must be registered (username and password) on mEDRA in order to achieve the registration. Request Registers valid DRS (Digital Rightsholder Statement) from request body ({application/xml; charset=utf-8, application/json; charset=utf-8})

##### Required data for ARDI registration as result of DRS (Digital Rightsholder Statement) submission

| Property        | Description                                | Type      | Mandatory |
| :-------        | :----------                                | :---      | :-------- |
| Authentication  | Basic Authentication (username:password)   | string    | yes       |
| request body    | valid DRS (Digital Rightsholder Statement) | xml/json  | yes       |

   + Request Method
 
         [POST]
  
   + Request Headers
      
         Accept: [application/json, application/xml]
         Authorization: Basic [username:password]
         
   + Request body: valid DRS (Digital Rightsholder Statement) ({application/xml; charset=utf-8, application/json; charset=utf-8}) according to the LCC DRS schema.
     
     ## application/xml; charset=utf-8
            
             {
              <?xml version="1.0" encoding="UTF-8" standalone="no"?>
              <DigitalRightsholderStatement xmlns="http://www.rightscom.com/2011/drs#" xmlns:drs="http://www.rightscom.com/2011/drs#"      
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.rightscom.com/2011/drs# medra-drs.xsd">
              <DrsProfileType>lcc:DrsProfile_ARDI</DrsProfileType>
	            <Right>	
		            <RightStatus>lcc:EffectiveRight</RightStatus>
		            <Rightsholder>
                  <Identifier IdentifierType="lcc:ISNI">
                    <IdentifierValue>1234-5678-9876-0000</IdentifierValue>
                  </Identifier>
                  <Identifier IdentifierType="lcc:ORCID">
                    <IdentifierValue>1234-5678-9876-0023</IdentifierValue>
                  </Identifier>
                  <Name>
                    <NameValue>Paola Pluto</NameValue>
                    <NamePart NamePartType="lcc:KeyName">Mazzucchi</NamePart>
                    <NamePart NamePartType="lcc:NamesBeforeKeyName">Paola</NamePart>
                  </Name>
                  <Contact>
                    <Name>Paola Pluto</Name>
                    <EmailAddress>paola.pippo@email.it</EmailAddress>
                    <PhoneNumber>02555555555</PhoneNumber>
                    <PostalAddress>Corso di Porta Romana, 108 Milano 20132</PostalAddress>
                    <URL>www.medra-dev.medra.org</URL>
                  </Contact>
                  <Contact>
                    <Name>Jehu Paperino</Name>
                    <EmailAddress>test-drs@email.it</EmailAddress>
                    <PhoneNumber>0255222555</PhoneNumber>
                    <PostalAddress>Corso di Porta Romana, 108 Milano 20132</PostalAddress>
                    <URL>www.ardi-dev.medra.org</URL>
                  </Contact>
		            </Rightsholder>
                <Rightsholder>
                  <Identifier IdentifierType="lcc:ORCID">
                    <IdentifierValue>1234-5678-9876-0023</IdentifierValue>
                  </Identifier>
                  <Identifier IdentifierType="lcc:ISNI">
                    <IdentifierValue>1234-5678-9876-2323</IdentifierValue>
                  </Identifier>
                  <Name>
                    <NameValue>mEDRA</NameValue>
                  </Name>
                  <Contact>
                      <Name>Pippo Pluto Paperino</Name>
                      <EmailAddress>ivana.medra@medra.com</EmailAddress>
                      <PhoneNumber>025522255521</PhoneNumber>
                      <PostalAddress>Corso di Porta Romana, 108 Milano 20132</PostalAddress>
                      <URL>www.ardi-dev.medra.org</URL>
                    </Contact>
                </Rightsholder>
                <Rightsholder>
                  <Identifier IdentifierType="lcc:ISNI">
                    <IdentifierValue>1234-5678-9876-2323</IdentifierValue>
                  </Identifier>
                  <Name>
                    <NameValue>mEDRA staff support</NameValue>
                    <NamePart NamePartType="lcc:KeyName">mEDRA tech</NamePart>
                    <NamePart NamePartType="lcc:NamesBeforeKeyName">staff support</NamePart>
                  </Name>
                  <Contact>
                    <Name>Contact Pippo (for test)</Name>
                    <EmailAddress>my.email@mail.it</EmailAddress>
                    <PhoneNumber>021122255521</PhoneNumber>
                    <PostalAddress>Corso di Porta Romana, 108 Milano 20132</PostalAddress>
                    <URL>www.ardi-dev.medra.org</URL>
                  </Contact>
                </Rightsholder>
                <ControlledCreation>
                  <Identifier IdentifierType="lcc:ISBN">
                    <IdentifierValue>99X09100000134</IdentifierValue>
                  </Identifier>
                  <Identifier IdentifierType="lcc:DOI">
                    <IdentifierValue>10.081.77910/000013447</IdentifierValue>
                  </Identifier>
                  <Identifier IdentifierType="lcc:ISBNA">
                    <IdentifierValue>2018.910.229101343</IdentifierValue>
                  </Identifier>
                  <Name>DRS name</Name>
                  <CreationType>lcc:LexicalWork</CreationType>
                </ControlledCreation>
              <UseType>lcc:All</UseType>
              <ControlType>lcc:All</ControlType>
              <RightsNotice>
                <Name>Paola Pippo (as a sample)</Name>
                <Name>mEDRA</Name>
                <Name>ARDITO</Name>
                <Year>2016</Year>
                <Year>2017</Year>
                <Extension Language="ita">Extension di test in lingua italiana</Extension>
                <Extension Language="eng">All rights reserved. (test for english language)</Extension>
              </RightsNotice>
              <FurtherRightsInformation> <!-- relates to RightsPolicyType = lcc:CC_License_BY_NC-->
                <RightsAssignmentType>lcc:CC_License_BY_NC</RightsAssignmentType> 
                <RelatedRightAssignment IdentifierType="lcc:URI"> 
                  <IdentifierValue>https://test.org/licenses/by-medra-staff/006/</IdentifierValue>  
                </RelatedRightAssignment>                            
                <FurtherRightsInformationType>lcc:ApplicableLicense</FurtherRightsInformationType> 
              </FurtherRightsInformation>
              <Territory>lcc:World</Territory>
              <StartTime>2018-06-13</StartTime>
              <EndTime>2018-12-31</EndTime>
              <PercentageShare>100</PercentageShare>
              <IsExclusive>lcc:True</IsExclusive>
	            </Right>
            <Asserter>
              <Identifier IdentifierType="lcc:ISNI">
                <IdentifierValue>1234-5678-9876-4444</IdentifierValue>
              </Identifier>
              <Name>PM (for test)</Name>
            </Asserter>
            <AssertionDateTime>2018-05-14T10:03:01</AssertionDateTime>
           </DigitalRightsholderStatement>
          }
       
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
## 2. Using the XML upload interface sending the file containing the DRS to the API, for manual registration
 HOST: https://ardi-dev.medra.org/ardi-ra/ardi/logon-page.html
### Authorization
 This interface requires a basic authentication, the user must be registered (username and password) on mEDRA in order to achieve the registration. Request Registers valid DRS (Digital Rightsholder Statement) from request body ({application/xml; charset=utf-8, application/json; charset=utf-8})

### Required data for ARDI registration as result of DRS (Digital Rightsholder Statement) submission

| Property        | Description                                     | Type      | Mandatory |
| :-------        | :----------                                     | :---      | :-------- |
| Authentication  | Basic Authentication (username:password)        | string    | yes       |
| request body    | valid DRS (Digital Rightsholder Statement) file | file      | yes       |

 After the user have been performed the login successfully, the following page is display to allow the user to select the file that contains the valid DRS to submitted.
 https://ardi-dev.medra.org/ardi-ra/ardi/reserved/upload-page.html
 
