---
title: 'Azure CosmosDB: Aanvraageenheden per minuut (RU/m) | Microsoft Docs'
description: Informatie over het om kosten te beperken door het gebruik van aanvraageenheden per minuut.
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
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Aanvraageenheden per minuut in Azure Cosmos-DB

Azure Cosmos DB is ontworpen om u helpen een snelle en voorspelbare prestaties en schaalbaarheid naadloos samen met de groei van uw toepassing. U kunt inrichten doorvoer in een Cosmos-DB-container op beide, per seconde en op granulaties per minuut (RU/m). De ingerichte doorvoer via de granulatie per minuut wordt gebruikt voor het opvangen van onverwachte pieken in de workload terwijl granulatie per seconde wordt gebruikt. 

Dit artikel bevat een overzicht van hoe de inrichting van eenheid aanvragen per minuut (RU/m) werkt. Het doel rekening met het leveren van RU/m is om een voorspelbare prestaties rond onvoorspelbare behoeften (met name als u wilt uitvoeren analytics boven op uw operationele gegevens) en spiky werkbelastingen te bieden. We willen hebben onze klanten meer doorvoer die ze inrichten zodat u snel kunt schalen met gemoedsrust gebruiken.

Na het lezen van dit artikel kunt u zich de volgende vragen beantwoorden:

* Hoe werkt een eenheid aanvragen per minuut
* Wat is het verschil tussen eenheid aanvragen per minuut en eenheid aanvragen per seconde?
* Het inrichten van RU/m?
* Onder welke scenario onderzoekt ik inrichten eenheid aanvragen per minuut?
* Het gebruik van de portal metrische gegevens om mijn kosten en prestaties te optimaliseren?
* Definiëren welk soort aanvraag kan uw budget RU/m gebruiken?

## <a name="provisioning-request-units-per-minute-rum"></a>Inrichting aanvraageenheden per minuut (RU/m)

Als u Azure Cosmos DB inrichten in de tweede samenvattingen (RU/s), krijgt u de garantie dat uw aanvraag is uitgevoerd op een lage latentie als de doorvoer niet de capaciteit ingericht binnen die seconde overschreden. Met RU/m, wordt de granulatie is op het moment met de garantie dat uw aanvraag is gelukt binnen die minuut. Vergeleken met het sturen van systemen, zorgen wij ervoor dat de prestaties u voorspelbare en erop kunt u plannen.

De manier waarop per minuut works inrichting is eenvoudig:

