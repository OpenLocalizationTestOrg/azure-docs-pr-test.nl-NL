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
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="16555-103">Azure Cosmos DB: Ontwikkelen met Hallo Graph API in .NET</span><span class="sxs-lookup"><span data-stu-id="16555-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="16555-104">Azure Cosmos-database is de service van Microsoft wereldwijd gedistribueerde database voor meerdere model.</span><span class="sxs-lookup"><span data-stu-id="16555-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="16555-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="16555-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="16555-106">Deze zelfstudie laat zien hoe toocreate een Azure DB die Cosmos-account met hello Azure-portal en hoe toocreate een graph-database en de container.</span><span class="sxs-lookup"><span data-stu-id="16555-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="16555-107">Hallo toepassing wordt vervolgens een eenvoudige sociaal netwerk maakt met vier mensen met Hallo [Graph API](graph-sdk-dotnet.md) (preview) en vervolgens passeert en query's met behulp van Gremlin Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="16555-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="16555-108">Deze zelfstudie behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="16555-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="16555-109">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="16555-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="16555-110">Een database van de grafiek en een container maken</span><span class="sxs-lookup"><span data-stu-id="16555-110">Create a graph database and container</span></span>
> * <span data-ttu-id="16555-111">Hoekpunten en randen too.NET objecten serialiseren</span><span class="sxs-lookup"><span data-stu-id="16555-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="16555-112">Hoekpunten en randen toevoegen</span><span class="sxs-lookup"><span data-stu-id="16555-112">Add vertices and edges</span></span>
> * <span data-ttu-id="16555-113">Query Hallo grafiek met Gremlin</span><span class="sxs-lookup"><span data-stu-id="16555-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="16555-114">De grafieken in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="16555-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="16555-115">U kunt Azure Cosmos DB toocreate-, update- en query-grafieken met Hallo [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="16555-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="16555-116">Hallo Microsoft.Azure.Graph-bibliotheek biedt een enkel extensiemethode `CreateGremlinQuery<T>` boven op Hallo `DocumentClient` klasse tooexecute Gremlin query's.</span><span class="sxs-lookup"><span data-stu-id="16555-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="16555-117">Gremlin is een functionele programmeertaal die ondersteuning biedt voor schrijven bewerkingen (DML) en query's en traversal bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="16555-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="16555-118">We enkele voorbeelden in dit artikel tooget uw gestart met Gremlin uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="16555-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="16555-119">Zie [Gremlin query's](gremlin-support.md) voor een gedetailleerd overzicht van Gremlin mogelijkheden beschikbaar zijn in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="16555-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="16555-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="16555-120">Prerequisites</span></span>
<span data-ttu-id="16555-121">Controleer of dat u de volgende Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="16555-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="16555-122">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="16555-122">An active Azure account.</span></span> <span data-ttu-id="16555-123">Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="16555-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="16555-124">U kunt ook hello gebruiken [Azure DocumentDB Emulator](local-emulator.md) voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="16555-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="16555-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="16555-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="16555-126">Databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="16555-126">Create database account</span></span>

