---
title: 'Azure Cosmos DB: een web-app ontwikkelen met Xamarin en Facebook-authenticatie | Microsoft-documenten'
description: Is een .NET-codevoorbeeld dat u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit Azure Cosmos DB
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
ms.openlocfilehash: 4ea97c2aca6769843d0210ffeae6f95531a21f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="c16d6-103">Azure Cosmos DB: een web-app ontwikkelen met .NET, Xamarin, en Facebook-authenticatie</span><span class="sxs-lookup"><span data-stu-id="c16d6-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="c16d6-104">Azure Cosmos DB is de globaal gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c16d6-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c16d6-105">U kunt snel databases maken van documenten, sleutel/waarde-paren en grafieken en hier query’s op uitvoeren. Deze databases genieten allemaal het voordeel van de globale distributie en horizontale schaalmogelijkheden die ten grondslag liggen aan Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c16d6-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="c16d6-106">Deze Quick Start laat zien hoe u een Azure Cosmos DB-account, een documentdatabase en een verzameling kunt maken met behulp van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c16d6-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="c16d6-107">Vervolgens ontwikkelt en implementeert u een web-app voor een takenlijst op basis van de [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), en de Azure Cosmos DB-autorisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="c16d6-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and the Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="c16d6-108">De web-app voor een takenlijst implementeert een gegevenspatroon per gebruiker waarmee gebruikers zich kunnen aanmelden met Facebook Auth en hun eigen to-do-items kunnen beheren.</span><span class="sxs-lookup"><span data-stu-id="c16d6-108">The todo list web app implements a per-user data pattern that enables users to login using Facebook Auth and manage their own to do items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c16d6-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c16d6-109">Prerequisites</span></span>

