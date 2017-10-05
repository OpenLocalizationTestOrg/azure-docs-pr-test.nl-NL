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
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a>Een Sails.js-web-app implementeren in Azure App Service
Deze zelfstudie laat zien hoe u een Sails.js-app implementeren in Azure App Service. In het proces kunt u een aantal algemene kennis over het configureren van uw Node.js-app in App Service uit te voeren verzamelen.

U leert hier nuttig vaardigheden, zoals:

* Configureer een Sails.js-app in App Service worden uitgevoerd.
* Een app in App Service implementeren vanaf de opdrachtregel.
* Lees stderr stdout logboeken en eventuele problemen met implementatie.
* Omgevingsvariabelen buiten broncodebeheer opslaan.
* Toegang tot Azure-omgevingsvariabelen van uw app.
* Verbinding maken met een database (MongoDB).

U hebt enige ervaring met Sails.js. Deze zelfstudie is niet bedoeld om u te helpen problemen met betrekking tot Sail.js in het algemeen wordt uitgevoerd.

## <a name="cli-versions-to-complete-the-task"></a>CLI-versies om de taak uit te voeren

U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md): onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel
- [Azure CLI 2.0](app-service-web-nodejs-sails.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel

## <a name="prerequisites"></a>Vereisten
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Azure CLI 2.0](/cli/azure/install-az-cli2)
* Een Microsoft Azure-account. Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account. U kunt een beginnerstoepassing maken en hier een uur mee spelen. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>Stap 1: Maken en configureren van een Sails.js-app lokaal
Snel Maak eerst een standaard Sails.js-app in uw ontwikkelingsomgeving met de volgende stappen:

1. Open de van uw keuze en `CD` in een werkmap.
2. Een Sails.js-app maken en uitvoeren:

        sails new <app_name>
        cd <app_name>
        sails lift

    Zorg ervoor dat u kunt naar de standaardstartpagina op http://localhost:1377 navigeren.

