---
title: 'Azure Cosmos DB: Ontwikkelen met Hallo Graph API in .NET | Microsoft Docs'
description: Meer informatie over hoe toodevelop met DocumentDB-API van Azure Cosmos DB met .NET
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Azure Cosmos DB: Ontwikkelen met Hallo Graph API in .NET
Azure Cosmos-database is de service van Microsoft wereldwijd gedistribueerde database voor meerdere model. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze zelfstudie laat zien hoe toocreate een Azure DB die Cosmos-account met hello Azure-portal en hoe toocreate een graph-database en de container. Hallo toepassing wordt vervolgens een eenvoudige sociaal netwerk maakt met vier mensen met Hallo [Graph API](graph-sdk-dotnet.md) (preview) en vervolgens passeert en query's met behulp van Gremlin Hallo-grafiek.

Deze zelfstudie behandelt Hallo taken te volgen:

> [!div class="checklist"]
> * Maak een Azure Cosmos DB-account 
> * Een database van de grafiek en een container maken
> * Hoekpunten en randen too.NET objecten serialiseren
> * Hoekpunten en randen toevoegen
> * Query Hallo grafiek met Gremlin

## <a name="graphs-in-azure-cosmos-db"></a>De grafieken in Azure Cosmos DB
U kunt Azure Cosmos DB toocreate-, update- en query-grafieken met Hallo [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) bibliotheek. Hallo Microsoft.Azure.Graph-bibliotheek biedt een enkel extensiemethode `CreateGremlinQuery<T>` boven op Hallo `DocumentClient` klasse tooexecute Gremlin query's.

Gremlin is een functionele programmeertaal die ondersteuning biedt voor schrijven bewerkingen (DML) en query's en traversal bewerkingen. We enkele voorbeelden in dit artikel tooget uw gestart met Gremlin uitgelegd. Zie [Gremlin query's](gremlin-support.md) voor een gedetailleerd overzicht van Gremlin mogelijkheden beschikbaar zijn in Azure Cosmos DB. 

## <a name="prerequisites"></a>Vereisten
Controleer of dat u de volgende Hallo hebt:

* Een actief Azure-account. Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/). 
    * U kunt ook hello gebruiken [Azure DocumentDB Emulator](local-emulator.md) voor deze zelfstudie.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-database-account"></a>Databaseaccount maken

Begint met het maken van een Azure DB die Cosmos-account in hello Azure-portal.  

> [!TIP]
> * Hebt u al een Azure DB die Cosmos-account? Als dit het geval is, gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS)
> * Hebt u een Azure-DocumentDB-account? Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan te[instellen van uw Visual Studio-oplossing](#SetupVS).  
> * Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS). 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Uw Visual Studio-oplossing instellen
1. Open **Visual Studio** op uw computer.
2. Op Hallo **bestand** selecteert u **nieuw**, en kies vervolgens **Project**.
3. In Hallo **nieuw Project** dialoogvenster Selecteer **sjablonen** / **Visual C#** / **Console-App (.NET Framework)**, Geef uw project en klik vervolgens op **OK**.
4. In Hallo **Solution Explorer**, klik met de rechtermuisknop op uw nieuwe consoletoepassing die zich onder uw Visual Studio-oplossing, en klik vervolgens op **NuGet-pakketten beheren...**
5. In Hallo **NuGet** tabblad **Bladeren**, en het type **Microsoft.Azure.Graphs** in het zoekvak Hallo en controle Hallo **voorlopige versiesopnemen**.
6. Binnen Hallo resultaten vinden **Microsoft.Azure.Graphs** en klik op **installeren**.
   
   Als u een bericht krijgt over het controleren van wijzigingen toohello oplossing, klikt u op **OK**. Als u een bericht ontvangt over het accepteren van de licentie, klikt u op **Accepteren**.
   
    Hallo `Microsoft.Azure.Graphs` -bibliotheek biedt een enkel uitbreidingsmethode `CreateGremlinQuery<T>` voor het uitvoeren van bewerkingen Gremlin. Gremlin is een functionele programmeertaal die ondersteuning biedt voor schrijven bewerkingen (DML) en query's en traversal bewerkingen. We enkele voorbeelden in dit artikel tooget uw gestart met Gremlin uitgelegd. [Query's gremlin](gremlin-support.md) heeft een gedetailleerd overzicht van Gremlin mogelijkheden in Azure Cosmos DB.

## <a id="add-references"></a>Verbinding maken met uw app

