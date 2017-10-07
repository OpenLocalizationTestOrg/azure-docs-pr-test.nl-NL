---
title: aaaGuide toocreating een gegevensservice voor Hallo Marketplace | Microsoft Docs
description: Gedetailleerde instructies waarmee toocreate, certificeren en implementeren van een Service voor gegevens aanschaffen op Hallo Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>Toewijzing van een bestaande web service tooOData via CSDL
> [!IMPORTANT]
> **Op dit moment wordt niet langer zijn voorbereiden op alle nieuwe gegevensservice uitgevers. Nieuwe dataservices wordt niet goedgekeurd voor de aanbieding.** Als u een SaaS-business-toepassing hebt wilt toopublish op AppSource vindt u meer informatie [hier](https://appsource.microsoft.com/partners). Als u beschikt over een IaaS-toepassingen of developer-service dat u zou zoals toopublish op Azure Marketplace vindt u meer informatie [hier](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

In dit artikel wordt een overzicht over het toouse een CSDL-toomap een bestaande service tooan compatibel OData-service. Hierin wordt uitgelegd hoe toocreate Hallo toewijzing document (CSDL) dat de invoeraanvraag van de client via een Serviceaanroep van de en Hallo HALLO hallo transformeert uitvoer (gegevens) terug toohello client via een compatibel OData-feed. Microsoft Azure Marketplace stelt services toohello eindgebruikers met behulp van Hallo OData-protocol. Services die beschikbaar worden gesteld door inhoudsproviders (eigenaren) beschikbaar worden gesteld in verschillende vormen, zoals REST, SOAP, enz.

## <a name="what-is-a-csdl-and-its-structure"></a>Wat is een CSDL en de structuur?
Een CSDL (conceptuele Schema Definition Language) is een specificatie definiëren hoe toodescribe webservice of database-service in algemene XML-bewoordingen toohello Azure Marketplace.

Eenvoudig overzicht van Hallo **stroom aanvragen:**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

Hallo **gegevensstroom** bevindt zich in Hallo tegengestelde richting:

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**Afbeelding 1** diagrammen hoe een client zou ophalen via een inhoudsprovider (uw service) door te gaan via hello Azure Marketplace.  Hallo CSDL wordt gebruikt door Hallo toewijzing/transformatie onderdeel toohandle Hallo aanvraag en gegevens uitwisselen tussen Hallo inhoud en van de provider dienst(en) Hallo vraagt de client.

*Afbeelding 1: Gedetailleerde stroom van aanvragende client toocontent provider via Azure Marketplace*

  ![tekenen](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

Raadpleeg voor de achtergrond van het Atom, Atom Pub en Hallo OData-protocol bij welke hello Azure Marketplace-extensies build: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

Fragment boven het koppeling: *'hello doel van Hallo Open Data protocol (hierna genoemde tooas OData) is een op REST gebaseerde tooprovide protocol voor CRUD-stijl-bewerkingen (maken, lezen, bijwerken en verwijderen) op basis van bronnen die worden weergegeven als dataservices. Een service"gegevens" is een eindpunt wanneer blootgesteld aan een of meer 'verzamelingen' elke met nul of meer 'posten', die bestaan uit gegevens hebt ingevoerd met de naam / waarde-paren. OData is gepubliceerd door Microsoft onder OASIS (organisatie voor Hallo verschuiving van gestructureerde gegevens standaarden) standaarden zodat iedereen die wil toocan bouwen servers, clients of hulpprogramma's zonder royalties of beperkingen."*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>Er zijn drie essentiële gegevens die gedefinieerd door Hallo CSDL toobe zijn:
* Hallo **eindpunt** Hallo Hallo serviceprovider Web adres (URI) Hallo Service
* Hallo **parameters voor** wordt doorgegeven als invoer toohello serviceprovider Hallo definities van Hallo parameters toohello inhoudsprovider-service niet actief toohello gegevenstype worden verzonden.
* **Schema** Hallo gegevens toohello Service aanvragen Hallo schema van Hallo-gegevens worden geleverd door Hallo inhoudsprovider-service wordt geretourneerd, met inbegrip van Container, verzamelingen/tabellen, variabelen/kolommen en gegevenstypen.

Hallo volgende diagram geeft een overzicht van Hallo stroom uit waarbij Hallo-client Hallo OData-instructie (aanroep toohello inhoud van de provider-webservice) toogetting Hallo resultaten/gegevens terug voert.

  ![tekenen](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>stappen:
1. Client stuurt via een aanroep van aanvraag met een invoer gedefinieerde Parameters in XML-toohello Azure Marketplace voltooid
2. CSDL is gebruikte toovalidate Hallo aanroep.
   * Hallo geformatteerd Service aanroepen gestuurd toohello inhoud Providers Service door hello Azure Marketplace
3. Hallo Webservice wordt uitgevoerd en tekstknooppunten Hallo actie Hallo Http-term wordt uitgevoerd (dat wil zeggen ophalen) Hallo gegevens worden geretourneerd tooAzure Marketplace waar Hallo gegevens aangevraagd (indien aanwezig) is zichtbaar gemaakt in XML-indeling toohello Client met behulp van de toewijzing is gedefinieerd in CSDL Hallo Hallo.
4. Hallo Client wordt verzonden hello gegevens (indien aanwezig) in XML- of JSON-indeling

## <a name="definitions"></a>Definities
### <a name="odata-atom-pub"></a>OData-ATOM pub
Een uitbreiding toohello ATOM pub waarbij elk item staat voor één rij met een resultaat ingesteld. Verbeterde toocontain Hallo waarden van Hallo rij – is inhoud deel van de Hallo van Hallo vermelding als sleutel-waardeparen. Meer informatie is hier vinden: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>CSDL - Conceptual Schema Definition Language
Hiermee kunt u definiëren functies (SPROCs) en de entiteiten die worden weergegeven via een database. Meer informatie hier vinden: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> Klik op Hallo **andere versies** vervolgkeuzelijst en selecteer een versie als er geen Hallo artikel.
> 
> 

### <a name="edm---entry-data-model"></a>EDM - gegevensmodel vermelding
* Overzicht: [http://msdn.microsoft.com/library/vstudio/ee382825 (v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* Voorbeeld: [http://msdn.microsoft.com/library/aa697428 (v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* Gegevenstypen: [http://msdn.microsoft.com/library/bb399548 (v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

Hallo hieronder vindt u Hallo gedetailleerde links tooRight stroom van het waarbij Hallo client Hallo OData-instructie (aanroep toohello inhoud van de provider-webservice) toogetting Hallo resultaten/gegevens terug invoert:

  ![tekenen](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>CSDL-basisbeginselen
Een CSDL (conceptuele Schema Definition Language) is een specificatie definiëren hoe toodescribe webservice of database-service in algemene XML-bewoordingen toohello Azure Marketplace. CSDL beschrijft Hallo kritieke stuks die **Hallo doorgeven van gegevens van Hallo gegevensbron toohello Azure Marketplace mogelijk maakt.** de belangrijkste onderdelen Hallo worden hier beschreven:

* Informatie over de interface met een beschrijving van alle openbaar beschikbare functies (FunctionImport knooppunt)
* Informatie over gegevenstypen voor alle bericht requests(input) en bericht responses(outputs) (EntitySet-EntityContainer/EntityType knooppunten)
* Informatie over Hallo transport protocol toobe binding gebruikt (Header knooppunt)
* Adresgegevens voor het zoeken van Hallo opgegeven service (BaseURI kenmerk)

Kortom, vertegenwoordigt Hallo CSDL een contract en taal-platformonafhankelijk tussen Hallo service aanvrager en Hallo-serviceprovider. Hallo CSDL gebruikt, kan een client een webservice service/database vinden en een van de openbaar beschikbare functies aanroepen.

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>In verband met een CSDL-tooa Database of een verzameling
**Hallo CSDL-specificatie**

CSDL is XML-grammatica voor het beschrijven van een webservice. Hallo-specificatie zelf is onderverdeeld in 4 belangrijke elementen: EntitySet, FunctionImport; Naamruimte en EntityType.

toomake deze abstractie eenvoudiger toounderstand kunt hebben CSDL tooa.

Houd er rekening mee;

  CSDL vertegenwoordigt een contract en taal-platformonafhankelijk tussen Hallo **service aanvrager** en Hallo **serviceprovider**. CSDL, met een **client** kunnen vinden een **servicedatabase/webservice** en aanroepen van de openbaar **functies.**

Voor een gegevensservice Hallo kunnen vier onderdelen van een CSDL in termen van een Database-, tabel-, kolom- of Store Procedure worden beschouwd.

Die betrekking hebben op deze als volgt voor een Service van gegevens:

* EntityContainer ~ = Database
* EntitySet ~ = tabel
* EntityType ~ kolommen =
* FunctionImport ~ opgeslagen Procedure =

**HTTP-termen die zijn toegestaan**

* – Retourneert waarden ophalen uit Hallo-db (retourneert een verzameling)
* POST – gebruikt toopass gegevens tooand optionele retourwaarden van Hallo-db (een nieuwe vermelding in de verzameling hello, return-id/URI maken)
* Hiermee verwijdert u gegevens van Hallo DB (een verzameling verwijdert) – verwijderen
* PUT – gegevens bijwerken in een database (vervangen door een verzameling of maak een)

## <a name="metadatamapping-document"></a>Metagegevens/toewijzing Document
Hallo metagegevens/toewijzing document is gebruikte toomap een inhoudsprovider bestaande webservices zodat deze kan worden weergegeven als een OData-webservice door hello Azure Marketplace-systeem. Deze is gebaseerd op CSDL en implementeert die toegankelijk is via Azure Marketplace-webservices op basis van enkele extensies tooCSDL tooaccommodate Hallo behoeften van de REST. Hallo-uitbreidingen zijn gevonden in Hallo [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) naamruimte.

Hier volgt een voorbeeld van Hallo CSDL: (kopiëren en plakken Hallo onderstaand voorbeeld CSDL in een XML-editor en wijzig toomatch uw Service.  Plak in CSDL toewijzing DataService tabblad bij het maken van uw service in Hallo [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).

**Voorwaarden:** die verband houden met Hallo CSDL termen toohello [Publishing Portal](https://publish.windowsazure.com) voorwaarden van de gebruikersinterface (PPUI).

* Bieden "Title" in hello PPUI tooMyWebOffer is gekoppeld
* Mijnbedrijf in Hallo PPUI te is gekoppeld**Publisher weergavenaam** in Hallo [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) gebruikersinterface
* Uw API is gekoppeld tooa Web- of Data-Service (een Plan in Hallo PPUI)

**Hiërarchie:** (inhoudsprovider) van een bedrijf eigenaar is van de aanbiedingen die Plan(s) hebben, namelijk service(s), welke uitgelijnd met een API.

### <a name="webservice-csdl-example"></a>WebService CSDL-voorbeeld
Maakt verbinding tooa-service die een eindpunt van de web-toepassing (zoals een C#-toepassing weergeeft)

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> Meer voorbeelden van de webservice CSDL weergeven in Hallo artikel [voorbeelden voor het toewijzen van een bestaande web service tooOData via CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>DataService CSDL-voorbeeld
Maakt verbinding tooa-service die weergeeft een databasetabel of weergave zoals een eindpunt onderstaand voorbeeld twee dat API CSDL toont (met kunt weergaven in plaats van tabellen) op basis van API's voor de databank.

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a>Zie ook
* Als u geïnteresseerd in learning en de specifieke kennis Hallo-knooppunten en de bijbehorende parameters bent, Lees dit artikel [Service OData toewijzing gegevensknooppunten](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) voor definities en uitleg, voorbeelden en gebruik case-context.
* Als u geïnteresseerd bent in de voorbeelden controleren, Lees dit artikel [gegevens Service OData toewijzing voorbeelden](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee voorbeeldcode en begrijpen codesyntaxis en in het contextmenu.
* tooreturn toohello pad voor het publiceren van een gegevensservice toohello Azure Marketplace Lees dit artikel voorgeschreven [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).