<span data-ttu-id="16555-127">Begint met het maken van een Azure DB die Cosmos-account in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="16555-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="16555-128">Hebt u al een Azure DB die Cosmos-account?</span><span class="sxs-lookup"><span data-stu-id="16555-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="16555-129">Als dit het geval is, gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="16555-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="16555-130">Hebt u een Azure-DocumentDB-account?</span><span class="sxs-lookup"><span data-stu-id="16555-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="16555-131">Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan te[instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="16555-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="16555-132">Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="16555-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="16555-133"><a id="SetupVS"></a>Uw Visual Studio-oplossing instellen</span><span class="sxs-lookup"><span data-stu-id="16555-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="16555-134">Open **Visual Studio** op uw computer.</span><span class="sxs-lookup"><span data-stu-id="16555-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="16555-135">Op Hallo **bestand** selecteert u **nieuw**, en kies vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="16555-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="16555-136">In Hallo **nieuw Project** dialoogvenster Selecteer **sjablonen** / **Visual C#** / **Console-App (.NET Framework)**, Geef uw project en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="16555-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="16555-137">In Hallo **Solution Explorer**, klik met de rechtermuisknop op uw nieuwe consoletoepassing die zich onder uw Visual Studio-oplossing, en klik vervolgens op **NuGet-pakketten beheren...**</span><span class="sxs-lookup"><span data-stu-id="16555-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="16555-138">In Hallo **NuGet** tabblad **Bladeren**, en het type **Microsoft.Azure.Graphs** in het zoekvak Hallo en controle Hallo **voorlopige versiesopnemen**.</span><span class="sxs-lookup"><span data-stu-id="16555-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="16555-139">Binnen Hallo resultaten vinden **Microsoft.Azure.Graphs** en klik op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="16555-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="16555-140">Als u een bericht krijgt over het controleren van wijzigingen toohello oplossing, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="16555-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="16555-141">Als u een bericht ontvangt over het accepteren van de licentie, klikt u op **Accepteren**.</span><span class="sxs-lookup"><span data-stu-id="16555-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="16555-142">Hallo `Microsoft.Azure.Graphs` -bibliotheek biedt een enkel uitbreidingsmethode `CreateGremlinQuery<T>` voor het uitvoeren van bewerkingen Gremlin.</span><span class="sxs-lookup"><span data-stu-id="16555-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="16555-143">Gremlin is een functionele programmeertaal die ondersteuning biedt voor schrijven bewerkingen (DML) en query's en traversal bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="16555-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="16555-144">We enkele voorbeelden in dit artikel tooget uw gestart met Gremlin uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="16555-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="16555-145">[Query's gremlin](gremlin-support.md) heeft een gedetailleerd overzicht van Gremlin mogelijkheden in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="16555-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="16555-146"><a id="add-references"></a>Verbinding maken met uw app</span><span class="sxs-lookup"><span data-stu-id="16555-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="16555-147">Deze twee constanten toevoegen en uw *client* variabele in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="16555-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="16555-148">Vervolgens head back-toohello [Azure-portal](https://portal.azure.com) tooretrieve uw eindpunt-URL en de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="16555-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="16555-149">Hallo eindpunt-URL en de primaire sleutel nodig zijn om uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding.</span><span class="sxs-lookup"><span data-stu-id="16555-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="16555-150">In hello Azure-portal, gaat u tooyour Azure DB die Cosmos-account, klikt u op **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**.</span><span class="sxs-lookup"><span data-stu-id="16555-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="16555-151">Hallo URI van de portal Hallo kopiëren en plakken via `Endpoint` in bovenstaande Hallo endpoint-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="16555-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="16555-152">Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plak deze in Hallo `AuthKey` eigenschap hierboven.</span><span class="sxs-lookup"><span data-stu-id="16555-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="16555-153">! [Schermopname van hello Azure-portal gebruikt door de zelfstudie toocreate Hallo een C#-toepassing.</span><span class="sxs-lookup"><span data-stu-id="16555-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="16555-154">Toont een Cosmos-DB Azure account Hallo knop sleutels gemarkeerd op Hallo Azure Cosmos DB navigatie en de waarden URI en primaire sleutel Hallo gemarkeerd op Hallo blade sleutels] [keys]</span><span class="sxs-lookup"><span data-stu-id="16555-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="16555-155"><a id="instantiate"></a>Hallo DocumentClient instantiëren</span><span class="sxs-lookup"><span data-stu-id="16555-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="16555-156">Maak vervolgens een nieuw exemplaar van Hallo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="16555-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="16555-157"><a id="create-database"></a>Een database maken</span><span class="sxs-lookup"><span data-stu-id="16555-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="16555-158">Maak nu een Cosmos Azure DB [database](documentdb-resources.md#databases) met behulp van Hallo [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) methode of [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) methode Hallo  **DocumentClient** klasse vanuit Hallo [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="16555-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="16555-159">Een grafiek maken</span><span class="sxs-lookup"><span data-stu-id="16555-159">Create a graph</span></span> 

<span data-ttu-id="16555-160">Maak vervolgens een grafiek container door gebruik te maken met behulp van Hallo Hallo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) methode of [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) methode Hallo **DocumentClient**  klasse.</span><span class="sxs-lookup"><span data-stu-id="16555-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="16555-161">Een verzameling is een container van grafiek entiteiten.</span><span class="sxs-lookup"><span data-stu-id="16555-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="16555-162"><a id="serializing"></a>Hoekpunten en randen too.NET objecten serialiseren</span><span class="sxs-lookup"><span data-stu-id="16555-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="16555-163">Gebruikt Azure Cosmos-DB Hallo [GraphSON draadindeling](gremlin-support.md), definieert een JSON-schema voor hoekpunten, randen en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="16555-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="16555-164">Hello Azure Cosmos DB .NET SDK omvat JSON.NET als een afhankelijkheid, en deze manier kunnen wij tooserialize/deserialiseren GraphSON in .NET-objecten waarmee we in de code kunt werken.</span><span class="sxs-lookup"><span data-stu-id="16555-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="16555-165">Als voorbeeld gaan we werken met een eenvoudige sociaal netwerk met vier mensen.</span><span class="sxs-lookup"><span data-stu-id="16555-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="16555-166">Kijken we hoe toocreate `Person` hoekpunten, toevoegen `Knows` relaties tussen deze twee, en vervolgens een query en kunt doorlopen Hallo grafiek toofind 'friend van vriend'-relaties.</span><span class="sxs-lookup"><span data-stu-id="16555-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="16555-167">Hallo `Microsoft.Azure.Graphs.Elements` naamruimte biedt `Vertex`, `Edge`, `Property` en `VertexProperty` klassen voor het deserialiseren van GraphSON antwoorden toowell gedefinieerde .NET-objecten.</span><span class="sxs-lookup"><span data-stu-id="16555-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="16555-168">Met behulp van CreateGremlinQuery Gremlin uitvoeren</span><span class="sxs-lookup"><span data-stu-id="16555-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="16555-169">Gremlin, zoals SQL, biedt ondersteuning voor lezen, schrijven en querybewerkingen.</span><span class="sxs-lookup"><span data-stu-id="16555-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="16555-170">Bijvoorbeeld: hello volgende fragment toont hoe toocreate hoekpunten, randen, voeren sommige voorbeeldquery's met behulp van `CreateGremlinQuery<T>`, en doorlopen asynchroon deze resultaten met `ExecuteNextAsync` en ' HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="16555-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

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

## <a name="add-vertices-and-edges"></a><span data-ttu-id="16555-171">Hoekpunten en randen toevoegen</span><span class="sxs-lookup"><span data-stu-id="16555-171">Add vertices and edges</span></span>

<span data-ttu-id="16555-172">We Hallo Gremlin instructies wordt weergegeven in de voorgaande sectie Hallo nader bekijken.</span><span class="sxs-lookup"><span data-stu-id="16555-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="16555-173">Eerste we enkele hoekpunten met behulp van Gremlin `addV` methode.</span><span class="sxs-lookup"><span data-stu-id="16555-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="16555-174">Hallo maakt volgende codefragment u bijvoorbeeld een hoekpunt 'Thomas Andersen' van het type 'Persoon' met eigenschappen voor de voornaam en achternaam leeftijd.</span><span class="sxs-lookup"><span data-stu-id="16555-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

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

<span data-ttu-id="16555-175">Vervolgens maken we enkele randen tussen deze hoekpunten met behulp van Gremlin `addE` methode.</span><span class="sxs-lookup"><span data-stu-id="16555-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

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

<span data-ttu-id="16555-176">We een bestaande hoekpunt kunt bijwerken met behulp van `properties` stap in Gremlin.</span><span class="sxs-lookup"><span data-stu-id="16555-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="16555-177">We Hallo aanroep tooexecute Hallo query via overslaan `HasMoreResults` en `ExecuteNextAsync` voor Hallo rest Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="16555-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="16555-178">U kunt neerzetten randen en hoekpunten met behulp van Gremlin `drop` stap.</span><span class="sxs-lookup"><span data-stu-id="16555-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="16555-179">Hier volgt een codefragment die laat zien hoe toodelete een hoekpunt en een rand.</span><span class="sxs-lookup"><span data-stu-id="16555-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="16555-180">Opmerking die u verwijdert een hoekpunt een trapsgewijze delete Hallo uitvoert randen gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="16555-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="16555-181">Query Hallo grafiek</span><span class="sxs-lookup"><span data-stu-id="16555-181">Query hello graph</span></span>

