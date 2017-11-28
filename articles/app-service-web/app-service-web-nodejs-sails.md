---
title: aaaDeploy een Sails.js web app tooAzure App Service | Microsoft Docs
description: Meer informatie over hoe toodeploy een Node.js-toepassing Azure App Service. Deze zelfstudie laat zien hoe een Sails.js toodeploy web-app.
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
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="3e9ec-104">Een Sails.js web app tooAzure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="3e9ec-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="3e9ec-105">Deze zelfstudie leert u hoe toodeploy een Sails.js app tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="3e9ec-106">Hallo verwerkt, kunt u enkele algemene kennis over het verzamelen tooconfigure uw toorun Node.js-app in App Service.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="3e9ec-107">U leert hier nuttig vaardigheden, zoals:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="3e9ec-108">Configureer een Sails.js-app in App Service worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="3e9ec-109">Een app-tooApp Service vanaf de opdrachtregel Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="3e9ec-110">Lezen stderr en stdout logboeken tootroubleshoot eventuele problemen bij de implementatie.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="3e9ec-111">Omgevingsvariabelen buiten broncodebeheer opslaan.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="3e9ec-112">Toegang tot Azure-omgevingsvariabelen van uw app.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="3e9ec-113">Verbinding maken met tooa-database (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="3e9ec-114">U hebt enige ervaring met Sails.js.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="3e9ec-115">Deze zelfstudie is niet bedoeld toohelp u met problemen in het algemeen toorunning Sail.js gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3e9ec-116">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="3e9ec-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="3e9ec-117">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="3e9ec-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen</span><span class="sxs-lookup"><span data-stu-id="3e9ec-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="3e9ec-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="3e9ec-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e9ec-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3e9ec-120">Prerequisites</span></span>
* [<span data-ttu-id="3e9ec-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="3e9ec-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="3e9ec-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="3e9ec-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="3e9ec-123">Git</span><span class="sxs-lookup"><span data-stu-id="3e9ec-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="3e9ec-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3e9ec-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="3e9ec-125">Een Microsoft Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-125">A Microsoft Azure account.</span></span> <span data-ttu-id="3e9ec-126">Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="3e9ec-127">U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="3e9ec-128">Een eenvoudige app maken en te spelen met voor up tooan uur--geen creditcard nodig en zonder verdere verplichtingen.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="3e9ec-129">Stap 1: Maken en configureren van een Sails.js-app lokaal</span><span class="sxs-lookup"><span data-stu-id="3e9ec-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="3e9ec-130">Snel Maak eerst een standaard Sails.js-app in uw ontwikkelingsomgeving met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="3e9ec-131">Open Hallo opdrachtregelprogramma terminal van uw keuze en `CD` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="3e9ec-132">Een Sails.js-app maken en uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="3e9ec-133">Zorg ervoor dat u kunt de standaardstartpagina toohello op http://localhost:1377 navigeren.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="3e9ec-134">Schakel vervolgens de logboekregistratie voor Azure.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="3e9ec-135">Maak een bestand met de naam in de hoofdmap `iisnode.yml` en Hallo volgende twee regels toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="3e9ec-136">Logboekregistratie is nu ingeschakeld voor Hallo [iisnode](https://github.com/tjanczuk/iisnode) server dat gebruikmaakt van Azure App Service toorun Node.js-apps.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="3e9ec-137">Zie voor meer informatie over hoe dit werkt [hoe toodebug een Node.js web-app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="3e9ec-138">Configureer vervolgens Hallo Sails.js app toouse Azure omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="3e9ec-139">Open config/env/production.js tooconfigure uw productieomgeving en stel `port` en `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="3e9ec-140">Vindt u documentatie voor deze configuratie-instellingen in de [Sails.js documentatie](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="3e9ec-141">Vervolgens hardcode hello Node.js-versie gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="3e9ec-142">Voeg in package.json, Hallo volgende `engines` eigenschap tooset hello Node.js versie tooone we willen.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="3e9ec-143">Ten slotte een Git-opslagplaats te initialiseren en uw bestanden wordt doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="3e9ec-144">In de hoofdmap van de toepassing is (package.json is) Hallo, Hallo volgende Git-opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="3e9ec-145">Uw code is gereed toobe geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="3e9ec-146">Stap 2: Een Azure-app maken en implementeren van Sails.js</span><span class="sxs-lookup"><span data-stu-id="3e9ec-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="3e9ec-147">Vervolgens Hallo App Service-resource in Azure maken en implementeren van uw app Sails.js tooit.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="3e9ec-148">aanmelden tooAzure als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="3e9ec-149">Ga als volgt Hallo vragen toocontinue Hallo aanmelding in een browser met een Microsoft-account op met uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="3e9ec-150">Hallo implementatie gebruikersgroep in te stellen voor App Service.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="3e9ec-151">U gaat later code implementeren met behulp van deze referenties.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="3e9ec-152">Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) met een naam.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="3e9ec-153">Voor deze zelfstudie over Node.js hoeft u niet zeker tooknow wat is.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="3e9ec-154">toosee welke mogelijke waarden u kunt gebruiken voor `<location>`, gebruik Hallo `az appservice list-locations` CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="3e9ec-155">Maken van een 'gratis' [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) met een naam.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="3e9ec-156">Deze zelfstudie over Node.js, net weten dat u voor web-apps geen in dit abonnement afgeschreven.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="3e9ec-157">Maak een nieuwe web-app met een unieke naam in `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="3e9ec-158">Stap 3: Configureer en implementeer uw app Sails.js</span><span class="sxs-lookup"><span data-stu-id="3e9ec-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="3e9ec-159">Lokale Git-implementatie voor uw nieuwe web-app te configureren met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="3e9ec-160">U ontvangt een JSON-uitvoer als volgt, wat betekent dat Hallo externe Git-opslagplaats is geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="3e9ec-161">Hallo-URL toevoegen in Hallo JSON als een externe Git voor uw lokale opslagplaats (aangeroepen `azure` voor eenvoud).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="3e9ec-162">Implementeer uw code voorbeeld toohello `azure` externe Git.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="3e9ec-163">Wanneer u wordt gevraagd, gebruikt u Hallo-implementatiereferenties die u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="3e9ec-164">Ten slotte uw live Azure-app in de browser Hallo NET starten:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="3e9ec-165">U ziet nu Hallo dezelfde Sails.js-startpagina.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="3e9ec-166">Problemen met uw implementatie oplossen</span><span class="sxs-lookup"><span data-stu-id="3e9ec-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="3e9ec-167">Als uw toepassing Sails.js voor een bepaalde reden in App Service mislukt, vinden Hallo stderr logboeken toohelp oplossen van dit probleem.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="3e9ec-168">Zie voor meer informatie [hoe toodebug een Node.js web-app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="3e9ec-169">Als het Hallo-app is gestart, Hallo stdout logboek moet worden weergegeven u bekend het Hallo-bericht:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

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
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="3e9ec-170">U kunt de granulatie van Hallo stdout Logboeken in Hallo beheren [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) bestand.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="3e9ec-171">Verbinding maken met tooa database in Azure</span><span class="sxs-lookup"><span data-stu-id="3e9ec-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="3e9ec-172">tooconnect tooa database in Azure, Hallo-database van uw keuze maakt in Azure, zoals Azure SQL Database, MySQL, MongoDB, Azure (Redis)-Cache, enz., en gebruik Hallo overeenkomt [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="3e9ec-173">Hallo stappen in deze sectie laten zien hoe u tooconnect tooMongoDB met behulp van een [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, die ondersteuning voor MongoDB-clientverbindingen bieden.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="3e9ec-174">[Maakt een Cosmos-DB-account met protocolondersteuning voor MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="3e9ec-175">[Maak een Cosmos-DB-verzameling en de database](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="3e9ec-176">Hallo-naam van Hallo verzameling maakt niet uit, maar u moet Hallo-naam van Hallo-database wanneer u verbinding vanaf Sails.js maakt.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="3e9ec-177">[Hallo verbindingsinformatie vinden voor uw database Cosmos DB](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="3e9ec-178">Vanaf de opdrachtregel terminal Hallo MongoDB-adapter te installeren:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="3e9ec-179">Open config/connections.js en Hallo verbinding toohello objectenlijst volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

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
    > <span data-ttu-id="3e9ec-180">Hallo `ssl: true` optie is belangrijk omdat [Cosmos DB vereist](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="3e9ec-181">Voor elke omgevingsvariabele (`process.env.*`), moet u tooset in App Service.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="3e9ec-182">toodo deze, Voer Hallo volgende opdrachten uit uw terminal.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="3e9ec-183">Hallo-verbindingsgegevens voor de Cosmos-DB gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="3e9ec-184">Als uw instellingen in Azure app-instellingen, houdt u gevoelige gegevens buiten uw broncodebeheer (Git).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="3e9ec-185">Vervolgens configureert u uw development environment toouse Hallo dezelfde verbindingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="3e9ec-186">Open config/local.js en Hallo na verbindingen object toevoegen:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="3e9ec-187">Deze configuratie vervangt Hallo-instellingen in het bestand config/connections.js voor Hallo lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="3e9ec-188">Dit bestand is uitgesloten door Hallo standaard .gitignore in uw project, zodat deze niet worden opgeslagen in Git.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="3e9ec-189">U bent nu, kunnen tooconnect tooyour Cosmos-DB (MongoDB)-database van uw Azure-web-app en van uw lokale ontwikkelingsomgeving.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="3e9ec-190">Open config/env/production.js tooconfigure uw productieomgeving en voeg de volgende Hallo `models` object:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="3e9ec-191">Open config/env/development.js tooconfigure uw ontwikkelomgeving en voeg de volgende Hallo `models` object:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="3e9ec-192">`migrate: 'alter'`u kunt database migratie functies toocreate gebruiken en eenvoudig database verzamelingen of -tabellen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="3e9ec-193">Echter, `migrate: 'safe'` wordt gebruikt voor uw omgeving voor Azure (productie) omdat Sails.js niet toe u toouse dat staat `migrate: 'alter'` in een productieomgeving (Zie [Sails.js documentatie](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="3e9ec-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="3e9ec-194">Van Hallo terminal [genereren](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) een Sails.js [API blauwdruk](http://sailsjs.org/documentation/concepts/blueprints) zoals u normaal doet, voer `sails lift` Hallo database maakt met de migratie van Sails.js-database.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="3e9ec-195">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="3e9ec-196">Hallo `mywidget` die worden gegenereerd door deze opdracht inhoudsmodel is leeg, maar we tooshow of er verbinding met de database kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="3e9ec-197">Bij het uitvoeren van `sails lift`, het Hallo ontbrekende verzamelingen maakt en tabellen voor Hallo modellen uw app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="3e9ec-198">Toegang Hallo blauwdruk API u zojuist hebt gemaakt in de browser Hallo.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="3e9ec-199">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="3e9ec-200">Hallo API Hallo gemaakt vermelding back tooyou moet worden geretourneerd in browservenster hello, wat betekent dat uw verzameling is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="3e9ec-201">Nu uw wijzigingen tooAzure push en tooyour app toomake ervoor werkt nog altijd bladeren.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="3e9ec-202">Hallo blauwdruk API toegang van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="3e9ec-203">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3e9ec-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="3e9ec-204">Als Hallo API een andere nieuwe vermelding retourneert, praten uw Azure-web-app tooyour Cosmos-DB (MongoDB)-database.</span><span class="sxs-lookup"><span data-stu-id="3e9ec-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="3e9ec-205">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="3e9ec-205">More resources</span></span>
* [<span data-ttu-id="3e9ec-206">Aan de slag met Node.js-web-apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3e9ec-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="3e9ec-207">Node.js-modules gebruiken met Azure-toepassingen</span><span class="sxs-lookup"><span data-stu-id="3e9ec-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
