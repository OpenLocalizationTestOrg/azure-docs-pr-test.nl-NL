---
title: aaaAzure zoeken aandachtspunten voor prestaties en optimalisatie | Microsoft Docs
description: Azure Search-prestaties afstemmen en optimale schaal configureren
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a>Azure Search-overwegingen voor prestaties en optimalisatie
Een goede zoekfunctie is een belangrijke toosuccess voor veel mobiele telefoons en webtoepassingen. Van vastgoed, tooused auto marktplaatsen tooonline catalogussen, snel zoeken en relevante resultaten heeft invloed op Hallo klantervaring. Dit document is bedoeld toohelp u aanbevolen procedures voor hoe tooget Hallo optimaal gebruik van Azure Search, met name voor geavanceerde scenario's met vereisten voor schaalbaarheid, ondersteuning van meerdere talen of aangepaste ranking geavanceerde detecteren.  Bovendien dit document bevat een overzicht van interne werking en bevat informatie over methoden die effectief in echte klant apps werken.

## <a name="performance-and-scale-tuning-for-search-services"></a>Prestaties en schaal afstemming voor Search-services
We zijn alle gebruikte toosearch engines zoals Bing en Google en Hallo hoge prestaties bieden.  Wanneer klanten uw zoekopdracht ingeschakeld web of mobiele toepassing gebruikt, wordt ze als gevolg hiervan vergelijkbare prestatiekenmerken verwachten.  Wanneer optimaliseren voor zoekprestaties, is een van de aanbevolen methoden Hallo toofocus op latentie, namelijk Hallo duurt voordat een query toocomplete en retourneren de resultaten.  Wanneer voor de zoekopdracht latentie is het belangrijk om te optimaliseren:

1. Kies een doellatentie (of de maximale hoeveelheid tijd) die een typische zoekaanvraag toocomplete moet uitvoeren.
2. Maken en testen van een echte werkbelasting op basis van uw search-service met een realistische gegevensset toomeasure deze snelheden latentie.
3. Beginnen met een klein aantal query's per seconde (QPS) en doorgaan tooincrease Hallo nummer in Hallo test uitgevoerd totdat Hallo query latentie zakt onder Hallo doellatentie gedefinieerd.  Dit is een belangrijk benchmark toohelp die u van plan voor schaal bent wanneer uw toepassing in gebruik groeit.
4. Waar mogelijk opnieuw gebruiken de HTTP-verbindingen.  Als u van hello Azure Search .NET SDK gebruikmaakt, betekent dit dat u opnieuw een exemplaar moet worden gebruikt of [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) instantie en als u Hallo REST-API, moet u een enkele HttpClient hergebruiken.

Tijdens het maken van deze test werkbelastingen, er zijn enkele kenmerken van Azure Search tookeep rekening:

1. Het is mogelijk toopush zoveel zoeken query in één keer, dat Hallo beschikbare resources in uw Azure Search-service zal worden overbelast.  Als dit gebeurt, ziet u HTTP 503-responscodes.  Daarom is aanbevolen toostart met verschillende bereiken van de search-aanvragen toosee Hallo verschillen in latentie tarieven omdat het toevoegen van meer search-aanvragen.
2. Uploaden van inhoud tooAzure zoeken is van invloed op prestaties Hallo en latentie van hello Azure Search-service.  Als u verwacht toosend gegevens dat terwijl gebruikers zoekopdrachten uitvoert, is het belangrijk tootake deze werkbelasting-account in uw tests uit.
3. Niet elke zoekopdracht wordt uitgevoerd op Hallo dezelfde prestatieniveaus.  Bijvoorbeeld, voert een document lookup- of suggestie doorgaans sneller dan een query met een groot aantal facetten en filters.  Het is aanbevolen tootake Hallo verschillende query's die u verwacht dat toosee in account bij het bouwen van uw tests uit.  
4. Variant van de search-aanvragen is belangrijk als u voortdurend Hallo uitvoert dezelfde aanvragen zoeken, in cache opslaan van gegevens, start toomake prestaties ziet er beter dan deze mogelijk met een meer uiteenlopende query ingesteld.

> [!NOTE]
> [Visual Studio Load testen](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) is een goede manier tooperform uw benchmark test omdat u tooexecute HTTP-aanvragen als nodig zou zijn voor het uitvoeren van een query uitgevoerd naar Azure Search en Hiermee garandeert van aanvragen.
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a>Azure Search voor hoge query tarieven schalen en beperkt aanvragen
Wanneer u te veel aanvragen voor beperkte ontvangt of groter zijn dan de tarieven van de latentie doel van een toegenomen querybelasting, kunt u toodecrease latentie tarieven raadplegen op twee manieren:

