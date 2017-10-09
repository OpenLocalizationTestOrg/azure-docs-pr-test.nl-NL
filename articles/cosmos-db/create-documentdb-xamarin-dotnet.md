---
title: 'Azure Cosmos DB: een web-app ontwikkelen met Xamarin en Facebook-authenticatie | Microsoft-documenten'
description: Geeft het voorbeeld van een .NET-code kunt u tooconnect tooand query uitvoeren op Azure Cosmos-DB
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
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="3b01d-103">Azure Cosmos DB: een web-app ontwikkelen met .NET, Xamarin, en Facebook-authenticatie</span><span class="sxs-lookup"><span data-stu-id="3b01d-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="3b01d-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3b01d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="3b01d-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="3b01d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="3b01d-106">Deze snel starten laat zien hoe Hallo toocreate een Cosmos-DB Azure-account, documentdatabase en verzameling met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3b01d-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="3b01d-107">U moet vervolgens bouwen en implementeren van een WebApp voor takenlijstjes gebouwd op Hallo [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), en hello Azure Cosmos DB autorisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="3b01d-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="3b01d-108">Hallo todo lijst web-app implementeert een per gebruiker gegevenspatroon waarmee gebruikers toologin met Facebook Auth en beheren hun eigen toodo-items.</span><span class="sxs-lookup"><span data-stu-id="3b01d-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b01d-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3b01d-109">Prerequisites</span></span>

<span data-ttu-id="3b01d-110">Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3b01d-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="3b01d-111">Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b01d-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="3b01d-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="3b01d-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="3b01d-113">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="3b01d-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="3b01d-114">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="3b01d-114">Clone hello sample application</span></span>

<span data-ttu-id="3b01d-115">Nu we de kloon een DocumentDB-API-app vanuit github Hallo verbindingsreeks instellen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3b01d-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="3b01d-116">U ziet hoe eenvoudig het is toowork met gegevens via een programma.</span><span class="sxs-lookup"><span data-stu-id="3b01d-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="3b01d-117">Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="3b01d-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="3b01d-118">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3b01d-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="3b01d-119">Open vervolgens Hallo DocumentDBTodo.sln bestand uit Hallo samples/xamarin/UserItems/xamarin.forms map in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b01d-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="3b01d-120">Hallo code bekijken</span><span class="sxs-lookup"><span data-stu-id="3b01d-120">Review hello code</span></span>

<span data-ttu-id="3b01d-121">Hallo-code in Hallo Xamarin map bevat:</span><span class="sxs-lookup"><span data-stu-id="3b01d-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="3b01d-122">Xamarin-app.</span><span class="sxs-lookup"><span data-stu-id="3b01d-122">Xamarin app.</span></span> <span data-ttu-id="3b01d-123">Hallo app slaat van Hallo gebruiker todo-items in een gepartitioneerde verzameling met de naam UserItems.</span><span class="sxs-lookup"><span data-stu-id="3b01d-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="3b01d-124">Resourcetokenbroker-API.</span><span class="sxs-lookup"><span data-stu-id="3b01d-124">Resource token broker API.</span></span> <span data-ttu-id="3b01d-125">Een eenvoudige ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello aangemelde gebruikers van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="3b01d-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="3b01d-126">Resource-tokens zijn tijdelijke toegangstokens waarmee Hallo app Hallo toegang toohello gegevens van een gebruiker aangemeld.</span><span class="sxs-lookup"><span data-stu-id="3b01d-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="3b01d-127">Hallo-verificatie en de gegevensstroom wordt weergegeven in Hallo diagram hieronder.</span><span class="sxs-lookup"><span data-stu-id="3b01d-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="3b01d-128">Hallo UserItems verzameling is gemaakt met de partitiesleutel Hallo ' / userid'.</span><span class="sxs-lookup"><span data-stu-id="3b01d-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="3b01d-129">Het opgeven van dat een partitiesleutel voor een verzameling kunt u Azure Cosmos DB tooscale oneindig als Hallo aantal gebruikers en items groeit.</span><span class="sxs-lookup"><span data-stu-id="3b01d-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="3b01d-130">Hallo Xamarin-app kan gebruikers toologin met Facebook-referenties.</span><span class="sxs-lookup"><span data-stu-id="3b01d-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="3b01d-131">Hallo Xamarin-app maakt gebruik van Facebook access token tooauthenticate met ResourceTokenBroker API</span><span class="sxs-lookup"><span data-stu-id="3b01d-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="3b01d-132">Hallo resource token broker API verifieert Hallo-aanvraag met de App Service Auth-functie en vraagt een token van de resource Azure Cosmos DB met lezen/schrijven toegang tooall documenten delen partitiesleutel Hallo geverifieerde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3b01d-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="3b01d-133">Resource token broker retourneert Hallo resource token toohello client-app.</span><span class="sxs-lookup"><span data-stu-id="3b01d-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="3b01d-134">Hallo-app heeft toegang tot van Hallo gebruiker todo-items met Hallo resource-token.</span><span class="sxs-lookup"><span data-stu-id="3b01d-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![Taken-app met voorbeeldgegevens](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="3b01d-136">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="3b01d-136">Update your connection string</span></span>

