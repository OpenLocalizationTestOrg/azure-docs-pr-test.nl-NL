---
title: 'Azure Cosmos DB: Een web-app met .NET bouwen en DocumentDB API Hallo | Microsoft Docs'
description: Geeft het voorbeeld van een .NET-code kunt u tooconnect tooand query hello Azure Cosmos DB DocumentDB-API
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="69677-103">Azure Cosmos DB: Een DocumentDB-API-web-app met .NET bouwen en hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="69677-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="69677-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="69677-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="69677-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="69677-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="69677-106">Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="69677-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="69677-107">U moet vervolgens bouwen en implementeren van een WebApp voor takenlijstjes gebouwd op Hallo [DocumentDB .NET API](documentdb-sdk-dotnet.md), zoals weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="69677-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![Taken-app met voorbeeldgegevens](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="69677-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="69677-109">Prerequisites</span></span>

<span data-ttu-id="69677-110">Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="69677-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="69677-111">Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.</span><span class="sxs-lookup"><span data-stu-id="69677-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="69677-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="69677-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="69677-113">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="69677-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="69677-114">Voorbeeldgegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="69677-114">Add sample data</span></span>

<span data-ttu-id="69677-115">U kunt nu gegevens tooyour nieuwe verzameling met behulp van Data Explorer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="69677-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="69677-116">In Data Explorer Hallo nieuwe database in deelvenster wordt weergegeven Hallo verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="69677-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="69677-117">Vouw Hallo **taken** database, vouw Hallo **Items** verzameling, klikt u op **documenten**, en klik vervolgens op **nieuwe documenten**.</span><span class="sxs-lookup"><span data-stu-id="69677-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Maken van nieuwe documenten in de Data Explorer in hello Azure-portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="69677-119">Voeg nu een documentverzameling toohello met Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="69677-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="69677-120">Zodra u hebt toegevoegd Hallo json toohello **documenten** tabblad **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="69677-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Kopieer in json-gegevens en klik op opslaan in Data Explorer in hello Azure-portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="69677-122">Maak een meer document waar u een unieke waarde voor Hallo invoegen en sla `id` eigenschap en andere eigenschappen Hallo wens naar wijzigen.</span><span class="sxs-lookup"><span data-stu-id="69677-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="69677-123">De nieuwe documenten kunnen elke gewenste structuur hebben, omdat in Azure Cosmos DB uw gegevens geen schema krijgen opgelegd.</span><span class="sxs-lookup"><span data-stu-id="69677-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="69677-124">U kunt uw gegevens nu query's in Data Explorer tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="69677-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="69677-125">Data Explorer gebruikt standaard `SELECT * FROM c` tooretrieve alle documenten in de verzameling hello, maar u kunt wijzigen die andere tooa [SQL-query](documentdb-sql-query.md), zoals `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn alle Hallo documenten in aflopende volgorde op basis van hun timestamp.</span><span class="sxs-lookup"><span data-stu-id="69677-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="69677-126">U kunt ook Data Explorer toocreate opgeslagen procedures, UDF's en triggers tooperform-bedrijfslogica server ook gebruiken als de doorvoer van de schaal.</span><span class="sxs-lookup"><span data-stu-id="69677-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="69677-127">Data Explorer toont alle Hallo ingebouwde programmatische toegang tot gegevens beschikbaar zijn in Hallo API's, maar biedt eenvoudige toegang tooyour gegevens in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="69677-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="69677-128">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="69677-128">Clone hello sample application</span></span>

<span data-ttu-id="69677-129">Nu gaan we tooworking met code.</span><span class="sxs-lookup"><span data-stu-id="69677-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="69677-130">We gaan een DocumentDB-API-app vanuit GitHub Hallo verbindingsreeks instellen en voer dit klonen.</span><span class="sxs-lookup"><span data-stu-id="69677-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="69677-131">U ziet hoe eenvoudig het is toowork met gegevens via een programma.</span><span class="sxs-lookup"><span data-stu-id="69677-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="69677-132">Open een git-terminalvenster zoals git bash en en `CD` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="69677-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="69677-133">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="69677-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="69677-134">Open vervolgens Hallo todo oplossingsbestand in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69677-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="69677-135">Hallo code bekijken</span><span class="sxs-lookup"><span data-stu-id="69677-135">Review hello code</span></span>

<span data-ttu-id="69677-136">We maken een kort overzicht van wat in Hallo-app gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="69677-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="69677-137">Open Hallo DocumentDBRepository.cs bestands- en u vindt dat deze regels code hello Azure Cosmos DB resources maken.</span><span class="sxs-lookup"><span data-stu-id="69677-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="69677-138">Hallo DocumentClient op regel 73 is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="69677-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="69677-139">Er wordt een nieuwe database gemaakt op regel 88.</span><span class="sxs-lookup"><span data-stu-id="69677-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="69677-140">Er wordt een nieuwe verzameling gemaakt op regel 107.</span><span class="sxs-lookup"><span data-stu-id="69677-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="69677-141">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="69677-141">Update your connection string</span></span>

<span data-ttu-id="69677-142">Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="69677-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="69677-143">In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**.</span><span class="sxs-lookup"><span data-stu-id="69677-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="69677-144">U gebruikt in web.config-bestand in de volgende stap Hallo HALLO hallo kopie knoppen aan de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="69677-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="69677-146">Open in Visual Studio-2017 Hallo web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="69677-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="69677-147">Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo Hallo eindpunt sleutelwaarde in web.config.</span><span class="sxs-lookup"><span data-stu-id="69677-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="69677-148">Vervolgens kopieert u de waarde van de primaire sleutel van Hallo-portal en maken het Hallo-waarde van Hallo authKey in web.config. U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="69677-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="69677-149">Hallo-web-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="69677-149">Run hello web app</span></span>
1. <span data-ttu-id="69677-150">In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="69677-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="69677-151">In Hallo NuGet **Bladeren** in het vak *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="69677-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="69677-152">Installeren in Hallo resultaten Hallo **Microsoft.Azure.DocumentDB** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="69677-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="69677-153">Hiermee installeert u Hallo Microsoft.Azure.DocumentDB pakket, evenals alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="69677-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="69677-154">Klik op CTRL + F5 toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="69677-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="69677-155">Uw app wordt in uw browser weergegeven.</span><span class="sxs-lookup"><span data-stu-id="69677-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="69677-156">Klik op **nieuw** in de browser Hallo en enkele nieuwe taken in uw app taak maken.</span><span class="sxs-lookup"><span data-stu-id="69677-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![Taken-app met voorbeeldgegevens](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="69677-158">U kunt nu gaat u terug tooData Explorer en Zie query, wijzigen en werken met deze nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="69677-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="69677-159">Sla's bekijken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="69677-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="69677-160">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="69677-160">Clean up resources</span></span>

<span data-ttu-id="69677-161">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="69677-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="69677-162">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="69677-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="69677-163">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="69677-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69677-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="69677-164">Next steps</span></span>

<span data-ttu-id="69677-165">In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een verzameling met Hallo Data Explorer maken en uitvoeren van een web-app.</span><span class="sxs-lookup"><span data-stu-id="69677-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="69677-166">U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren.</span><span class="sxs-lookup"><span data-stu-id="69677-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="69677-167">Gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="69677-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