* RU/m wordt in rekening gebracht per uur en naast RU/s. Voor meer informatie gaat u naar Azure Cosmos DB [pagina met prijzen](https://aka.ms/acdbpricing).
* RU/m kan worden ingeschakeld op niveau verzameling. Dat kan worden gedaan via de SDK's (Node.js, Java of .net) of via de portal (ook MongoDB API werkbelastingen bevatten)
* Als RU/m is ingeschakeld voor elke 100 RU/s ingericht, krijgt u ook 1000 RU/m ingericht (de verhouding is 10 x)
* Op een tweede opgegeven, een aanvraag-eenheid verbruikt uw RU/m inrichting alleen als u hebt overschreden uw per tweede inrichting binnen die seconde
* Als de periode 60 seconden (UTC) is beëindigd, de per minuut inrichting wordt aangevuld
* RU/m kan alleen worden ingeschakeld voor verzamelingen met een maximale inrichting van 5000 RU/s per partitie. Als u de doorvoerbehoeften van uw schalen en een hoog niveau voor het leveren van per partitie, ontvangt u een waarschuwingsbericht weergegeven

Hieronder wordt een voorbeeld van een concreet, waarin een klant 10kRU/s met 100kRU/m kunt inrichten 73% opslaan in kosten inrichten voor piek (bij 50kRU per seconde) tot en met een periode van 90 seconden op een verzameling die 10.000 is RU/s en 100.000 RU/m ingericht:

* 1 seconde: het budget RU/m is ingesteld op 100.000
* tweede 3e: tijdens deze tweede is het verbruik van aanvragen eenheid 11,010 RUs, 1,010 RUs boven het inrichten van RU/s. Daarom worden 1,010 RUs van het budget RU/m afgetrokken. 98,990 RUs zijn beschikbaar voor de volgende 57 seconden in het budget RU/m
* 29 seconde: tijdens deze tweede, een grote piek is er gebeurd (> 4 x hoger is dan de inrichting per seconde) en het verbruik van aanvragen eenheid 46,920 RUs is. 36,920 RUs worden afgetrokken van het budget RU/m verwijderd uit 92,323 RUs (28 seconde) naar 55,403 RUs (29 seconde)
* 61st seconde: RU/m budget wordt opnieuw ingesteld op 100.000 RUs.
 
![Grafiek weer met het verbruik en de inrichting van Azure DB die Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>Capaciteit van de aanvraag-eenheid opgeven met RU/m

Bij het maken van een verzameling Azure Cosmos DB u opgeven dat het aantal aanvraageenheden per seconde (ru/s per seconde) die u wilt reserveren voor de verzameling. U kunt ook bepalen of u wilt toevoegen RU per minuut. Dit kan worden gedaan via de Portal of de SDK. 

### <a name="through-the-portal"></a>Via de Portal

In- of uitschakelen van RU per minuut hoeven alleen een Klik bij het inrichten van een verzameling. 

 ![Schermopname die laat zien hoe RU/m instelt in de Azure portal](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a>Via de SDK
Eerst is dit belangrijk te weten RU/m is alleen beschikbaar voor de volgende SDK's:

* .NET 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

Hier volgt een codefragment voor het maken van een verzameling met 3000 aanvraageenheden per tweede en 30.000 aanvraageenheden per minuut met de .NET SDK:

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

Hier volgt een codefragment voor het wijzigen van de doorvoer van een verzameling in 5000 aanvraageenheden per seconde zonder inrichting RU per minuut met de .NET SDK:

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>Goede aanpassen aan scenario 's

In deze sectie bieden we een overzicht van scenario's die geschikt zijn voor het inschakelen van aanvraageenheden per minuut.

**Omgeving dev/Test:** geschikt. Tijdens de ontwikkeling, als u uw toepassing met verschillende werkbelastingen, test krijgt RU/m u de flexibiliteit in deze fase. Terwijl de [emulator](local-emulator.md) is een uitstekend gratis hulpprogramma voor het testen van Azure Cosmos DB. Maar als u starten in een cloudomgeving wilt, hebt u een hoge mate van flexibiliteit met RU/m voor de behoeften van uw ad-hoc-prestaties. U kwijt meer tijd ontwikkelt, minder zorgen over prestatiebehoeften op het eerste. We het beste beginnen met de minimale RU/s-inrichting en RU/m inschakelen.

**Onvoorspelbare, spiky, minuut granulatie moet:** goed past – besparingen: 25 75%. Wij hebben grote verbetering van RU/m en de meeste scenario's voor productie zijn in die groep. Als u een IoT-werkbelasting met piek enkele keren in een minuut hebt als u een query uitvoeren wanneer het systeem massaopslag invoegen op hetzelfde moment laat hebt, moet u extra capaciteit voor handeling spiky behoeften. Het is raadzaam om uw resourcebehoeften optimaliseren door het toepassen van onze onderstaande stapsgewijze benadering.

 ![Grafiek met aanvraag verbruik in vijf minuten granulatie](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Afbeelding - RU verbruik benchmark*

**Gemoedsrust:** goed past – besparingen: 10-20%. Soms wilt gemoedsrust hebt en u geen zorgen over potentiële pieken en beperking. Deze functie is de juiste is voor u. In dat geval wordt aangeraden RU/m inschakelen en iets lagere uw per tweede inrichten. In dit geval verschilt van de bovenstaande als u niet wilt optimaliseren agressief uw inrichten. Dit is van een 'Nul beperking' denkt in.

Kritieke bewerkingen met ad-hoc-behoeften: soms het is raadzaam om alleen kritieke bewerkingen toegang RU/m budget zodat het budget niet gebruiken met ad-hoc of minder belangrijke bewerkingen. Dat kan eenvoudig worden gedefinieerd in de onderstaande sectie.

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a>Met behulp van de portal metrische gegevens om kosten en prestaties te optimaliseren

**De komende weken wordt er verdere ontwikkeling van de inhoud om de bewaking van RUs minuut verbruik voor het optimaliseren van de doorvoerbehoeften van uw.**

Via de portal metrische gegevens en kunt u zien hoeveel reguliere RU seconden u versus RU verbruikt minuten. Bewaking van deze metrische gegevens kunt u uw inrichting optimaliseren. 

U wordt aangeraden een stapsgewijze benadering voor het gebruik van RU/m in uw voordeel. Voor elke stap moet u een overzicht van het RU-verbruik voor een volledige cyclus van uw werkbelasting (mogelijk uren, dagen, of zelfs weken) hebben en inzichten te verkrijgen over het gebruik van wat u inrichten.

Het principe achter deze benadering is om de doorvoer inrichting zo dicht mogelijk bij een inrichting punt die overeenkomt met de van de onderstaande prestatiecriteria. 

![Grafiek met aanvraag verbruik in samenvattingen van 5 minuten](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
Om de optimale inrichting punt voor uw workload te begrijpen, moet u begrijpen:

* Verbruik patronen: Nee, incidentele of volgehouden pieken? (2 x gemiddelde) klein, Gemiddeld of grote (> 10 x gemiddelde) pieken?
* Percentage van beperkte aanvragen: bent u ervan overtuigd bent als er een stukje beperking? Zo ja, in welke mate? 

Als u wat uw doelstellingen zijn weet, kunt u zich kunt dichter bij de optimale inrichting.

Om u te helpen, willen we bieden een algemene richtlijn voor het optimaliseren van de inrichting op basis van uw verbruik RU/m. In deze richtlijnen niet van toepassing op alle soort werkbelasting, maar is gebaseerd op de kennis private preview. Dergelijke basislijnen kan worden gewijzigd als er meer informatie:

|RU/m % gebruik|Mate van gebruik van RU/m|Aanbevolen acties voor het inrichten|
|---|---|---|
|0-1%|Onder gebruik|Lagere RU/s meer RU/m gebruiken|
|1-10%|Gebruik in orde|Bewaren van hetzelfde niveau van inrichting|
|Meer dan 10%|Overmatig gebruik|RU/s minder op RU/m beroep te verhogen|

## <a name="select-which-operations-can-consume-the-rum-budget"></a>Selecteer welke bewerkingen kunnen het budget RU/m gebruiken

Op het niveau van de aanvraag, u kunt ook in-of uitschakelen RU/m-budget voor de aanvraag ongeacht bewerkingstype. Als reguliere ingerichte RUs per seconde budget verbruikt en de aanvraag kan niet het budget RU/m gebruiken, is deze aanvraag wordt beperkt. Standaard wordt elk verzoek afgehandeld door RU/m budget als RU/m doorvoer budget is geactiveerd. 

Hier volgt een codefragment voor het uitschakelen van RU/m budget met de DocumentDB-API voor CRUD en query-bewerkingen.

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>Volgende stappen

In dit artikel hebt wordt beschreven hoe partitionering werkt in Azure Cosmos DB, hoe u gepartitioneerde verzamelingen kunt maken en hoe u een goede partitiesleutel kunt verzamelen voor uw toepassing.

* Schaal en prestaties testen met Azure Cosmos DB uitvoeren. Zie [prestaties en schaal testen met Azure Cosmos DB](performance-testing.md) voor een voorbeeld.
* Aan de slag programmeren met de [SDK's](documentdb-sdk-dotnet.md) of de [REST-API](/rest/api/documentdb/).
* Meer informatie over [ingerichte doorvoer](request-units.md) in Azure Cosmos-DB 

