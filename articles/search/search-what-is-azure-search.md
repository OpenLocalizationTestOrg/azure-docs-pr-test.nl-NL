---
title: aaaWhat is Azure Search | Microsoft Docs
description: Azure Search is een volledig beheerde gehoste cloud search-service. Meer informatie in het Functieoverzicht van deze.
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>Wat is Azure Search?
Azure Search is een search-as-a-service cloudoplossing die biedt ontwikkelaars API's en hulpprogramma's voor het toevoegen van een uitgebreide zoekervaring via uw gegevens in toepassingen met web, mobiel en enterprise.

Functionaliteit is beschikbaar gemaakt via een eenvoudige [REST-API](/rest/api/searchservice/) of [.NET SDK](search-howto-dotnet-sdk.md) die maskeert Hallo inherente complexiteit van de search-technologie. In aanvulling tooAPIs biedt hello Azure-portal van beheer en maken van een prototype-ondersteuning. Infrastructuur en beschikbaarheid worden beheerd door Microsoft.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>Functieoverzicht

| Category | Functies |
|----------|----------|
|Zoekopdracht in volledige tekst en analyse van tekst | [**Zoekopdracht in volledige tekst** ](search-lucene-query-architecture.md) is een primaire gebruiksvoorbeeld voor de meeste zoekopdrachten gebaseerde apps. Query's kunnen worden geformuleerd met een ondersteunde syntaxis: <br/><br/>[**Vereenvoudigde querysyntaxis**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search), die logische operators, Zoekoperators woordgroep, achtervoegsel operators, voorrang operators biedt.<br/><br/>[**Lucene-querysyntaxis** ](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) biedt alle eenvoudige ondersteuning, plus fuzzy zoeken, zoeken bij benadering, zoekterm prestatieverbetering en reguliere expressies.| 
| Gegevensintegratie | Azure Search-index accepteren gegevens uit een bron, mits dit als een JSON-gegevensstructuur is ingediend. <br/><br/> U kunt desgewenst voor ondersteunde gegevensbronnen in Azure, kunt u [ **indexeerfuncties** ](search-indexer-overview.md) tooautomatically verkenning [Azure SQL Database](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [Azure Cosmos DB](search-howto-index-documentdb.md), of [Azure Blob storage](search-howto-indexing-azure-blob-storage.md) toosync uw search-index de inhoud van met uw primaire gegevensopslag. Azure Blob-Indexeerfuncties kunnen uitvoeren *document kraken* voor [belangrijke bestandsindelingen indexeren](search-howto-indexing-azure-blob-storage.md), met inbegrip van Microsoft Office-, PDF- en HTML-documenten. |
| Analytics zoeken | [**Aangepaste lexicale analyzers** ](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) beschikbaar zijn voor complexe zoekopdrachten met fonetische overeenkomende en reguliere expressies. |
| Taalondersteuning | [**Taalanalyse** ](https://docs.microsoft.com/rest/api/searchservice/language-support) van Lucene, evenals Microsoft de processors van natuurlijke taal beschikbaar in verschillende talen 56 toointelligently ingang taalspecifieke linguistics zoals werkwoordsvormen, geslacht, onregelmatige meervoud de volgende zelfstandige naamwoorden (bijvoorbeeld ' muis' versus 'muizen'), word ongedaan wordt samengesteld, woordafbreking (voor talen zonder spaties), en meer. |
| Geo-zoeken | Azure zoekactie op intelligente wijze worden verwerkt, filters en geografische locaties. Gebruikers kunnen met behulp tooexplore gegevens gebaseerd op Hallo nabijheid van een zoekopdracht resultaat tooa fysieke locatie. [Bekijk deze video](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) of [controleren van dit voorbeeld](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) toolearn meer. |
| Functies voor de ervaring | [**Zoeksuggesties** ](https://docs.microsoft.com/rest/api/searchservice/suggesters) kan worden ingeschakeld voor automatisch aangevulde query's in een zoekbalk. Werkelijke documenten in uw index worden voorgesteld als gebruikers deelzoekopdrachten invoer invoeren. <br/><br/>[**Meervoudige navigatie** ](https://docs.microsoft.com/azure/search/search-faceted-navigation) wordt ingeschakeld via een enkele queryparameter. Azure Search retourneert een meervoudige navigatie-structuur die u als Hallo code achter een categorieënlijst voor te filteren (bijvoorbeeld toofilter catalogusitems door prijs bereik of merk gebruiken kunt). <br/><br/> [**Filters** ](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) gebruikte tooincorporate meervoudige navigatie in de gebruikersinterface van uw toepassing kan worden, query formulering verbeteren en filter op basis van gebruiker of ontwikkelaar opgegeven criteria. Maak filters met Hallo OData-syntaxis.<br/><br/> [**Markeren** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) van toepassing is visual formulier atting tooa die overeenkomt met het sleutelwoord in de zoekresultaten. U kunt kiezen welke velden gemarkeerde codefragmenten retourneren.<br/><br/>[**Sorteren** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) wordt aangeboden voor meerdere velden via Hallo Indexeer schema en vervolgens tijdens de query met een enkele zoekparameter is uitgeschakeld.<br/><br/> [**Wisselgeheugengebruik** ](search-pagination-page-layout.md) en uw zoekresultaten beperking is eenvoudig met Hallo afgestemd-besturingselement dat Azure Search dan de zoekresultaten biedt.  
| Relevantie | [**Score berekenen voor eenvoudige** ](/rest/api/searchservice/add-scoring-profiles-to-a-search-index) is een belangrijk voordeel van Azure Search. Scoreprofiel profielen zijn gebruikte toomodel relevantie als een functie van waarden in Hallo zelf documenten. Bijvoorbeeld wellicht nieuwere producten of producten tooappear hoger in de zoekresultaten Hallo met korting. U kunt ook scoreprofiel profielen met de labels voor persoonlijke score berekenen op basis van de klant Zoekvoorkeuren u hebt gevolgd en opgeslagen afzonderlijk maken. |
| Controle en rapportage | [**Zoek traffic analytics** ](search-traffic-analytics.md) worden verzameld en geanalyseerd toounlock inzicht in wat gebruikers in het zoekvak Hallo typt. <br/><br/>Metrische gegevens over query's per seconde, latentie en beperking worden vastgelegd en worden gerapporteerd in de portal-pagina's zonder aanvullende configuratie vereist. U kunt ook eenvoudig monitor index en document telt zodat u capaciteit naar wens kunt aanpassen. Zie voor meer informatie [Service-beheer](search-manage.md) |
| Hulpprogramma's voor het maken van een prototype en controle | In het Hallo-portal, kunt u Hallo [ **wizard gegevens importeren** ](search-import-data-portal.md) tooconfigure indexeerfuncties, index-designer toostand van een index en [ **Search explorer** ](search-explorer.md) tootest bevraagt en scoreprofiel profielen verfijnen. U kunt een index tooview ook het schema is openen. |
| Infrastructuur | Hallo **maximaal beschikbare platform** zorgt ervoor dat een zeer betrouwbare service zoekfunctie. Wanneer geschaald naar behoren [Azure Search biedt een SLA met 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).<br/><br/> **Volledig beheerde en schaalbare** als een end-to-end-oplossing vereist Azure Search helemaal geen infrastructuurbeheer. Uw service kan worden aangepast tooyour behoeften schaling in twee dimensies toohandle meer documentopslag, hogere querybelasting of beide.

## <a name="how-it-works"></a>Hoe werkt het?
### <a name="step-1-provision-service"></a>Stap 1: Inrichting service
U kunt draaien van een Azure Search-service in Hallo [Azure-portal](https://portal.azure.com/) of via Hallo [Azure Resource Management-API](/rest/api/searchmanagement/). U kunt beide Hallo gratis service gedeeld met andere abonnees, of een [betaald laag](https://azure.microsoft.com/pricing/details/search/) die dedicates bronnen alleen gebruikt door uw service. Voor betaalde lagen, kunt u een service in twee dimensies schalen: 

- Toevoegen van replica's toogrow die uw capaciteit toohandle zware query wordt geladen.   
- Partities toogrow opslag voor meer documenten toevoegen. 

Door de opslag- en doorvoer document afzonderlijk verwerkt, kunt u kalibreren resourcing op basis van behoeften voor productie.

### <a name="step-2-create-index"></a>Stap 2: De index maken
Voordat u inhoud uploaden kunt, moet u eerst een Azure Search-index definiëren. Een index is vergelijkbaar met een databasetabel die uw gegevens bevat en zoekquery's kan accepteren. U definieert Hallo index schema toomap tooreflect Hallo structuur van Hallo documenten die u wenst toosearch, vergelijkbare toofields in een database.

Een schema kan worden gemaakt in hello Azure portal of programmatisch met Hallo [.NET SDK](search-howto-dotnet-sdk.md) of [REST-API](/rest/api/searchservice/).

### <a name="step-3-index-data"></a>Stap 3: Indexgegevens
Wanneer u een index definiëren, bent u klaar tooupload inhoud. U kunt een push of pull model gebruiken.

Hallo pull-model haalt gegevens uit externe gegevensbronnen. Het wordt ondersteund door *indexeerfuncties* die stroomlijnen en automatiseren aspecten van gegevensopname zoals verbinding maken met, lezen en gegevens serialiseren. [Indexeerfuncties](/rest/api/searchservice/Indexer-operations) beschikbaar zijn voor Azure Cosmos DB, Azure SQL Database, Azure Blob Storage en SQL Server die wordt gehost in een Azure VM. U kunt een indexeerfunctie voor configureren op de vraag of de geplande gegevensvernieuwing.

Hallo pushmodel is beschikbaar via Hallo SDK of REST API's gebruikt voor het verzenden van bijgewerkte documenten tooan index. U kunt gegevens pushen vanaf vrijwel elke gegevensset Hallo JSON-indeling. Zie [toevoegen, bijwerken of verwijderen en documenten](/rest/api/searchservice/addupdate-or-delete-documents) of [hoe toouse .NET SDK Hallo)](search-howto-dotnet-sdk.md) voor hulp bij het laden van gegevens.

### <a name="step-4-search"></a>Stap 4: zoeken
Na een index te vullen, kunt u [zoekquery's uitgeven](/rest/api/searchservice/Search-Documents) tooyour service-eindpunt met eenvoudige HTTP-aanvragen met de REST-API of Hallo .NET SDK.

## <a name="how-it-compares"></a>Vergelijking

Klanten vaak vragen hoe [zoeken in volledige tekst in Azure Search](search-lucene-query-architecture.md) worden vergeleken met [zoeken in volledige tekst](https://en.wikipedia.org/wiki/Full_text_search) in hun databaseproduct. Onze antwoord is dat Azure Search taal mogelijkheden uitgebreidere en flexibeler, met ondersteuning voor Lucene-query's, taalanalyse van Lucene en Microsoft, aangepaste analyzers voor fonetische of andere speciale invoer en Hallo mogelijkheid toomerge gegevens uit meerdere bronnen in Hallo search-index. 

Een ander infecties punt is dat een zoekoplossing Hallo gehele zoekervaring adressen. Bijvoorbeeld, wilt u mogelijk aangepaste scoren van resultaten, facetnavigatie voor te filteren, treffers markeringen en typeahead Querysuggesties. 

Hulpprogramma's voor controle en kennis van de queryactiviteit kunnen ook rekening te houden in een oplossing zoeken beslissing. Azure Search ondersteunt bijvoorbeeld [zoeken traffic analytics](search-traffic-analytics.md) van metrische gegevens op clickthrough tarief boven wordt gezocht, zoeken zonder te klikken, enzovoort. Producten waar search een invoegtoepassing is, bent u waarschijnlijk niet toofind deze functies.

Resourcegebruik is een andere overweging. Zoeken in natuurlijke taal is vaak rekenkracht. Enkele van onze klanten offloaded zoeken operations tooAzure zoeken als een manier toopreserve machine resources voor de transactieverwerking. U kunt eenvoudig scale toomatch query volume door externalizing zoekopdracht aanpassen.

Zodra u hebt besloten toogo met speciale search, is uw volgende beslissing tussen een service in de cloud of een on-premises server. Een cloudservice is de juiste keuze Hallo als u wilt een [directe oplossing met minimale overhead en onderhoud en aanpasbare schaal](#cloud-service-advantage).

Binnen Hallo cloud veiligheid bieden verschillende providers vergelijkbare basislijn-functies met zoeken in volledige tekst, geo-search en Hallo mogelijkheid toohandle een bepaalde mate van dubbelzinnigheid in invoer zoeken. Normaal gesproken heeft een [gespecialiseerde functie](#feature-drilldown), of Hallo eenvoudig en algemene eenvoud van API's, hulpprogramma's en beheer waarmee wordt bepaald Hallo zodat deze optimaal passen.

Tussen cloudproviders is de Azure Search sterkste voor volledige tekst zoeken werkbelastingen via inhoud archieven en databases op Azure, voor apps die afhankelijk voornamelijk van zoeken naar ophalen van gegevens en inhoud navigatie zijn. Belangrijkste voordelen zijn:

+ Azure gegevensintegratie (crawlers) op Hallo indexering laag
+ Azure-portal voor Centraal beheer
+ Azure schaal, betrouwbaarheid en beschikbaarheid van hoogwaardige
+ Taalkundige en aangepaste analyse, met analyzers voor zoekopdrachten in volledige tekst effen in 56 talen
+ [Core functies veelgebruikte toosearch gericht apps](#feature-drilldown): score berekenen, facetten, suggesties, synoniemen, geo-search en meer.

> [!Note]
> toobe wissen, niet-Azure-gegevensbronnen worden volledig ondersteund, maar afhankelijk zijn van een meer code-intensieve push-methode in plaats van indexeerfuncties. Onze API's kunt u een JSON-document verzameling tooan Azure Search-index doorsluizen.

Tussen onze klanten zijn die kunnen tooleverage Hallo groot aantal functies in Azure Search online catalogussen line-of-business-programma's en toepassingen voor detectie van documenten.

## <a name="rest-api--net-sdk"></a>REST-API | .net SDK

Hoewel veel taken kunnen worden uitgevoerd in de portal hello, Azure Search bedoeld is voor ontwikkelaars willen toointegrate functionaliteit voor het zoeken naar bestaande toepassingen. Hallo volgende API's zijn beschikbaar.

|Platform |Beschrijving |
|-----|------------|
|[REST](/rest/api/searchservice/) | HTTP-opdrachten die door alle programming platform en taal, met inbegrip van Xamarin, Java en JavaScript ondersteund|
|[.NET SDK](search-howto-dotnet-sdk.md) | .NET-wrapper voor Hallo REST-API biedt een efficiënte coderen in C# en andere talen voor beheerde code die gericht is op Hallo .NET Framework |

## <a name="free-trial"></a>Gratis proefversie
Azure-abonnees kunnen [inrichten van een service in de gratis laag Hallo](search-create-service-portal.md).

Als u niet een abonnee, kunt u [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). U ontvangt tegoed voor het uitproberen van betaalde Azure-services. Nadat ze zijn gebruikt, kunt u Hallo account houden en gebruiken [gratis Azure-services](https://azure.microsoft.com/free/). Uw creditcard is nooit in rekening gebracht tenzij u expliciet de instellingen wijzigen en vraag toobe in rekening gebracht.

U kunt ook [voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): uw MSDN-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken. 

## <a name="how-tooget-started"></a>Hoe tooget gestart

1. Maken van een service in Hallo [gratis laag](search-create-service-portal.md).

2. Een of meer van de volgende zelfstudies Hallo doorlopen. 

  + [Hoe toouse .NET SDK Hallo](search-howto-dotnet-sdk.md) demonstreert Hallo belangrijkste stappen in beheerde code.  
  + [Aan de slag met Hallo REST-API](https://github.com/Azure-Samples/search-rest-api-getting-started) toont Hallo dezelfde stappen met Hallo REST-API.  
  + [Maken van uw eerste index in Hallo portal](search-get-started-portal.md) ziet u de ingebouwde indexeren en prototype functies Hallo-portal.   

Zoekmachines zijn de stuurprogramma's voor Hallo algemene ophalen van informatie in mobiele apps, op Hallo web en in bedrijf gegevensarchieven. Azure Search biedt u hulpprogramma's voor het maken van een zoekopdracht ervaring vergelijkbare toothose op grote commerciële websites.

In deze 9 minuten durende video van programmamanager Liam Cavanagh meer informatie over hoe het integreren van een zoekmachine uw app kunt profiteren. Korte demonstraties betrekking hebben op belangrijke functies in Azure Search en hoe een gangbare werkstroom eruit ziet. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ 0-3 minuten dekt belangrijke functies en use cases.
+ 3 en 4 minuten bevat informatie over het inrichten van de service. 
+ 4-6 minuten omvat gegevens importeren wizard gebruikt toocreate een index met behulp van Hallo ingebouwde vastgoed gegevensset.
+ 6-9 minuten behandelt Search Explorer en verschillende query's.


