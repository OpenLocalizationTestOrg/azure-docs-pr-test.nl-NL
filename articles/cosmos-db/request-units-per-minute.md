---
title: 'Azure CosmosDB: Aanvraageenheden per minuut (RU/m) | Microsoft Docs'
description: Meer informatie over hoe tooreduce kosten door het gebruik van aanvraageenheden per minuut.
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Aanvraageenheden per minuut in Azure Cosmos-DB

Azure Cosmos DB is ontworpen toohelp u een snelle en voorspelbare prestaties en schaalbaarheid naadloos samen met de groei van uw toepassing bereiken. U kunt inrichten doorvoer in een Cosmos-DB-container op beide, per seconde en op granulaties per minuut (RU/m). Hallo ingerichte doorvoer per minuut samenvattingen is gebruikte toomanage onverwachte pieken in Hallo werkbelasting optreedt samenvattingen per seconde. 

Dit artikel bevat een overzicht van de werking Hallo inrichting van eenheid aanvragen per minuut (RU/m). Hallo doel rekening met het leveren van RU/m is tooprovide een voorspelbare prestaties rond onvoorspelbare behoeften (met name als u toorun analyses nodig boven op uw operationele gegevens) en spiky werkbelastingen. We willen toohave die onze klanten meer Hallo doorvoer die ze inrichten zodat u snel kunt schalen met gemoedsrust gebruiken.

Na het lezen van dit artikel kunt u zich kunt tooanswer Hallo vragen te volgen:

* Hoe werkt een eenheid aanvragen per minuut
* Wat is Hallo verschil tussen eenheid aanvragen per minuut en eenheid aanvragen per seconde?
* Hoe tooprovision RU/m?
* Onder welke scenario onderzoekt ik inrichten eenheid aanvragen per minuut?
* Hoe Hallo toouse portal metrische gegevens toooptimize mijn kosten en prestaties?
* Definiëren welk soort aanvraag kan uw budget RU/m gebruiken?

## <a name="provisioning-request-units-per-minute-rum"></a>Inrichting aanvraageenheden per minuut (RU/m)

Als u Azure Cosmos DB inricht Hallo tweede samenvattingen (RU/s), krijgt u Hallo garanderen dat uw aanvraag is uitgevoerd op een lage latentie als de doorvoer niet Hallo capaciteit ingericht binnen die seconde overschreden. Met RU/m is het Hallo granulatie op Hallo minuut met Hallo garanderen dat uw aanvraag is gelukt binnen die minuut. Vergeleken toobursting systemen, zorgen wij ervoor dat Hallo prestaties u voorspelbare en erop kunt u plannen.

Hallo manier per minuut works inrichting is eenvoudig:

