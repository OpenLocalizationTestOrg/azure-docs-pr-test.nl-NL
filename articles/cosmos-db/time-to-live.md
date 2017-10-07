---
title: aaaExpire gegevens in Azure Cosmos DB met tijd toolive | Microsoft Docs
description: De TTL biedt Microsoft Azure Cosmos DB Hallo mogelijkheid toohave documenten automatisch opgeschoond van Hallo systeem na een bepaalde periode.
services: cosmos-db
documentationcenter: 
keywords: tijd toolive
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>Gegevens in Azure Cosmos DB verzamelingen automatisch met tijd toolive verloopt
Toepassingen kunnen maken en opslaan van de enorme hoeveelheden gegevens. Sommige van deze gegevens, zoals machine gegenereerde gegevens, logboeken en gebruiker gebeurtenissessie informatie is alleen nuttig voor een beperkte periode. Zodra Hallo gegevens wordt overtollige toohello behoeften van de toepassing hello veilige toopurge is deze gegevens en verminderen het Hallo-opslagbehoeften van een toepassing.

Microsoft Azure Cosmos DB biedt 'keer toolive' of TTL Hallo mogelijkheid toohave documenten automatisch opgeschoond uit Hallo database na een bepaalde periode. Hallo standaardtijd toolive worden ingesteld op niveau van de verzameling Hallo en op basis van per document wordt genegeerd. Zodra TTL is ingesteld, de standaardwaarde voor een verzameling of op het documentniveau van een, wordt Cosmos DB documenten die bestaan na die periode, in seconden, omdat ze het laatst zijn gewijzigd automatisch verwijderd.

Tijd toolive in Cosmos-database maakt gebruik van een offset tegen wanneer Hallo-document voor het laatst is gewijzigd. toodo hello maakt gebruik van deze deze `_ts` veld dat op elk document bestaat. Hallo _ts veld is een unix-stijl-epoche tijdstempel die Hallo datum en tijd. Hallo `_ts` veld wordt telkens bijgewerkt wanneer een document wordt gewijzigd. 

## <a name="ttl-behavior"></a>TTL gedrag
Hallo TTL functie wordt bepaald door de TTL-eigenschappen op twee niveaus - Hallo verzameling niveau en Hallo document. Hallo-waarden worden ingesteld in seconden en worden behandeld als een delta van Hallo `_ts` dat document Hallo voor het laatst is gewijzigd op.

1. DefaultTTL voor Hallo-verzameling
   
   * Als u documenten ontbreekt (of set toonull) worden niet automatisch verwijderd.
   * Als deze aanwezig is en het Hallo-waarde is '-' 1 = oneindige – documenten verloopt niet standaard
   * Als deze aanwezig is en Hallo-waarde is een nummer ("n") – documenten laten verlopen "n" seconden na de laatste wijziging
2. De TTL voor Hallo documenten: 
   
   * Eigenschap is alleen van toepassing als DefaultTTL voor Hallo bovenliggende verzameling aanwezig.
   * Hallo DefaultTTL waarde voor de verzameling van bovenliggende Hallo overschrijft.

Zodra het Hallo-document is verlopen (`ttl`  +  `_ts` > = huidige servertijd), Hallo document is gemarkeerd als 'verlopen'. Er is geen bewerking is toegestaan op deze documenten na deze tijd en ze zullen worden uitgesloten van Hallo resultaten van alle query's uitgevoerd. Hallo-documenten in Hallo-systeem fysiek zijn verwijderd en worden verwijderd op de achtergrond Hallo optioneel wordt op een later tijdstip. Dit verbruikt geen een [Aanvraageenheden (RUs)](request-units.md) uit Hallo verzameling budget.

Hallo hierboven logica kan worden weergegeven in Hallo matrix te volgen:

|  | DefaultTTL ontbreekt of niet is ingesteld op Hallo-verzameling | DefaultTTL = -1 op verzameling | DefaultTTL = "n" voor verzameling |
| --- |:--- |:--- |:--- |
| TTL ontbreekt op document |Er is niets toooverride op documentniveau omdat zowel de Hallo-document als de verzameling hebt geen concept van TTL. |Er zijn geen documenten in deze verzameling verloopt. |Hallo-documenten in deze verzameling verlopen wanneer n interval is verstreken. |
| TTL = -1 op document |Niets toooverride op documentniveau Hallo omdat Hallo verzameling bevat geen definitie van Hallo DefaultTTL-eigenschap die een document kunt negeren. TTL voor een document is niet geïnterpreteerde door Hallo-systeem. |Er zijn geen documenten in deze verzameling verloopt. |Hallo-document met TTL =-1 in deze verzameling verloopt nooit. Alle andere documenten verloopt na "n" interval. |
| TTL = n op document |Er is niets toooverride op documentniveau Hallo. TTL voor een document in niet geïnterpreteerde door Hallo-systeem. |Hallo-document met TTL = n verloopt na interval n, in seconden. Andere documenten wordt overgenomen van het interval van -1 en nooit verlopen. |Hallo-document met TTL = n verloopt na interval n, in seconden. Andere documenten overneemt "n" interval van Hallo verzameling. |

## <a name="configuring-ttl"></a>TTL configureren
Standaard is de tijd toolive standaard in alle Cosmos DB verzamelingen en op alle documenten uitgeschakeld.