1. **Replica's vergroten:** een replica is vergelijkbaar met een kopie van uw gegevens meerdere exemplaren van Azure Search tooload saldo aanvragen tegen Hallo toestaan.  Alle load balancing en replicatie van gegevens over de replica's wordt beheerd door de Azure Search en kunt u Hallo aantal replica's die zijn toegewezen voor uw service op elk gewenst moment wijzigen.  U kunt toewijzen van too12 replica's in een standaard-zoekservice en 3 replica's in een Basic search-service. Replica's kunnen worden aangepast vanaf Hallo [Azure-portal](search-create-service-portal.md) of [PowerShell](search-manage-powershell.md).
2. **Toename zoeken laag:** Azure Search wordt geleverd een [aantal lagen](https://azure.microsoft.com/pricing/details/search/) en elk van deze lagen biedt verschillende niveaus van prestaties.  In sommige gevallen mogelijk hebt u zo veel query's die Hallo laag op tarieven voldoende lage latentie, niet opgeven, zelfs wanneer de replica's volledig worden benut uit.  In dit geval kunt u gebruik van een hogere zoeken lagen zoals hello Azure Search S3 laag die is geschikt voor scenario's met een groot aantal documenten en zeer hoge query werkbelastingen Hallo tooconsider.

## <a name="scaling-azure-search-for-slow-individual-queries"></a>Schalen van Azure Search voor langzame afzonderlijke query 's
Er is een andere reden waarom latentie tarieven kunnen traag zijn van één query toocomplete te lang duurt.  In dit geval wordt verbeterd het toevoegen van replica's niet latentie tarieven.  Voor deze aanvraag zijn twee opties beschikbaar:

1. **Partities verhogen** een partitie is een mechanisme voor het splitsen van uw gegevens over extra bronnen.  Om deze reden dat wanneer u een tweede partitie toevoegen uw gegevens opgehaald opgesplitst in twee.  Een derde partitie splitst uw index in drie, enzovoort.  Dit heeft ook Hallo effect dat in sommige gevallen trage query's wordt sneller vanwege toohello garandeert van de berekening.  Er zijn enkele voorbeelden van wanneer we dit garandeert extreem met query's met lage selectiviteit query's werken hebben gezien.  Dit proces bestaat uit de query's die overeenkomen met veel documenten of wanneer facetten moet tooprovide telt via een groot aantal documenten.  Omdat er dat veel van de berekening tooscore Hallo relevantie Hallo documenten of toocount Hallo cijfers documenten, toe te voegen extra partities kunt tooprovide aanvullende berekeningen nodig.  
   
   Er zijn mag maximaal 12 partities in de standaard-zoekservice en 1 partitie in Hallo basic search-service.  Partities kunnen worden aangepast vanaf Hallo [Azure-portal](search-create-service-portal.md) of [PowerShell](search-manage-powershell.md).
2. **Limiet hoge kardinaliteit velden:** een veld van hoge kardinaliteit bestaat uit een geschikt voor facetten of Filterbaar veld dat een groot aantal unieke waarden heeft, en hierdoor neemt veel bronnen toocompute resultaten op.   Bijvoorbeeld, zouden instellen van een Product-ID of beschrijving veld als geschikt voor facetten/Filterbaar voor hoge kardinaliteit omdat de meeste Hallo-waarden uit het document toodocument uniek zijn. Waar mogelijk het aantal velden van hoge kardinaliteit Hallo beperken.
3. **Toename zoeken laag:** omhoog tooa hogere verplaatst Azure Search-laag kan een andere manier tooimprove-prestaties van trage query's zijn.  Elke laag hoger biedt ook snellere processor en meer geheugen die een positieve invloed op prestaties van query's hebben kan.

## <a name="scaling-for-availability"></a>Schaal van beschikbaarheid
Replica's niet alleen te reduceren latentie van query maar kunnen ook de mogelijkheid voor hoge beschikbaarheid.  Met een enkele replica verwachte periodieke uitvaltijd vanwege tooserver opnieuw wordt opgestart nadat de software-updates of voor andere onderhoud gebeurtenissen die zich voordoen.  Als gevolg hiervan, is het belangrijk tooconsider als uw toepassing vereist een hoge beschikbaarheid van zoekopdrachten (query's) en schrijfbewerkingen (indexering gebeurtenissen).  Azure Search biedt SLA-opties op alle Hallo de offerings betaald zoeken Hello volgende kenmerken:

* 2 replica's voor hoge beschikbaarheid van alleen-lezen werkbelastingen (query's)
* 3 of meer replica's voor hoge beschikbaarheid van alleen-lezen-werkbelastingen (query's en indexeren)

