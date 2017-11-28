---
title: een Azure Cosmos DB .NET-toepassing gebruikt aaaBuild Hallo tabel-API | Microsoft Docs
description: Aan de slag met de Table-API van Azure Cosmos DB met behulp van .NET
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a><span data-ttu-id="33c81-103">Azure Cosmos DB: Een .NET-toepassing hello tabel API met bouwen</span><span class="sxs-lookup"><span data-stu-id="33c81-103">Azure Cosmos DB: Build a .NET application using hello Table API</span></span>

<span data-ttu-id="33c81-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="33c81-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="33c81-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="33c81-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="33c81-106">Deze snel starten laat zien hoe toocreate een Cosmos Azure DB account en het maken van een tabel in dat account met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="33c81-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, and create a table within that account using hello Azure portal.</span></span> <span data-ttu-id="33c81-107">U moet vervolgens schrijven van code tooinsert, update en delete-entiteiten en enkele query's met Hallo nieuwe [Windows Azure-opslag Premium Table](https://aka.ms/premiumtablenuget) (preview)-pakket van NuGet.</span><span class="sxs-lookup"><span data-stu-id="33c81-107">You'll then write code tooinsert, update, and delete entities, and run some queries using hello new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="33c81-108">Deze bibliotheek heeft Hallo dezelfde klassen- en handtekeningen als Hallo openbaar [Windows Azure-opslag-SDK](https://www.nuget.org/packages/WindowsAzure.Storage), maar heeft ook Hallo mogelijkheid tooconnect tooAzure Cosmos DB accounts met Hallo [tabel API](table-introduction.md) (preview).</span><span class="sxs-lookup"><span data-stu-id="33c81-108">This library has hello same classes and method signatures as hello public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has hello ability tooconnect tooAzure Cosmos DB accounts using hello [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="33c81-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="33c81-109">Prerequisites</span></span>

<span data-ttu-id="33c81-110">Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="33c81-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="33c81-111">Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.</span><span class="sxs-lookup"><span data-stu-id="33c81-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="33c81-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="33c81-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="33c81-113">Een tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="33c81-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="33c81-114">Voorbeeldgegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="33c81-114">Add sample data</span></span>

<span data-ttu-id="33c81-115">U kunt nu gegevens tooyour nieuwe tabel met behulp van Data Explorer (Preview) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="33c81-115">You can now add data tooyour new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="33c81-116">Vouw in Data Explorer **sample-table** uit, klik op **Entiteiten** en klik vervolgens op **Entiteit toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="33c81-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Maken van nieuwe entiteiten in de Data Explorer in hello Azure-portal](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="33c81-118">Nu gegevens toohello PartitionKey waarde vakken en RowKey waarde toevoegen en klik op **entiteit toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="33c81-118">Now add data toohello PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Stel Hallo partitie en sleutel van de rij voor een nieuwe entiteit](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="33c81-120">U kunt nu meer entiteiten tooyour tabel toevoegen, bewerken van uw entiteiten of de gegevens in Data Explorer zoeken.</span><span class="sxs-lookup"><span data-stu-id="33c81-120">You can now add more entities tooyour table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="33c81-121">Data Explorer is ook kunt u uw doorvoer schalen en opgeslagen procedures, door de gebruiker gedefinieerde functies en triggers tooyour tabel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="33c81-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers tooyour table.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="33c81-122">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="33c81-122">Clone hello sample application</span></span>

<span data-ttu-id="33c81-123">Nu gaan we een tabel-app vanuit github Hallo verbindingsreeks instellen en voer dit klonen.</span><span class="sxs-lookup"><span data-stu-id="33c81-123">Now let's clone a Table app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="33c81-124">U ziet hoe eenvoudig het is toowork met gegevens via een programma.</span><span class="sxs-lookup"><span data-stu-id="33c81-124">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="33c81-125">Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="33c81-125">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="33c81-126">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="33c81-126">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="33c81-127">Open het oplossingsbestand Hallo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33c81-127">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="33c81-128">Hallo code bekijken</span><span class="sxs-lookup"><span data-stu-id="33c81-128">Review hello code</span></span>

<span data-ttu-id="33c81-129">We maken een kort overzicht van wat in Hallo-app gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="33c81-129">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="33c81-130">Het bestand Program.cs Open Hallo en u vindt dat deze regels code hello Azure Cosmos DB resources maken.</span><span class="sxs-lookup"><span data-stu-id="33c81-130">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="33c81-131">Hallo CloudTableClient is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="33c81-131">hello CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="33c81-132">Er wordt een nieuwe tabel gemaakt als er nog geen tabel bestaat.</span><span class="sxs-lookup"><span data-stu-id="33c81-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="33c81-133">Er wordt een nieuwe Table-container gemaakt.</span><span class="sxs-lookup"><span data-stu-id="33c81-133">A new Table container is created.</span></span> <span data-ttu-id="33c81-134">Hier ziet u deze code vergelijkbaar tooregular Azure Table storage SDK.</span><span class="sxs-lookup"><span data-stu-id="33c81-134">You will notice this code very similar tooregular Azure Table storage SDK.</span></span> 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="33c81-135">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="33c81-135">Update your connection string</span></span>

