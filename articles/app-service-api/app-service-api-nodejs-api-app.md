---
title: Node.js-API-app in Azure App Service | Microsoft Docs
description: Informatie over het maken van een Node.js-RESTful-API en deze implementeren in een API-app in Azure App Service.
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
ms.openlocfilehash: 806585edd43b9d2d678bfa41523e4d9d40af8cba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a><span data-ttu-id="10905-103">Een Node.js-RESTful-API maken en deze implementeren in een API-app in Azure</span><span class="sxs-lookup"><span data-stu-id="10905-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="10905-104">In deze snelstartgids wordt uitgelegd hoe u een REST-API kunt maken die is geschreven met Node.js [Express](http://expressjs.com/) met behulp van een [Swagger](http://swagger.io/)-definitie en deze als [API-app](app-service-api-apps-why-best-platform.md) kunt implementeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="10905-104">This quickstart shows how to create a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="10905-105">U maakt de app met opdrachtregelprogramma's, configureert resources met de [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) en implementeert de app met Git.</span><span class="sxs-lookup"><span data-stu-id="10905-105">You create the app using command-line tools, configure resources with the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy the app using Git.</span></span>  <span data-ttu-id="10905-106">Wanneer u klaar bent, hebt u een werkende voorbeeld-REST API die wordt uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="10905-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10905-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="10905-107">Prerequisites</span></span>

