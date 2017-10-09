---
title: 'Azure Cosmos DB: Ontwikkelen met Hallo API in .NET DocumentDB | Microsoft Docs'
description: Meer informatie over hoe toodevelop met DocumentDB-API van Azure Cosmos DB met .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a>Azure CosmosDB: Ontwikkelen met Hallo DocumentDB API in .NET

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze zelfstudie laat zien hoe toocreate een Cosmos-DB Azure account met behulp van Azure-portal Hallo en maak vervolgens een documentdatabase en verzameling met een [partitiesleutel](documentdb-partition-data.md#partition-keys) met Hallo [DocumentDB .NET API](documentdb-introduction.md). Wanneer u een verzameling maakt, definieert een partitiesleutel, wordt uw toepassing voorbereid tooscale moeiteloos wanneer uw gegevens groeit. 

Deze zelfstudie behandelt Hallo volgende taken met behulp van Hallo [DocumentDB .NET API](documentdb-sdk-dotnet.md):

> [!div class="checklist"]
> * Maak een Azure Cosmos DB-account
> * Een database en verzameling maken met een partitiesleutel
> * JSON-documenten maken
> * Een document bijwerken
> * Gepartitioneerde verzamelingen opvragen
> * Opgeslagen procedures worden uitgevoerd
> * Een document verwijderen
> * Een database verwijderen

## <a name="prerequisites"></a>Vereisten
Controleer of dat u de volgende Hallo hebt:

* Een actief Azure-account. Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/). 
    * U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie als u wilt toouse een lokale omgeving waarin hello Azure DocumentDB-service voor ontwikkelingsdoeleinden worden geëmuleerd.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-an-azure-cosmos-db-account"></a>Maak een Azure Cosmos DB-account

Begint met het maken van een Azure DB die Cosmos-account in hello Azure-portal.