<span data-ttu-id="16555-182">U kunt query's en traversals ook met Gremlin uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="16555-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="16555-183">Hallo codefragment volgende wordt bijvoorbeeld getoond hoe toocount aantal hoekpunten in de grafiek Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="16555-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="16555-184">U kunt uitvoeren met behulp van Gremlin filters `has` en `hasLabel` stappen en deze te combineren met `and`, `or`, en `not` toobuild complexer filtert:</span><span class="sxs-lookup"><span data-stu-id="16555-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="16555-185">U kunt bepaalde eigenschappen in queryresultaten Hallo Hallo met projecteren `values` stap:</span><span class="sxs-lookup"><span data-stu-id="16555-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="16555-186">Tot nu toe hebt we alleen query's die in elke database werken gezien.</span><span class="sxs-lookup"><span data-stu-id="16555-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="16555-187">Grafieken zijn snelle en efficiënte voor traversal bewerkingen wanneer u toonavigate toorelated randen en hoekpunten nodig.</span><span class="sxs-lookup"><span data-stu-id="16555-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="16555-188">We vinden alle vrienden of van Thomas.</span><span class="sxs-lookup"><span data-stu-id="16555-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="16555-189">We doen dit met behulp van Gremlin `outE` toofind alle Hallo uitgaande van Thomas randen stap en klik vervolgens in hoekpunten toohello doorlopen van de randen van Gremlin met `inV` stap:</span><span class="sxs-lookup"><span data-stu-id="16555-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="16555-190">de volgende query Hallo voert twee hops toofind alle Thomas 'vrienden of van vrienden ', door het aanroepen van `outE` en `inV` twee keer.</span><span class="sxs-lookup"><span data-stu-id="16555-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="16555-191">Kunt u complexere query's maken en implementeren van krachtige grafiek traversal logica met Gremlin, inclusief groeperen filter expressies uitvoeren met behulp van lussen Hallo `loop` stap en uitvoering voorwaardelijke navigatie met Hallo `choose` stap.</span><span class="sxs-lookup"><span data-stu-id="16555-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="16555-192">Meer informatie over wat u met doen kunt [Gremlin ondersteuning](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="16555-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="16555-193">Deze zelfstudie Azure Cosmos DB is voltooid, dat is alles!</span><span class="sxs-lookup"><span data-stu-id="16555-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="16555-194">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="16555-194">Clean up resources</span></span>

<span data-ttu-id="16555-195">Als u deze app niet toocontinue toouse gaat, gebruikt u Hallo stappen toodelete alle resources die zijn gemaakt met deze zelfstudie in hello Azure-portal te volgen.</span><span class="sxs-lookup"><span data-stu-id="16555-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="16555-196">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16555-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="16555-197">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="16555-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16555-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16555-198">Next Steps</span></span>

<span data-ttu-id="16555-199">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="16555-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="16555-200">Een Azure DB die Cosmos-account gemaakt</span><span class="sxs-lookup"><span data-stu-id="16555-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="16555-201">Een grafiek database en de container gemaakt</span><span class="sxs-lookup"><span data-stu-id="16555-201">Created a graph database and container</span></span>
> * <span data-ttu-id="16555-202">Geserialiseerde hoekpunten en randen too.NET objecten</span><span class="sxs-lookup"><span data-stu-id="16555-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="16555-203">Toegevoegde hoekpunten en randen</span><span class="sxs-lookup"><span data-stu-id="16555-203">Added vertices and edges</span></span>
> * <span data-ttu-id="16555-204">De query Hallo grafiek met Gremlin</span><span class="sxs-lookup"><span data-stu-id="16555-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="16555-205">U kunt nu complexere query's maken en met Gremlin krachtige logica implementeren om door een graaf te gaan.</span><span class="sxs-lookup"><span data-stu-id="16555-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="16555-206">Query’s uitvoeren met Gremlin</span><span class="sxs-lookup"><span data-stu-id="16555-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