1. Schakel vervolgens de logboekregistratie voor Azure. Maak een bestand met de naam in de hoofdmap `iisnode.yml` en voeg de volgende twee regels:

        loggingEnabled: true
        logDirectory: iisnode

    Logboekregistratie is nu ingeschakeld voor de [iisnode](https://github.com/tjanczuk/iisnode) server die de Azure App Service gebruikt voor het uitvoeren van Node.js-apps. 
    Zie voor meer informatie over hoe dit werkt [fouten opsporen in een Node.js-web-app in Azure App Service](web-sites-nodejs-debug.md).

2. Configureer vervolgens de Sails.js-app voor het gebruik van Azure omgevingsvariabelen. Open config/env/production.js voor het configureren van uw productieomgeving en stel `port` en `hookTimeout`:

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    Vindt u documentatie voor deze configuratie-instellingen in de [Sails.js documentatie](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Vervolgens hardcode voor de Node.js-versie die u wilt gebruiken. In package.json, voeg de volgende `engines` eigenschap de Node.js-versie die we willen instellen.

        "engines": {
            "node": "6.9.1"
        },

5. Ten slotte een Git-opslagplaats te initialiseren en uw bestanden wordt doorgevoerd. In de hoofdmap van de toepassing (package.json is), voer de volgende Git-opdrachten:

        git init
        git add .
        git commit -m "<your commit message>"

Uw code is gereed om te worden geïmplementeerd. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>Stap 2: Een Azure-app maken en implementeren van Sails.js

Vervolgens de App Service-resource maken in Azure en uw Sails.js-app te implementeren.

1. Meld u aan bij Azure achtige dus:

        az login

    Volg de aanwijzing om de aanmelding in een browser voort te zetten met het Microsoft-account waarmee u uw Azure-abonnement hebt afgesloten.

3. Stel de implementatiegebruiker in voor App Service. U gaat later code implementeren met behulp van deze referenties.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) met een naam. Voor deze zelfstudie Node.js moet niet wat u weten wat het.

        az group create --location "<location>" --name my-sailsjs-app-group

    Gebruik de CLI-opdracht `az appservice list-locations` om te zien welke waarden u kunt gebruiken voor `<location>`.

3. Maken van een 'gratis' [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) met een naam. Deze zelfstudie over Node.js, net weten dat u voor web-apps geen in dit abonnement afgeschreven.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. Maak een nieuwe web-app met een unieke naam in `<app_name>`.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Stap 3: Configureer en implementeer uw app Sails.js

1. Configureer een lokale Git-implementatie voor uw nieuwe web-app. Doe dit met de volgende opdracht:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    U ziet JSON-uitvoer zoals hieronder, wat betekent dat de externe Git-opslagplaats is geconfigureerd:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Voeg de URL in de JSON toe als een externe Git voor uw lokale opslagplaats (voor de duidelijkheid `azure` genoemd).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Implementeer de voorbeeldcode in de externe Git `azure`. Gebruik wanneer dit wordt gevraagd de implementatiereferenties die u eerder hebt geconfigureerd.

        git push azure master

7. Ten slotte uw live Azure-app in de browser net start:

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    U ziet nu de dezelfde Sails.js-startpagina.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Problemen met uw implementatie oplossen
Als uw toepassing Sails.js voor een bepaalde reden in App Service mislukt, vindt u de logboeken stderr bij het oplossen van deze.
Zie voor meer informatie [fouten opsporen in een Node.js-web-app in Azure App Service](web-sites-nodejs-debug.md).
Als de app is gestart, het logboek stdout moet u de vertrouwde bericht weergeven:

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

U kunt de granulatie van de logboeken stdout in beheren de [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) bestand.

## <a name="connect-to-a-database-in-azure"></a>Verbinding maken met een database in Azure
Voor verbinding met een database in Azure, u de database van uw keuze maken in Azure, zoals Azure SQL Database, MySQL, MongoDB, Azure (Redis)-Cache, enz., en de bijbehorende [datastore adapter](https://github.com/balderdashy/sails#compatibility) tot stand te brengen. De stappen in deze sectie ziet u hoe u met MongoDB te maken met een [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, die ondersteuning voor MongoDB-clientverbindingen bieden.

1. [Maakt een Cosmos-DB-account met protocolondersteuning voor MongoDB](../documentdb/documentdb-create-mongodb-account.md).
2. [Maak een Cosmos-DB-verzameling en de database](../documentdb/documentdb-create-collection.md). De naam van de verzameling maakt niet uit, maar u moet de naam van de database als u verbinding vanaf Sails.js maakt.
3. [De verbindingsgegevens voor de database van de Cosmos-DB vinden](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Vanaf de opdrachtregel terminal de MongoDB-adapter te installeren:

        npm install sails-mongo --save

3. Open config/connections.js en het volgende verbindingsobject toevoegen aan de lijst:

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
    > De `ssl: true` optie is belangrijk omdat [Cosmos DB vereist](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Voor elke omgevingsvariabele (`process.env.*`), moet u deze eigenschap instellen in App Service. Voer hiertoe de volgende opdrachten vanaf uw computer. Gebruik de gegevens voor uw Cosmos-DB.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Als uw instellingen in Azure app-instellingen, houdt u gevoelige gegevens buiten uw broncodebeheer (Git). Vervolgens configureert u uw ontwikkelomgeving voor het gebruik van dezelfde verbindingsinformatie.
5. Open config/local.js en voeg de volgende verbindingen-object:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Deze configuratie vervangt de instellingen in het bestand config/connections.js voor de lokale omgeving. Dit bestand is uitgesloten door de standaard .gitignore in uw project, zodat deze niet worden opgeslagen in Git. U bent nu verbinding kunnen maken met uw database Cosmos-DB (MongoDB) van uw Azure-web-app en van uw lokale ontwikkelingsomgeving.
6. Open config/env/production.js voor het configureren van uw productieomgeving en voeg de volgende `models` object:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Open config/env/development.js voor het configureren van uw ontwikkelomgeving en voeg de volgende `models` object:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`kunt u migratie databasefuncties maken en bijwerken van database verzamelingen of tabellen eenvoudig te gebruiken. Echter, `migrate: 'safe'` wordt gebruikt voor uw omgeving voor Azure (productie) omdat Sails.js staat niet toe dat u gebruikt `migrate: 'alter'` in een productieomgeving (Zie [Sails.js documentatie](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. Vanaf de terminal [genereren](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) een Sails.js [API blauwdruk](http://sailsjs.org/documentation/concepts/blueprints) zoals u normaal doet, voer `sails lift` maken van de database met Sails.js database wilt migreren. Bijvoorbeeld:

         sails generate api mywidget
         sails lift

    De `mywidget` die worden gegenereerd door deze opdracht inhoudsmodel is leeg, maar we kunnen deze gebruiken om weer te geven of er verbinding met de database.
    Bij het uitvoeren van `sails lift`, worden de ontbrekende verzamelingen en tabellen voor de modellen uw app wordt gebruikt.
9. Toegang tot de blauwdruk API die u zojuist hebt gemaakt in de browser. Bijvoorbeeld:

        http://localhost:1337/mywidget/create

    De API moet de gemaakte vermelding retourneren aan u in het browservenster, wat betekent dat uw verzameling is gemaakt.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Nu pusht u uw wijzigingen naar Azure en blader naar uw app om ervoor te zorgen dat het nog steeds werkt.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Toegang tot de blauwdruk API van uw Azure-web-app. Bijvoorbeeld:

         http://<appname>.azurewebsites.net/mywidget/create

     Als de API een andere nieuwe vermelding retourneert, wordt uw Azure-web-app communiceren met uw database Cosmos-DB (MongoDB).

## <a name="more-resources"></a>Meer bronnen
* [Aan de slag met Node.js-web-apps in Azure App Service](app-service-web-get-started-nodejs.md)
* [Node.js-modules gebruiken met Azure-toepassingen](../nodejs-use-node-modules-azure-apps.md)
