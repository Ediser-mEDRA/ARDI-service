# ARDI REGISTRATION FORMAT

The DOI system is based on a flexible and extensible metadata framework that allows for the development of different application profiles 
targeted at the needs of different communities of users. Such a flexible approach has enabled each RA to develop DOI-based services for the 
persistent identification and description of different entities in different contexts of application, from the publishing sector to the 
dataset domain as well as to other media sectors. In order to allow users (rightholders or services for rightholders) to assign an ARDI to 
a DRS using the service developed by mEDRA, the following options were discussed and assessed:


*	define an ad hoc proprietary registration schema;
*	reuse constructs from other mEDRA DOI registration formats based on ONIX standard;
*	adopt the LCC DRS standard format.

After having analysed strengths and weaknesses of each option in terms of scalability to different content assets, expressiveness of rights 
data, compliance to a standard, ease of implementation for users, openness to other players on the DOI market, the decision to use the LCC 
DRS standard format was taken.
Starting from requirements provided by mEDRA, an exemplary DRS Profile for ARDITO has been created to allow the ARDI registration 
(lcc:DrsProfile_ARDI). From this point on, extensive work has been done to fine tune the schema and several iteration of requirements, 
specifications and schema enhancements have been exchanged, discussed and agreed upon, between mEDRA technical team and metadata experts 
and the Copyright Hub experts (subcontractor Rightscom). The resulting schema for the DRS Profile for ARDI registration is thus a 
simplified version of the LCC DRS Schema, which means it’s compliant with the LCC DRS schema (i.e. each xml file validated against this 
schema is valid also against the LCC DRS Schema). 

In order to allow the deposit of simple statement, the ARDI registration format contains a subset of group of elements taken from the DRS 
schema. Thus in mEDRA application a Digital Rightsholder Statement is described by the following high level information:

In mEDRA application, we have decided to simplify the structure of a Right, starting from two basic use cases:
*	an (self-published) author wishing to declare his/her copyright ownership on a content
*	a publisher wishing to indicate some basic copyright info and licence info (especially related to Open Access) on a content
Thus in mEDRA application a Right is described by the following information:
