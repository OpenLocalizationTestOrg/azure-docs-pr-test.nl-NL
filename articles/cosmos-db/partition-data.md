---
title: Partitionering en horizontaal schalen in Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe partitionering werkt in Azure Cosmos DB, partitie-sleutels en configureren met het partitioneren en het kiezen van de juiste partitiesleutel voor uw toepassing.
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2d2847276e553d7511241ff323c3e00aad8e5c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-partition-and-scale-in-azure-cosmos-db"></a>Partitioneren en schaal in Azure Cosmos-DB

[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is een globale gedistribueerde, meerdere model-database-service waarmee u snel, voorspelbare prestaties en schaalbaarheid naadloos samen met uw toepassing bereiken wanneer deze groeit. Dit artikel biedt een overzicht van hoe partitionering werkt voor alle gegevensmodellen in Azure Cosmos DB en wordt beschreven hoe u Azure DB die Cosmos-containers wilt effectief schalen uw toepassingen kunt configureren.

Partitionering en partitiesleutels worden ook besproken in deze Azure video met Scott Hanselman en Azure Cosmos DB Principal Engineering Manager, Shireesh Thota vrijdag.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Partitioneren in Azure Cosmos DB
U kunt in Azure Cosmos DB, opslaan en opvragen van schema minder gegevens met de volgorde van milliseconde reactietijden op elke schaal. Cosmos DB containers biedt voor het opslaan van gegevens aangeroepen **verzamelingen (voor het document), grafieken of tabellen**. Containers zijn logische resources en kunnen een of meer fysieke partities of servers omvatten. Het aantal partities wordt bepaald door de Cosmos-DB op basis van de grootte van de opslagruimte en de ingerichte doorvoer van de container. Elke partitie in Cosmos-database heeft een vaste hoeveelheid back SSD opslag gekoppeld en is gerepliceerd voor hoge beschikbaarheid. Beheer van de partitie is volledig beheerd door Azure Cosmos DB en er geen complexe code schrijven of beheren van de partities. Cosmos DB containers zijn onbeperkte in termen van opslag en doorvoer. 

![horizontale](./media/introduction/azure-cosmos-db-partitioning.png) 

Partitioneren is transparant voor uw toepassing. Snelle leesbewerkingen en schrijfbewerkingen, query's, transactionele logica, consistentieniveaus en verfijnd toegangsbeheer via methoden/API's aan een enkele containerresource biedt ondersteuning voor cosmos DB. De service verwerkt distributie gegevens over partities en routering queryaanvragen aan de juiste partitie. 

Hoe partitioneren werkt? Elk item moet hebben een partitiesleutel en een rijsleutel die worden geïdentificeerd. De partitiesleutel fungeert als een logische partitie voor uw gegevens en de grens van een natuurlijke Cosmos DB biedt voor het distribueren van gegevens meerdere partities. Kort samengevat: dit is hoe partitioneren werkt in Azure Cosmos DB:

* Inrichten van een Cosmos-DB-container met `T` doorvoer van aanvragen/s
* Achter de schermen Cosmos DB partities nodig om te fungeren richt `T` aanvragen/s. Als `T` hoger is dan de maximale doorvoer per partitie `t`, klikt u vervolgens de bepalingen van de Cosmos-DB `N`  =  `T/t` partities
* Cosmos DB wordt de sleutel ruimte van de partitie sleutel hashes gelijkmatig meerdere de `N` partities. Dus elke partitie (fysieke partitie) als host fungeert voor de partitie 1 N sleutelwaarden (logische partities)
* Wanneer een fysieke partitie `p` bereikt de opslaglimiet bereikt, Cosmos DB naadloos splitst `p` in twee nieuwe partities `p1` en `p2` en waarden die overeenkomen met ongeveer de helft van de sleutels aan elk van de partities die worden gedistribueerd. Deze bewerking gesplitste is onzichtbaar voor uw toepassing.
* Op dezelfde manier als het inrichten van doorvoer die hoger is dan `t*N` doorvoer, Cosmos DB splitst een of meer van de partities ter ondersteuning van de hogere doorvoer

De semantiek voor partitiesleutels zijn enigszins verschillen overeenkomen met de semantiek van elke API, zoals wordt weergegeven in de volgende tabel:

| API | Partitiesleutel | Rijsleutel |
| --- | --- | --- |
| DocumentDB | Aangepaste partitie sleutelpad | vaste`id` | 
| MongoDB | aangepaste shard-sleutel  | vaste`_id` | 
| Graph | Aangepaste partitie sleuteleigenschap | vaste`id` | 
| Tabel | vaste`PartitionKey` | vaste`RowKey` | 

Cosmos DB gebruikt op basis van de hash partitionering. Bij het schrijven van een item wordt Cosmos DB de waarde voor de partitiesleutel-hashes en hash resultaat gebruiken om te bepalen welke partitie voor het opslaan van het item in. Cosmos DB slaat alle items met dezelfde partitiesleutel op dezelfde fysieke partitie. De keuze van de partitiesleutel is een belangrijke beslissing die u moet aanbrengen in de ontwerpfase. U moet een eigenschapsnaam die heeft een breed scala aan waarden en zelfs toegangspatronen kiezen.

> [!NOTE]
> Het is een best practice om een partitiesleutel met veel afzonderlijke waarden (100s-1000 minimaal).
>

Azure DB Cosmos-containers kunnen worden gemaakt als 'fixed' of "onbeperkte." Containers met vaste grootte hebben een maximale limiet van 10 GB en doorvoer van 10.000 RU/s. Sommige API's maken de partitiesleutel moeten worden weggelaten voor containers met vaste grootte. U moet een minimale doorvoer van 2500 RU/s opgeven voor het maken van een container als onbeperkt.

## <a name="partitioning-and-provisioned-throughput"></a>Partitionering en ingerichte doorvoer
Cosmos DB is ontworpen voor voorspelbare prestaties. Wanneer u een container maakt, u doorvoer in termen van reserveren  **[aanvraageenheden](request-units.md) (RU) per seconde met een potentiële invoegtoepassing voor RU per minuut**. Elke aanvraag is een aanvraag eenheid kosten die evenredig aan de hoeveelheid systeembronnen, zoals CPU, geheugen en i/o verbruikt door de bewerking is toegewezen. Het lezen van een document 1 KB met sessieconsistentie verbruikt één eenheid van de aanvraag. Een leesbewerking is 1 RU ongeacht het aantal items die zijn opgeslagen of het aantal gelijktijdige aanvragen die actief zijn op hetzelfde moment. Grotere items moet hoger aanvraageenheden afhankelijk van de grootte. Als u de grootte van de entiteiten en het aantal leesbewerkingen die u wilt ondersteunen voor uw toepassing weet, kunt u de exacte hoeveelheid doorvoer die nodig is voor uw toepassing moet vindt inrichten. 

> [!NOTE]
> Voor de volledige doorvoer van de container, moet u een partitiesleutel waarmee u aanvragen tussen sommige sleutelwaarden afzonderlijke partitie gelijkmatig wordt verdeeld.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-the-azure-cosmos-db-apis"></a>Werken met de Azure Cosmos DB-API 's
U kunt de Azure portal of Azure CLI gebruiken containers maken en op elk gewenst moment worden geschaald. Deze sectie wordt beschreven hoe containers maken en de sleuteldefinitie doorvoer en partitie opgeven in elk van de ondersteunde API's.

### <a name="documentdb-api"></a>DocumentDB-API
Het volgende voorbeeld laat zien hoe een container (verzameling) met de DocumentDB-API maken. U vindt meer informatie in [partitioneren met DocumentDB API](partition-data.md).

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Vindt u een item (document) met behulp van de `GET` methode in de REST API of met behulp van `ReadDocumentAsync` in een van de SDK's.

```csharp
// Read document. Needs the partition key and the ID to be specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>MongoDB-API
U kunt een verzameling shard via uw favoriete hulpprogramma, stuurprogramma of SDK maken met de MongoDB-API. In dit voorbeeld gebruiken we de Mongo-Shell voor het maken van de verzameling.

In de Mongo-Shell:

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
Resultaten:

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>Tabel-API

Met de tabel-API u de doorvoer voor tabellen in de appSettings-configuratie voor uw toepassing:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Vervolgens maakt u een tabel met de SDK van Azure Table storage. De partitiesleutel is impliciet gemaakt als de `PartitionKey` waarde. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

U kunt met behulp van het volgende fragment één entiteit ophalen:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Zie [ontwikkelen met de API van de tabel](tutorial-develop-table-dotnet.md) voor meer informatie.

### <a name="graph-api"></a>Graph API

Met de Graph-API, moet u de Azure portal of CLI om containers maken. U kunt ook omdat Azure Cosmos DB met meerdere modellen, kunt u een van de andere modellen te maken en schalen van uw grafiek container.

U kunt geen hoekpunt of edge met de partitiesleutel en -id in Gremlin lezen. Bijvoorbeeld: voor een grafiek met regio ('VS') als de partitiesleutel en "Seattle" Als de rijsleutel vindt u een hoekpunt met de volgende syntaxis:

```
g.V(['USA', 'Seattle'])
```

Dezelfde met randen, u kunt verwijzen naar een edge met behulp van de partitie en rijsleutel.

```
g.E(['USA', 'I5'])
```

Zie [Gremlin ondersteuning voor Cosmos DB](gremlin-support.md) voor meer informatie.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Ontwerpen voor het partitioneren
Als u wilt schalen effectief met Azure Cosmos DB, moet u een goede partitiesleutel kiezen wanneer u de container maken. Er zijn twee belangrijke overwegingen voor het kiezen van een partitiesleutel:

* **Grens voor query's en transacties**: uw keuze van partitiesleutel moet een balans vinden tussen de noodzaak om het gebruik van transacties de vereiste voor de distributie van de entiteiten over meerdere partitiesleutels om ervoor te zorgen schaalbare oplossing. U kunt dezelfde partitiesleutel instellen voor alle objecten op één extreme, maar dit kan de schaalbaarheid van uw oplossing beperken. Het andere uiterste, kunt u een unieke partitiesleutel voor elk item dat is zeer schaalbaar, maar zou voorkomen dat u over verschillende document transacties via opgeslagen procedures en triggers toewijzen. Een ideaal is een partitiesleutel die u kunt gebruiken efficiënt query's en met voldoende kardinaliteit om te controleren of dat uw oplossing schaalbaar is. 
* **Er is geen opslag en prestaties knelpunten**: het is belangrijk dat u een eigenschap waarmee schrijfbewerkingen verdeeld over verschillende afzonderlijke waarden kiezen. Aanvragen voor dezelfde partitiesleutel mag niet langer dan de doorvoer van één partitie en zijn beperkt. Het is daarom belangrijk dat u kiest een partitiesleutel die niet in 'hotspots' in uw toepassing resulteert. Omdat de gegevens voor een sleutel die één partitie moet worden opgeslagen in een partitie, ook verdient om te voorkomen dat partitiesleutels die grote hoeveelheden gegevens voor dezelfde waarde hebben. 

Bekijk enkele praktijkscenario's en goede partitiesleutels voor elk:
* Als u een back-end gebruiker profiel implementeren, is een goede keuze voor partitiesleutel met de gebruikers-ID.
* Als u IoT gegevens bijvoorbeeld de status van het apparaat opslaat, wordt door een apparaat-ID een goede keuze voor de partitiesleutel is.
* Als u van Azure DB die Cosmos gebruikmaakt voor timeseries gegevens in een logboek, is de hostnaam of het proces-ID een goede keuze voor partitiesleutel.
* Als u een architectuur met meerdere tenants hebt, is de tenant-ID een goede keuze voor partitiesleutel.

Gebruik in sommige gevallen, zoals IoT- en profielen, de partitiesleutel kan niet hetzelfde zijn als uw id (documentsleutel). In andere gevallen zoals het gegevenstype van de reeks tijd wellicht u een partitiesleutel die anders is dan de id.

### <a name="partitioning-and-loggingtime-series-data"></a>Partitionering en logboekregistratie-tijdreeks gegevens
Een van de algemene gebruiksvoorbeelden van Cosmos-database is voor logboekregistratie en telemetrie. Het is belangrijk om op te halen van een goede partitiesleutel omdat u enorme hoeveelheden gegevens lezen wellicht/schrijven. De keuze is afhankelijk van uw lezen en schrijven tarieven en typen query's die u verwacht te worden uitgevoerd. Hier volgen enkele tips over het kiezen van een goede partitiesleutel.

* Als uw gebruiksvoorbeeld een klein aantal omvat schrijft opgebouwd gedurende een lange periode, en moeten query door bereiken van tijdstempels en andere filters en vervolgens met behulp van een updatepakket van het tijdstempel, bijvoorbeeld als een partitiesleutel is een goede benadering datum. Hiermee kunt u query via alle gegevens voor een datum van één partitie. 
* Als uw werkbelasting is geschreven zware die veelvoorkomende, moet u een partitiesleutel die niet gebaseerd op tijdstempel zodat Cosmos DB schrijfbewerkingen meerdere verschillende partities verdelen kunt. Een hostnaam, proces-ID, activiteits-ID of een andere eigenschap met hoge kardinaliteit is hier een goede keuze. 
* Een derde aanpak is een hybride een waarbij er meerdere containers, één voor elke dag/maand en de partitiesleutel is een gedetailleerd eigenschap als de hostnaam. Dit heeft als voordeel dat u kunt verschillende doorvoer op basis van de periode instellen, bijvoorbeeld de container voor de huidige maand is ingericht met hogere doorvoer omdat dit lees- en schrijfbewerkingen, terwijl de voorafgaande maanden met doorvoer omdat ze alleen lager leesbewerkingen fungeren.

### <a name="partitioning-and-multi-tenancy"></a>Partitionering en multi-tenancymodus
Als u een multitenant-toepassing met behulp van de Cosmos-DB implementeert, zijn er twee populaire patronen – een partitiesleutel per tenant en een container per tenant. Hier volgen de voordelen en nadelen voor elk:

* Een partitiesleutel per tenant: In dit model tenants binnen een enkele container worden geplaatst. Maar query's en voegt voor items binnen een enkele tenant kunnen worden uitgevoerd op een enkele partitie. U kunt ook transactionele logica implementeren voor alle items in een tenant. Omdat meerdere tenants een container delen, kunt u opslag en doorvoer kosten besparen door groeperen van bronnen voor tenants binnen een enkele container dan extra ruimte voor elke tenant wordt ingericht. Het nadeel is dat u geen isolatie van de prestaties per tenant hebt. Toename van prestaties/doorvoer van toepassing op de volledige container tegenover gerichte toeneemt voor tenants.
* Een Container per tenant: elke tenant heeft zijn eigen container. In dit model, kunt u de prestaties per tenant reserveren. Dit model is met het Cosmos-database nieuwe leveren prijzen model, rendabeler voor multitenant-toepassingen met een paar tenants.

U kunt ook een combinatie/gelaagde benadering die kleine tenants collocates en grotere tenants naar hun eigen container wordt gemigreerd.

## <a name="next-steps"></a>Volgende stappen
In dit artikel wordt een overzicht opgegeven voor een overzicht van de concepten en aanbevolen procedures voor het partitioneren van Azure Cosmos DB API. 

* Meer informatie over [ingerichte doorvoer in Azure Cosmos-DB](request-units.md)
* Meer informatie over [globale distributie in Azure Cosmos-DB](distribute-data-globally.md)