<span data-ttu-id="c16d6-110">Als u Visual Studio 2017 nog niet hebt geïnstalleerd, kunt u het downloaden en de **gratis** [Community Edition van Visual Studio 2017](https://www.visualstudio.com/downloads/) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c16d6-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="c16d6-111">Zorg ervoor dat u **Azure-ontwikkeling** inschakelt tijdens de installatie van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c16d6-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="c16d6-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="c16d6-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="c16d6-113">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="c16d6-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="c16d6-114">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="c16d6-114">Clone the sample application</span></span>

<span data-ttu-id="c16d6-115">We gaan nu een DocumentDB API-app klonen vanuit GitHub, de verbindingsreeks instellen en de app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c16d6-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="c16d6-116">U zult zien hoe gemakkelijk het is om op een programmatische manier met gegevens te werken.</span><span class="sxs-lookup"><span data-stu-id="c16d6-116">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="c16d6-117">Open een venster in een git-terminal zoals git bash en `cd` naar een werkmap.</span><span class="sxs-lookup"><span data-stu-id="c16d6-117">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="c16d6-118">Voer de volgende opdracht uit om de voorbeeldopslagplaats te klonen.</span><span class="sxs-lookup"><span data-stu-id="c16d6-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="c16d6-119">Open vervolgens het bestand DocumentDBTodo.sln in de map samples/xamarin/UserItems/xamarin.forms in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c16d6-119">Then open the DocumentDBTodo.sln file from the samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="c16d6-120">De code bekijken</span><span class="sxs-lookup"><span data-stu-id="c16d6-120">Review the code</span></span>

<span data-ttu-id="c16d6-121">De code in de map Xamarin bevat het volgende:</span><span class="sxs-lookup"><span data-stu-id="c16d6-121">The code in the Xamarin folder contains:</span></span>

* <span data-ttu-id="c16d6-122">Xamarin-app.</span><span class="sxs-lookup"><span data-stu-id="c16d6-122">Xamarin app.</span></span> <span data-ttu-id="c16d6-123">De app slaat de to-do-items van de gebruiker op in een gepartitioneerde verzameling met de naam UserItems.</span><span class="sxs-lookup"><span data-stu-id="c16d6-123">The app stores the user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="c16d6-124">Resourcetokenbroker-API.</span><span class="sxs-lookup"><span data-stu-id="c16d6-124">Resource token broker API.</span></span> <span data-ttu-id="c16d6-125">Een eenvoudige ASP.NET Web-API om Azure Cosmos DB-resourcetokens ter beschikking te stellen aan de aangemelde gebruikers van de app.</span><span class="sxs-lookup"><span data-stu-id="c16d6-125">A simple ASP.NET Web API to broker Azure Cosmos DB resource tokens to the logged in users of the app.</span></span> <span data-ttu-id="c16d6-126">Resourcetokens zijn kortdurende toegangstokens die de app voorzien van toegang tot de gegevens van de aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c16d6-126">Resource tokens are short-lived access tokens that provide the app with the access to the logged in user's data.</span></span>

<span data-ttu-id="c16d6-127">De authenticatie- en gegevenstroom wordt afgebeeld in onderstaand diagram.</span><span class="sxs-lookup"><span data-stu-id="c16d6-127">The authentication and data flow is illustrated in the diagram below.</span></span>

* <span data-ttu-id="c16d6-128">De verzameling UserItems wordt gemaakt met de partitiesleutel '/userid'.</span><span class="sxs-lookup"><span data-stu-id="c16d6-128">The UserItems collection is created with the partition key '/userid'.</span></span> <span data-ttu-id="c16d6-129">Door een partitiesleutel op te geven voor een verzameling kan Azure Cosmos DB oneindig worden geschaald naarmate het aantal gebruikers en items toeneemt.</span><span class="sxs-lookup"><span data-stu-id="c16d6-129">Specifying a partition key for a collection allows Azure Cosmos DB to scale infinitely as the number of users and items grows.</span></span>
* <span data-ttu-id="c16d6-130">Met de Xamarin-app zijn gebruikers in staat om aan te melden met hun Facebook-referenties.</span><span class="sxs-lookup"><span data-stu-id="c16d6-130">The Xamarin app allows users to login with Facebook credentials.</span></span>
* <span data-ttu-id="c16d6-131">De Xamarin-app gebruikt Facebook-toegangstokens om te authenticeren met de ResourceTokenBroker-API</span><span class="sxs-lookup"><span data-stu-id="c16d6-131">The Xamarin app uses Facebook access token to authenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="c16d6-132">De resourcetokenbroker-API authenticeert het verzoek met behulp van de functie App Service Auth en verzoekt om een Azure Cosmos DB-resourcetoken met lees-/schrijftoegang tot alle documenten die de geauthenticeerde partitiesleutel van de gebruiker delen.</span><span class="sxs-lookup"><span data-stu-id="c16d6-132">The resource token broker API authenticates the request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access to all documents sharing the authenticated user's partition key.</span></span>
* <span data-ttu-id="c16d6-133">Resourcetokenbroker retourneert de resourcetoken naar de client-app.</span><span class="sxs-lookup"><span data-stu-id="c16d6-133">Resource token broker returns the resource token to the client app.</span></span>
* <span data-ttu-id="c16d6-134">De app gebruikt de resourcetoken om toegang te krijgen tot de to-do-items van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c16d6-134">The app accesses the user's todo items using the resource token.</span></span>

![Taken-app met voorbeeldgegevens](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="c16d6-136">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="c16d6-136">Update your connection string</span></span>

<span data-ttu-id="c16d6-137">Ga nu terug naar Azure Portal om de verbindingsreeksinformatie op te halen en kopieer deze in de app.</span><span class="sxs-lookup"><span data-stu-id="c16d6-137">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="c16d6-138">Klik in [Azure Portal](http://portal.azure.com/), in uw Azure Cosmos DB-account, in het linker navigatiegedeelte op **Sleutels** en klik vervolgens op **Sleutels voor lezen/schrijven**.</span><span class="sxs-lookup"><span data-stu-id="c16d6-138">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="c16d6-139">In de volgende stap gebruikt u de kopieerknoppen aan de rechterkant van het scherm om de URI en primaire sleutel in het bestand web.config te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c16d6-139">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the Web.config file in the next step.</span></span>

    ![Een toegangssleutel bekijken en kopiëren in Azure Portal, blade Sleutels](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="c16d6-141">Open het bestand Web.config in de map azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c16d6-141">In Visual Studio 2017, open the Web.config file in the azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="c16d6-142">Kopieer uw URI-waarde vanaf de portal (met de kopieerknop) en geef deze als waarde aan de accountUrl in Web.config.</span><span class="sxs-lookup"><span data-stu-id="c16d6-142">Copy your URI value from the portal (using the copy button) and make it the value of the accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="c16d6-143">Kopieer vervolgens de waarde van uw PRIMAIRE SLEUTEL vanaf de portal en geef deze waarde aan accountKey in web.config.</span><span class="sxs-lookup"><span data-stu-id="c16d6-143">Then copy your PRIMARY KEY value from the portal and make it the value of the accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="c16d6-144">U hebt uw app nu bijgewerkt met alle informatie die nodig is voor de communicatie met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c16d6-144">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-the-web-app"></a><span data-ttu-id="c16d6-145">De web-app ontwikkelen en implementeren</span><span class="sxs-lookup"><span data-stu-id="c16d6-145">Build and deploy the web app</span></span>

1. <span data-ttu-id="c16d6-146">Maak een App Service-website in de Azure Portal om de Resourcetokenbroker-API te hosten.</span><span class="sxs-lookup"><span data-stu-id="c16d6-146">In the Azure portal, create an App Service website to host the Resource token broker API.</span></span>
2. <span data-ttu-id="c16d6-147">Open in de Azure Portal de blade App Settings van de website van de Resourcetokenbroker-API.</span><span class="sxs-lookup"><span data-stu-id="c16d6-147">In the Azure portal, open the App Settings blade of the Resource token broker API website.</span></span> <span data-ttu-id="c16d6-148">Vul de volgende instellingen in voor de app:</span><span class="sxs-lookup"><span data-stu-id="c16d6-148">Fill in the following app settings:</span></span>

    * <span data-ttu-id="c16d6-149">accountUrl - de URL van het Azure Cosmos DB-account van het tabblad Sleutels van uw Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="c16d6-149">accountUrl - The Azure Cosmos DB account URL from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="c16d6-150">accountKey - de hoofdsleutel van het Azure Cosmos DB-account van het tabblad Sleutels van uw Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="c16d6-150">accountKey - The Azure Cosmos DB account master key from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="c16d6-151">databaseId en collectionId van de database en verzameling die u hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="c16d6-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="c16d6-152">Publiceer de ResourceTokenBroker-oplossing op de website die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c16d6-152">Publish the ResourceTokenBroker solution to your created website.</span></span>

4. <span data-ttu-id="c16d6-153">Open het Xamarin-project en ga naar TodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="c16d6-153">Open the Xamarin project, and navigate to TodoItemManager.cs.</span></span> <span data-ttu-id="c16d6-154">Vul de waarden in voor accountURL, collectionId, databaseId, en voor resourceTokenBrokerURL als de basis https-url voor de website van de resourcetokenbroker.</span><span class="sxs-lookup"><span data-stu-id="c16d6-154">Fill in the values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as the base https url for the resource token broker website.</span></span>

5. <span data-ttu-id="c16d6-155">Voltooi de zelfstudie [Hoe u uw App Service-toepassing moet configureren om aanmelding via Facebook te gebruiken](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) om Facebook-authenticatie in te stellen en de ResourceTokenBroker-website te configureren.</span><span class="sxs-lookup"><span data-stu-id="c16d6-155">Complete the [How to configure your App Service application to use Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial to setup Facebook authentication and configure the ResourceTokenBroker website.</span></span>

    <span data-ttu-id="c16d6-156">Voer de Xamarin-app uit.</span><span class="sxs-lookup"><span data-stu-id="c16d6-156">Run the Xamarin app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="c16d6-157">SLA’s bekijken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c16d6-157">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c16d6-158">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="c16d6-158">Clean up resources</span></span>

<span data-ttu-id="c16d6-159">Als u deze app niet verder gaat gebruiken, kunt u alle resources verwijderen die door deze Quick Start zijn aangemaakt door onderstaande stappen te volgen in Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="c16d6-159">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="c16d6-160">Klik in het menu aan de linkerkant in Azure Portal op **Resourcegroepen** en klik vervolgens op de naam van de resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c16d6-160">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you just created.</span></span> 
2. <span data-ttu-id="c16d6-161">Klik op de pagina van uw resourcegroep op **Verwijderen**, typ de naam van de resource die u wilt verwijderen in het tekstvak en klik vervolgens op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c16d6-161">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c16d6-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c16d6-162">Next steps</span></span>

<span data-ttu-id="c16d6-163">In deze Quick Start hebt u geleerd hoe u een Azure Cosmos DB-account kunt maken en hebt u een verzameling gemaakt met de Data Explorer en een Xamarin-app ontwikkeld en geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c16d6-163">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="c16d6-164">Nu kunt u aanvullende gegevens in uw Cosmos DB-account importeren.</span><span class="sxs-lookup"><span data-stu-id="c16d6-164">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c16d6-165">Gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c16d6-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
