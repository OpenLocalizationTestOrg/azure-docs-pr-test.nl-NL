---
title: aaaNode.js API-app in Azure App Service | Microsoft Docs
description: Meer informatie over hoe toocreate een Node.js-RESTful-API en deze tooan API-app in Azure App Service implementeren.
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="af427-103">Een Node.js-RESTful-API maken en deze tooan API-app in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="af427-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="af427-104">Deze snelstartgids toont hoe toocreate een REST-API geschreven met behulp van Node.js [Express](http://expressjs.com/)met een [Swagger](http://swagger.io/) definitie en implementeren als een [API-app](app-service-api-apps-why-best-platform.md) op Azure.</span><span class="sxs-lookup"><span data-stu-id="af427-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="af427-105">U Hallo-app met opdrachtregelprogramma's maken, configureren van resources met Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), Hallo-app met Git en implementeren.</span><span class="sxs-lookup"><span data-stu-id="af427-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="af427-106">Wanneer u klaar bent, hebt u een werkende voorbeeld-REST API die wordt uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="af427-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af427-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="af427-107">Prerequisites</span></span>

* [<span data-ttu-id="af427-108">Git</span><span class="sxs-lookup"><span data-stu-id="af427-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="af427-109">Node.js en NPM</span><span class="sxs-lookup"><span data-stu-id="af427-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="af427-110">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="af427-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="af427-111">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="af427-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="af427-112">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="af427-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="af427-113">Uw omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="af427-113">Prepare your environment</span></span>

1. <span data-ttu-id="af427-114">Voer in een terminalvenster Hallo opdracht tooclone Hallo voorbeeld tooyour lokale computer te volgen.</span><span class="sxs-lookup"><span data-stu-id="af427-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="af427-115">Toohello map waarin de voorbeeldcode Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="af427-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="af427-116">Installeer [Swaggerize](https://www.npmjs.com/package/swaggerize-express) op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="af427-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="af427-117">Swaggerize is een hulpprogramma dat Node.js-code genereert voor uw REST API van een Swagger-definitie.</span><span class="sxs-lookup"><span data-stu-id="af427-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="af427-118">Node.js-code genereren</span><span class="sxs-lookup"><span data-stu-id="af427-118">Generate Node.js code</span></span> 

<span data-ttu-id="af427-119">Deze sectie van de zelfstudie Hallo modellen een API ontwikkelingswerkstroom getoond waarin u eerst Swagger-metagegevens maken en gebruiken die tooscaffold (automatisch genereren) servercode voor Hallo API.</span><span class="sxs-lookup"><span data-stu-id="af427-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="af427-120">Wijzigen van de directory toohello *start* map, voer `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="af427-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="af427-121">Swaggerize maakt een Node.js-project voor uw API van Hallo Swagger-definitie in *api.json*.</span><span class="sxs-lookup"><span data-stu-id="af427-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="af427-122">Wanneer in Swaggerize om een projectnaam wordt gevraagd, gebruikt u *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="af427-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="af427-123">Hallo projectcode aanpassen</span><span class="sxs-lookup"><span data-stu-id="af427-123">Customize hello project code</span></span>

1. <span data-ttu-id="af427-124">Kopiëren Hallo *lib* map in Hallo *ContactList* map gemaakt door `yo swaggerize`, wijzigt u vervolgens de directory in *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="af427-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="af427-125">Hallo installeren `jsonpath` en `swaggerize-ui` NPM-modules.</span><span class="sxs-lookup"><span data-stu-id="af427-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="af427-126">Vervang de code Hallo in Hallo *handlers/contacts.js* Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="af427-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="af427-127">Deze code gebruikt Hallo JSON-gegevens opgeslagen in *lib/contacts.json* afgehandeld door *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="af427-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="af427-128">Hallo nieuwe *contacts.js* code retourneert alle contactpersonen in het Hallo-opslagplaats als JSON-nettolading.</span><span class="sxs-lookup"><span data-stu-id="af427-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="af427-129">Vervang de code Hallo in Hallo **handlers/contacts/{id}.js** bestand met de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="af427-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="af427-130">Deze code kunt u een contactpersoon voor pad variabele tooreturn Hallo alleen gebruiken met een opgegeven ID.</span><span class="sxs-lookup"><span data-stu-id="af427-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="af427-131">Vervang de code Hallo in **server.js** Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="af427-131">Replace hello code in **server.js** with hello following code:</span></span>

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    <span data-ttu-id="af427-132">Deze code maakt een aantal kleine wijzigingen toolet het werken met Azure App Service en een interactieve webinterface voor uw API beschrijft.</span><span class="sxs-lookup"><span data-stu-id="af427-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="af427-133">Test Hallo API lokaal</span><span class="sxs-lookup"><span data-stu-id="af427-133">Test hello API locally</span></span>

1. <span data-ttu-id="af427-134">Hallo Node.js-app starten</span><span class="sxs-lookup"><span data-stu-id="af427-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="af427-135">Blader toohttp://localhost:8000 / tooview Hallo JSON contactpersonen voor Hallo complete lijst met contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="af427-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. <span data-ttu-id="af427-136">Blader toohttp://localhost:8000/contacts/2 tooview Hallo contact met een `id` van twee.</span><span class="sxs-lookup"><span data-stu-id="af427-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="af427-137">Hallo-API met Hallo Swagger webinterface op http://localhost: 8000/docs testen.</span><span class="sxs-lookup"><span data-stu-id="af427-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Swagger-webinterface](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="af427-139"><a id="createapiapp"></a> Een API-app maken</span><span class="sxs-lookup"><span data-stu-id="af427-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="af427-140">In deze sectie gebruikt u hello Azure CLI 2.0 toocreate Hallo resources toohost Hallo API in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="af427-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="af427-141">Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="af427-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="af427-142">Als u meerdere Azure-abonnementen hebt, gewenste wijziging Hallo standaard abonnement toohello een.</span><span class="sxs-lookup"><span data-stu-id="af427-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="af427-143">Hallo-API met Git implementeren</span><span class="sxs-lookup"><span data-stu-id="af427-143">Deploy hello API with Git</span></span>

<span data-ttu-id="af427-144">Implementeer uw code toohello API-app door doorvoeracties te pushen van uw lokale Git-opslagplaats tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="af427-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="af427-145">Initialiseren van een nieuwe opslagplaats in Hallo *ContactList* directory.</span><span class="sxs-lookup"><span data-stu-id="af427-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="af427-146">Hallo uitsluiten *node_modules* directory gemaakt door npm in een eerdere stap in de zelfstudie Hallo van Git.</span><span class="sxs-lookup"><span data-stu-id="af427-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="af427-147">Maak een nieuwe `.gitignore` -bestand in de huidige map Hallo en Hallo tekst volgen op een nieuwe regel overal in het Hallo-bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="af427-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="af427-148">Hallo bevestigen `node_modules` map wordt genegeerd met `git status`.</span><span class="sxs-lookup"><span data-stu-id="af427-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="af427-149">Hallo wijzigingen toohello opslagplaats doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="af427-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="af427-150">Test Hallo API in Azure</span><span class="sxs-lookup"><span data-stu-id="af427-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="af427-151">Open een browser toohttp://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="af427-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="af427-152">U ziet dat dezelfde JSON geretourneerd als wanneer u lokaal Hallo-aanvraag heeft ingediend eerder in de zelfstudie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="af427-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. <span data-ttu-id="af427-153">Ga in een browser toohello `http://app_name.azurewebsites.net/docs` eindpunt tootry uit Hallo Swagger-gebruikersinterface die zijn uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="af427-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Swagger-UI](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="af427-155">U kunt nu updates toohello voorbeeld API tooAzure implementeren door doorvoeracties toohello Azure Git-opslagplaats te pushen.</span><span class="sxs-lookup"><span data-stu-id="af427-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="af427-156">Opruimen</span><span class="sxs-lookup"><span data-stu-id="af427-156">Clean up</span></span>

<span data-ttu-id="af427-157">tooclean Hallo-resources die zijn gemaakt in deze snelstartgids, Hallo na Azure CLI-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="af427-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="af427-158">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="af427-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="af427-159">API-apps van JavaScript-clients gebruiken met CORS</span><span class="sxs-lookup"><span data-stu-id="af427-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

