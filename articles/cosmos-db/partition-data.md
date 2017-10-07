---
title: aaaPartitioning en horizontaal schalen in Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe partitionering werkt in Azure Cosmos DB hoe tooconfigure partitioneren en partitiesleutels en hoe toopick Hallo rechts partitie-sleutel voor uw toepassing.
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
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>Hoe toopartition en schalen in Azure Cosmos-DB

[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is een globale gedistribueerde en modellen database service ontworpen toohelp u bereiken snelle en voorspelbare prestaties en schaalbaarheid naadloos samen met uw toepassing wanneer het groeit. Dit artikel bevat een overzicht van hoe partitioneren werkt voor alle Hallo-gegevens in Azure Cosmos DB modellen, en wordt beschreven hoe u kunt configureren Azure Cosmos DB containers tooeffectively schalen uw toepassingen.

Partitionering en partitiesleutels worden ook besproken in deze Azure video met Scott Hanselman en Azure Cosmos DB Principal Engineering Manager, Shireesh Thota vrijdag.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Partitioneren in Azure Cosmos DB
U kunt in Azure Cosmos DB, opslaan en opvragen van schema minder gegevens met de volgorde van milliseconde reactietijden op elke schaal. Cosmos DB containers biedt voor het opslaan van gegevens aangeroepen **verzamelingen (voor het document), grafieken of tabellen**. Containers zijn logische resources en kunnen een of meer fysieke partities of servers omvatten. Hallo aantal partities wordt bepaald door de Cosmos-DB op basis van Hallo opslaggrootte en ingerichte doorvoer Hallo van Hallo-container. Elke partitie in Cosmos-database heeft een vaste hoeveelheid back SSD opslag gekoppeld en is gerepliceerd voor hoge beschikbaarheid. Partitie management volledig wordt beheerd door Azure Cosmos DB, en u niet hebt toowrite complexe code of beheren van uw partities. Cosmos DB containers zijn onbeperkte in termen van opslag en doorvoer. 

![horizontale](./media/introduction/azure-cosmos-db-partitioning.png) 

Partitioneren is transparant tooyour toepassing. Snelle leest en schrijft, query's, transactionele logica, consistentieniveaus en verfijnd toegangsbeheer via de methoden/API's tooa enkele containerresource biedt ondersteuning voor cosmos DB. Hallo-service verwerkt gegevens over partities verdeeld en routering query aanvragen toohello rechts partitie. 

Hoe partitioneren werkt? Elk item moet hebben een partitiesleutel en een rijsleutel die worden geïdentificeerd. De partitiesleutel fungeert als een logische partitie voor uw gegevens en de grens van een natuurlijke Cosmos DB biedt voor het distribueren van gegevens meerdere partities. Kort samengevat: dit is hoe partitioneren werkt in Azure Cosmos DB:

* Inrichten van een Cosmos-DB-container met `T` doorvoer van aanvragen/s
* Achter de schermen hello, Cosmos DB bepalingen partities nodig tooserve `T` aanvragen/s. Als `T` hoger is dan de maximale doorvoer per partitie Hallo `t`, klikt u vervolgens de bepalingen van de Cosmos-DB `N`  =  `T/t` partities
* Cosmos DB ruimte wordt toegewezen Hallo sleutel van de partitie sleutel hashes gelijkmatig over Hallo `N` partities. Dus elke partitie (fysieke partitie) als host fungeert voor de partitie 1 N sleutelwaarden (logische partities)
* Wanneer een fysieke partitie `p` bereikt de opslaglimiet bereikt, Cosmos DB naadloos splitst `p` in twee nieuwe partities `p1` en `p2` en waarden die overeenkomen tooroughly half Hallo sleutels tooeach Hallo distribueert partities. Deze bewerking gesplitste is onzichtbaar tooyour toepassing.
* Op dezelfde manier als het inrichten van doorvoer die hoger is dan `t*N` doorvoer, Cosmos DB splitst een of meer van de partities toosupport Hallo hogere doorvoer

Hallo semantiek voor partitiesleutels zijn enigszins verschillen toomatch Hallo semantiek van elke API, zoals wordt weergegeven in de volgende tabel Hallo:

| API | Partitiesleutel | Rijsleutel |
| --- | --- | --- |
| DocumentDB | Aangepaste partitie sleutelpad | vaste`id` | 
| MongoDB | aangepaste shard-sleutel  | vaste`_id` | 
| Graph | Aangepaste partitie sleuteleigenschap | vaste`id` | 
| Tabel | vaste`PartitionKey` | vaste`RowKey` | 

Cosmos DB gebruikt op basis van de hash partitionering. Bij het schrijven van een item Cosmos DB hash-waarde voor de partitiesleutel Hallo en gebruik Hallo opgedeeld resultaat toodetermine welke partitie toostore Hallo-item in. Cosmos DB slaat alle items met dezelfde partitiesleutel in Hallo Hallo dezelfde fysieke partitie. Hallo gekozen Hallo partitiesleutel is erg belangrijk dat u hebt de toomake tijdens de ontwerpfase. U moet een eigenschapsnaam die heeft een breed scala aan waarden en zelfs toegangspatronen kiezen.

> [!NOTE]
> Het is een best practice toohave een partitiesleutel met veel afzonderlijke waarden (100s-1000 minimaal).
>

Azure DB Cosmos-containers kunnen worden gemaakt als 'fixed' of "onbeperkte." Containers met vaste grootte hebben een maximale limiet van 10 GB en doorvoer van 10.000 RU/s. Sommige API's maken Hallo partitie sleutel toobe voor vaste grootte containers worden weggelaten. een container als onbeperkte toocreate, moet u een minimale doorvoer van 2500 RU/s.

## <a name="partitioning-and-provisioned-throughput"></a>Partitionering en ingerichte doorvoer
Cosmos DB is ontworpen voor voorspelbare prestaties. Wanneer u een container maakt, u doorvoer in termen van reserveren  **[aanvraageenheden](request-units.md) (RU) per seconde met een potentiële invoegtoepassing voor RU per minuut**. Elke aanvraag is een aanvraag eenheid kosten die evenredig toohello hoeveelheid systeembronnen, zoals CPU, geheugen en i/o verbruikt door Hallo-bewerking is toegewezen. Het lezen van een document 1 KB met sessieconsistentie verbruikt één eenheid van de aanvraag. Een leesbewerking is 1 RU ongeacht het aantal items Hallo opgeslagen of het aantal gelijktijdige aanvragen die actief zijn op Hallo Hallo hetzelfde moment. Grotere items moet hoger aanvraageenheden, afhankelijk van Hallo grootte. Als u weet Hallo grootte van de entiteiten en aantal leesbewerkingen Hallo moet u toosupport voor uw toepassing, kunt u de exacte hoeveelheid doorvoer die nodig is voor uw toepassing moet vindt Hallo inrichten. 

> [!NOTE]
> tooachieve hello volledige doorvoer van Hallo-container, moet u een partitiesleutel waarmee u tooevenly distribueren aanvragen tussen sommige sleutelwaarden afzonderlijke partitie.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>Werken met hello Azure Cosmos DB API 's
U kunt gebruiken hello Azure-portal of Azure CLI toocreate containers en op elk gewenst moment worden geschaald. Deze sectie wordt beschreven hoe toocreate containers en geef Hallo doorvoer en partitie sleuteldefinitie in elk Hallo API's ondersteund.

### <a name="documentdb-api"></a>DocumentDB-API
Hallo volgende voorbeeld ziet u hoe een container (verzameling) met toocreate Hallo DocumentDB-API. U vindt meer informatie in [partitioneren met DocumentDB API](partition-data.md).

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

Vindt u een item (document) met behulp van Hallo `GET` methode in Hallo REST-API of met behulp van `ReadDocumentAsync` in een Hallo SDK's.

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>MongoDB-API
Met de Hallo MongoDB-API, kunt u een verzameling shard via uw favoriete hulpprogramma, het stuurprogramma of de SDK. In dit voorbeeld gebruiken we Hallo Mongo-Shell voor het maken van de verzameling Hallo.

Hallo Mongo-Shell in:

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

Met Hallo tabel API u Hallo doorvoer voor tabellen in Hallo appSettings-configuratie voor uw toepassing:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Vervolgens maakt u een tabel met hello Azure Table storage SDK. Hallo partitiesleutel is impliciet gemaakt als Hallo `PartitionKey` waarde. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

U kunt met behulp van de volgende codefragment Hallo één entiteit ophalen:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Zie [ontwikkelen met Hallo tabel API](tutorial-develop-table-dotnet.md) voor meer informatie.

### <a name="graph-api"></a>Graph API

Met de Hallo Graph API, moet u hello Azure-portal of CLI toocreate containers. U kunt ook omdat Azure Cosmos DB met meerdere modellen, kunt u een Hallo andere toocreate modellen en schalen van uw grafiek container.

U kunt geen hoekpunt of edge met Hallo partitiesleutel en -id in Gremlin lezen. Voor een grafiek met regio ('VS') als partitiesleutel Hallo en "Seattle" Als de rijsleutel hello, kunt u bijvoorbeeld een hoekpunt met behulp van de volgende syntaxis Hallo vinden:

```
g.V(['USA', 'Seattle'])
```

Dezelfde met randen, u kunt verwijzen naar een edge met behulp van de partitiesleutel Hallo en rijsleutel.

```
g.E(['USA', 'I5'])
```

Zie [Gremlin ondersteuning voor Cosmos DB](gremlin-support.md) voor meer informatie.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Ontwerpen voor het partitioneren
tooscale effectief met Azure Cosmos DB, moet u een goede partitiesleutel toopick wanneer u de container maken. Er zijn twee belangrijke overwegingen voor het kiezen van een partitiesleutel:

* **Grens voor query's en transacties**: uw keuze van partitiesleutel moet worden verdeeld Hallo tooenable Hallo moet het gebruik van transacties tegen Hallo vereiste toodistribute uw entiteiten meerdere partitie sleutels tooensure schaalbare oplossing. Op één extreme, kunt u instellen Hallo dezelfde partitiesleutel voor alle objecten, maar dit Hallo schaalbaarheid van uw oplossing kan beperken. Op Hallo andere extreme, kunt u een unieke partitiesleutel voor elk item dat is zeer schaalbaar, maar zou voorkomen dat u over verschillende document transacties via opgeslagen procedures en triggers toewijzen. Een ideaal partitiesleutel is een waarmee u toouse efficiënt query's en met voldoende kardinaliteit tooensure uw oplossing schaalbaar is. 
* **Er is geen opslag en prestaties knelpunten**: het is belangrijk een eigenschap waarmee toopick schrijft toobe verdeeld over verschillende afzonderlijke waarden. Aanvragen toohello dezelfde partitiesleutel mag niet langer dan de doorvoer Hallo van één partitie en zijn beperkt. Het is daarom belangrijk toopick partitiesleutel niet in 'hotspots' in uw toepassing resulteert. Omdat alle Hallo-gegevens voor een sleutel met één partitie moet worden opgeslagen in een partitie ook verdient tooavoid partitiesleutels waarvoor grote hoeveelheden gegevens voor Hallo dezelfde waarde. 

Bekijk enkele praktijkscenario's en goede partitiesleutels voor elk:
* Als u een back-end gebruiker profiel implementeren, is een goede keuze voor partitiesleutel met Hallo gebruikers-ID.
* Als u IoT gegevens bijvoorbeeld de status van het apparaat opslaat, wordt door een apparaat-ID een goede keuze voor de partitiesleutel is.
* Als u van Azure DB die Cosmos gebruikmaakt voor logboekregistratie timeseries gegevens, vervolgens Hallo hostnaam of proces-ID is een goede keuze voor partitiesleutel.
* Als u een architectuur met meerdere tenants hebt, is Hallo tenant-ID een goede keuze voor partitiesleutel.

In sommige gevallen, zoals IoT en gebruikersprofielen, Hallo partitiesleutel mogelijk gebruik Hallo u dezelfde als uw id (documentsleutel). In andere gevallen zoals Hallo tijd reeksgegevens wellicht u een partitiesleutel die anders is dan het Hallo-id.

### <a name="partitioning-and-loggingtime-series-data"></a>Partitionering en logboekregistratie-tijdreeks gegevens
Een van de algemene gebruiksvoorbeelden Hallo van Cosmos-database is voor logboekregistratie en telemetrie. Het is belangrijk toopick een goede partitiesleutel aangezien u tooread schrijftijd enorme hoeveelheden gegevens wellicht. Hallo keuze is afhankelijk van uw lezen en schrijven tarieven en typen query's die u toorun verwacht. Hier volgen enkele tips voor het toochoose een goede partitiesleutel.

* Als uw gebruiksvoorbeeld een klein aantal omvat schrijft opgebouwd gedurende een langere periode van de tijd moet tooquery door bereiken van tijdstempels en andere filters en vervolgens met behulp van een updatepakket van het Hallo timestamp, bijvoorbeeld als een partitiesleutel is een goede benadering datum. Hiermee kunt u tooquery via alle Hallo-gegevens voor een datum van één partitie. 
* Als uw werkbelasting is geschreven zware die veelvoorkomende, moet u een partitiesleutel die niet gebaseerd op tijdstempel zodat Cosmos DB schrijfbewerkingen meerdere verschillende partities verdelen kunt. Een hostnaam, proces-ID, activiteits-ID of een andere eigenschap met hoge kardinaliteit is hier een goede keuze. 
* Een derde aanpak is een hybride een wanneer u meerdere containers, één voor elke dag/maand werkt en Hallo partitiesleutel is een gedetailleerd eigenschap als de hostnaam. Hallo voordeel die u kunt verschillende doorvoer op basis van het tijdvenster Hallo instellen is, bijvoorbeeld Hallo-container voor de huidige maand Hallo is ingericht met hogere doorvoer omdat dit lees- en schrijfbewerkingen, terwijl de voorafgaande maanden met lagere doorvoer sinds ze bedienen leest alleen.

### <a name="partitioning-and-multi-tenancy"></a>Partitionering en multi-tenancymodus
Als u een multitenant-toepassing met behulp van de Cosmos-DB implementeert, zijn er twee populaire patronen – een partitiesleutel per tenant en een container per tenant. Hier volgen Hallo-voor- en nadelen voor elk:

* Een partitiesleutel per tenant: In dit model tenants binnen een enkele container worden geplaatst. Maar query's en voegt voor items binnen een enkele tenant kunnen worden uitgevoerd op een enkele partitie. U kunt ook transactionele logica implementeren voor alle items in een tenant. Omdat meerdere tenants een container delen, kunt u opslag en doorvoer kosten besparen door groeperen van bronnen voor tenants binnen een enkele container dan extra ruimte voor elke tenant wordt ingericht. Hallo nadeel is dat u geen isolatie van de prestaties per tenant hebt. Prestaties/doorvoer toeneemt toepassing toohello volledige container tegenover gericht toeneemt voor tenants.
* Een Container per tenant: elke tenant heeft zijn eigen container. In dit model, kunt u de prestaties per tenant reserveren. Dit model is met het Cosmos-database nieuwe leveren prijzen model, rendabeler voor multitenant-toepassingen met een paar tenants.

U kunt ook een combinatie/gelaagde benadering die kleine tenants collocates en grotere tenants tootheir eigen container wordt gemigreerd.

## <a name="next-steps"></a>Volgende stappen
In dit artikel wordt een overzicht opgegeven voor een overzicht van de concepten en aanbevolen procedures voor het partitioneren van Azure Cosmos DB API. 

* Meer informatie over [ingerichte doorvoer in Azure Cosmos-DB](request-units.md)
* Meer informatie over [globale distributie in Azure Cosmos-DB](distribute-data-globally.md)



