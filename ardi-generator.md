# ARDI generator identifier

While typically DOI registrants are assigned with their own DOI prefix and are free to define a unique suffix for each asset identified 
with a DOI, in the case of the ARDI service the decision was taken to automatically and centrally generate ARDI identifiers. This decision 
has been taken to address the following aspects:
* minimise the effort for ARDI registrants, considering that one of the target users will be individual creators;
*	streamline the process of assigning ARDI to DRS by allowing to reuse as much as possible DRS produced for other purposes and application, 
thus facilitating interoperability;
*	maintain authoritative control on the issuing of ARDI names;
*	avoid proliferation of “syntaxes”;
*	provide an easy-to-plug-in service for any third party or intermediary offering services to creators including ARDI assignment.

Therefore one DOI prefix has been assigned to the ARDI service (10.29414 for the development phase) and a simple algorithm using the 
timestamp of the DRS submission has been implemented. The resulting syntax for an ARDI name is [ARDI DOI Prefix]/ardi:[timestamp]. 

As this first release of the ARDI service allows for the deposit of one DRS at the time, the solution implemented is sufficient to ensure 
uniqueness of the identifier, however the need for a more robust algorithm as well as the need for multiple prefixes for different 
services, content industry or DRS provider will be assessed.
