---
title: aaaGuide toocreating een gegevensservice voor Hallo Marketplace | Microsoft Docs
description: Gedetailleerde instructies waarmee toocreate, certificeren en implementeren van een Service voor gegevens aanschaffen op Hallo Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>Wat is Hallo knooppunten schema voor het toewijzen van een bestaande web service tooOData via CSDL?
> [!IMPORTANT]
> **Op dit moment wordt niet langer zijn voorbereiden op alle nieuwe gegevensservice uitgevers. Nieuwe dataservices wordt niet goedgekeurd voor de aanbieding.** Als u een SaaS-business-toepassing hebt wilt toopublish op AppSource vindt u meer informatie [hier](https://appsource.microsoft.com/partners). Als u beschikt over een IaaS-toepassingen of developer-service dat u zou zoals toopublish op Azure Marketplace vindt u meer informatie [hier](https://azure.microsoft.com/marketplace/programs/certified/).
>
>

Dit document helpt Hallo knooppunt structuur voor het toewijzen van een OData-protocol tooCSDL verduidelijken. Het is belangrijk toonote dat Hallo knooppunt structuur goed is gevormd XML. Basis-, bovenliggende en onderliggende schema kan worden gebruikt bij het ontwerpen van uw OData-toewijzing.

## <a name="ignored-elements"></a>Genegeerd elementen
Hallo volgen Hallo hoog niveau CSDL-elementen (XML-knooppunten) die niet gebruikt door hello Azure Marketplace back-end tijdens het importeren van metagegevens Hallo webservice Hallo toobe gaat. Ze kunnen worden gebruikt, maar worden genegeerd.

| Element | Bereik |
| --- | --- |
| Met behulp van Element |Hallo-knooppunt, subknooppunten en alle kenmerken |
| Documentation-Element |Hallo-knooppunt, subknooppunten en alle kenmerken |
| ComplexType |Hallo-knooppunt, subknooppunten en alle kenmerken |
| Koppelingelement |Hallo-knooppunt, subknooppunten en alle kenmerken |
| Uitgebreide eigenschap |Hallo-knooppunt, subknooppunten en alle kenmerken |
| EntityContainer |Alleen hello volgende kenmerken worden genegeerd: *breidt* en *AssociationSet* |
| Schema |Alleen hello volgende kenmerken worden genegeerd: *Namespace* |
| FunctionImport |Alleen hello volgende kenmerken worden genegeerd: *modus* (de standaardwaarde van RG wordt gebruikt) |
| EntityType |Alleen hello volgende subknooppunten worden genegeerd: *sleutel* en *PropertyRef* |

Hallo hieronder wordt Hallo wijzigingen (toegevoegd en elementen genegeerd) toohello verschillende CSDL-XML-knooppunt in detail beschreven.

## <a name="functionimport-node"></a>FunctionImport knooppunt
Een FunctionImport-knooppunt vertegenwoordigt een URL (toegangspunt) waarmee een service toohello door eindgebruikers. Hallo-knooppunt kan met een beschrijving van hoe Hallo-URL is gericht, welke parameters zijn beschikbaar toohello eindgebruikers en hoe deze parameters worden opgegeven.

Meer informatie over dit knooppunt worden gevonden op [hier][MSDNFunctionImportLink](https://msdn.microsoft.com/library/cc716710.aspx)

Hallo hieronder vindt u aanvullende kenmerken hello (of toevoegingen tooattributes) die beschikbaar worden gesteld door Hallo FunctionImport knooppunt:

**d:BaseUri** -Hallo URI-sjabloon voor Hallo REST-resource die blootgestelde tooMarketplace. Marketplace maakt gebruik van query's tooconstruct van Hallo-sjabloon op Hallo REST-webservice. Hallo URI sjabloon bevat de tijdelijke aanduidingen voor Hallo-parameters in de vorm Hallo van {parameterName}, waarbij parameterName Hallo naam is van Hallo-parameter. Bijvoorbeeld apiVersion = {apiVersion}.
Parameters mogen tooappear als parameters van de URI of als onderdeel van het Hallo-URI-pad. In geval van Hallo uiterlijk in Hallo pad Hallo zijn ze altijd verplicht (kan niet worden gemarkeerd als null-waarden). *Voorbeeld:*`d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**Naam** -naam Hallo Hallo functie geïmporteerd.  Kan niet hetzelfde als andere gedefinieerde namen in Hallo CSDL worden Hallo.  Bijvoorbeeld Naam = 'GetModelUsageFile'

**EntitySet** *(optioneel)* - als Hallo functie een verzameling van Entiteitstypen, Hallo-waarde van Hallo retourneert **EntitySet** moet Hallo entiteit toowhich Hallo verzameling behoort. Anders Hallo **EntitySet** kenmerk mag niet worden gebruikt. *Voorbeeld:*`EntitySet="GetUsageStatisticsEntitySet"`

**ReturnType** *(optioneel)* -Hiermee geeft u Hallo type elementen die zijn geretourneerd door Hallo URI.  Gebruik dit kenmerk niet als Hallo functie geen waarde retourneert. Hallo volgen Hallo ondersteunde typen:

* **Verzameling (<Entity type name>)**: Hiermee geeft u een verzameling van gedefinieerde Entiteitstypen. Hallo-naam is aanwezig in Hallo naamkenmerk van Hallo EntityType knooppunt. Een voorbeeld is een verzameling (WXC. HourlyResult).
* **Onbewerkte (<mime type>)**: Hiermee geeft u een onbewerkte document/blob die toohello gebruiker wordt geretourneerd. Een voorbeeld is Raw(image/jpeg) andere voorbeelden:

  * ReturnType="Raw(text/plain)'
  * ReturnType = "verzameling (sage. DeleteAllUsageFilesEntity) ' *

**d:paging** -geeft aan hoe paginering wordt verwerkt door Hallo REST-resource. parameter waarden worden gebruikt binnen de accolades braches Hello, bijvoorbeeld pagina = {$page} & itemsperpage = {$size} Hallo beschikbare opties zijn:

* **Geen:** geen paginering is beschikbaar
* **Overslaan:** paginering wordt uitgedrukt door middel van een logische 'overslaan' en 'uitvoeren' (boven). Overslaan vroom M-elementen en onderneemt in vervolgens retourneert Hallo volgende N-elementen. Parameterwaarde: $skip
* **Los het:** nemen Hallo volgende N elementen geretourneerd. Parameterwaarde: $take
* **PageSize:** paginering wordt gerealiseerd via een logische pagina en de grootte (items per pagina). Pagina vertegenwoordigt Hallo huidige pagina die wordt geretourneerd. Parameterwaarde: $page
* **Grootte:** grootte van het aantal items geretourneerd voor elke pagina Hallo vertegenwoordigt. Parameterwaarde: $size

**d:AllowedHttpMethods** *(optioneel)* -geeft aan welke term wordt verwerkt door Hallo REST-resource. Ook beperkt geaccepteerde term toohello opgegeven waarde.  Standaardinstelling = POST.  *Voorbeeld:* `d:AllowedHttpMethods="GET"` Hallo beschikbare opties zijn:

* **GET:** tooreturn gegevens meestal wordt gebruikt
* **POST:** tooinsert nieuwe gegevens meestal wordt gebruikt
* **PUT:** tooupdate gegevens meestal wordt gebruikt
* **VERWIJDEREN:** toodelete gegevens gebruikt

Extra onderliggende knooppunten (die niet wordt gedekt door Hallo CSDL documentatie) in Hallo FunctionImport-knooppunt zijn:

**d:RequestBody** *(optioneel)* -Hallo aanvraag hoofdtekst gebruikte tooindicate die Hallo aanvraag is een instantie toobe verzonden verwacht. Parameters kunnen worden opgegeven in de aanvraagtekst Hallo. Ze worden uitgedrukt in de accolades, bijvoorbeeld {parameterName}. Deze parameters worden toegewezen uit Hallo gebruikersinvoer in Hallo-instantie die wordt overgedragen toohello inhoud provider-service. Hallo requestBody element heeft een kenmerk met naam httpMethod. Hallo-kenmerk kunt u twee waarden:

* **POST:** gebruikt als het Hallo-aanvraag is een HTTP POST
* **GET:** gebruikt als het Hallo-aanvraag is een HTTP GET

    Voorbeeld:

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:Namespaces** en **d:Namespace** -beschrijving van dit knooppunt Hallo naamruimten die zijn gedefinieerd in Hallo XML-bestand dat wordt geretourneerd door Hallo functie-import (URI eindpunt). XML-bestand dat wordt geretourneerd door de back-endservice Hallo Hallo bevatten mogelijk een willekeurig aantal naamruimten toodifferentiate Hallo inhoud die wordt geretourneerd. **Alle deze naamruimten als d:Map of d:Match XPath-query's gebruikt, moeten toobe vermeld.** Hallo d:Namespaces knooppunt bevat een setlijst van d:Namespace knooppunten. Elk van deze bevat een naamruimte die wordt gebruikt in het antwoord Hallo back-end-service. Hallo volgen Hallo-kenmerk van Hallo d:Namespace knooppunt:

* **d:prefix:** Hallo voorvoegsel voor naamruimte hello, zoals in Hallo XML-resultaten worden geretourneerd door de service hello, zoals f:FirstName, f:LastName, waarbij f Hallo voorvoegsel is.
* **d:URI:** Hallo volledige URI van Hallo naamruimte in Hallo resultaat document gebruikt. Het Hallo-waarde vertegenwoordigt Hallo voorvoegsel wordt omgezet tooat runtime.

**d:ErrorHandling** *(optioneel)* -dit knooppunt bevat de voorwaarden voor foutafhandeling. Elk van de condities Hallo is gevalideerd met Hallo resultaat dat wordt geretourneerd door Hallo inhoud van de provider-service. Als een voorwaarde overeenkomt met HTTP-foutcode voorgestelde hello wordt een foutbericht toohello eindgebruiker geretourneerd.

**d:ErrorHandling** *(optioneel)* en **d:Condition** *(optioneel)* -een voorwaarde-knooppunt bevat een voorwaarde die is ingeschakeld in Hallo resultaat geretourneerd door Hallo inhoud van de provider-service. Hallo volgen Hallo **vereist** kenmerken:

* **d:match:** een XPath-expressie die wordt gevalideerd of een bepaalde knooppuntwaarde aanwezig in de inhoudsprovider Hallo is XML-uitvoer. Hallo XPath wordt uitgevoerd op Hallo uitvoer en waar als het Hallo-voorwaarde een overeenkomst of ONWAAR anders moet retourneren.
* **d:HttpStatusCode:** HTTP-statuscode die moet worden geretourneerd door Marketplace in overeenkomt met de voorwaarde van de Hallo case Hallo Hallo. Marketplace signalizes fouten toohello gebruiker via HTTP-statuscodes. Een lijst met HTTP-statuscodes zijn beschikbaar op http://en.wikipedia.org/wiki/HTTP_status_code
* **d:errorMessage:** Hallo foutbericht weergegeven dat is geretourneerd: met Hallo HTTP-statuscode: toohello door eindgebruikers. Dit moet een beschrijvende foutbericht die geen geen geheimen bevat zijn.

**d:Title** *(optioneel)* -kunt Hallo titel van de functie Hallo beschrijven. Hallo-waarde voor de titel van de Hallo afkomstig is van

* Hallo optionele map kenmerk (een xpath) die aangeeft waar toofind Hallo titel in het Hallo-antwoord geretourneerd van Hallo serviceaanvraag.
* - Of - Hallo titel is opgegeven als de waarde van Hallo-knooppunt.

**d:Rights** *(optioneel)* -Hallo rechten die zijn gekoppeld aan het Hallo-functie (bijvoorbeeld auteursrecht). Hallo-waarde voor Hallo rechten afkomstig is van:

* Hallo optionele map kenmerk (een xpath) die aangeeft waar toofind Hallo rechten in Hallo antwoord geretourneerd van Hallo serviceaanvraag.
* - Of - Hallo rechten die zijn opgegeven als de waarde van Hallo-knooppunt.

**d:Description** *(optioneel)* : een korte beschrijving voor de Hallo-functie. Hallo-waarde voor de beschrijving van de Hallo afkomstig is van

* Hallo optionele map kenmerk (een xpath) die aangeeft waar toofind Hallo beschrijving in het Hallo-antwoord geretourneerd van Hallo serviceaanvraag.
* - Of – Hallo beschrijving is opgegeven als de waarde van Hallo-knooppunt.

**d:EmitSelfLink** - *bovenstaande voorbeeld 'FunctionImport 'Gewisseld' via geretourneerde gegevens'*

**d:EncodeParameterValue** -optionele uitbreiding tooOData

**d:QueryResourceCost** -optionele uitbreiding tooOData

**d:map** -optionele uitbreiding tooOData

**d:headers** -optionele uitbreiding tooOData

**d:headers** -optionele uitbreiding tooOData

**d:Value** -optionele uitbreiding tooOData

**d:HttpStatusCode** -optionele uitbreiding tooOData

**d:errorMessage** -optionele uitbreiding tooOData

## <a name="parameter-node"></a>De parameterknooppunt
Dit knooppunt vertegenwoordigt een parameter die wordt weergegeven als onderdeel van de URI-sjabloon Hallo / aanvraagtekst die is opgegeven in Hallo FunctionImport knooppunt.

Een documentpagina zeer nuttige informatie over Hallo ' Parameter ' elementknooppunt bevindt zich in [hier](http://msdn.microsoft.com/library/ee473431.aspx) (gebruik Hallo **andere versie** dropdown tooselect een andere versie als de benodigde tooview Hallo documentatie). *Voorbeeld:*`<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| De Parameterkenmerk | Is vereist | Waarde |
| --- | --- | --- |
| Naam |Ja |Hallo-naam van Hallo-parameter. Hoofdlettergevoelig!  Hallo BaseUri geval overeen. **Voorbeeld:**`<Property Name="IsDormant" Type="Byte" />` |
| Type |Ja |Hallo-parametertype. Hallo-waarde moet een **EDMSimpleType** of een complex type die zich binnen het bereik van Hallo model Hallo. Zie '6 ondersteunde Parameter of de eigenschap typen' voor meer informatie.  (Hoofdlettergevoelig! Eerste teken is een hoofdletter, rest kleine letters.)  Zie ook, [conceptuele Model typen (CSDL)][MSDNParameterLink](http://msdn.microsoft.com/library/bb399548.aspx). **Voorbeeld:**`<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Modus |Nee |**In**, Out of InOut, afhankelijk van het feit Hallo-parameter is een invoer, uitvoer of input/output-parameter. (Alleen 'IN' is beschikbaar in Azure Marketplace.) **Voorbeeld:**`<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| maxLength |Nee |Hallo maximaal toegestane lengte van Hallo-parameter. **Voorbeeld:**`<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| precisie |Nee |Hallo precisie van Hallo-parameter. **Voorbeeld:**`<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| Schalen |Nee |Hallo schaal van Hallo-parameter. **Voorbeeld:**`<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

Hallo volgen Hallo kenmerken die toohello CSDL-specificatie zijn toegevoegd:

| De Parameterkenmerk | Beschrijving |
| --- | --- |
| **d:Regex** *(optioneel)* |Een instructie regex gebruikt toovalidate Hallo invoerwaarde voor Hallo-parameter. Als de invoerwaarde Hallo komt niet overeen met de Hallo instructie Hallo waarde geweigerd. Hierdoor kunnen toospecify ook een set van waarden in, bijvoorbeeld ^ [0-9] +? $ tooonly kunt u getallen. **Voorbeeld:** ' < parameternaam = "name" modus = "In" Type = 'Tekenreeks' d: null-waarden bevatten = 'false' d:Regex = ' ^ [a-zA-Z] * $' d:Description = "een naam die kan geen spaties of niet-alfanumerieke niet-Engelse tekens bevatten' d:SampleValues ="George |
| **d:Enum** *(optioneel)* |Een pipe gescheiden lijst met waarden die geldig voor Hallo-parameter. Hallo type Hallo waarden moet toomatch Hallo gedefinieerd type Hallo-parameter. Voorbeeld: ' Engels |
| **d: null-waarden bevatten** *(optioneel)* |Hiermee kunt u definiëren of een parameter kan niet null zijn. Hallo standaardwaarde is: true. Parameters die beschikbaar worden gesteld als onderdeel van het pad in de URI-sjabloon Hallo Hallo kunnen echter niet null. Hallo-kenmerk is ingesteld toofalse voor deze parameters – Hallo gebruikersinvoer onderdrukt. **Voorbeeld:**`<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue** *(optioneel)* |Een voorbeeld waarde toodisplay als een opmerking toohello Client in Hallo gebruikersinterface.  Het is mogelijk verschillende waarden met behulp van een pipe gescheiden tooadd wilt weergeven, dat wil zeggen, een |

## <a name="entitytype-node"></a>EntityType knooppunt
Dit knooppunt vertegenwoordigt een van de Hallo-typen die worden geretourneerd van Marketplace toohello eindgebruiker. Het bevat ook Hallo-toewijzing van Hallo-uitvoer die wordt geretourneerd door Hallo van inhoudsprovider service toohello waarden die worden geretourneerd door eindgebruikers toohello.

Meer informatie over dit knooppunt worden gevonden op [hier](http://msdn.microsoft.com/library/bb399206.aspx) (gebruik Hallo **andere versie** dropdown tooselect een andere versie als de benodigde tooview Hallo documentatie.)

| Naam van kenmerk | Is vereist | Waarde |
| --- | --- | --- |
| Naam |Ja |Hallo-naam van het entiteitstype Hallo. **Voorbeeld:**`<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| BaseType |Nee |Hallo-naam van een andere entiteitstype dat Hallo basistype van entiteitstype Hallo die wordt gedefinieerd. **Voorbeeld:**`<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

Hallo volgen Hallo kenmerken die toohello CSDL-specificatie zijn toegevoegd:

**d:map** -uitgevoerd tegen Hallo service uitvoer van een XPath-expressie. Hallo veronderstelling hier is dat Hallo service uitvoer een set met elementen die, bevat herhalen zoals een ATOM-feed waar er is een set van vermelding knooppunten die worden herhaald. Elk van deze herhalende knooppunten bevat één record. Hallo XPath wordt opgegeven toopoint op Hallo afzonderlijke herhalende knooppunt in het resultaat van Hallo inhoud van de provider-service die Hallo-waarden voor een afzonderlijke record bevat. Voorbeeld van uitvoer van Hallo-service:

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

Hallo XPath-expressie is /foo/bar omdat elk Hallo balk knooppunt hello, herhalende knooppunt in het Hallo-uitvoer en het Hallo werkelijke inhoud bevat die wordt geretourneerd door eindgebruikers toohello.

**Sleutel** -dit kenmerk wordt genegeerd door de Marketplace. REST op basis van webservices, niet beschikbaar in het algemeen een primaire sleutel.

## <a name="property-node"></a>Eigenschapsknooppunt
Dit knooppunt bevat een eigenschap van het Hallo-record.

Meer informatie over dit knooppunt worden gevonden op [http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (gebruik Hallo **andere versie** dropdown tooselect een andere versie als de benodigde tooview Hallo documentatie.) *Voorbeeld:*`<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| AttributeName | Vereist | Waarde |
| --- | --- | --- |
| Naam |Ja |Hallo-naam van Hallo-eigenschap. |
| Type |Ja |Hallo-type van de eigenschapswaarde Hallo. Hallo waarde eigenschapstype moet een **EDMSimpleType** of een complex type (aangeduid door een volledig gekwalificeerde naam) die zich binnen het bereik van Hallo-model. Zie conceptuele Model-typen (CSDL) voor meer informatie. |
| Null-waarden bevatten |Nee |**De waarde True** (standaardwaarde Hallo) of **False** afhankelijk van of Hallo eigenschap een null-waarde kan hebben. Opmerking: In Hallo versie van CSDL aangegeven door Hallo [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm) naamruimte, moet een complex type-eigenschap hebben die null-waarden bevatten = 'False'. |
| Standaardwaarde |Nee |standaardwaarde Hallo van Hallo-eigenschap. |
| maxLength |Nee |Hallo maximale lengte van de eigenschapswaarde Hallo. |
| FixedLength |Nee |**De waarde True** of **False** afhankelijk van of de waarde van de eigenschap Hallo met een tekenreekslengte fiexed wordt opgeslagen. |
| precisie |Nee |Maximum aantal cijfers tooretain in Hallo numerieke waarde toohello verwijst. |
| Schalen |Nee |Maximum aantal decimalen tooretain in Hallo numerieke waarde. |
| Unicode |Nee |**De waarde True** of **False** afhankelijk van of de waarde van de eigenschap Hallo worden opgeslagen als een Unicode-tekenreeks. |
| Sortering |Nee |Een tekenreeks die opgeeft Hallo sequence toobe gebruikt in de gegevensbron Hallo sorteren. |
| ConcurrencyMode |Nee |**Geen** (standaardwaarde Hallo) of **vast**. Als Hallo waarde is te**vast**, eigenschapswaarde hello worden gebruikt voor de optimistische gelijktijdigheid controles. |

Hallo volgen Hallo extra kenmerken die toohello CSDL-specificatie zijn toegevoegd:

**d:map** -XPath-expressie uitgevoerd tegen Hallo service uitvoer en extraheert een eigenschap van het Hallo-uitvoer. Hallo XPath opgegeven is relatieve toohello herhalende knooppunt dat is geselecteerd in XPath Hallo EntityType van het knooppunt. Het is ook mogelijk toospecify een absolute XPath tooallow met inbegrip van een statische resource in elk Hallo knooppunten, zoals bijvoorbeeld copyrightinformatie die alleen wordt gevonden wanneer in Hallo oorspronkelijke service uitvoer maar aanwezig zijn in elk Hallo rijen in Hallo OData moet uitvoer uitvoer. Voorbeeld van Hallo-service:

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

Hier Hallo XPath-expressie zijn ./bar/baz0 tooget hello baz0 knooppunt uit Hallo inhoud provider-service.

**d:CharMaxLength** -voor het type string, kunt u de maximale lengte Hallo opgeven. Zie DataService CSDL-voorbeeld

**d:IsPrimaryKey** -geeft aan of Hallo kolom Hallo primaire sleutel in Hallo tabel of weergave. Zie DataService CSDL-voorbeeld.

**d:isExposed** -bepaalt als Hallo tabelschema is beschikbaar gemaakt (meestal true). Zie DataService CSDL-voorbeeld

**d:IsView** *(optioneel)* : true als dit is gebaseerd op een weergave in plaats van een tabel.  Zie DataService CSDL-voorbeeld

**d:Tableschema** -Zie DataService CSDL-voorbeeld

**d:columnName** -naam is Hallo van Hallo kolom in Hallo tabel of weergave.  Zie DataService CSDL-voorbeeld

**d:IsReturned** -Hallo Booleaanse waarde die bepaalt als Hallo Service stelt deze waarde toohello client beschikbaar Is.  Zie DataService CSDL-voorbeeld

**d:IsQueryable** -Hallo Booleaanse waarde die bepaalt als Hallo kolom kan worden gebruikt in een databasequery Is.   Zie DataService CSDL-voorbeeld

**d:OrdinalPosition** -Hallo van numerieke kolompositie van uiterlijk, x, in Hallo tabel of weergave hello, waarbij x van het aantal kolommen in tabel Hallo 1 toohello staat Is.  Zie DataService CSDL-voorbeeld

**d:DatabaseDataType** -Hallo-gegevenstype van kolom Hallo in Hallo-database, dat wil zeggen SQL-gegevenstype. Zie DataService CSDL-voorbeeld

## <a name="supported-parametersproperty-types"></a>Ondersteunde Parameters of de eigenschap typen
Hallo volgen Hallo ondersteunde typen voor parameters en eigenschappen. (Hoofdlettergevoelig)

| Primitieve typen | Beschrijving |
| --- | --- |
| Null |Hallo afwezigheid van een waarde vertegenwoordigt |
| Booleaanse waarde |Hallo wiskundige concept van logic binaire waarden vertegenwoordigt |
| Byte |Niet-ondertekende 8-bits geheel getal |
| Datum/tijd |Datum en tijd vertegenwoordigt met waarden die variëren van 12:00:00 middernacht, 1 januari 1753 A.D. tot en met 11:59:59 uur, December 9999 A.D. |
| Decimale |Numerieke waarden met vaste precision en scale vertegenwoordigt. Dit type wordt beschreven en een numerieke waarde variërend van het negatieve 10 ^ 255 + 1 toopositive 10 ^ 255 -1 |
| dubbele |Hiermee geeft u een getal met 15 cijfers precisie waarbij waarden met een benadering bereik van + 2.23E-308 via + 1.79E drijvende komma +308. **Gebruik decimale vanwege tooExel export probleem** |
| Één |Hiermee geeft u een getal met 7 cijfers precisie waarbij waarden met een benadering bereik van + 1.18E-38 3.40E + tot en met drijvende komma +38 |
| GUID |Hiermee geeft u een waarde van de unieke id van 16 bytes (128-bits) |
| Int16 |Hiermee geeft u een ondertekende 16-bits geheel getal |
| Int32 |Hiermee geeft u een ondertekende 32-bits geheel getal |
| Int64 |Hiermee geeft u een ondertekende 64-bits geheel getal |
| Tekenreeks |Hiermee geeft u of variabele-tekengegevens met vaste lengte |

## <a name="see-also"></a>Zie ook
* Als u geïnteresseerd bent in kennis Hallo algehele proces voor OData-toewijzing en het doel, Lees dit artikel [gegevens Service OData-toewijzing](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definities, structuren en instructies.
* Als u geïnteresseerd bent in de voorbeelden controleren, Lees dit artikel [gegevens Service OData toewijzing voorbeelden](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee voorbeeldcode en begrijpen codesyntaxis en in het contextmenu.
* tooreturn toohello pad voor het publiceren van een gegevensservice toohello Azure Marketplace Lees dit artikel voorgeschreven [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).