Bezoek voor meer informatie over dit Hallo [Azure Search Service Level Agreement](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

Omdat replica's zijn kopieën van uw gegevens, met meerdere replica's kunnen Azure Search toodo computer is opgestart en onderhoud op basis van een replica op een tijdstip terwijl de handtekeningsleutels toocontinue toobe uitgevoerd met een query Hallo andere replica's.  Daarom moet u ook tooconsider hoe Hallo-query's die u nu toobe uitgevoerd met één exemplaar van Hallo gegevens minder hebt mogelijk van invloed op deze uitvaltijd.

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a>Geografisch verspreide werkbelastingen schalen en geografische redundantie bieden
Voor geografisch verspreide werkbelastingen, zult u merken dat gebruikers zich verre Hallo Datacenter waar uw Azure Search-service wordt gehost hogere latentie tarieven hebben.  Daarom is het vaak belangrijk toohave zoeken op meerdere services in regio's die in dichter nabijheid toothese gebruikers.  Azure Search biedt momenteel geen een automatische methode van Azure Search-index geo-replicatie tussen regio's, maar er zijn bepaalde technieken die kunnen worden gebruikt die u kunnen dit proces eenvoudige tooimplement maken en beheren. Deze worden beschreven in Hallo volgende secties.

Hallo doel van een set geografisch verspreide zoekservices is toohave twee of meer indexen die beschikbaar zijn in twee of meer regio's waar een gebruiker worden gerouteerd toohello Azure Search-service biedt de laagste latentie Hallo gezien in dit voorbeeld:

   ![Cross-tabblad van services per regio][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a>Gegevens synchroon te houden op meerdere Azure Search-services
Er zijn twee opties voor het bewaren van uw gedistribueerde zoekservices synchroon die bestaan uit een met behulp van Hallo [Azure Search-indexeerfunctie](search-indexer-overview.md) of Hallo Push-API (ook wel aangeduid tooas hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/)).  

### <a name="azure-search-indexers"></a>Indexeerfuncties in Azure Search
Als u van Azure Search-indexeerfunctie hello gebruikmaakt, importeert u al gegevenswijzigingen van een centrale datastore zoals Azure SQL DB- of Azure Cosmos DB. Wanneer u een nieuwe zoekopdracht Service, maakt u gewoon een nieuwe Azure Search-indexeerfunctie voor de service ook maken die punten toothis hetzelfde gegevensarchief. Op die manier wanneer nieuwe wijzigingen in het gegevensarchief hello, komen ze vervolgens worden geïndexeerd door Hallo verschillende indexeerfuncties.  

Hier volgt een voorbeeld van hoe die architectuur eruit zou.

   ![Één gegevensbron met gedistribueerde indexeerfunctie en combinaties van service][2]

### <a name="push-api"></a>Push-API
Als u Hallo u Azure Search Push-API te[bijwerken van inhoud in uw Azure Search-index](https://docs.microsoft.com/rest/api/searchservice/update-index), kunt u de verschillende zoekservices synchroon door te pushen wijzigingen tooall search-services wanneer een update vereist is.  Wanneer dit te doen is het belangrijk toomake ervoor toohandle gevallen waarbij een update tooone search-service mislukt en een of meer updates is mislukt.

## <a name="leveraging-azure-traffic-manager"></a>Gebruik van Azure Traffic Manager
[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) kunt u tooroute aanvragen toomultiple geo zich websites die vervolgens worden ondersteund door meerdere Azure Search-Services.  Een voordeel van Hallo Traffic Manager is het kan probe Azure Search tooensure dat deze beschikbaar is en gebruikers tooalternate search-services in de gebeurtenis Hallo uitvaltijd te routeren.  Bovendien, als u de search-aanvragen via de Azure-websites worden routering, kunt Azure Traffic Manager u tooload saldo gevallen waarbij Hallo Website actief is, maar geen Azure Search.  Hier volgt een voorbeeld van welke architectuur Hallo die gebruikmaakt van Traffic Manager.

   ![Cross-tabblad van services per regio, met centrale Traffic Manager][3]

## <a name="monitoring-performance"></a>Prestaties bewaken
Azure Search biedt Hallo mogelijkheid tooanalyze en Hallo de prestaties controleren van de service via [Search Traffic Analytics (STA)](search-traffic-analytics.md). Via STA zijn, kunt u eventueel Hallo afzonderlijke zoekopdrachten, evenals een samengevoegde metrische gegevens tooan Azure Storage-account die vervolgens kan worden verwerkt voor analyse of weergegeven in Power BI registreren.  STA metrische gegevens kunt u prestatiestatistieken zoals gemiddelde aantal query's of reactietijden van de query bekijken.  Bovendien kunt Hallo bewerking logboekregistratie u toodrill op gegevens van specifieke zoekopdrachten.

STA is een waardevol hulpmiddel toounderstand latentie tarieven vanuit het perspectief van die Azure Search.  Aangezien maatstaven voor prestaties van Hallo query geregistreerd zijn gebaseerd op Hallo tijd een query doet toobe volledig verwerkt in Azure Search (van Hallo tijd van het aangevraagde toowhen wordt verstuurd is), bent u toouse kunnen deze toodetermine als latentieproblemen afkomstig uit hello Azure Search-service zijn zijde of buiten Hallo service, bijvoorbeeld wanneer wordt netwerklatentie.  

## <a name="next-steps"></a>Volgende stappen
Zie toolearn meer informatie over de prijzen van lagen en limieten voor services voor elk adres Hallo [Servicelimieten in Azure Search](search-limits-quotas-capacity.md).

Ga naar [capaciteitsplanning](search-capacity-planning.md) toolearn meer over combinaties van partitie en replica.

Bekijk voor meer analyse van prestaties en sommige demonstraties van hoe tooimplement optimalisaties Hallo in dit artikel besproken toosee Hallo video te volgen:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png