* [<span data-ttu-id="10905-108">Git</span><span class="sxs-lookup"><span data-stu-id="10905-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="10905-109">Node.js en NPM</span><span class="sxs-lookup"><span data-stu-id="10905-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="10905-110">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="10905-110">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="10905-111">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="10905-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="10905-112">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="10905-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="10905-113">Uw omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="10905-113">Prepare your environment</span></span>

1. <span data-ttu-id="10905-114">Voer in een terminalvenster de volgende opdracht uit om het voorbeeld naar uw lokale machine te klonen.</span><span class="sxs-lookup"><span data-stu-id="10905-114">In a terminal window, run the following command to clone the sample to your local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="10905-115">Ga naar de map die de voorbeeldcode bevat.</span><span class="sxs-lookup"><span data-stu-id="10905-115">Change to the directory that contains the sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="10905-116">Installeer [Swaggerize](https://www.npmjs.com/package/swaggerize-express) op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="10905-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="10905-117">Swaggerize is een hulpprogramma dat Node.js-code genereert voor uw REST API van een Swagger-definitie.</span><span class="sxs-lookup"><span data-stu-id="10905-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="10905-118">Node.js-code genereren</span><span class="sxs-lookup"><span data-stu-id="10905-118">Generate Node.js code</span></span> 

<span data-ttu-id="10905-119">In deze sectie van de zelfstudie wordt een API-ontwikkelingswerkstroom getoond waarin u eerst Swagger-metagegevens maakt en deze vervolgens gebruikt om automatisch servercode voor de API te genereren.</span><span class="sxs-lookup"><span data-stu-id="10905-119">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span></span> 

<span data-ttu-id="10905-120">Wijzig de map naar de map *start* en voer `yo swaggerize` uit.</span><span class="sxs-lookup"><span data-stu-id="10905-120">Change directory to the *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="10905-121">Swaggerize maakt een Node.js-project voor uw API van de Swagger-definitie in *api.json*.</span><span class="sxs-lookup"><span data-stu-id="10905-121">Swaggerize creates a Node.js project for your API from the Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="10905-122">Wanneer in Swaggerize om een projectnaam wordt gevraagd, gebruikt u *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="10905-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a><span data-ttu-id="10905-123">De projectcode aanpassen</span><span class="sxs-lookup"><span data-stu-id="10905-123">Customize the project code</span></span>

1. <span data-ttu-id="10905-124">Kopieer de map *lib* naar de map *ContactList* die door `yo swaggerize` is gemaakt en wijzig de map naar *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="10905-124">Copy the *lib* folder into the *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="10905-125">Installeer de NPM-modules `jsonpath` en `swaggerize-ui`.</span><span class="sxs-lookup"><span data-stu-id="10905-125">Install the `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="10905-126">Vervang de code in het bestand *handlers/contacts.js* door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="10905-126">Replace the code in the *handlers/contacts.js* with the following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="10905-127">Deze code gebruikt de JSON-gegevens die zijn opgeslagen in het bestand *lib/contacts.json* dat gebruikmaakt van *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="10905-127">This code uses the JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="10905-128">De nieuwe code *contacts.js* retourneert alle contactpersonen in de opslagplaats als JSON-nettolading.</span><span class="sxs-lookup"><span data-stu-id="10905-128">The new *contacts.js* code returns all contacts in the repository as a JSON payload.</span></span> 

4. <span data-ttu-id="10905-129">Vervang de code in het bestand **handlers/contacts/{id}.js** door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="10905-129">Replace the code in the **handlers/contacts/{id}.js** file with the following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="10905-130">Met deze code kunt u een padvariabele gebruiken om alleen de contactpersoon met een bepaalde id te retourneren.</span><span class="sxs-lookup"><span data-stu-id="10905-130">This code lets you use a path variable to return only the contact with a given ID.</span></span>

5. <span data-ttu-id="10905-131">Vervang de code in **server.js** door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="10905-131">Replace the code in **server.js** with the following code:</span></span>

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

    <span data-ttu-id="10905-132">Deze code brengt een aantal kleine wijzigingen aan zodat deze werkt met Azure App Service en maakt een interactieve webinterface voor uw API beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="10905-132">This code makes some small changes to let it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-the-api-locally"></a><span data-ttu-id="10905-133">De API lokaal testen</span><span class="sxs-lookup"><span data-stu-id="10905-133">Test the API locally</span></span>

1. <span data-ttu-id="10905-134">De Node.js-app starten</span><span class="sxs-lookup"><span data-stu-id="10905-134">Start up the Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="10905-135">Blader naar http://localhost:8000/contacts om de JSON voor de volledige lijst met contactpersonen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="10905-135">Browse to http://localhost:8000/contacts to view the JSON for the entire contact list.</span></span>
   
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

3. <span data-ttu-id="10905-136">Blader naar http://localhost:8000/contacts/2 om de contactpersoon met een `id` van twee weer te geven.</span><span class="sxs-lookup"><span data-stu-id="10905-136">Browse to http://localhost:8000/contacts/2 to view the contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="10905-137">Test de API met behulp van de Swagger-webinterface op http://localhost:8000/docs.</span><span class="sxs-lookup"><span data-stu-id="10905-137">Test the API using the Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Swagger-webinterface](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="10905-139"><a id="createapiapp"></a> Een API-app maken</span><span class="sxs-lookup"><span data-stu-id="10905-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="10905-140">In deze sectie kunt u de Azure CLI 2.0 gebruiken om de resources te maken om de API op Azure App Service te hosten.</span><span class="sxs-lookup"><span data-stu-id="10905-140">In this section, you use the Azure CLI 2.0 to create the resources to host the API on Azure App Service.</span></span> 

1.  <span data-ttu-id="10905-141">Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm.</span><span class="sxs-lookup"><span data-stu-id="10905-141">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="10905-142">Als u meerdere Azure-abonnementen hebt, wijzigt u het standaardabonnement naar het gewenste abonnement.</span><span class="sxs-lookup"><span data-stu-id="10905-142">If you have multiple Azure subscriptions, change the default subscription to the desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a><span data-ttu-id="10905-143">De API implementeren met Git</span><span class="sxs-lookup"><span data-stu-id="10905-143">Deploy the API with Git</span></span>

<span data-ttu-id="10905-144">Implementeer uw code in de API-app door doorvoeracties van uw lokale Git-opslagplaats naar Azure App Service te pushen.</span><span class="sxs-lookup"><span data-stu-id="10905-144">Deploy your code to the API app by pushing commits from your local Git repository to Azure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="10905-145">Initialiseer een nieuwe opslagplaats in de map *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="10905-145">Initialize a new repo in the *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="10905-146">Sluit de map *node_modules* uit die via NPM is gemaakt in een eerdere stap in de zelfstudie over Git.</span><span class="sxs-lookup"><span data-stu-id="10905-146">Exclude the *node_modules* directory created by npm in an earlier step in the tutorial from Git.</span></span> <span data-ttu-id="10905-147">Maak een nieuw `.gitignore`-bestand in de huidige map en voeg ergens in het bestand de volgende tekst toe op een nieuwe regel.</span><span class="sxs-lookup"><span data-stu-id="10905-147">Create a new `.gitignore` file in the current directory and add the following text on a new line anywhere in the file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="10905-148">Bevestig met `git status` dat de `node_modules`-map wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="10905-148">Confirm the `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="10905-149">Voer de wijzigingen door in de map.</span><span class="sxs-lookup"><span data-stu-id="10905-149">Commit the changes to the repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a><span data-ttu-id="10905-150">De API testen in Azure</span><span class="sxs-lookup"><span data-stu-id="10905-150">Test the API  in Azure</span></span>

1. <span data-ttu-id="10905-151">Open http://app_name.azurewebsites.net/contacts in een browservenster.</span><span class="sxs-lookup"><span data-stu-id="10905-151">Open a browser to http://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="10905-152">Dezelfde JSON wordt geretourneerd als toen u de aanvraag eerder in de zelfstudie lokaal indiende.</span><span class="sxs-lookup"><span data-stu-id="10905-152">You see the same JSON returned as when you made the request locally earlier in the tutorial.</span></span>

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

2. <span data-ttu-id="10905-153">Ga in een browser naar het eindpunt `http://app_name.azurewebsites.net/docs` om de Swagger-UI uit te proberen die in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10905-153">In a browser, go to the `http://app_name.azurewebsites.net/docs` endpoint to try out the Swagger UI running on Azure.</span></span>

    ![Swagger-UI](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="10905-155">U kunt nu updates voor de voorbeeld-API implementeren in Azure door doorvoeracties naar de Azure Git-opslagplaats te pushen.</span><span class="sxs-lookup"><span data-stu-id="10905-155">You can now deploy updates to the sample API to Azure simply by pushing commits to the Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="10905-156">Opruimen</span><span class="sxs-lookup"><span data-stu-id="10905-156">Clean up</span></span>

<span data-ttu-id="10905-157">Voer de volgende Azure CLI-opdracht uit als u alle resources wilt verwijderen die door deze snelstartgids zijn gemaakt:</span><span class="sxs-lookup"><span data-stu-id="10905-157">To clean up the resources created in this quickstart, run the following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="10905-158">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="10905-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="10905-159">API-apps van JavaScript-clients gebruiken met CORS</span><span class="sxs-lookup"><span data-stu-id="10905-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

