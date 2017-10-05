---
title: 'Azure Cosmos DB: een webapp ontwikkelen met .NET en de DocumentDB API | Microsoft Docs'
description: "Biedt een voorbeeld van .NET-code dat u kunt gebruiken om verbinding te maken met de DocumentDB API van Azure Cosmos DB en er query’s op uit te voeren"
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
ms.openlocfilehash: 9bb863261da64c97f99757d4a0cb3474a7755591
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="cdd4a-103">Azure Cosmos DB: een DocumentDB API-webapp ontwikkelen met .NET en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cdd4a-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="cdd4a-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="cdd4a-105">U kunt snel databases maken van documenten, sleutel/waarde-paren en grafieken en hier query’s op uitvoeren. Deze databases genieten allemaal het voordeel van de globale distributie en horizontale schaalmogelijkheden die ten grondslag liggen aan Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="cdd4a-106">Deze Quick Start laat zien hoe u een Azure Cosmos DB-account, een documentdatabase en een verzameling kunt maken met behulp van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="cdd4a-107">U moet vervolgens een Takenlijst-web-app maken en implementeren op de [DocumentDB .NET API](documentdb-sdk-dotnet.md), zoals wordt weergegeven in de volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in the following screenshot.</span></span> 

![Taken-app met voorbeeldgegevens](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="cdd4a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cdd4a-109">Prerequisites</span></span>

<span data-ttu-id="cdd4a-110">Als u Visual Studio 2017 nog niet hebt geïnstalleerd, kunt u het downloaden en de **gratis** [Community Edition van Visual Studio 2017](https://www.visualstudio.com/downloads/) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="cdd4a-111">Zorg ervoor dat u **Azure-ontwikkeling** inschakelt tijdens de installatie van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="cdd4a-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="cdd4a-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="cdd4a-113">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="cdd4a-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="cdd4a-114">Voorbeeldgegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="cdd4a-114">Add sample data</span></span>

<span data-ttu-id="cdd4a-115">U kunt nu gegevens aan uw nieuwe verzameling toevoegen met behulp van Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-115">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="cdd4a-116">De nieuwe database wordt in Data Explorer weergegeven in het deelvenster Verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-116">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="cdd4a-117">Vouw de database **Taken** uit, vouw de verzameling **Items** uit, klik op **Documenten** en klik vervolgens op **Nieuwe documenten**.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-117">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Nieuwe documenten maken in Data Explorer in de Azure Portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="cdd4a-119">Voeg nu een document toe aan de verzameling met de volgende structuur.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-119">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="cdd4a-120">Zodra u de JSON hebt toegevoegd aan het tabblad **Documenten** klikt u op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-120">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![JSON-gegevens kopiëren en op Opslaan klikken in Data Explorer in Azure Portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="cdd4a-122">Maak nog één document en sla dit op. In het document voegt u een unieke waarde toe voor de eigenschap `id`. Wijzig de andere eigenschappen naar eigen inzicht.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-122">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="cdd4a-123">De nieuwe documenten kunnen elke gewenste structuur hebben, omdat in Azure Cosmos DB uw gegevens geen schema krijgen opgelegd.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="cdd4a-124">U kunt nu query's in Data Explorer gebruiken om uw gegevens te halen.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-124">You can now use queries in Data Explorer to retrieve your data.</span></span> <span data-ttu-id="cdd4a-125">Data Explorer maakt standaard gebruik van `SELECT * FROM c` om alle documenten in de verzameling op te halen. U kunt dit wijzigen in een andere [SQL-query](documentdb-sql-query.md), zoals `SELECT * FROM c ORDER BY c._ts DESC`, om alle documenten terug te zetten in aflopende volgorde op basis van hun timestamp.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-125">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="cdd4a-126">U kunt Data Explorer ook gebruiken voor het maken van opgeslagen procedures, UDF's en triggers om bedrijfslogica aan de serverzijde uit te voeren en doorvoer te schalen.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-126">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="cdd4a-127">In Data Explorer wordt alle ingebouwde programmatische gegevenstoegang zichtbaar die beschikbaar is in de API's, maar biedt eenvoudige toegang tot uw gegevens in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-127">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="cdd4a-128">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="cdd4a-128">Clone the sample application</span></span>

<span data-ttu-id="cdd4a-129">Nu gaan we werken met code.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-129">Now let's switch to working with code.</span></span> <span data-ttu-id="cdd4a-130">We gaan nu een DocumentDB API-app klonen vanuit GitHub, de verbindingsreeks instellen en de app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-130">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="cdd4a-131">U zult zien hoe gemakkelijk het is om op een programmatische manier met gegevens te werken.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-131">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="cdd4a-132">Open een venster in een git-terminal zoals git bash en `CD` naar een werkmap.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-132">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="cdd4a-133">Voer de volgende opdracht uit om de voorbeeldopslagplaats te klonen.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-133">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="cdd4a-134">Open vervolgens het todo-oplossingenbestand in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-134">Then open the todo solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="cdd4a-135">De code bekijken</span><span class="sxs-lookup"><span data-stu-id="cdd4a-135">Review the code</span></span>

<span data-ttu-id="cdd4a-136">Laten we eens kijken wat er precies gebeurt in de app.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-136">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="cdd4a-137">Open het bestand DocumentDBRepository.cs en u zult zien dat deze regels code de Azure Cosmos DB-resources maken.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-137">Open the DocumentDBRepository.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="cdd4a-138">De DocumentClient wordt geïnitialiseerd op regel 73.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-138">The DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="cdd4a-139">Er wordt een nieuwe database gemaakt op regel 88.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="cdd4a-140">Er wordt een nieuwe verzameling gemaakt op regel 107.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="cdd4a-141">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="cdd4a-141">Update your connection string</span></span>

<span data-ttu-id="cdd4a-142">Ga nu terug naar Azure Portal om de verbindingsreeksinformatie op te halen en kopieer deze in de app.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-142">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="cdd4a-143">Klik in [Azure Portal](http://portal.azure.com/), in uw Azure Cosmos DB-account, in het linker navigatiegedeelte op **Sleutels** en klik vervolgens op **Sleutels voor lezen/schrijven**.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-143">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="cdd4a-144">In de volgende stap gebruikt u de kopieerknoppen aan de rechterkant van het scherm om de URI en primaire sleutel in het bestand web.config te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-144">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the web.config file in the next step.</span></span>

    ![Een toegangssleutel bekijken en kopiëren in Azure Portal, blade Sleutels](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="cdd4a-146">Open in Visual Studio 2017 het bestand web.config.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-146">In Visual Studio 2017, open the web.config file.</span></span> 

3. <span data-ttu-id="cdd4a-147">Kopieer uw URI-waarde vanaf de portal (met de kopieerknop) en geef deze als waarde aan de eindpuntsleutel in web.config.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-147">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="cdd4a-148">Kopieer vervolgens de waarde van uw PRIMAIRE SLEUTEL vanaf de portal en geef deze als authKey-waarde in web.config. U hebt uw app nu bijgewerkt met alle informatie die nodig is voor de communicatie met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-148">Then copy your PRIMARY KEY value from the portal and make it the value of the authKey in web.config. You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-the-web-app"></a><span data-ttu-id="cdd4a-149">De web-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cdd4a-149">Run the web app</span></span>
1. <span data-ttu-id="cdd4a-150">Klik in Visual Studio met de rechtermuisknop op het project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-150">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="cdd4a-151">Typ in het NuGet-vak **Bladeren** *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-151">In the NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="cdd4a-152">Installeer vanuit de resultaten de bibliotheek **Microsoft.Azure.DocumentDB**.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-152">From the results, install the **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="cdd4a-153">Hiermee installeert u het pakket Microsoft.Azure.DocumentDB, evenals alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-153">This installs the Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="cdd4a-154">Klik op CTRL+F5 om de toepassing te starten.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-154">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="cdd4a-155">Uw app wordt in uw browser weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="cdd4a-156">Klik op **Nieuwe maken** in de browser en maak een paar nieuwe taken in uw taken-app.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-156">Click **Create New** in the browser and create a few new tasks in your to-do app.</span></span>

   ![Taken-app met voorbeeldgegevens](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="cdd4a-158">U kunt nu teruggaan naar Data Explorer en deze nieuwe gegevens bekijken, wijzigen, een query erop uitvoeren of er iets anders mee doen.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-158">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="cdd4a-159">SLA’s bekijken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cdd4a-159">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="cdd4a-160">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="cdd4a-160">Clean up resources</span></span>

<span data-ttu-id="cdd4a-161">Als u deze app niet verder gaat gebruiken, kunt u alle resources verwijderen die door deze Quick Start zijn aangemaakt door onderstaande stappen te volgen in Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="cdd4a-161">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="cdd4a-162">Klik in het menu aan de linkerkant in Azure Portal op **Resourcegroepen** en klik vervolgens op de resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-162">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="cdd4a-163">Klik op de pagina van uw resourcegroep op **Verwijderen**, typ de naam van de resource die u wilt verwijderen in het tekstvak en klik vervolgens op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-163">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdd4a-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cdd4a-164">Next steps</span></span>

<span data-ttu-id="cdd4a-165">In deze Quick Start hebt u geleerd hoe u een Azure Cosmos DB-account kunt maken, hoe u een verzameling kunt maken met Data Explorer en hebt u een web-app uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-165">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a web app.</span></span> <span data-ttu-id="cdd4a-166">Nu kunt u aanvullende gegevens in uw Cosmos DB-account importeren.</span><span class="sxs-lookup"><span data-stu-id="cdd4a-166">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cdd4a-167">Gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cdd4a-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


