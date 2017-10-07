---
title: 'Azure Cosmos DB: Een web-app met .NET bouwen en Hallo MongoDB-API | Microsoft Docs'
description: Geeft het voorbeeld van een .NET-code kunt u tooconnect tooand query hello Azure Cosmos DB MongoDB-API
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="e6033-103">Azure Cosmos DB: Een web-app van de MongoDB-API met .NET bouwen en hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e6033-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="e6033-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e6033-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="e6033-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="e6033-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="e6033-106">Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e6033-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="e6033-107">U vervolgens bouwen en implementeren van een taken lijst web-app gebouwd op Hallo [MongoDB .NET stuurprogramma](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="e6033-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e6033-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e6033-108">Prerequisites</span></span>

<span data-ttu-id="e6033-109">Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e6033-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="e6033-110">Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6033-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="e6033-111">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="e6033-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="e6033-112">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="e6033-112">Clone hello sample application</span></span>

<span data-ttu-id="e6033-113">Nu we de kloon een MongoDB-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e6033-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="e6033-114">U ziet hoe eenvoudig het is toowork met gegevens via een programma.</span><span class="sxs-lookup"><span data-stu-id="e6033-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="e6033-115">Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="e6033-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="e6033-116">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e6033-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="e6033-117">Open het oplossingsbestand Hallo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6033-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="e6033-118">Hallo code bekijken</span><span class="sxs-lookup"><span data-stu-id="e6033-118">Review hello code</span></span>

<span data-ttu-id="e6033-119">We maken een kort overzicht van wat in Hallo-app gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="e6033-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="e6033-120">Open Hallo **Dal.cs** bestand onder Hallo **DAL** directory en u vindt dat deze regels code hello Azure Cosmos DB resources maken.</span><span class="sxs-lookup"><span data-stu-id="e6033-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="e6033-121">Hallo Mongo-Client initialiseren.</span><span class="sxs-lookup"><span data-stu-id="e6033-121">Initialize hello Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="e6033-122">Hallo-database en verzameling Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="e6033-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="e6033-123">Haal alle documenten op.</span><span class="sxs-lookup"><span data-stu-id="e6033-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="e6033-124">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="e6033-124">Update your connection string</span></span>

<span data-ttu-id="e6033-125">Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="e6033-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="e6033-126">In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **verbindingsreeks**, en klik vervolgens op **lezen-schrijven sleutels**.</span><span class="sxs-lookup"><span data-stu-id="e6033-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="e6033-127">U gebruikt in Hallo Dal.cs bestand in de volgende stap Hallo Hallo kopie knoppen aan de rechterkant Hallo Hallo scherm toocopy Hallo gebruikersnaam, wachtwoord en Host.</span><span class="sxs-lookup"><span data-stu-id="e6033-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="e6033-128">Open Hallo **Dal.cs** bestand in Hallo **DAL** directory.</span><span class="sxs-lookup"><span data-stu-id="e6033-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="e6033-129">Kopieer uw **gebruikersnaam** waarde uit de Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het waarde Hallo Hallo **gebruikersnaam** in uw **Dal.cs** bestand.</span><span class="sxs-lookup"><span data-stu-id="e6033-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="e6033-130">Kopieer uw **host** waarde uit de portal hello, waardoor het Hallo-waarde van Hallo **host** in uw **Dal.cs** bestand.</span><span class="sxs-lookup"><span data-stu-id="e6033-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="e6033-131">Ten slotte Kopieer uw **wachtwoord** waarde uit de portal hello, waardoor het Hallo waarde Hallo **wachtwoord** in uw **Dal.cs** bestand.</span><span class="sxs-lookup"><span data-stu-id="e6033-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="e6033-132">U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e6033-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="e6033-133">Hallo-web-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e6033-133">Run hello web app</span></span>

1. <span data-ttu-id="e6033-134">In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="e6033-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="e6033-135">In Hallo NuGet **Bladeren** in het vak *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="e6033-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="e6033-136">Installeren in Hallo resultaten Hallo **MongoDB.Driver** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="e6033-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="e6033-137">Hiermee installeert u Hallo MongoDB.Driver pakket, evenals alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e6033-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="e6033-138">Klik op CTRL + F5 toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e6033-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="e6033-139">Uw app wordt in uw browser weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e6033-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="e6033-140">Klik op **maken** in de browser Hallo en enkele nieuwe taken in uw app van de lijst taak maken.</span><span class="sxs-lookup"><span data-stu-id="e6033-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="e6033-141">Sla's bekijken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e6033-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="e6033-142">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="e6033-142">Clean up resources</span></span>

<span data-ttu-id="e6033-143">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e6033-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="e6033-144">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e6033-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="e6033-145">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="e6033-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6033-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e6033-146">Next steps</span></span>

<span data-ttu-id="e6033-147">In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account en voer een app met Hallo API voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e6033-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="e6033-148">U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren.</span><span class="sxs-lookup"><span data-stu-id="e6033-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e6033-149">Gegevens importeren in Azure Cosmos DB voor Hallo MongoDB-API</span><span class="sxs-lookup"><span data-stu-id="e6033-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