* RU/m wordt in rekening gebracht per uur en toevoeging tooRU/s. Voor meer informatie gaat u naar Azure Cosmos DB [pagina met prijzen](https://aka.ms/acdbpricing).
* RU/m kan worden ingeschakeld op niveau verzameling. Dat kan worden gedaan via Hallo SDK's (Node.js, Java of .net) of via de portal hello (ook MongoDB API werkbelastingen bevatten)
* Als RU/m is ingeschakeld voor elke 100 RU/s ingericht, krijgt u ook 1000 RU/m ingericht (Hallo verhouding is 10 x)
* Op een tweede opgegeven, een aanvraag-eenheid verbruikt uw RU/m inrichting alleen als u hebt overschreden uw per tweede inrichting binnen die seconde
* Eenmaal Hallo 60 seconden tijd (UTC) ends, Hallo per minuut inrichting is gevuld.
* RU/m kan alleen worden ingeschakeld voor verzamelingen met een maximale inrichting van 5000 RU/s per partitie. Als u de doorvoerbehoeften van uw schalen en een hoog niveau voor het leveren van per partitie, ontvangt u een waarschuwingsbericht weergegeven

Hieronder wordt een voorbeeld van een concreet, waarin een klant 10kRU/s met 100kRU/m kunt inrichten 73% opslaan in kosten inrichten voor piek (bij 50kRU per seconde) tot en met een periode van 90 seconden op een verzameling die 10.000 is RU/s en 100.000 RU/m ingericht:

* tweede 1e: Hallo RU/m budget is ingesteld op 100.000
* tweede 3e: tijdens deze tweede Hallo verbruik van aanvragen eenheid 11,010 RUs, 1,010 RUs hierboven Hallo RU/s inrichting is. Daarom worden 1,010 RUs van Hallo RU/m budget afgetrokken. 98,990 RUs zijn beschikbaar voor Hallo volgende 57 seconden in Hallo RU/m budget
* 29 seconde: tijdens deze tweede, een grote piek is er gebeurd (> 4 x hoger is dan de inrichting per seconde) en Hallo verbruik van aanvragen eenheid 46,920 RUs is. 36,920 RUs worden afgetrokken van Hallo RU/m budget verwijderd uit 92,323 RUs (28 seconde) too55, 403 RUs (29 seconde)
* 61st seconde: RU/m budget terug too100, 000 RUs is ingesteld.
 
![Grafiek weergeven Hallo verbruik en het inrichten van Azure DB die Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>Capaciteit van de aanvraag-eenheid opgeven met RU/m

Bij het maken van een verzameling Azure Cosmos DB u Hallo-nummer opgeven aantal aanvraageenheden per seconde (ru/s per seconde) u wilt dat gereserveerd voor Hallo-verzameling. U kunt ook aangeven of u wilt dat tooadd RU per minuut. Dit kan worden gedaan via Hallo Portal of Hallo SDK. 

### <a name="through-hello-portal"></a>Via Hallo Portal

In- of uitschakelen van RU per minuut hoeven alleen een Klik bij het inrichten van een verzameling. 

 ![Schermopname die laat zien hoe tooset RU/m in hello Azure-portal](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>Via Hallo SDK
Dit is eerst belangrijk toonote RU/m is alleen beschikbaar voor Hallo SDK's te volgen:

* .NET 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

Hier volgt een codefragment voor het maken van een verzameling met 3000 aanvraageenheden per tweede en 30.000 aanvraageenheden per minuut Hallo .NET SDK gebruiken:

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

Hier volgt een codefragment voor het wijzigen van Hallo doorvoer van een verzameling too5, 000 aanvraageenheden per seconde zonder RU inrichting per minuut gebruik Hallo .NET SDK:

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>Goede aanpassen aan scenario 's

In deze sectie bieden we een overzicht van scenario's die geschikt zijn voor het inschakelen van aanvraageenheden per minuut.

**Omgeving dev/Test:** geschikt. Tijdens het Hallo-ontwikkeling, als u uw toepassing met verschillende werkbelastingen, test kunt RU/m bieden Hallo flexibiliteit in deze fase. Tijdens het Hallo [emulator](local-emulator.md) is een uitstekend gratis hulpprogramma tootest Azure Cosmos DB. Maar als u toostart in een cloudomgeving wilt, hebt u een hoge mate van flexibiliteit met RU/m voor de behoeften van uw ad-hoc-prestaties. U kwijt meer tijd ontwikkelt, minder zorgen over prestatiebehoeften op het eerste. We het beste beginnen met het inrichten Hallo minimale RU/s en RU/m inschakelen.

**Onvoorspelbare, spiky, minuut granulatie moet:** goed past – besparingen: 25 75%. Wij hebben grote verbetering van RU/m en de meeste scenario's voor productie zijn in die groep. Als u een IoT-werkbelasting met piek enkele keren in een minuut hebt, hebt u query's wanneer het systeem laat massaal invoegen op Hallo dezelfde tijd, moet u extra capaciteit voor handeling spiky. Het is raadzaam om uw resourcebehoeften optimaliseren door het toepassen van onze onderstaande stapsgewijze benadering.

 ![Grafiek met aanvraag verbruik in vijf minuten granulatie](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Afbeelding - RU verbruik benchmark*

**Gemoedsrust:** goed past – besparingen: 10-20%. Soms wilt toohave gemoedsrust en u geen zorgen over potentiële pieken en beperking. Deze functie is Hallo rechts een voor u. In dat geval wordt aangeraden RU/m inschakelen en iets lagere uw per tweede inrichten. In dit geval wijkt af van Hallo hierboven als u wordt niet geprobeerd toooptimize agressief uw inrichten. Dit is van een 'Nul beperking' denkt in.

Kritieke bewerkingen met ad-hoc-behoeften: soms aangeraden tooonly kunnen kritieke bewerkingen toegang RU/m budget Hallo budget niet ophalen door de ad-hoc of minder belangrijke bewerkingen verbruiken. Dat kan eenvoudig worden gedefinieerd in Hallo onderstaande sectie.

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>Met behulp van Hallo portal metrische gegevens toooptimize kosten en prestaties

**De komende weken hello ontwikkelen we verder Hallo inhoud rond de bewaking van RUs minuut verbruik toooptimize die uw doorvoer moet.**

Via de portal metrics hello, kunt u zien hoeveel reguliere RU seconden u versus RU verbruikt minuten. Bewaking van deze metrische gegevens kunt u uw inrichting optimaliseren. 

Een stapsgewijze benadering voor het wordt aangeraden toouse RU/m tooyour profiteren. Voor elke stap moet u een overzicht van Hallo RU verbruik voor een volledige cyclus van uw werkbelasting (mogelijk uren, dagen, of zelfs weken) hebben en inzichten verkrijgen op Hallo-gebruik van wat u inrichten.

Hallo principe achter deze benadering is toomake uw doorvoer inrichten als sluiten als mogelijke tooa punt die overeenkomt met de van de onderstaande prestatiecriteria wordt ingericht. 

![Grafiek met aanvraag verbruik in samenvattingen van 5 minuten](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand hello optimale inrichting punt voor uw workload, moet u toounderstand:

* Verbruik patronen: Nee, incidentele of volgehouden pieken? (2 x gemiddelde) klein, Gemiddeld of grote (> 10 x gemiddelde) pieken?
* Percentage van beperkte aanvragen: bent u ervan overtuigd bent als er een stukje beperking? Zo ja, in welke mate? 

Als u wat uw doelstellingen zijn weet, kunt u zich kunt tooget dichter toohello optimale inrichten.

tooassist, willen we tooprovide een algemene richtlijnen voor hoe toooptimize op uw inrichting basis van uw verbruik RU/m. In deze richtlijnen tooall soort werkbelasting is niet van toepassing, maar is gebaseerd op kennis van Hallo private preview. Dergelijke basislijnen kan worden gewijzigd als er meer informatie:

|RU/m % gebruik|Mate van gebruik van RU/m|Aanbevolen acties voor het inrichten|
|---|---|---|
|0-1%|Onder gebruik|Lagere RU/s tooconsume meer RU/m|
|1-10%|Gebruik in orde|Hello Houd dezelfde inrichting niveau|
|Meer dan 10%|Overmatig gebruik|RU/s toorely minder op RU/m verhogen|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>Selecteer welke bewerkingen kunnen Hallo RU/m budget gebruiken

Op het niveau van de aanvraag, u kunt ook in-of uitschakelen RU/m budget tooserve Hallo aanvraag ongeacht bewerkingstype. Als reguliere ingerichte RUs per seconde budget verbruikt en Hallo-aanvraag kan niet Hallo RU/m budget verbruikt, worden deze aanvraag wordt beperkt. Standaard wordt elk verzoek afgehandeld door RU/m budget als RU/m doorvoer budget is geactiveerd. 

Hier volgt een codefragment voor het uitschakelen van RU/m budget Hallo DocumentDB API gebruiken CRUD en query-bewerkingen.

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>Volgende stappen

In dit artikel hebt wordt beschreven hoe partitionering werkt in Azure Cosmos DB, hoe u gepartitioneerde verzamelingen kunt maken en hoe u een goede partitiesleutel kunt verzamelen voor uw toepassing.

* Schaal en prestaties testen met Azure Cosmos DB uitvoeren. Zie [prestaties en schaal testen met Azure Cosmos DB](performance-testing.md) voor een voorbeeld.
* Aan de slag met Hallo coderen [SDK's](documentdb-sdk-dotnet.md) of Hallo [REST-API](/rest/api/documentdb/).
* Meer informatie over [ingerichte doorvoer](request-units.md) in Azure Cosmos-DB 

