Access to rights data via identification technologies optimisation - Right-aware DOI suite 
# Right-aware DOI suite overview
This service describes the technical features of the new tool that achieves the registration of a Digital Rightsholder Statement (DRS). The tool is a new web App for ARDITO taking care of the registration process of an ARDI identifier to be assigned to rights declarations,
and includes a new registration schema based on the LCC DRS format and a new landing page making accessible to any users the chain of declarations for a given identified content asset and interfaces for registrants. From technical point of view, the registration of a DRS involves at least two infrastructures: 
 * The handle system that receive the ARDI identifier created, and persisted it for management purpose, resolution URL, etc.
 * The Open Permissions Platform Onboarding Service that receive the identifiers (isbn, doi, ardi, etc.) and onboard them to a repository within the Hub.
## ARDITO registration tool
The point of entry is the ARDI registration service REST API that allows a user to submit a DRS (Digital Rightsholder Statement) expressing a rights notice on an individual content asset (creation in LCC terms) according to the LCC DRS schema.
The registration of an ARDI is handled in two ways:

### 1. Directly via the API that hold the DRS as request body, for B2B registrations
 HOST: https://ardi-dev.medra.org/statement
 ### Authorization
 This API requires a basic authentication, the user must be registered (username and password) on mEDRA in order to achieve the registration.
 ### Registered a DRS (Digital Rightsholder Statement) [https://ardi-dev.medra.org/statement]
 
 + Request Register valid DRS (Digital Rightsholder Statement) from request body ({application/xml; charset=utf-8, application/json; charset=utf-8})
    + Headers
         Accept: [application/json, application/xml]
         Authorization: Basic [username:password]
  
    + Response 200 (application/json; charset=UTF-8)
        + Body
        
  