## <a name="enabling-ttl"></a>TTL inschakelen
tooenable TTL op een verzameling of Hallo documenten binnen een verzameling, moet u tooset Hallo DefaultTTL eigenschap van een verzameling tooeither -1 of een positief getal zijn dan nul. Instelling Hallo DefaultTTL te-1 betekent dat standaard alle documenten in de verzameling Hallo permanent wordt live maar Hallo Cosmos-DB-service moet worden gecontroleerd door deze verzameling voor documenten waarvoor deze standaardinstelling worden genegeerd.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>Standaard-TTL op een verzameling configureren
U bent een toolive standaardtijd kunnen tooconfigure op het niveau van een verzameling. tooset hello TTL op een verzameling, moet u een niet-nul positief getal dat Hallo-outperiode in seconden, tooexpire aangeeft tooprovide alle documenten in de verzameling Hallo nadat Hallo tijdstempel van Hallo document laatst gewijzigd (`_ts`). Of u Hallo standaard te-1, wat betekent dat dat alle documenten die worden ingevoegd in de verzameling toohello voor onbepaalde tijd standaard wordt live kunt instellen.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>De instelling van TTL op een document
Bovendien toosetting een standaard TTL-waarde op een verzameling kunt u instellen specifieke TTL op het documentniveau van een. Hierdoor wordt standaard Hallo van Hallo verzameling overschreven.

* tooset hello TTL op een document, moet u een niet-nul positief getal waarmee wordt aangegeven Hallo periode, in seconden, tooexpire Hallo document nadat Hallo laatst gewijzigd tijdstempel van Hallo document tooprovide (`_ts`).
* Als een document geen TTL-veld heeft, vervolgens Hallo standaard van Hallo-verzameling van toepassing.
* Als TTL is uitgeschakeld op niveau van de verzameling hello, worden Hallo TTL op Hallo document genegeerd totdat de TTL opnieuw is ingeschakeld op Hallo-verzameling.

Hier volgt een codefragment die laat zien hoe tooset Hallo TTL verloopt op een document:

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>TTL op een bestaand document uitbreiden
U kunt Hallo TTL voor een document opnieuw instellen als volgt een schrijfbewerking voor Hallo-document. Hierdoor wordt ingesteld Hallo `_ts` toohello huidige tijd en Hallo aftelling toohello document verloop, zoals ingesteld door Hallo `ttl`, opnieuw wordt gestart. U kunt eventueel toochange hello `ttl` van een document, kunt u Hallo veld bijwerken zoals u met een ander veld worden ingesteld doen kunt.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>TTL verwijderen uit een document
Als een TTL-waarde is ingesteld op een document en niet langer dat document tooexpire wilt, kunt vervolgens u Hallo-document ophalen, verwijder Hallo TTL-veld en vervang Hallo-document op Hallo-server. Wanneer de TTL-veld Hallo van Hallo document wordt verwijderd, wordt standaard Hallo van Hallo verzameling worden toegepast. toostop een document verlopen en niet overgenomen van Hallo-verzameling moet u tooset Hallo TTL-waarde te-1.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>TTL uitschakelen
toodisable TTL volledig op een verzameling en stop Hallo achtergrond verwerken van zoekt verlopen documenten Hallo DefaultTTL eigenschap op Hallo-verzameling moet worden verwijderd. Als u deze eigenschap verschilt van de instelling voor het te-1. Toohello verzameling permanent wordt live, maar u kunt deze waarschuwing negeren op specifieke documenten in de verzameling Hallo instellen te-1 betekent dat nieuwe documenten worden toegevoegd. Verwijderen van deze eigenschap volledig uit verzameling Hallo betekent dat er geen documenten verloopt, zelfs als er documenten waarvoor een eerdere standaard expliciet worden genegeerd.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>Veelgestelde vragen
**Wat TTL kost mij?**

Er is geen extra kosten toosetting TTL voor een document.

**Hoe lang duurt toodelete mijn document zodra Hallo TTL is?**

Hallo-documenten zijn verlopen onmiddellijk nadat Hallo TTL opgestart is, en niet meer toegankelijk via CRUD of de query API's. 

**Wordt de TTL voor een document invloed hebben op RU kosten**

Nee, er zijn geen gevolgen op RU kosten voor verwijderingen van verlopen documenten via TTL in Cosmos-database.

**Hallo TTL functie alleen geldt tooentire documenten of kan ik afzonderlijke document eigenschapswaarden verloopt?**

TTL geldt toohello hele document. Als u tooexpire wilt wordt slechts een deel van een document, dan wordt aanbevolen Hallo gedeelte extraheren uit de belangrijkste document Hallo in tooa afzonderlijk 'gekoppelde' document uit te voeren en gebruik vervolgens de TTL op het uitgepakte document.

**Heeft Hallo TTL functie ook specifieke vereisten voor indexering?**

Ja. Hallo-verzameling moet hebben [indexeren groepsbeleid](indexing-policies.md) tooeither consistente of Lazy. Probeert tooset DefaultTTL op een verzameling met indexeren set tooNone leidt tot een fout als poging tooturn uitschakelen indexeren op een verzameling met een DefaultTTL al ingesteld.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Azure Cosmos DB verwijzen toohello service [ *documentatie* ](https://azure.microsoft.com/documentation/services/cosmos-db/) pagina.