Deze twee constanten toevoegen en uw *client* variabele in uw toepassing. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
Vervolgens head back-toohello [Azure-portal](https://portal.azure.com) tooretrieve uw eindpunt-URL en de primaire sleutel. Hallo eindpunt-URL en de primaire sleutel nodig zijn om uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding. 

In hello Azure-portal, gaat u tooyour Azure DB die Cosmos-account, klikt u op **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**. 

Hallo URI van de portal Hallo kopiëren en plakken via `Endpoint` in bovenstaande Hallo endpoint-eigenschap. Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plak deze in Hallo `AuthKey` eigenschap hierboven. 

! [Schermopname van hello Azure-portal gebruikt door de zelfstudie toocreate Hallo een C#-toepassing. Toont een Cosmos-DB Azure account Hallo knop sleutels gemarkeerd op Hallo Azure Cosmos DB navigatie en de waarden URI en primaire sleutel Hallo gemarkeerd op Hallo blade sleutels] [keys] 
 
## <a id="instantiate"></a>Hallo DocumentClient instantiëren 
Maak vervolgens een nieuw exemplaar van Hallo **DocumentClient**.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>Een database maken 

Maak nu een Cosmos Azure DB [database](documentdb-resources.md#databases) met behulp van Hallo [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) methode of [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) methode Hallo  **DocumentClient** klasse vanuit Hallo [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>Een grafiek maken 

Maak vervolgens een grafiek container door gebruik te maken met behulp van Hallo Hallo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) methode of [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) methode Hallo **DocumentClient**  klasse. Een verzameling is een container van grafiek entiteiten. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>Hoekpunten en randen too.NET objecten serialiseren
Gebruikt Azure Cosmos-DB Hallo [GraphSON draadindeling](gremlin-support.md), definieert een JSON-schema voor hoekpunten, randen en eigenschappen. Hello Azure Cosmos DB .NET SDK omvat JSON.NET als een afhankelijkheid, en deze manier kunnen wij tooserialize/deserialiseren GraphSON in .NET-objecten waarmee we in de code kunt werken.

Als voorbeeld gaan we werken met een eenvoudige sociaal netwerk met vier mensen. Kijken we hoe toocreate `Person` hoekpunten, toevoegen `Knows` relaties tussen deze twee, en vervolgens een query en kunt doorlopen Hallo grafiek toofind 'friend van vriend'-relaties. 

Hallo `Microsoft.Azure.Graphs.Elements` naamruimte biedt `Vertex`, `Edge`, `Property` en `VertexProperty` klassen voor het deserialiseren van GraphSON antwoorden toowell gedefinieerde .NET-objecten.

## <a name="run-gremlin-using-creategremlinquery"></a>Met behulp van CreateGremlinQuery Gremlin uitvoeren
Gremlin, zoals SQL, biedt ondersteuning voor lezen, schrijven en querybewerkingen. Bijvoorbeeld: hello volgende fragment toont hoe toocreate hoekpunten, randen, voeren sommige voorbeeldquery's met behulp van `CreateGremlinQuery<T>`, en doorlopen asynchroon deze resultaten met `ExecuteNextAsync` en ' HasMoreResults.

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>Hoekpunten en randen toevoegen

We Hallo Gremlin instructies wordt weergegeven in de voorgaande sectie Hallo nader bekijken. Eerste we enkele hoekpunten met behulp van Gremlin `addV` methode. Hallo maakt volgende codefragment u bijvoorbeeld een hoekpunt 'Thomas Andersen' van het type 'Persoon' met eigenschappen voor de voornaam en achternaam leeftijd.

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

Vervolgens maken we enkele randen tussen deze hoekpunten met behulp van Gremlin `addE` methode. 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

We een bestaande hoekpunt kunt bijwerken met behulp van `properties` stap in Gremlin. We Hallo aanroep tooexecute Hallo query via overslaan `HasMoreResults` en `ExecuteNextAsync` voor Hallo rest Hallo voorbeelden.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

U kunt neerzetten randen en hoekpunten met behulp van Gremlin `drop` stap. Hier volgt een codefragment die laat zien hoe toodelete een hoekpunt en een rand. Opmerking die u verwijdert een hoekpunt een trapsgewijze delete Hallo uitvoert randen gekoppeld.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>Query Hallo grafiek

U kunt query's en traversals ook met Gremlin uitvoeren. Hallo codefragment volgende wordt bijvoorbeeld getoond hoe toocount aantal hoekpunten in de grafiek Hallo Hallo:

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
U kunt uitvoeren met behulp van Gremlin filters `has` en `hasLabel` stappen en deze te combineren met `and`, `or`, en `not` toobuild complexer filtert:

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

U kunt bepaalde eigenschappen in queryresultaten Hallo Hallo met projecteren `values` stap:

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

Tot nu toe hebt we alleen query's die in elke database werken gezien. Grafieken zijn snelle en efficiënte voor traversal bewerkingen wanneer u toonavigate toorelated randen en hoekpunten nodig. We vinden alle vrienden of van Thomas. We doen dit met behulp van Gremlin `outE` toofind alle Hallo uitgaande van Thomas randen stap en klik vervolgens in hoekpunten toohello doorlopen van de randen van Gremlin met `inV` stap:

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

de volgende query Hallo voert twee hops toofind alle Thomas 'vrienden of van vrienden ', door het aanroepen van `outE` en `inV` twee keer. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

Kunt u complexere query's maken en implementeren van krachtige grafiek traversal logica met Gremlin, inclusief groeperen filter expressies uitvoeren met behulp van lussen Hallo `loop` stap en uitvoering voorwaardelijke navigatie met Hallo `choose` stap. Meer informatie over wat u met doen kunt [Gremlin ondersteuning](gremlin-support.md)!

Deze zelfstudie Azure Cosmos DB is voltooid, dat is alles! 

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, gebruikt u Hallo stappen toodelete alle resources die zijn gemaakt met deze zelfstudie in hello Azure-portal te volgen.  

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Een Azure DB die Cosmos-account gemaakt 
> * Een grafiek database en de container gemaakt
> * Geserialiseerde hoekpunten en randen too.NET objecten
> * Toegevoegde hoekpunten en randen
> * De query Hallo grafiek met Gremlin

U kunt nu complexere query's maken en met Gremlin krachtige logica implementeren om door een graaf te gaan. 

> [!div class="nextstepaction"]
> [Query’s uitvoeren met Gremlin](tutorial-query-graph.md)
