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
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="173c0-103">Azure CosmosDB: Ontwikkelen met Hallo DocumentDB API in .NET</span><span class="sxs-lookup"><span data-stu-id="173c0-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="173c0-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="173c0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="173c0-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="173c0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="173c0-106">Deze zelfstudie laat zien hoe toocreate een Cosmos-DB Azure account met behulp van Azure-portal Hallo en maak vervolgens een documentdatabase en verzameling met een [partitiesleutel](documentdb-partition-data.md#partition-keys) met Hallo [DocumentDB .NET API](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="173c0-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="173c0-107">Wanneer u een verzameling maakt, definieert een partitiesleutel, wordt uw toepassing voorbereid tooscale moeiteloos wanneer uw gegevens groeit.</span><span class="sxs-lookup"><span data-stu-id="173c0-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="173c0-108">Deze zelfstudie behandelt Hallo volgende taken met behulp van Hallo [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="173c0-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="173c0-109">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="173c0-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="173c0-110">Een database en verzameling maken met een partitiesleutel</span><span class="sxs-lookup"><span data-stu-id="173c0-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="173c0-111">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="173c0-111">Create JSON documents</span></span>
> * <span data-ttu-id="173c0-112">Een document bijwerken</span><span class="sxs-lookup"><span data-stu-id="173c0-112">Update a document</span></span>
> * <span data-ttu-id="173c0-113">Gepartitioneerde verzamelingen opvragen</span><span class="sxs-lookup"><span data-stu-id="173c0-113">Query partitioned collections</span></span>
> * <span data-ttu-id="173c0-114">Opgeslagen procedures worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="173c0-114">Run stored procedures</span></span>
> * <span data-ttu-id="173c0-115">Een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="173c0-115">Delete a document</span></span>
> * <span data-ttu-id="173c0-116">Een database verwijderen</span><span class="sxs-lookup"><span data-stu-id="173c0-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="173c0-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="173c0-117">Prerequisites</span></span>
<span data-ttu-id="173c0-118">Controleer of dat u de volgende Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="173c0-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="173c0-119">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="173c0-119">An active Azure account.</span></span> <span data-ttu-id="173c0-120">Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="173c0-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="173c0-121">U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie als u wilt toouse een lokale omgeving waarin hello Azure DocumentDB-service voor ontwikkelingsdoeleinden worden geëmuleerd.</span><span class="sxs-lookup"><span data-stu-id="173c0-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="173c0-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="173c0-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="173c0-123">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="173c0-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="173c0-124">Begint met het maken van een Azure DB die Cosmos-account in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="173c0-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="173c0-125">Hebt u al een Azure DB die Cosmos-account?</span><span class="sxs-lookup"><span data-stu-id="173c0-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="173c0-126">Als dit het geval is, gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="173c0-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="173c0-127">Hebt u een Azure-DocumentDB-account?</span><span class="sxs-lookup"><span data-stu-id="173c0-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="173c0-128">Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan te[instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="173c0-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="173c0-129">Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="173c0-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="173c0-130"><a id="SetupVS"></a>Uw Visual Studio-oplossing instellen</span><span class="sxs-lookup"><span data-stu-id="173c0-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="173c0-131">Open **Visual Studio** op uw computer.</span><span class="sxs-lookup"><span data-stu-id="173c0-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="173c0-132">Op Hallo **bestand** selecteert u **nieuw**, en kies vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="173c0-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="173c0-133">In Hallo **nieuw Project** dialoogvenster Selecteer **sjablonen** / **Visual C#** / **Console-App (.NET Framework)**, Geef uw project en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="173c0-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="173c0-134">![Schermopname van het venster Hallo-nieuw Project](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="173c0-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="173c0-135">In Hallo **Solution Explorer**, klik met de rechtermuisknop op uw nieuwe consoletoepassing die zich onder uw Visual Studio-oplossing, en klik vervolgens op **NuGet-pakketten beheren...**</span><span class="sxs-lookup"><span data-stu-id="173c0-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Schermopname van Hallo rechts op wordt geklikt Menu voor Hallo Project](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="173c0-137">In Hallo **NuGet** tabblad **Bladeren**, en het type **documentdb** in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="173c0-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="173c0-138">Binnen Hallo resultaten vinden **Microsoft.Azure.DocumentDB** en klik op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="173c0-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="173c0-139">Hallo pakket-id voor hello Azure Cosmos DB-clientbibliotheek [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="173c0-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="173c0-140">![Schermopname van het Hallo NuGet-Menu voor het vinden van Client-SDK van Azure Cosmos DB](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="173c0-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="173c0-141">Als u een bericht krijgt over het controleren van wijzigingen toohello oplossing, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="173c0-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="173c0-142">Als u een bericht ontvangt over het accepteren van de licentie, klikt u op **Accepteren**.</span><span class="sxs-lookup"><span data-stu-id="173c0-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="173c0-143"><a id="Connect"></a>Verwijzingen tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="173c0-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="173c0-144">Hallo resterende stappen in deze zelfstudie Geef Hallo DocumentDB API code codefragmenten vereiste toocreate en update Azure Cosmos DB resources in uw project.</span><span class="sxs-lookup"><span data-stu-id="173c0-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="173c0-145">Voeg eerst deze verwijzingen tooyour-toepassing.</span><span class="sxs-lookup"><span data-stu-id="173c0-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="173c0-146"><a id="add-references"></a>Verbinding maken met uw app</span><span class="sxs-lookup"><span data-stu-id="173c0-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="173c0-147">Vervolgens voegt u deze twee constanten en uw *client* variabele in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="173c0-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="173c0-148">Vervolgens head back-toohello [Azure-portal](https://portal.azure.com) tooretrieve uw eindpunt-URL en de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="173c0-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="173c0-149">Hallo eindpunt-URL en de primaire sleutel nodig zijn om uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding.</span><span class="sxs-lookup"><span data-stu-id="173c0-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="173c0-150">In hello Azure-portal, gaat u tooyour Azure DB die Cosmos-account, klikt u op **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**.</span><span class="sxs-lookup"><span data-stu-id="173c0-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="173c0-151">Hallo URI van de portal Hallo kopiëren en plakken via `<your endpoint URL>` in het bestand program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="173c0-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="173c0-152">Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plakt u deze via `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="173c0-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="173c0-153">Ervoor tooremove Hallo worden `<` en `>` van uw waarden.</span><span class="sxs-lookup"><span data-stu-id="173c0-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![Schermopname van hello Azure-portal gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="173c0-156"><a id="instantiate"></a>Hallo DocumentClient instantiëren</span><span class="sxs-lookup"><span data-stu-id="173c0-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="173c0-157">Maak nu een nieuw exemplaar van Hallo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="173c0-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="173c0-158"><a id="create-database"></a>Een database maken</span><span class="sxs-lookup"><span data-stu-id="173c0-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="173c0-159">Maak vervolgens een Cosmos Azure DB [database](documentdb-resources.md#databases) met behulp van Hallo [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) methode of [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) methode Hallo  **DocumentClient** klasse vanuit Hallo [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="173c0-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="173c0-160">Een database is een logische container voor documentopslag, gepartitioneerd in verzamelingen JSON Hallo.</span><span class="sxs-lookup"><span data-stu-id="173c0-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="173c0-161">Bepaal een partitiesleutel</span><span class="sxs-lookup"><span data-stu-id="173c0-161">Decide on a partition key</span></span> 

<span data-ttu-id="173c0-162">Verzamelingen zijn containers voor het opslaan van documenten.</span><span class="sxs-lookup"><span data-stu-id="173c0-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="173c0-163">Ze zijn logische resources en kunnen [omvatten een of meer fysieke partities](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="173c0-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="173c0-164">Een [partitiesleutel](documentdb-partition-data.md) is een eigenschap (of pad) in uw documenten die gebruikte toodistribute uw gegevens tussen Hallo servers of partities.</span><span class="sxs-lookup"><span data-stu-id="173c0-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="173c0-165">Alle documenten met dezelfde partitiesleutel worden opgeslagen in Hallo Hallo dezelfde partitie.</span><span class="sxs-lookup"><span data-stu-id="173c0-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="173c0-166">Bepalen van een partitiesleutel is een belangrijke beslissing toomake voordat u een verzameling maken.</span><span class="sxs-lookup"><span data-stu-id="173c0-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="173c0-167">Partitiesleutels zijn een eigenschap (of pad) in uw documenten die kunnen worden gebruikt door Azure Cosmos DB toodistribute uw gegevens tussen meerdere servers of partities.</span><span class="sxs-lookup"><span data-stu-id="173c0-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="173c0-168">Cosmos DB hash-waarde voor de partitiesleutel Hallo en Hallo opgedeeld resultaat toodetermine Hallo partitie in welke toostore Hallo-document gebruikt.</span><span class="sxs-lookup"><span data-stu-id="173c0-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="173c0-169">Alle documenten met dezelfde partitiesleutel worden opgeslagen in Hallo Hallo dezelfde partitie en partitiesleutels kunnen niet worden gewijzigd zodra een verzameling is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="173c0-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="173c0-170">Voor deze zelfstudie gaan we tooset Hallo partitiesleutel te`/deviceId` zodanig dat alle Hallo gegevens Hallo voor één apparaat is opgeslagen in één partitie.</span><span class="sxs-lookup"><span data-stu-id="173c0-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="173c0-171">Gewenste toochoose een partitiesleutel die een groot aantal waarden, die elk worden gebruikt op over Hallo dezelfde frequentie tooensure Cosmos DB kunt verdelen als uw gegevens groeit en de volledige doorvoer van verzameling Hallo Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="173c0-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="173c0-172">Zie voor meer informatie over partitioneren [hoe toopartition en schalen in Azure Cosmos DB?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="173c0-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="173c0-173"><a id="CreateColl"></a>Een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="173c0-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="173c0-174">Nu dat we onze partitiesleutel weten `/deviceId`, kunt maken van een [verzameling](documentdb-resources.md#collections) met behulp van Hallo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) methode of [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="173c0-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="173c0-175">Een verzameling is een container van JSON-documenten en eventuele bijbehorende JavaScript-toepassingslogica.</span><span class="sxs-lookup"><span data-stu-id="173c0-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="173c0-176">Maken van een verzameling heeft gevolgen, zoals u bij het reserveren van doorvoer voor Hallo toepassing toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="173c0-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="173c0-177">Ga voor meer informatie naar onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="173c0-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
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

<span data-ttu-id="173c0-178">Deze methode maakt een REST-API aanroepen tooAzure Cosmos-database en service voorziet in een aantal partities op basis van de aangevraagde doorvoer Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="173c0-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="173c0-179">U kunt Hallo doorvoer van een verzameling wijzigen wanneer de prestaties van uw behoeften ontwikkelen met Hallo SDK of Hallo [Azure-portal](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="173c0-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="173c0-180"><a id="CreateDoc"></a>JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="173c0-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="173c0-181">Laten we enkele JSON-documenten in Azure Cosmos DB invoegen.</span><span class="sxs-lookup"><span data-stu-id="173c0-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="173c0-182">Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="173c0-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="173c0-183">Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud.</span><span class="sxs-lookup"><span data-stu-id="173c0-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="173c0-184">Deze voorbeeldklasse bevat een apparaat bij het lezen en een aanroep van tooCreateDocumentAsync tooinsert een nieuw apparaat lezen in een verzameling.</span><span class="sxs-lookup"><span data-stu-id="173c0-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

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
## <a name="read-data"></a><span data-ttu-id="173c0-185">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="173c0-185">Read data</span></span>

<span data-ttu-id="173c0-186">We lezen Hallo document door de partitiesleutel en Id via Hallo ReadDocumentAsync methode.</span><span class="sxs-lookup"><span data-stu-id="173c0-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="173c0-187">Opmerking dat Hallo leesbewerkingen een waarde PartitionKey bevatten (overeenkomstige toohello `x-ms-documentdb-partitionkey` aanvraagheader in Hallo REST-API).</span><span class="sxs-lookup"><span data-stu-id="173c0-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="173c0-188">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="173c0-188">Update data</span></span>

<span data-ttu-id="173c0-189">Nu gaan we werken sommige gegevens via Hallo ReplaceDocumentAsync-methode.</span><span class="sxs-lookup"><span data-stu-id="173c0-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="173c0-190">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="173c0-190">Delete data</span></span>

<span data-ttu-id="173c0-191">U kunt nu een document door partitiesleutel en id via Hallo DeleteDocumentAsync methode verwijderen.</span><span class="sxs-lookup"><span data-stu-id="173c0-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="173c0-192">Gepartitioneerde verzamelingen opvragen</span><span class="sxs-lookup"><span data-stu-id="173c0-192">Query partitioned collections</span></span>

<span data-ttu-id="173c0-193">Als u automatisch een query met gegevens in gepartitioneerde verzamelingen, Azure Cosmos DB Hallo routes query toohello partities overeenkomt toohello partitie sleutelwaarden die zijn opgegeven in het Hallo-filter (wanneer aanwezig).</span><span class="sxs-lookup"><span data-stu-id="173c0-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="173c0-194">Deze query is bijvoorbeeld gerouteerde toojust Hallo partitie met Hallo partitiesleutel 'XMS-0001'.</span><span class="sxs-lookup"><span data-stu-id="173c0-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="173c0-195">Hallo volgende query heeft geen een filter op Hallo partitiesleutel (DeviceId) en is fanned van tooall-partities waar deze wordt uitgevoerd tegen index Hallo-partitie.</span><span class="sxs-lookup"><span data-stu-id="173c0-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="173c0-196">Opmerking u toospecify hello EnableCrossPartitionQuery hebt (`x-ms-documentdb-query-enablecrosspartition` in Hallo REST-API) toohave Hallo SDK tooexecute een query meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="173c0-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="173c0-197">Parallelle queryuitvoering</span><span class="sxs-lookup"><span data-stu-id="173c0-197">Parallel query execution</span></span>
<span data-ttu-id="173c0-198">Hello Azure Cosmos DB DocumentDB SDK's 1.9.0 en hierboven ondersteuning parallelle uitvoering queryopties, waarmee u kunt de lage latentie tooperform opgevraagd tegen gepartitioneerde verzamelingen, zelfs wanneer ze nodig hebben tootouch een groot aantal partities.</span><span class="sxs-lookup"><span data-stu-id="173c0-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="173c0-199">Hallo na query is bijvoorbeeld geconfigureerde toorun parallel meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="173c0-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="173c0-200">U kunt parallelle queryuitvoering beheren door afstemmen Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="173c0-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="173c0-201">Door in te stellen `MaxDegreeOfParallelism`, kunt u bepalen Hallo mate van parallelle uitvoering, dat wil zeggen, Hallo maximum aantal gelijktijdige netwerk verbindingen toohello verzameling van partities.</span><span class="sxs-lookup"><span data-stu-id="173c0-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="173c0-202">Als u deze te 1 instelt, worden Hallo mate van parallelle uitvoering wordt beheerd door Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="173c0-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="173c0-203">Als hello `MaxDegreeOfParallelism` is niet opgegeven of stel too0, de standaardwaarde hello is, zal er een netwerk met één verbinding toohello verzameling partities.</span><span class="sxs-lookup"><span data-stu-id="173c0-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="173c0-204">Door in te stellen `MaxBufferedItemCount`, kunt u handelt uit query latentie en client-side geheugengebruik.</span><span class="sxs-lookup"><span data-stu-id="173c0-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="173c0-205">Als u deze parameter of stel deze optie te-1, wordt het aantal items in de buffer opgeslagen tijdens parallelle queryuitvoering hello wordt beheerd door Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="173c0-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="173c0-206">Hallo gegeven dezelfde toestand van de verzameling Hallo een parallelle query retourneert resultaten in dezelfde als in seriële uitvoering volgorde Hallo.</span><span class="sxs-lookup"><span data-stu-id="173c0-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="173c0-207">Bij het uitvoeren van een query voor cross-partitie met sorteren (ORDER BY en/of boven) hello DocumentDB SDK-Hallo query parallel meerdere partities uitgeeft en gedeeltelijk gesorteerde resulteert in een Hallo client side tooproduce globaal besteld resultaten worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="173c0-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="173c0-208">Opgeslagen procedures worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="173c0-208">Execute stored procedures</span></span>
<span data-ttu-id="173c0-209">Ten slotte kunt u atomische transacties tegen documenten met uitvoeren Hallo dezelfde apparaat-ID, bijvoorbeeld als u statistische functies onderhoudt of Hallo meest recente toestand van een apparaat in één document door toe te voegen Hallo tooyour CodeProject te volgen.</span><span class="sxs-lookup"><span data-stu-id="173c0-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="173c0-210">En dat is alles!</span><span class="sxs-lookup"><span data-stu-id="173c0-210">And that's it!</span></span> <span data-ttu-id="173c0-211">Hallo belangrijkste onderdelen van een Azure DB die Cosmos-toepassing die gebruikmaakt van een partitie sleutel tooefficiently scale-gegevensdistributie meerdere partities zijn.</span><span class="sxs-lookup"><span data-stu-id="173c0-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="173c0-212">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="173c0-212">Clean up resources</span></span>

<span data-ttu-id="173c0-213">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze zelfstudie in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="173c0-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="173c0-214">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo unieke naam van Hallo resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="173c0-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="173c0-215">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="173c0-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="173c0-216">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="173c0-216">Next steps</span></span>

<span data-ttu-id="173c0-217">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="173c0-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="173c0-218">Een Azure DB die Cosmos-account gemaakt</span><span class="sxs-lookup"><span data-stu-id="173c0-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="173c0-219">Een database en verzameling gemaakt met een partitiesleutel</span><span class="sxs-lookup"><span data-stu-id="173c0-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="173c0-220">Gemaakte JSON-documenten</span><span class="sxs-lookup"><span data-stu-id="173c0-220">Created JSON documents</span></span>
> * <span data-ttu-id="173c0-221">Een document wordt bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="173c0-221">Updated a document</span></span>
> * <span data-ttu-id="173c0-222">De query gepartitioneerde verzamelingen</span><span class="sxs-lookup"><span data-stu-id="173c0-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="173c0-223">Een opgeslagen procedure is uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="173c0-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="173c0-224">Een document verwijderd</span><span class="sxs-lookup"><span data-stu-id="173c0-224">Deleted a document</span></span>
> * <span data-ttu-id="173c0-225">Een database wordt verwijderd</span><span class="sxs-lookup"><span data-stu-id="173c0-225">Deleted a database</span></span>

<span data-ttu-id="173c0-226">U kunt nu doorgaan toohello volgende zelfstudie en aanvullende gegevens tooyour Cosmos DB account importeren.</span><span class="sxs-lookup"><span data-stu-id="173c0-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="173c0-227">Gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="173c0-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
