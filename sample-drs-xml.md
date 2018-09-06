# Example of the DRS to register an ARDI for a book
	
        
	<?xml version="1.0" encoding="UTF-8"?>
        <DigitalRightsholderStatement xmlns="http://www.rightscom.com/2011/drs#" xmlns:drs="http://www.rightscom.com/2011/drs#" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.rightscom.com/2011/drs# medra-drs.xsd">
	<!-- obbligatorio: inseriremo sempre il valore lcc:DrsProfile_ARDI-->
	<DrsProfileType>lcc:DrsProfile_ARDI</DrsProfileType>
	<!-- obbligatorio -->
	<Right>
		<!-- sarà sempre lcc:EffectiveRight -->		
		<RightStatus>lcc:EffectiveRight</RightStatus>
		<!-- almeno 1 RightsHolder-->		
		<Rightsholder>
		<!-- bisogna indicare sempre almeno uno tra Identifier e Name: quali valori prendo e da dove? -->
			<Identifier IdentifierType="lcc:ORCID"> <!-- oppure "lcc:ORCID"-->
				<IdentifierValue>http://orcid.org/0000-0001-6157-8808</IdentifierValue>
			</Identifier>
			<Name>
				<NameValue>Anna Lionetti</NameValue>
			</Name>
		</Rightsholder>
		<!-- obbligatoria -->
		<ControlledCreation>
		<!-- indicare Identifier o Name: quali valori prendo? -->
						<Identifier IdentifierType="lcc:ISBN">
				<IdentifierValue>9788889637821</IdentifierValue>
			</Identifier>
			<Identifier IdentifierType="lcc:ISBNA">
				<IdentifierValue>10.978.8889637/821</IdentifierValue>
			</Identifier>
			<Name>Il dato è tratto</Name>
			<!-- opzionale -->
			<CreationType>lcc:Book</CreationType>
		</ControlledCreation>
		<!-- Cosa metto? -->
		<UseType>lcc:All</UseType>
		<!-- Cosa metto? -->
		<ControlType>lcc:All</ControlType>
		<!-- Opzionale: cosa metto? -->
		<RightsNotice>
			<Name>Anna Lionetti</Name>
			<Name>mEDRA</Name>
			<Year>2015</Year>
			<Extension Language="eng">All rights reserved.</Extension>
		</RightsNotice>
		<!-- obbligatorio: cosa metto? -->
		<Territory>lcc:World</Territory>
		<!-- obbligatorio: cosa metto? -->
		<PercentageShare>100</PercentageShare>
		<!-- obbligatorio: cosa metto? -->
		<IsExclusive>lcc:True</IsExclusive>
	</Right>
	<!-- obbligatorio: cosa metto? -->
	<Asserter>
		 <!-- Identifier o Name obbligatorio -->
		<Identifier IdentifierType="lcc:ISNI">
			<IdentifierValue>1234-5678-9876-4444</IdentifierValue>
		</Identifier>
		<Name>Paola Mazzucchi</Name>
	</Asserter>
	<!-- obbligatorio: cosa metto? -->
	<AssertionDateTime>2018-07-01T17:26:01</AssertionDateTime>
     </DigitalRightsholderStatement>
