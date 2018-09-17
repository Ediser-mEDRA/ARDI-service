# Example of the DRS to register an ARDI for a book
	
      <?xml version="1.0" encoding="UTF-8"?>
      <DigitalRightsholderStatement xmlns="http://www.rightscom.com/2011/drs#" 
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
	xsi:schemaLocation="http://www.rightscom.com/2011/drs# https://ardi-dev.medra.org/ardi-ra/schema/drs/1.0/medra-drs.xsd">
	<!-- always input lcc DrsProfile_ARDI-->
	<DrsProfileType>lcc:DrsProfile_ARDI</DrsProfileType>
	<!-- mandatory -->
	<Right>
		<!-- always input lcc:EffectiveRight -->
		<RightStatus>lcc:EffectiveRight</RightStatus>
		<!-- at least 1 RightsHolder-->
		<Rightsholder>
			<!-- at least one of Identifier and Name -->
			<Identifier IdentifierType="lcc:ORCID">
				<IdentifierValue>http://orcid.org/0000-0001-6157-8808</IdentifierValue>
			</Identifier>
			<Name>
				<NameValue>Anna Lionetti</NameValue>
			</Name>
		</Rightsholder>
		<!-- mandatory -->
		<ControlledCreation>
			<Identifier IdentifierType="lcc:ISBN">
				<IdentifierValue>9788889637821</IdentifierValue>
			</Identifier>
			<Identifier IdentifierType="lcc:ISBNA">
				<IdentifierValue>10.978.8889637/821</IdentifierValue>
			</Identifier>
			<Name>Il dato è tratto</Name>
			<CreationType>lcc:Book</CreationType>
		</ControlledCreation>
		<UseType>lcc:All</UseType>
		<ControlType>lcc:All</ControlType>
		<RightsNotice>
			<Name>Anna Lionetti</Name>
			<Name>mEDRA</Name>
			<Year>2015</Year>
			<Extension Language="eng">All rights reserved.</Extension>
		</RightsNotice>
		<Territory>lcc:World</Territory>
		<PercentageShare>100</PercentageShare>
		<IsExclusive>lcc:True</IsExclusive>
	</Right>
	<Asserter>
		<Identifier IdentifierType="lcc:ISNI">
			<IdentifierValue>1234-5678-9876-4444</IdentifierValue>
		</Identifier>
		<Name>Paola Mazzucchi</Name>
	</Asserter>
	<AssertionDateTime>2018-07-01T17:26:01</AssertionDateTime>
    </DigitalRightsholderStatement>  
