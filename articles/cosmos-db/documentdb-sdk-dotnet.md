---
title: aaaAzure bronnen & Cosmos DB .NET SDK | Microsoft Docs
description: Meer informatie over Hallo .NET API en SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van hello Azure Cosmos DB .NET SDK.
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>Azure Cosmos DB .NET SDK: Downloaden en release-opmerkingen
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [.NET-Feed van wijzigen](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [REST-resourceprovider](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**SDK downloaden**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**API-documentatie**</td><td>[.NET API-naslagdocumentatie](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Voorbeelden**</td><td>[.NET-codevoorbeelden](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Aan de slag**</td><td>[Aan de slag met hello Azure Cosmos DB .NET SDK](documentdb-get-started.md)</td></tr>

<tr><td>**Zelfstudie voor web-app**</td><td>[Ontwikkeling van webtoepassing met Azure Cosmos-DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Huidige ondersteunde framework**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Releaseopmerkingen

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* Ondersteuning toegevoegd voor PartitionKeyRangeId als een FeedOption voor het vaststellen van de query resultaten tooa specifieke sleutel partitiebereikwaarde. 
* Ondersteuning toegevoegd voor StartTime als een ChangeFeedOption toostart Hallo wijzigingen zoekt na dit tijdstip.

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Een probleem opgelost in Hallo JsonSerializable-klasse die een stackoverloopuitzondering kan veroorzaken.

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   Een probleem opgelost die van toepassing hello vanwege toohello introductie van JsonSerializerSettings als een optionele parameter in Hallo DocumentClient constructor compileren vereist.
* Gemarkeerde Hallo DocumentClient constructor verouderd die JsonSerializerSettings vereist als de laatste parameter tooallow voor standaardwaarden van parameters ConnectionPolicy en ConsistencyLevel Hallo als in de parameter JsonSerializerSettings wordt doorgegeven.

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   Toegevoegde ondersteuning voor het opgeven van aangepaste JsonSerializerSettings tijdens het instantiëren van [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   Een probleem dat van invloed op een x64 vaste machines die geen ondersteuning voor SSE4 instructie en genereert een SEHException bij het uitvoeren van query's Azure Cosmos DB DocumentDB API.

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   Ondersteuning toegevoegd voor een nieuwe consistentieniveau ConsistentPrefix genoemd.
*   Ondersteuning toegevoegd voor query metrische gegevens voor afzonderlijke partities.
*   Ondersteuning toegevoegd voor het beperken van de grootte van de Hallo van Hallo vervolgtoken voor query's.
*   Ondersteuning toegevoegd voor meer gedetailleerde tracering van mislukte aanvragen.
*   Een aantal verbeteringen aangebracht in Hallo SDK.

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* Functioneel hetzelfde als 1.13.3. Interne wijzigingen aangebracht.

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* Functioneel hetzelfde als 1.13.2. Interne wijzigingen aangebracht.

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* Een probleem dat genegeerd Hallo PartitionKey waarde die is opgegeven in FeedOptions voor cumulatieve query's opgelost.
* Een probleem opgelost in transparante verwerking van de partitie management tijdens de vlucht halverwege cross-partitie Order By queryuitvoering.

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Een probleem waardoor impassen in een aantal asynchrone Hallo API's bij gebruik binnen de context van ASP.NET opgelost.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* Toomake SDK corrigeert meer robuuste tooautomatic failover onder bepaalde omstandigheden.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* Herstel voor een probleem dat soms een WebException veroorzaakt: Hallo externe naam kan niet worden omgezet.
* Hallo toegevoegde ondersteuning voor het rechtstreeks lezen van een getypt document door nieuwe overloads tooReadDocumentAsync API toe te voegen.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* Toegevoegde ondersteuning voor LINQ voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem).
* Herstel voor een probleem geheugen-geheugenlek voor Hallo ConnectionPolicy object veroorzaakt door Hallo gebruik van gebeurtenis-handler.
* Herstel voor een probleem waarbij de UpsertAttachmentAsync niet werkt is wanneer ETag is gebruikt.
* Herstel voor een probleem waarin cross partitie volgorde door de voortzetting van de query niet werken is bij het sorteren van tekenreeksveld.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Ondersteuning toegevoegd voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem). Zie [aggregatie ondersteuning](documentdb-sql-query.md#Aggregates).
* Minimaal doorvoer voor gepartitioneerde verzamelingen uit 10,100 RU/s too2500 RU/s verlaagd.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* Herstel voor een probleem waarin Hallo cross-partitie zoekopdrachten in Hallo host 32-bits proces zijn mislukt.
* Herstel voor een probleem waarin Hallo sessie container niet met Hallo token voor mislukte aanvragen in de modus van de Gateway bijgewerkt is.
* Herstel voor een probleem waarbij een query met UDF-aanroepen in de projectie in sommige gevallen is mislukt.
* Client side prestaties oplossingen voor het verhogen van Hallo lezen en schrijven van doorvoer van Hallo aanvragen.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* Oplossing voor een probleem waarin Hallo sessie container is niet bijgewerkt met Hallo token voor mislukte aanvragen.
* Ondersteuning toegevoegd voor Hallo SDK toowork in een 32-bits host-proces. Houd er rekening mee dat als u over verschillende partitie query's gebruikt, 64-bits host verwerken wordt aanbevolen voor betere prestaties.
* Verbeterde prestaties voor scenario's met betrekking tot query's met een groot aantal belangrijke waarden van de partitie in een IN-expressie.
* Verschillende resource quotum statistieken in Hallo ResourceResponse ingevuld voor documentverzameling schijfleesaanvragen als PopulateQuotaInfo aanvraagoptie is ingesteld.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Secundaire prestaties fix voor Hallo CreateDocumentCollectionIfNotExistsAsync API die is geïntroduceerd in 1.11.0.
* Prestaties te herstellen in Hallo SDK voor scenario's voor hoge mate van gelijktijdige aanvragen.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Ondersteuning voor nieuwe klassen en methoden tooprocess hello [wijzigen van de feed](change-feed.md) van documenten binnen een verzameling.
* Ondersteuning voor cross-partitiequery voortzetting en enkele verbeteringen perf voor cross-partitie query's.
* Toevoeging van CreateDatabaseIfNotExistsAsync en CreateDocumentCollectionIfNotExistsAsync methoden.
* Ondersteuning voor LINQ voor systeemfuncties: IsDefined-, IsNull- en IsPrimitive.
* Herstel voor automatische binplacing van Microsoft.Azure.Documents.ServiceInterop.dll en DocumentDB.Spatial.Sql.dll assembly's tooapplication de bin-map bij het gebruik van Hallo Nuget-pakket met projecten waarvoor project.json tooling.
* Ondersteuning voor het verzenden van client side ETW traceringen die handig zijn in scenario's voor foutopsporing kan worden.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Directe verbinding toegevoegde ondersteuning voor gepartitioneerde verzamelingen.
* Verbeterde prestaties voor gebonden veroudering consistentieniveau Hallo.
* Toegevoegde veelhoek en LineString DataTypes tijdens het opgeven van de verzameling beleid voor geofencing ruimtelijke query's te indexeren.
* LINQ ondersteuning toegevoegd voor StringEnumConverter, IsoDateTimeConverter en UnixDateTimeConverter bij het vertalen van predicaten.
* Verschillende SDK oplossingen voor problemen.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Een probleem opgelost dat veroorzaakt Hallo NotFoundException te volgen: Hallo lezen sessie is niet beschikbaar voor Hallo invoer sessietoken. Deze uitzondering is opgetreden in sommige gevallen bij het opvragen van Hallo lezen-gebied van een geografische distributie-account.
* Hallo ResponseStream eigenschap in Hallo ResourceResponse klasse, waardoor u directe toegang toohello onderliggende stroom van een antwoord wordt weergegeven.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Gewijzigde Hallo ResourceResponse, FeedResponse, StoredProcedureResponse en MediaResponse klassen tooimplement hello openbare interface overeenkomt, zodat ze kunnen worden mocked voor test gebaseerde implementatie (TDD).
* Een probleem bij het gebruik van een aangepaste JsonSerializerSettings-object om gegevens te serialiseren, waardoor de koptekst van een onjuist gevormd partitie opgelost.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Een probleem dat langdurige query's toofail met de fout heeft vast: verificatietoken is niet geldig op Hallo huidige tijd.
* Vaste een probleem dat verwijderd Hallo oorspronkelijke SqlParameterCollection van cross-partitie boven/volgorde-by-query's.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Ondersteuning toegevoegd voor parallelle query's voor gepartitioneerde verzamelingen.
* Ondersteuning toegevoegd voor cross-partitie ORDER BY en boven-query's voor gepartitioneerde verzamelingen.
* Vaste hello ontbrekende verwijzingen tooDocumentDB.Spatial.Sql.dll en Microsoft.Azure.Documents.ServiceInterop.dll die vereist zijn wanneer u verwijst naar een Azure DB die Cosmos-project met een verwijzing toohello Azure Cosmos DB Nuget-pakket.
* Vaste Hallo mogelijkheid toouse parameters van de verschillende typen bij gebruik van de gebruiker gedefinieerde functies in LINQ. 
* Een bug voor globaal gerepliceerde accounts vast waar Upsert aanroepen gerichte tooread locaties in plaats van schrijven locaties zijn wordt.
* Toegevoegde methoden toohello IDocumentClient interface die ontbraken: 
  * UpsertAttachmentAsync-methode die mediaStream en opties als parameters
  * CreateAttachmentAsync-methode die opties als parameter
  * De methode CreateOfferQuery die querySpec als parameter.
* Niet-verzegeld openbare klassen die beschikbaar zijn in Hallo IDocumentClient interface.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Hallo toegevoegde ondersteuning voor meerdere landen/regio database accounts.
* Ondersteuning toegevoegd voor nieuwe pogingen bij beperkte aanvragen.  Gebruiker kan het aantal nieuwe pogingen Hallo aanpassen en Hallo maximale wachttijd door Hallo ConnectionPolicy.RetryOptions eigenschap configureren.
* Een nieuwe IDocumentClient interface die Hallo handtekeningen van alle DocumenClient eigenschappen en methoden definieert toegevoegd.  Als onderdeel van deze wijziging ook gewijzigd uitbreidingsmethoden die IQueryable en IOrderedQueryable toomethods op Hallo DocumentClient klasse zelf hebt gemaakt.
* Configuratie optie tooset hello ServicePoint.ConnectionLimit voor een opgegeven Uri van de Azure DB die Cosmos-eindpunt toegevoegd.  Gebruik ConnectionPolicy.MaxConnectionLimit toochange Hallo standaardwaarde, die too50 is ingesteld.
* Afgeschafte IPartitionResolver en de uitvoering ervan.  Ondersteuning voor IPartitionResolver is nu verouderd. Het verdient aanbeveling gebruik te maken van verzamelingen gepartitioneerd voor hogere opslag en doorvoer.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Toegevoegd dat executestoredprocedureasync-methode die RequestOptions als een parameter op basis van een tooUri overbelasting.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Tijd toolive (TTL) is ondersteuning toegevoegd voor documenten.

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Heeft een fout in de Nuget-pakketten van de .NET SDK voor het verpakken van als onderdeel van een Azure Cloud Service-oplossing.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* Geïmplementeerd [gepartitioneerde verzamelingen](partition-data.md) en [prestatieniveaus die door de gebruiker gedefinieerde](performance-levels.md). 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[Vaste]**  Genereert Azure Cosmos-DB opvragen eindpunt: ' System.Net.Http.HttpRequestException: fout bij het kopiëren van inhoud tooa stream'.

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* Uitgebreide LINQ ondersteunen met inbegrip van nieuwe operators voor paginering, heeft voorwaardelijke expressies en vergelijking liggen.
  * Operator tooenable Selecteer TOP gedrag duren in LINQ
  * CompareTo operator tooenable tekenreeksvergelijkingen-bereik
  * Voorwaardelijke (?) en coalesce-operators (?)
* **[Vaste]**  Opgetreden bij het combineren van Model projectie waar In een LINQ-query. [#81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[Vaste]**  Als Select niet het laatste expressie Hallo Hallo is LINQ-Provider ervan uitgegaan dat geen projectie en selecteer geproduceerd * onjuist.  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Geïmplementeerde Upsert, UpsertXXXAsync toegevoegd methoden
* Verbeterde prestaties voor alle aanvragen
* Ondersteuning van de LINQ-Provider voor voorwaardelijk, coalesce, en CompareTo methoden voor tekenreeksen
* **[Vaste]**  LINQ-provider--> implementeren bevat de methode op de lijst toogenerate Hallo dezelfde SQL op IEnumerable en matrix
* **[Vaste]**  BackoffRetryUtility gebruikt Hallo dezelfde HttpRequestMessage opnieuw in plaats van het maken van een nieuwe taak opnieuw wordt uitgevoerd
* **[Verouderd]**  UriFactory.CreateCollection--> UriFactory.CreateDocumentCollection moet nu worden gebruikt.

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[Vaste]**  Lokalisatie problemen bij het gebruik van de cultuurgegevens niet nl zoals nl-NL, enzovoort. 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Id's gebaseerde routering toegevoegd
  * Nieuwe UriFactory helper tooassist met koppelingen naar hulpbronnen op basis van een ID maken
  * Nieuwe overloads op DocumentClient tootake in URI
* IsValid() en IsValidDetailed() in LINQ voor georuimtelijke toegevoegd
* Verbeterde ondersteuning voor LINQ-Provider:
  * **Math** -Abs, BOOGCOS, Asin, BOOGTAN, maximum, CO Exp, Floor, logboek, Log10, Pow, Round, aanmelding, Sin, Sqrt, Tan, afkappen
  * **Tekenreeks** -Concat, bevat, EndsWith, IndexOf, Count, ToLower, TrimStart, vervangen, omkeren, TrimEnd, StartsWith, subtekenreeks, ToUpper
  * **Matrix** -Concat, bevat, aantal
  * **IN** operator

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Ondersteuning toegevoegd voor indexering beleid wijzigen.
  * Nieuwe ReplaceDocumentCollectionAsync-methode in DocumentClient
  * Nieuwe IndexTransformationProgress-eigenschap in ResourceResponse<T> voor het percentage van de voortgang van de index beleidswijzigingen bijhouden
  * DocumentCollection.IndexingPolicy is nu veranderlijke
* Ondersteuning toegevoegd voor ruimtelijke query en indexeren.
  * Nieuwe Microsoft.Azure.Documents.Spatial naamruimte voor het serialiseren/deserialiseren van ruimtelijke typen, zoals Point- and -veelhoek
  * Nieuwe SpatialIndex klasse voor indexeren GeoJSON-gegevens die zijn opgeslagen in Cosmos-DB
* **[Vaste]**  Onjuist SQL-query is gegenereerd op basis van een LINQ-expressie [#38](https://github.com/Azure/azure-documentdb-net/issues/38).

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Een afhankelijkheid op Newtonsoft.Json v5.0.7 toegevoegd.
* Gemaakte wijzigingen toosupport Order By:
  
  * Ondersteuning voor LINQ-provider voor OrderBy() of OrderByDescending()
  * IndexingPolicy toosupport Order By 
    
    **Mogelijk belangrijke wijziging** 
    
    Als u bestaande code die voorziet in verzamelingen met een aangepast indexeringsbeleid hebt, wordt uw bestaande code behoeften toobe toosupport Hallo nieuwe IndexingPolicy klasse bijgewerkt. Als u geen aangepaste indexeringsbeleid hebt, klikt u vervolgens deze wijziging geldt niet voor u.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Ondersteuning toegevoegd voor het partitioneren van gegevens met behulp van de nieuwe HashPartitionResolver en RangePartitionResolver klassen Hallo en Hallo IPartitionResolver.
* Toegevoegde DataContract-serialisatie.
* Toegevoegde GUID ondersteuning in een LINQ-provider.
* Toegevoegde UDF ondersteund in LINQ.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK

## <a name="release--retirement-dates"></a>Release & buiten gebruik stellen datums
Microsoft biedt melding ten minste **12 maanden** voordat het buiten gebruik stellen van een SDK in de volgorde toosmooth Hallo overgang tooa nieuwere/ondersteunde versie.

Nieuwe functies en functionaliteit en optimalisaties worden alleen toegevoegd toohello huidige SDK, omdat het wordt aanbevolen dat u altijd upgrade toohello nieuwste SDK-versie zo spoedig mogelijk. 

Alle aanvragen tooAzure Cosmos-database met behulp van een buiten gebruik gestelde SDK zijn afgewezen door Hallo-service.

<br/>

| Versie | Releasedatum | Vervaldatum |
| --- | --- | --- |
| [1.17.0](#1.17.0) |10 augustus 2017 |--- |
| [1.16.1](#1.16.1) |07 augustus 2017 |--- |
| [1.16.0](#1.16.0) |02 augustus 2017 |--- |
| [1.15.0](#1.15.0) |30 juni 2017 |--- |
| [1.14.1](#1.14.1) |23 mei 2017 |--- |
| [1.14.0](#1.14.0) |10 mei 2017 |--- |
| [1.13.4](#1.13.4) |09 mei 2017 |--- |
| [1.13.3](#1.13.3) |06 mei 2017 |--- |
| [1.13.2](#1.13.2) |19 april 2017 |--- |
| [1.13.1](#1.13.1) |29 maart 2017 |--- |
| [1.13.0](#1.13.0) |24 maart 2017 |--- |
| [1.12.2](#1.12.2) |20 maart 2017 |--- |
| [1.12.1](#1.12.1) |14 maart 2017 |--- |
| [1.12.0](#1.12.0) |15 februari 2017 |--- |
| [1.11.4](#1.11.4) |06 februari 2017 |--- |
| [1.11.3](#1.11.3) |26 januari 2017 |--- |
| [1.11.1](#1.11.1) |21 december 2016 |--- |
| [1.11.0](#1.11.0) |08 december 2016 |--- |
| [1.10.0](#1.10.0) |27 september 2016 |--- |
| [1.9.5](#1.9.5) |01 september 2016 |--- |
| [1.9.4](#1.9.4) |24 augustus 2016 |--- |
| [1.9.3](#1.9.3) |15 augustus 2016 |--- |
| [1.9.2](#1.9.2) |23 juli 2016 |--- |
| [1.8.0](#1.8.0) |14 juni 2016 |--- |
| [1.7.1](#1.7.1) |06 mei 2016 |--- |
| [1.7.0](#1.7.0) |26 april 2016 |--- |
| [1.6.3](#1.6.3) |08 april 2016 |--- |
| [1.6.2](#1.6.2) |29 maart 2016 |--- |
| [1.5.3](#1.5.3) |19 februari 2016 |--- |
| [1.5.2](#1.5.2) |14 december 2015 |--- |
| [1.5.1](#1.5.1) |23 november 2015 |--- |
| [1.5.0](#1.5.0) |05 oktober 2015 |--- |
| [1.4.1](#1.4.1) |25 augustus 2015 |--- |
| [1.4.0](#1.4.0) |13 augustus 2015 |--- |
| [1.3.0](#1.3.0) |05 augustus 2015 |--- |
| [1.2.0](#1.2.0) |06 juli 2015 |--- |
| [1.1.0](#1.1.0) |30 april 2015 |--- |
| [1.0.0](#1.0.0) |08 april 2015 |--- |


## <a name="faq"></a>Veelgestelde vragen
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Zie ook
Zie toolearn meer informatie over de Cosmos-DB [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service. 