<span data-ttu-id="33c81-136">Nu ontvangt updates verbindingsreeksgegevens Hallo zodat uw app tooAzure Cosmos DB kan communiceren.</span><span class="sxs-lookup"><span data-stu-id="33c81-136">Now we'll update hello connection string information so your app can talk tooAzure Cosmos DB.</span></span> 

1. <span data-ttu-id="33c81-137">Open in Visual Studio Hallo app.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="33c81-137">In Visual Studio, open hello app.config file.</span></span> 

2. <span data-ttu-id="33c81-138">In Hallo [Azure-portal](http://portal.azure.com/), in hello Azure Cosmos DB navigatiemenu links, klikt u op **verbindingsreeks**.</span><span class="sxs-lookup"><span data-stu-id="33c81-138">In hello [Azure portal](http://portal.azure.com/), in hello Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="33c81-139">Klik vervolgens in het nieuwe deelvenster Hallo op knop voor het kopiëren voor de verbindingsreeks Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="33c81-139">Then in hello new pane click hello copy button for hello connection string.</span></span> 

    ![Bekijken en kopiëren Hallo eindpunt en Accountsleutel in Hallo verbindingsreeks deelvenster](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="33c81-141">Hallo-waarde in Hallo app.config-bestand als de waarde Hallo Hallo PremiumStorageConnectionString plakken.</span><span class="sxs-lookup"><span data-stu-id="33c81-141">Paste hello value into hello app.config file as hello value of hello PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="33c81-142">U kunt laten Hallo StandardStorageConnectionString is.</span><span class="sxs-lookup"><span data-stu-id="33c81-142">You can leave hello StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="33c81-143">U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="33c81-143">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-web-app"></a><span data-ttu-id="33c81-144">Hallo-web-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="33c81-144">Run hello web app</span></span>

1. <span data-ttu-id="33c81-145">In Visual Studio met de rechtermuisknop op Hallo **PremiumTableGetStarted** project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="33c81-145">In Visual Studio, right-click on hello **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="33c81-146">In Hallo NuGet **Bladeren** in het vak *WindowsAzure.Storage PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="33c81-146">In hello NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="33c81-147">Controleer de Hallo **Include prerelease** vak.</span><span class="sxs-lookup"><span data-stu-id="33c81-147">Check hello **Include prerelease** box.</span></span> 

4. <span data-ttu-id="33c81-148">Installeren in Hallo resultaten Hallo **WindowsAzure.Storage PremiumTable** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="33c81-148">From hello results, install hello **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="33c81-149">Hiermee installeert u Hallo preview pakket Azure Cosmos DB tabel API, evenals alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="33c81-149">This installs hello preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="33c81-150">Houd er rekening mee dat dit een andere NuGet-pakket dan Hallo Windows Azure Storage-pakket wordt gebruikt door Azure Table storage is.</span><span class="sxs-lookup"><span data-stu-id="33c81-150">Note that this is a different NuGet package than hello Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="33c81-151">Klik op CTRL + F5 toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="33c81-151">Click CTRL + F5 toorun hello application.</span></span>

    <span data-ttu-id="33c81-152">Hallo-consolevenster weergegeven Hallo gegevens wordt toegevoegd, opgehaald, opgevraagd, vervangen en verwijderd uit de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="33c81-152">hello console window displays hello data being added, retrieved, queried, replaced and deleted from hello table.</span></span> <span data-ttu-id="33c81-153">Wanneer het Hallo-script is voltooid, drukt u op elke sleutel tooclose Hallo-consolevenster.</span><span class="sxs-lookup"><span data-stu-id="33c81-153">When hello script completes, press any key tooclose hello console window.</span></span> 
    
    ![Console-uitvoer van Hallo Quick Start](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="33c81-155">Als u wilt dat toosee Hallo nieuwe entiteiten in Data Explorer alleen commentaar regels 188 208 in program.cs zodat ze niet worden verwijderd, Voer Hallo voorbeeld opnieuw.</span><span class="sxs-lookup"><span data-stu-id="33c81-155">If you want toosee hello new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run hello sample again.</span></span> 

    <span data-ttu-id="33c81-156">U kunt nu teruggaan tooData Explorer, klikt u op **vernieuwen**, vouw Hallo **mensen** tabel en klik op **entiteiten**, en werk met deze nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="33c81-156">You can now go back tooData Explorer, click **Refresh**, expand hello **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Nieuwe entiteiten in Data Explorer](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="33c81-158">Sla's bekijken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="33c81-158">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="33c81-159">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="33c81-159">Clean up resources</span></span>

<span data-ttu-id="33c81-160">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="33c81-160">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="33c81-161">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="33c81-161">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="33c81-162">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="33c81-162">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33c81-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33c81-163">Next steps</span></span>

<span data-ttu-id="33c81-164">In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een tabel maken met de Hallo Data Explorer en een app uitvoert.</span><span class="sxs-lookup"><span data-stu-id="33c81-164">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a table using hello Data Explorer, and run an app.</span></span>  <span data-ttu-id="33c81-165">U kunt nu uw gegevens dankzij Hallo tabel API opvragen.</span><span class="sxs-lookup"><span data-stu-id="33c81-165">Now you can query your data using hello Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="33c81-166">Query met Hallo tabel-API</span><span class="sxs-lookup"><span data-stu-id="33c81-166">Query using hello Table API</span></span>](tutorial-query-table.md)

