---
title: Een Sails.js-web-app implementeren in Azure App Service | Microsoft Docs
description: Informatie over het implementeren van een Node.js-toepassing Azure App Service. Deze zelfstudie laat zien hoe u een Sails.js-web-app implementeren.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="d2ac6-104">Een Sails.js-web-app implementeren in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d2ac6-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="d2ac6-105">Deze zelfstudie laat zien hoe u een Sails.js-app implementeren in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="d2ac6-106">In het proces kunt u een aantal algemene kennis over het configureren van uw Node.js-app in App Service uit te voeren verzamelen.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="d2ac6-107">U leert hier nuttig vaardigheden, zoals:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="d2ac6-108">Configureer een Sails.js-app in App Service worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="d2ac6-109">Een app in App Service implementeren vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="d2ac6-110">Lees stderr stdout logboeken en eventuele problemen met implementatie.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="d2ac6-111">Omgevingsvariabelen buiten broncodebeheer opslaan.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="d2ac6-112">Toegang tot Azure-omgevingsvariabelen van uw app.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="d2ac6-113">Verbinding maken met een database (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="d2ac6-114">U hebt enige ervaring met Sails.js.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="d2ac6-115">Deze zelfstudie is niet bedoeld om u te helpen problemen met betrekking tot Sail.js in het algemeen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="d2ac6-116">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="d2ac6-116">CLI versions to complete the task</span></span>

<span data-ttu-id="d2ac6-117">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="d2ac6-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md): onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="d2ac6-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="d2ac6-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="d2ac6-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2ac6-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d2ac6-120">Prerequisites</span></span>
* [<span data-ttu-id="d2ac6-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="d2ac6-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="d2ac6-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="d2ac6-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="d2ac6-123">Git</span><span class="sxs-lookup"><span data-stu-id="d2ac6-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="d2ac6-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d2ac6-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="d2ac6-125">Een Microsoft Azure-account.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-125">A Microsoft Azure account.</span></span> <span data-ttu-id="d2ac6-126">Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="d2ac6-127">U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="d2ac6-128">U kunt een beginnerstoepassing maken en hier een uur mee spelen. U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="d2ac6-129">Stap 1: Maken en configureren van een Sails.js-app lokaal</span><span class="sxs-lookup"><span data-stu-id="d2ac6-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="d2ac6-130">Snel Maak eerst een standaard Sails.js-app in uw ontwikkelingsomgeving met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="d2ac6-131">Open de van uw keuze en `CD` in een werkmap.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="d2ac6-132">Een Sails.js-app maken en uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="d2ac6-133">Zorg ervoor dat u kunt naar de standaardstartpagina op http://localhost:1377 navigeren.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="d2ac6-134">Schakel vervolgens de logboekregistratie voor Azure.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="d2ac6-135">Maak een bestand met de naam in de hoofdmap `iisnode.yml` en voeg de volgende twee regels:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="d2ac6-136">Logboekregistratie is nu ingeschakeld voor de [iisnode](https://github.com/tjanczuk/iisnode) server die de Azure App Service gebruikt voor het uitvoeren van Node.js-apps.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="d2ac6-137">Zie voor meer informatie over hoe dit werkt [fouten opsporen in een Node.js-web-app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="d2ac6-138">Configureer vervolgens de Sails.js-app voor het gebruik van Azure omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="d2ac6-139">Open config/env/production.js voor het configureren van uw productieomgeving en stel `port` en `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="d2ac6-140">Vindt u documentatie voor deze configuratie-instellingen in de [Sails.js documentatie](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="d2ac6-141">Vervolgens hardcode voor de Node.js-versie die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="d2ac6-142">In package.json, voeg de volgende `engines` eigenschap de Node.js-versie die we willen instellen.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="d2ac6-143">Ten slotte een Git-opslagplaats te initialiseren en uw bestanden wordt doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="d2ac6-144">In de hoofdmap van de toepassing (package.json is), voer de volgende Git-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="d2ac6-145">Uw code is gereed om te worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="d2ac6-146">Stap 2: Een Azure-app maken en implementeren van Sails.js</span><span class="sxs-lookup"><span data-stu-id="d2ac6-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="d2ac6-147">Vervolgens de App Service-resource maken in Azure en uw Sails.js-app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="d2ac6-148">Meld u aan bij Azure achtige dus:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="d2ac6-149">Volg de aanwijzing om de aanmelding in een browser voort te zetten met het Microsoft-account waarmee u uw Azure-abonnement hebt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="d2ac6-150">Stel de implementatiegebruiker in voor App Service.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="d2ac6-151">U gaat later code implementeren met behulp van deze referenties.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="d2ac6-152">Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) met een naam.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="d2ac6-153">Voor deze zelfstudie Node.js moet niet wat u weten wat het.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="d2ac6-154">Gebruik de CLI-opdracht `az appservice list-locations` om te zien welke waarden u kunt gebruiken voor `<location>`.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="d2ac6-155">Maken van een 'gratis' [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) met een naam.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="d2ac6-156">Deze zelfstudie over Node.js, net weten dat u voor web-apps geen in dit abonnement afgeschreven.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="d2ac6-157">Maak een nieuwe web-app met een unieke naam in `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="d2ac6-158">Stap 3: Configureer en implementeer uw app Sails.js</span><span class="sxs-lookup"><span data-stu-id="d2ac6-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="d2ac6-159">Configureer een lokale Git-implementatie voor uw nieuwe web-app. Doe dit met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="d2ac6-160">U ziet JSON-uitvoer zoals hieronder, wat betekent dat de externe Git-opslagplaats is geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="d2ac6-161">Voeg de URL in de JSON toe als een externe Git voor uw lokale opslagplaats (voor de duidelijkheid `azure` genoemd).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="d2ac6-162">Implementeer de voorbeeldcode in de externe Git `azure`.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="d2ac6-163">Gebruik wanneer dit wordt gevraagd de implementatiereferenties die u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="d2ac6-164">Ten slotte uw live Azure-app in de browser net start:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="d2ac6-165">U ziet nu de dezelfde Sails.js-startpagina.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="d2ac6-166">Problemen met uw implementatie oplossen</span><span class="sxs-lookup"><span data-stu-id="d2ac6-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="d2ac6-167">Als uw toepassing Sails.js voor een bepaalde reden in App Service mislukt, vindt u de logboeken stderr bij het oplossen van deze.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="d2ac6-168">Zie voor meer informatie [fouten opsporen in een Node.js-web-app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="d2ac6-169">Als de app is gestart, het logboek stdout moet u de vertrouwde bericht weergeven:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="d2ac6-170">U kunt de granulatie van de logboeken stdout in beheren de [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) bestand.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="d2ac6-171">Verbinding maken met een database in Azure</span><span class="sxs-lookup"><span data-stu-id="d2ac6-171">Connect to a database in Azure</span></span>
<span data-ttu-id="d2ac6-172">Voor verbinding met een database in Azure, u de database van uw keuze maken in Azure, zoals Azure SQL Database, MySQL, MongoDB, Azure (Redis)-Cache, enz., en de bijbehorende [datastore adapter](https://github.com/balderdashy/sails#compatibility) tot stand te brengen.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="d2ac6-173">De stappen in deze sectie ziet u hoe u met MongoDB te maken met een [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, die ondersteuning voor MongoDB-clientverbindingen bieden.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="d2ac6-174">[Maakt een Cosmos-DB-account met protocolondersteuning voor MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="d2ac6-175">[Maak een Cosmos-DB-verzameling en de database](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="d2ac6-176">De naam van de verzameling maakt niet uit, maar u moet de naam van de database als u verbinding vanaf Sails.js maakt.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="d2ac6-177">[De verbindingsgegevens voor de database van de Cosmos-DB vinden](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="d2ac6-178">Vanaf de opdrachtregel terminal de MongoDB-adapter te installeren:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="d2ac6-179">Open config/connections.js en het volgende verbindingsobject toevoegen aan de lijst:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-179">Open config/connections.js and add the following connection object to the list:</span></span>

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > <span data-ttu-id="d2ac6-180">De `ssl: true` optie is belangrijk omdat [Cosmos DB vereist](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="d2ac6-181">Voor elke omgevingsvariabele (`process.env.*`), moet u deze eigenschap instellen in App Service.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="d2ac6-182">Voer hiertoe de volgende opdrachten vanaf uw computer.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="d2ac6-183">Gebruik de gegevens voor uw Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="d2ac6-184">Als uw instellingen in Azure app-instellingen, houdt u gevoelige gegevens buiten uw broncodebeheer (Git).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="d2ac6-185">Vervolgens configureert u uw ontwikkelomgeving voor het gebruik van dezelfde verbindingsinformatie.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="d2ac6-186">Open config/local.js en voeg de volgende verbindingen-object:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="d2ac6-187">Deze configuratie vervangt de instellingen in het bestand config/connections.js voor de lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="d2ac6-188">Dit bestand is uitgesloten door de standaard .gitignore in uw project, zodat deze niet worden opgeslagen in Git.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="d2ac6-189">U bent nu verbinding kunnen maken met uw database Cosmos-DB (MongoDB) van uw Azure-web-app en van uw lokale ontwikkelingsomgeving.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="d2ac6-190">Open config/env/production.js voor het configureren van uw productieomgeving en voeg de volgende `models` object:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="d2ac6-191">Open config/env/development.js voor het configureren van uw ontwikkelomgeving en voeg de volgende `models` object:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="d2ac6-192">`migrate: 'alter'`kunt u migratie databasefuncties maken en bijwerken van database verzamelingen of tabellen eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="d2ac6-193">Echter, `migrate: 'safe'` wordt gebruikt voor uw omgeving voor Azure (productie) omdat Sails.js staat niet toe dat u gebruikt `migrate: 'alter'` in een productieomgeving (Zie [Sails.js documentatie](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="d2ac6-194">Vanaf de terminal [genereren](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) een Sails.js [API blauwdruk](http://sailsjs.org/documentation/concepts/blueprints) zoals u normaal doet, voer `sails lift` maken van de database met Sails.js database wilt migreren.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="d2ac6-195">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="d2ac6-196">De `mywidget` die worden gegenereerd door deze opdracht inhoudsmodel is leeg, maar we kunnen deze gebruiken om weer te geven of er verbinding met de database.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="d2ac6-197">Bij het uitvoeren van `sails lift`, worden de ontbrekende verzamelingen en tabellen voor de modellen uw app wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="d2ac6-198">Toegang tot de blauwdruk API die u zojuist hebt gemaakt in de browser.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="d2ac6-199">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="d2ac6-200">De API moet de gemaakte vermelding retourneren aan u in het browservenster, wat betekent dat uw verzameling is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="d2ac6-201">Nu pusht u uw wijzigingen naar Azure en blader naar uw app om ervoor te zorgen dat het nog steeds werkt.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="d2ac6-202">Toegang tot de blauwdruk API van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="d2ac6-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="d2ac6-203">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d2ac6-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="d2ac6-204">Als de API een andere nieuwe vermelding retourneert, wordt uw Azure-web-app communiceren met uw database Cosmos-DB (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="d2ac6-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="d2ac6-205">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="d2ac6-205">More resources</span></span>
* [<span data-ttu-id="d2ac6-206">Aan de slag met Node.js-web-apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d2ac6-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="d2ac6-207">Node.js-modules gebruiken met Azure-toepassingen</span><span class="sxs-lookup"><span data-stu-id="d2ac6-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
