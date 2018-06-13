# ARDI Service Low Level Design

Once the registration message is received and validated, the following operations are executed:
* Generation of the ARDI identifier
* Minting of the ARDI in the DOI Handle System, exploiting the existing functionalities of mEDRA DOI Registration Agency (Handle System 
service)
* Onboarding in the Copyright Hub Platform through an API that extracts from the DRS the metadata set agreed with Copyright Hub and therefore 
in mEDRA Hub repository on mEDRA servers, through the dedicated API (Hub service)	
* Storage of the full DRS metadata in the mEDRA ARDI database, residing in mEDRA servers (Metadata service)
* Storage of accounting data with results of the operations above in mEDRA ARDI database (Metadata service)

The following diagram depicts the entire process of registering a DRS, and onboard the metadata agreed with the Copyright Hub in the mEDRA Hub 
repository.

![low-level-design](https://user-images.githubusercontent.com/39902417/41361845-4c93ca44-6f30-11e8-92a9-3a26a843f281.png)

