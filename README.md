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
   
   application/xml; charset=utf-8
   ==============================
   
   application/json; charset=utf-8
   ==============================
   
   Using the XML upload interface for manual registration
   ======================================================
   Using the XML upload interface sending the file containing the DRS to the API, for manual registration
