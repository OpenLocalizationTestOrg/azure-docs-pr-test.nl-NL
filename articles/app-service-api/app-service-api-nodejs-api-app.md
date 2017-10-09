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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>Een Node.js-RESTful-API maken en deze tooan API-app in Azure implementeren
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Deze snelstartgids toont hoe toocreate een REST-API geschreven met behulp van Node.js [Express](http://expressjs.com/)met een [Swagger](http://swagger.io/) definitie en implementeren als een [API-app](app-service-api-apps-why-best-platform.md) op Azure. U Hallo-app met opdrachtregelprogramma's maken, configureren van resources met Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), Hallo-app met Git en implementeren.  Wanneer u klaar bent, hebt u een werkende voorbeeld-REST API die wordt uitgevoerd op Azure.

## <a name="prerequisites"></a>Vereisten

* [Git](https://git-scm.com/)
* [Node.js en NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Uw omgeving voorbereiden

1. Voer in een terminalvenster Hallo opdracht tooclone Hallo voorbeeld tooyour lokale computer te volgen.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Toohello map waarin de voorbeeldcode Hallo wijzigen.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Installeer [Swaggerize](https://www.npmjs.com/package/swaggerize-express) op uw lokale machine. Swaggerize is een hulpprogramma dat Node.js-code genereert voor uw REST API van een Swagger-definitie.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Node.js-code genereren 

Deze sectie van de zelfstudie Hallo modellen een API ontwikkelingswerkstroom getoond waarin u eerst Swagger-metagegevens maken en gebruiken die tooscaffold (automatisch genereren) servercode voor Hallo API. 

Wijzigen van de directory toohello *start* map, voer `yo swaggerize`. Swaggerize maakt een Node.js-project voor uw API van Hallo Swagger-definitie in *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Wanneer in Swaggerize om een projectnaam wordt gevraagd, gebruikt u *ContactList*.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>Hallo projectcode aanpassen

1. Kopiëren Hallo *lib* map in Hallo *ContactList* map gemaakt door `yo swaggerize`, wijzigt u vervolgens de directory in *ContactList*.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Hallo installeren `jsonpath` en `swaggerize-ui` NPM-modules. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Vervang de code Hallo in Hallo *handlers/contacts.js* Hello code te volgen: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Deze code gebruikt Hallo JSON-gegevens opgeslagen in *lib/contacts.json* afgehandeld door *lib/contactRepository.js*. Hallo nieuwe *contacts.js* code retourneert alle contactpersonen in het Hallo-opslagplaats als JSON-nettolading. 

4. Vervang de code Hallo in Hallo **handlers/contacts/{id}.js** bestand met de volgende code Hallo:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Deze code kunt u een contactpersoon voor pad variabele tooreturn Hallo alleen gebruiken met een opgegeven ID.

5. Vervang de code Hallo in **server.js** Hello code te volgen:

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

    Deze code maakt een aantal kleine wijzigingen toolet het werken met Azure App Service en een interactieve webinterface voor uw API beschrijft.

### <a name="test-hello-api-locally"></a>Test Hallo API lokaal

1. Hallo Node.js-app starten
    ```bash
    npm start
    ```
    
2. Blader toohttp://localhost:8000 / tooview Hallo JSON contactpersonen voor Hallo complete lijst met contactpersonen.
   
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

3. Blader toohttp://localhost:8000/contacts/2 tooview Hallo contact met een `id` van twee.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. Hallo-API met Hallo Swagger webinterface op http://localhost: 8000/docs testen.
   
    ![Swagger-webinterface](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> Een API-app maken

In deze sectie gebruikt u hello Azure CLI 2.0 toocreate Hallo resources toohost Hallo API in Azure App Service. 

1.  Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.

    ```azurecli-interactive
    az login
    ```

2. Als u meerdere Azure-abonnementen hebt, gewenste wijziging Hallo standaard abonnement toohello een.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>Hallo-API met Git implementeren

Implementeer uw code toohello API-app door doorvoeracties te pushen van uw lokale Git-opslagplaats tooAzure App Service.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Initialiseren van een nieuwe opslagplaats in Hallo *ContactList* directory. 

    ```bash
    git init .
    ```

3. Hallo uitsluiten *node_modules* directory gemaakt door npm in een eerdere stap in de zelfstudie Hallo van Git. Maak een nieuwe `.gitignore` -bestand in de huidige map Hallo en Hallo tekst volgen op een nieuwe regel overal in het Hallo-bestand toevoegen.

    ```
    node_modules/
    ```
    Hallo bevestigen `node_modules` map wordt genegeerd met `git status`.

4. Hallo wijzigingen toohello opslagplaats doorvoeren.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>Test Hallo API in Azure

1. Open een browser toohttp://app_name.azurewebsites.net/contacts. U ziet dat dezelfde JSON geretourneerd als wanneer u lokaal Hallo-aanvraag heeft ingediend eerder in de zelfstudie Hallo Hallo.

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

2. Ga in een browser toohello `http://app_name.azurewebsites.net/docs` eindpunt tootry uit Hallo Swagger-gebruikersinterface die zijn uitgevoerd op Azure.

    ![Swagger-UI](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    U kunt nu updates toohello voorbeeld API tooAzure implementeren door doorvoeracties toohello Azure Git-opslagplaats te pushen.

## <a name="clean-up"></a>Opruimen

tooclean Hallo-resources die zijn gemaakt in deze snelstartgids, Hallo na Azure CLI-opdracht uitvoeren:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Volgende stap 
> [!div class="nextstepaction"]
> [API-apps van JavaScript-clients gebruiken met CORS](app-service-api-cors-consume-javascript.md)

