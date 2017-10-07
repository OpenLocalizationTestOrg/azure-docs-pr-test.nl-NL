---
title: aaaBuild mobiele toepassingen met Xamarin en Azure Cosmos DB | Microsoft Docs
description: Een zelfstudie waarmee u een Xamarin iOS, Android of formulieren maakt met behulp van Azure Cosmos DB een toepassing. Azure Cosmos DB is een snelle, schaal wereld, cloud-database voor mobiele apps.
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>Mobiele toepassingen met Xamarin en Azure Cosmos DB maken
De meeste mobiele apps moeten toostore gegevens in de cloud Hallo en Azure Cosmos DB is een cloud-database voor mobiele apps. Heeft alles wat die een mobiele ontwikkelaar nodig heeft. Er is een volledig beheerde database als een service die wordt geschaald op aanvraag. Dit brengt uw gegevens tooyour toepassing transparant, waar uw gebruikers bevinden zich hele Hallo wereld. Met behulp van Hallo [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md), kunt u Xamarin mobiele apps toointeract rechtstreeks met Azure Cosmos DB, zonder de middelste laag inschakelen.

Dit artikel bevat een zelfstudie voor het bouwen van mobiele apps met Xamarin en Azure Cosmos DB. U vindt de volledige broncode Hallo Hallo-zelfstudie op [Xamarin en Azure Cosmos DB op GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin), met inbegrip van hoe toomanage gebruikers en machtigingen.

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>Mogelijkheden voor mobiele apps van Azure DB Cosmos
Azure Cosmos DB biedt Hallo belangrijke mogelijkheden voor ontwikkelaars van mobiele app te volgen:

![Mogelijkheden voor mobiele apps van Azure DB Cosmos](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* Uitgebreide query's over schemaloos gegevens. Azure Cosmos DB slaat gegevens als schemaloos JSON-documenten in heterogene verzamelingen. Dit biedt [snel en uitgebreide query's](documentdb-sql-query.md) zonder Hallo moeten tooworry over schema's of indexen.
* De doorvoer van snelle. Het duurt slechts enkele milliseconden tooread en write documenten met Azure Cosmos DB. Ontwikkelaars kunnen opgeven Hallo doorvoer die ze nodig hebben en Azure Cosmos DB respecteert deze met 99,99 procent Sla's.
* Oneindig schaal. Uw Azure Cosmos DB verzamelingen [groeien wanneer uw app groeit](partition-data.md). U kunt beginnen met kleine gegevenssets en de doorvoer van honderden aanvragen per seconde. Uw verzamelingen kunnen toopetabytes van gegevens en willekeurig grote doorvoer met honderden miljoenen aanvragen per seconde worden uitgebreid.
* Globaal gedistribueerd. Mobiele app gebruikers zijn aangemeld Hallo gaat vaak over Hallo wereld. Azure Cosmos-database is een [globaal gedistribueerde database](distribute-data-globally.md). Klik op Hallo kaart toomake uw gegevens toegankelijk tooyour gebruikers.
* Ingebouwde uitgebreide autorisatie. Met Azure Cosmos DB, kunt u eenvoudig populaire patronen zoals implementeren [gegevens per gebruiker](https://aka.ms/documentdb-xamarin-todouser) of gegevens, zonder complexe aangepaste autorisatie-code voor meerdere gebruikers worden gedeeld.
* Georuimtelijke query's. Veel mobiele apps bieden vandaag geo-contextafhankelijke ervaringen. Met uitstekende ondersteuning voor [georuimtelijke typen](geospatial.md), Azure Cosmos DB maakt het creëren van deze gemakkelijk tooaccomplish ervaringen.
* Binaire bijlagen. Uw appgegevens bevatten vaak binaire blobs. Systeemeigen ondersteuning voor bijlagen maakt het eenvoudiger toouse Azure Cosmos DB als een één loket voor uw appgegevens.

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Azure DB Cosmos en Xamarin-zelfstudie
Hallo volgende zelfstudie ziet hoe toobuild een mobiele toepassing met Xamarin en Azure Cosmos DB. U vindt de volledige broncode Hallo Hallo-zelfstudie op [Xamarin en Azure Cosmos DB op GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).

### <a name="get-started"></a>Aan de slag
Het is gemakkelijk tooget de slag met Azure Cosmos DB. Ga toohello Azure-portal en maak een nieuwe Azure DB die Cosmos-account. Klik op Hallo **snel starten** tabblad. Download Hallo Xamarin Forms taak lijst voorbeeld is al verbonden tooyour Azure DB die Cosmos-account. 

![Azure Cosmos DB snel starten voor mobiele apps](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

Of als u een bestaande Xamarin-app hebt, kunt u toevoegen Hallo [Azure Cosmos DB NuGet-pakket](documentdb-sdk-dotnet-core.md). Azure Cosmos DB ondersteunt Xamarin.IOS, Xamarin.Android, en Xamarin Forms gedeelde bibliotheken.

### <a name="work-with-data"></a>Werken met gegevens
De records van uw gegevens worden opgeslagen in Azure Cosmos DB als schemaloos JSON-documenten in heterogene verzamelingen. U kunt documenten met verschillende structuren opslaan in Hallo dezelfde verzameling:

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

U kunt geïntegreerde language-query's in uw Xamarin-projecten gebruiken via schemaloos gegevens:

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>Gebruikers toevoegen
Net als veel gestart voorbeelden ophalen, verifieert hello Azure Cosmos DB voorbeeld gedownloade toohello service met behulp van een hoofdsleutel vastgelegd in het Hallo-app-code. Deze standaard is niet verstandig voor een app die u toorun overal, met uitzondering van plan op uw lokale emulator bent. Als een onbevoegde gebruiker Hallo-hoofdsleutel hebt verkregen, kan alle Hallo van gegevens over uw Azure DB die Cosmos-account worden geschonden. In plaats daarvan wilt u dat uw app tooaccess Hallo alleen records voor Hallo aangemelde gebruiker. Azure Cosmos DB kunnen ontwikkelaars toogrant toepassing lezen of lezen/schrijven machtiging tooa verzameling, een verzameling van documenten die zijn gegroepeerd op een partitiesleutel, of een bepaald document. 

Volg deze stappen toomodify Hallo taak lijst app tooa voor meerdere gebruikers taak lijst-app: 

  1. Aanmelding tooyour app toevoegen via Facebook, Active Directory of een andere provider.

  2. Maken van een verzameling Azure Cosmos DB UserItems met **/userId** als partitiesleutel Hallo. Geven de partitiesleutel Hallo voor uw verzameling kunt u Azure Cosmos DB tooscale oneindig als Hallo-nummer van uw app-gebruikers groeit, maar blijft toooffer snelle query's.

  3. Azure Cosmos DB Resource Token Broker toevoegen. Deze eenvoudige Web-API verifieert gebruikers en tokens tijdelijke toosigned gebruikers problemen met toegang alleen toohello documenten in hun partitie. In dit voorbeeld wordt Resource Token Broker gehost in App Service.

  4. Hallo app tooauthenticate tooResource Token Broker met Facebook wijzigen en Hallo resource tokens voor Hallo aangemelde Facebook gebruikers aanvragen. U kunt vervolgens toegang tot hun gegevens in Hallo UserItems verzameling.  

U vindt een steekproef van de volledige code van dit patroon op [Resource Token Broker op GitHub](http://aka.ms/documentdb-xamarin-todouser). Dit diagram wordt Hallo-oplossing:

![Azure DB Cosmos-broker voor gebruikers en machtigingen](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

Als u wilt dat twee gebruikers toohave toegang toohello dezelfde takenlijst, kunt u extra machtigingen toohello toegangstoken in Token Broker Resource toevoegen.

### <a name="scale-on-demand"></a>Schalen op aanvraag
Azure Cosmos-database is een beheerde database als een service. Wanneer uw gebruikersgroep groeit, hoeft u geen tooworry over het inrichten van virtuele machines of kernen verhogen. Tootell Azure Cosmos DB hoeft u uw app moet het aantal bewerkingen per seconde (doorvoer). U kunt opgeven dat Hallo doorvoer via Hallo **Scale** tabblad met behulp van een meting van doorvoer aangeroepen (RUs) Aanvraageenheden per seconde. Bijvoorbeeld, een leesbewerking op een document van 1 KB vereist 1 RU. U kunt ook waarschuwingen toohello toevoegen **doorvoer** metrische toomonitor Hallo verkeer groei en Hallo doorvoer fire waarschuwingen via programmacode wijzigen.

![Azure DB Cosmos scale doorvoer op aanvraag](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>Ga wereld schaal
Als uw app toeneemt populariteit, kunt u gebruikers mogelijk krijgen via Hallo wereld. Of misschien wilt u toobe voorbereid voor onvoorziene gebeurtenissen. Ga toohello Azure-portal en open uw Azure DB die Cosmos-account. Klik op Hallo kaart toomake uw gegevens continu repliceren tooany aantal regio's over Hallo wereld. Hierdoor kunt u uw gegevens beschikbaar waar uw gebruikers zijn. U kunt ook de failover-beleid toobe voorbereid voor diverse risico's toevoegen.

![Azure DB Cosmos schaal tussen de geografische regio 's](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

Gefeliciteerd. U Hallo oplossing hebt voltooid en een mobiele App met Xamarin en Azure Cosmos DB. Volg dezelfde stappen toobuild Cordova-apps met behulp van hello Azure Cosmos DB JavaScript SDK en systeemeigen iOS/Android-apps met behulp van Azure Cosmos DB REST API's.

## <a name="next-steps"></a>Volgende stappen
* De broncode Hallo voor weergeven [Xamarin en Azure Cosmos DB op GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).
* Hallo downloaden [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md).
* Meer voorbeelden van code voor vinden [.NET-toepassingen](documentdb-dotnet-samples.md).
* Meer informatie over [Azure Cosmos DB uitgebreide mogelijkheden query](documentdb-sql-query.md).
* Meer informatie over [georuimtelijke ondersteuning in Azure Cosmos DB](geospatial.md).