<span data-ttu-id="3b01d-137">Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="3b01d-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="3b01d-138">In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**.</span><span class="sxs-lookup"><span data-stu-id="3b01d-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="3b01d-139">U gebruikt in Web.config-bestand in de volgende stap Hallo HALLO hallo kopie knoppen aan de rechterkant Hallo Hallo scherm toocopy Hallo URI en primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="3b01d-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![Bekijken en kopiëren van een toegangssleutel in hello Azure-portal, de blade sleutels](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="3b01d-141">Open in Visual Studio-2017 Hallo Web.config-bestand in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker map.</span><span class="sxs-lookup"><span data-stu-id="3b01d-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="3b01d-142">Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo-waarde van Hallo accountUrl in Web.config.</span><span class="sxs-lookup"><span data-stu-id="3b01d-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="3b01d-143">Vervolgens kopieert u de waarde van de primaire sleutel van Hallo-portal en maken het Hallo-waarde van Hallo accountKey in Web.congif.</span><span class="sxs-lookup"><span data-stu-id="3b01d-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="3b01d-144">U hebt nu uw app bijgewerkt met alle Hallo info moet toocommunicate met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3b01d-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="3b01d-145">Hallo-web-app bouwen en implementeren</span><span class="sxs-lookup"><span data-stu-id="3b01d-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="3b01d-146">In hello Azure-portal, maakt u een App Service-website toohost Hallo Resource token broker API.</span><span class="sxs-lookup"><span data-stu-id="3b01d-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="3b01d-147">Open in hello Azure-portal, Hallo App-instellingen blade van Hallo Resource token broker API-website.</span><span class="sxs-lookup"><span data-stu-id="3b01d-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="3b01d-148">Vul Hallo volgende app-instellingen:</span><span class="sxs-lookup"><span data-stu-id="3b01d-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="3b01d-149">accountUrl - hello Azure Cosmos DB account-URL op Hallo sleutels tabblad van uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="3b01d-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="3b01d-150">accountKey - hello Azure Cosmos DB account hoofdsleutel Hallo sleutels tabblad van uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="3b01d-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="3b01d-151">databaseId en collectionId van de database en verzameling die u hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="3b01d-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="3b01d-152">Publiceer Hallo ResourceTokenBroker oplossing tooyour website gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3b01d-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="3b01d-153">Open Hallo Xamarin-project en tooTodoItemManager.cs navigeren.</span><span class="sxs-lookup"><span data-stu-id="3b01d-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="3b01d-154">Hallo-waarden voor accountURL, collectionId, databaseId, evenals resourceTokenBrokerURL vult als Hallo base https-url voor Hallo resource token broker website.</span><span class="sxs-lookup"><span data-stu-id="3b01d-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="3b01d-155">Volledige Hallo [hoe tooconfigure uw App Service-toepassing toouse Facebook aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) zelfstudie toosetup Facebook verificatie Hallo ResourceTokenBroker-website configureert.</span><span class="sxs-lookup"><span data-stu-id="3b01d-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="3b01d-156">Hallo Xamarin-app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3b01d-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="3b01d-157">Sla's bekijken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3b01d-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="3b01d-158">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="3b01d-158">Clean up resources</span></span>

<span data-ttu-id="3b01d-159">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3b01d-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="3b01d-160">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van Hallo-resource die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3b01d-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="3b01d-161">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="3b01d-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b01d-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b01d-162">Next steps</span></span>

<span data-ttu-id="3b01d-163">In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account, een verzameling met Hallo Data Explorer maken en bouwen en implementeren van een Xamarin-app.</span><span class="sxs-lookup"><span data-stu-id="3b01d-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="3b01d-164">U kunt nu aanvullende gegevens tooyour Cosmos DB account importeren.</span><span class="sxs-lookup"><span data-stu-id="3b01d-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b01d-165">Gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3b01d-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