> [!TIP]
> * Hebt u al een Azure DB die Cosmos-account? Als dit het geval is, gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS)
> * Hebt u een Azure-DocumentDB-account? Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan te[instellen van uw Visual Studio-oplossing](#SetupVS).  
> * Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Uw Visual Studio-oplossing instellen
1. Open **Visual Studio** op uw computer.
2. Op Hallo **bestand** selecteert u **nieuw**, en kies vervolgens **Project**.
3. In Hallo **nieuw Project** dialoogvenster Selecteer **sjablonen** / **Visual C#** / **Console-App (.NET Framework)**, Geef uw project en klik vervolgens op **OK**.
   ![Schermopname van het venster Hallo-nieuw Project](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)

4. In Hallo **Solution Explorer**, klik met de rechtermuisknop op uw nieuwe consoletoepassing die zich onder uw Visual Studio-oplossing, en klik vervolgens op **NuGet-pakketten beheren...**
    
    ![Schermopname van Hallo rechts op wordt geklikt Menu voor Hallo Project](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. In Hallo **NuGet** tabblad **Bladeren**, en het type **documentdb** in het zoekvak Hallo.
<!---stopped here--->
6. Binnen Hallo resultaten vinden **Microsoft.Azure.DocumentDB** en klik op **installeren**.
   Hallo pakket-id voor hello Azure Cosmos DB-clientbibliotheek [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).
   ![Schermopname van het Hallo NuGet-Menu voor het vinden van Client-SDK van Azure Cosmos DB](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)

    Als u een bericht krijgt over het controleren van wijzigingen toohello oplossing, klikt u op **OK**. Als u een bericht ontvangt over het accepteren van de licentie, klikt u op **Accepteren**.

## <a id="Connect"></a>Verwijzingen tooyour project toevoegen
Hallo resterende stappen in deze zelfstudie Geef Hallo DocumentDB API code codefragmenten vereiste toocreate en update Azure Cosmos DB resources in uw project.

Voeg eerst deze verwijzingen tooyour-toepassing.
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <a id="add-references"></a>Verbinding maken met uw app

Vervolgens voegt u deze twee constanten en uw *client* variabele in uw toepassing.

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

Vervolgens head back-toohello [Azure-portal](https://portal.azure.com) tooretrieve uw eindpunt-URL en de primaire sleutel. Hallo eindpunt-URL en de primaire sleutel nodig zijn om uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding.

In hello Azure-portal, gaat u tooyour Azure DB die Cosmos-account, klikt u op **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**.

Hallo URI van de portal Hallo kopiëren en plakken via `<your endpoint URL>` in het bestand program.cs Hallo. Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plakt u deze via `<your primary key>`. Ervoor tooremove Hallo worden `<` en `>` van uw waarden.

![Schermopname van hello Azure-portal gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing. Ziet u een account Azure Cosmos DB met Hallo sleutels gemarkeerd op de blade-hello Azure Cosmos DB account en Hallo URI en primaire sleutel waarden die zijn gemarkeerd op de blade sleutels Hallo](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <a id="instantiate"></a>Hallo DocumentClient instantiëren

Maak nu een nieuw exemplaar van Hallo **DocumentClient**.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <a id="create-database"></a>Een database maken

Maak vervolgens een Cosmos Azure DB [database](documentdb-resources.md#databases) met behulp van Hallo [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) methode of [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) methode Hallo  **DocumentClient** klasse vanuit Hallo [DocumentDB .NET SDK](documentdb-sdk-dotnet.md). Een database is een logische container voor documentopslag, gepartitioneerd in verzamelingen JSON Hallo.

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a>Bepaal een partitiesleutel 

Verzamelingen zijn containers voor het opslaan van documenten. Ze zijn logische resources en kunnen [omvatten een of meer fysieke partities](partition-data.md). Een [partitiesleutel](documentdb-partition-data.md) is een eigenschap (of pad) in uw documenten die gebruikte toodistribute uw gegevens tussen Hallo servers of partities. Alle documenten met dezelfde partitiesleutel worden opgeslagen in Hallo Hallo dezelfde partitie. 

Bepalen van een partitiesleutel is een belangrijke beslissing toomake voordat u een verzameling maken. Partitiesleutels zijn een eigenschap (of pad) in uw documenten die kunnen worden gebruikt door Azure Cosmos DB toodistribute uw gegevens tussen meerdere servers of partities. Cosmos DB hash-waarde voor de partitiesleutel Hallo en Hallo opgedeeld resultaat toodetermine Hallo partitie in welke toostore Hallo-document gebruikt. Alle documenten met dezelfde partitiesleutel worden opgeslagen in Hallo Hallo dezelfde partitie en partitiesleutels kunnen niet worden gewijzigd zodra een verzameling is gemaakt. 

Voor deze zelfstudie gaan we tooset Hallo partitiesleutel te`/deviceId` zodanig dat alle Hallo gegevens Hallo voor één apparaat is opgeslagen in één partitie. Gewenste toochoose een partitiesleutel die een groot aantal waarden, die elk worden gebruikt op over Hallo dezelfde frequentie tooensure Cosmos DB kunt verdelen als uw gegevens groeit en de volledige doorvoer van verzameling Hallo Hallo bereiken. 

Zie voor meer informatie over partitioneren [hoe toopartition en schalen in Azure Cosmos DB?](partition-data.md) 

## <a id="CreateColl"></a>Een verzameling maken 

Nu dat we onze partitiesleutel weten `/deviceId`, kunt maken van een [verzameling](documentdb-resources.md#collections) met behulp van Hallo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) methode of [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) methode Hallo **DocumentClient** klasse. Een verzameling is een container van JSON-documenten en eventuele bijbehorende JavaScript-toepassingslogica. 

> [!WARNING]
> Maken van een verzameling heeft gevolgen, zoals u bij het reserveren van doorvoer voor Hallo toepassing toocommunicate met Azure Cosmos DB. Ga voor meer informatie naar onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

Deze methode maakt een REST-API aanroepen tooAzure Cosmos-database en service voorziet in een aantal partities op basis van de aangevraagde doorvoer Hallo Hallo. U kunt Hallo doorvoer van een verzameling wijzigen wanneer de prestaties van uw behoeften ontwikkelen met Hallo SDK of Hallo [Azure-portal](set-throughput.md).

## <a id="CreateDoc"></a>JSON-documenten maken
Laten we enkele JSON-documenten in Azure Cosmos DB invoegen. Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) methode Hallo **DocumentClient** klasse. Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud. Deze voorbeeldklasse bevat een apparaat bij het lezen en een aanroep van tooCreateDocumentAsync tooinsert een nieuw apparaat lezen in een verzameling.

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a>Gegevens lezen

We lezen Hallo document door de partitiesleutel en Id via Hallo ReadDocumentAsync methode. Opmerking dat Hallo leesbewerkingen een waarde PartitionKey bevatten (overeenkomstige toohello `x-ms-documentdb-partitionkey` aanvraagheader in Hallo REST-API).

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a>Gegevens bijwerken

Nu gaan we werken sommige gegevens via Hallo ReplaceDocumentAsync-methode.

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a>Gegevens verwijderen

U kunt nu een document door partitiesleutel en id via Hallo DeleteDocumentAsync methode verwijderen.

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a>Gepartitioneerde verzamelingen opvragen

Als u automatisch een query met gegevens in gepartitioneerde verzamelingen, Azure Cosmos DB Hallo routes query toohello partities overeenkomt toohello partitie sleutelwaarden die zijn opgegeven in het Hallo-filter (wanneer aanwezig). Deze query is bijvoorbeeld gerouteerde toojust Hallo partitie met Hallo partitiesleutel 'XMS-0001'.

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Hallo volgende query heeft geen een filter op Hallo partitiesleutel (DeviceId) en is fanned van tooall-partities waar deze wordt uitgevoerd tegen index Hallo-partitie. Opmerking u toospecify hello EnableCrossPartitionQuery hebt (`x-ms-documentdb-query-enablecrosspartition` in Hallo REST-API) toohave Hallo SDK tooexecute een query meerdere partities.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a>Parallelle queryuitvoering
Hello Azure Cosmos DB DocumentDB SDK's 1.9.0 en hierboven ondersteuning parallelle uitvoering queryopties, waarmee u kunt de lage latentie tooperform opgevraagd tegen gepartitioneerde verzamelingen, zelfs wanneer ze nodig hebben tootouch een groot aantal partities. Hallo na query is bijvoorbeeld geconfigureerde toorun parallel meerdere partities.

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
U kunt parallelle queryuitvoering beheren door afstemmen Hallo volgende parameters:

* Door in te stellen `MaxDegreeOfParallelism`, kunt u bepalen Hallo mate van parallelle uitvoering, dat wil zeggen, Hallo maximum aantal gelijktijdige netwerk verbindingen toohello verzameling van partities. Als u deze te 1 instelt, worden Hallo mate van parallelle uitvoering wordt beheerd door Hallo SDK. Als hello `MaxDegreeOfParallelism` is niet opgegeven of stel too0, de standaardwaarde hello is, zal er een netwerk met één verbinding toohello verzameling partities.
* Door in te stellen `MaxBufferedItemCount`, kunt u handelt uit query latentie en client-side geheugengebruik. Als u deze parameter of stel deze optie te-1, wordt het aantal items in de buffer opgeslagen tijdens parallelle queryuitvoering hello wordt beheerd door Hallo SDK.

Hallo gegeven dezelfde toestand van de verzameling Hallo een parallelle query retourneert resultaten in dezelfde als in seriële uitvoering volgorde Hallo. Bij het uitvoeren van een query voor cross-partitie met sorteren (ORDER BY en/of boven) hello DocumentDB SDK-Hallo query parallel meerdere partities uitgeeft en gedeeltelijk gesorteerde resulteert in een Hallo client side tooproduce globaal besteld resultaten worden samengevoegd.

## <a name="execute-stored-procedures"></a>Opgeslagen procedures worden uitgevoerd
Ten slotte kunt u atomische transacties tegen documenten met uitvoeren Hallo dezelfde apparaat-ID, bijvoorbeeld als u statistische functies onderhoudt of Hallo meest recente toestand van een apparaat in één document door toe te voegen Hallo tooyour CodeProject te volgen.

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

En dat is alles! Hallo belangrijkste onderdelen van een Azure DB die Cosmos-toepassing die gebruikmaakt van een partitie sleutel tooefficiently scale-gegevensdistributie meerdere partities zijn.  

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze zelfstudie in hello Azure-portal met Hallo stappen te volgen:

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo unieke naam van Hallo resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan: 

> [!div class="checklist"]
> * Een Azure DB die Cosmos-account gemaakt
> * Een database en verzameling gemaakt met een partitiesleutel
> * Gemaakte JSON-documenten
> * Een document wordt bijgewerkt
> * De query gepartitioneerde verzamelingen
> * Een opgeslagen procedure is uitgevoerd
> * Een document verwijderd
> * Een database wordt verwijderd

U kunt nu doorgaan toohello volgende zelfstudie en aanvullende gegevens tooyour Cosmos DB account importeren. 

> [!div class="nextstepaction"]
> [Gegevens importeren in Azure Cosmos DB](import-data.md)
