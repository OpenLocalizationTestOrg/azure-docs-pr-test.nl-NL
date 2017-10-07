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
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>Een Sails.js web app tooAzure App Service implementeren
Deze zelfstudie leert u hoe toodeploy een Sails.js app tooAzure App Service. Hallo verwerkt, kunt u enkele algemene kennis over het verzamelen tooconfigure uw toorun Node.js-app in App Service.

U leert hier nuttig vaardigheden, zoals:

* Configureer een Sails.js-app in App Service worden uitgevoerd.
* Een app-tooApp Service vanaf de opdrachtregel Hallo implementeren.
* Lezen stderr en stdout logboeken tootroubleshoot eventuele problemen bij de implementatie.
* Omgevingsvariabelen buiten broncodebeheer opslaan.
* Toegang tot Azure-omgevingsvariabelen van uw app.
* Verbinding maken met tooa-database (MongoDB).

U hebt enige ervaring met Sails.js. Deze zelfstudie is niet bedoeld toohelp u met problemen in het algemeen toorunning Sail.js gerelateerd.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen
- [Azure CLI 2.0](app-service-web-nodejs-sails.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="prerequisites"></a>Vereisten
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Azure CLI 2.0](/cli/azure/install-az-cli2)
* Een Microsoft Azure-account. Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account. Een eenvoudige app maken en te spelen met voor up tooan uur--geen creditcard nodig en zonder verdere verplichtingen.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>Stap 1: Maken en configureren van een Sails.js-app lokaal
Snel Maak eerst een standaard Sails.js-app in uw ontwikkelingsomgeving met de volgende stappen:

1. Open Hallo opdrachtregelprogramma terminal van uw keuze en `CD` tooa werkmap.
2. Een Sails.js-app maken en uitvoeren:

        sails new <app_name>
        cd <app_name>
        sails lift

    Zorg ervoor dat u kunt de standaardstartpagina toohello op http://localhost:1377 navigeren.

1. Schakel vervolgens de logboekregistratie voor Azure. Maak een bestand met de naam in de hoofdmap `iisnode.yml` en Hallo volgende twee regels toe te voegen:

        loggingEnabled: true
        logDirectory: iisnode

    Logboekregistratie is nu ingeschakeld voor Hallo [iisnode](https://github.com/tjanczuk/iisnode) server dat gebruikmaakt van Azure App Service toorun Node.js-apps. 
    Zie voor meer informatie over hoe dit werkt [hoe toodebug een Node.js web-app in Azure App Service](web-sites-nodejs-debug.md).

2. Configureer vervolgens Hallo Sails.js app toouse Azure omgevingsvariabelen. Open config/env/production.js tooconfigure uw productieomgeving en stel `port` en `hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    Vindt u documentatie voor deze configuratie-instellingen in de [Sails.js documentatie](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Vervolgens hardcode hello Node.js-versie gewenste toouse. Voeg in package.json, Hallo volgende `engines` eigenschap tooset hello Node.js versie tooone we willen.

        "engines": {
            "node": "6.9.1"
        },

5. Ten slotte een Git-opslagplaats te initialiseren en uw bestanden wordt doorgevoerd. In de hoofdmap van de toepassing is (package.json is) Hallo, Hallo volgende Git-opdrachten uitvoeren:

        git init
        git add .
        git commit -m "<your commit message>"

Uw code is gereed toobe geïmplementeerd. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>Stap 2: Een Azure-app maken en implementeren van Sails.js

Vervolgens Hallo App Service-resource in Azure maken en implementeren van uw app Sails.js tooit.

1. aanmelden tooAzure als volgt te werk:

        az login

    Ga als volgt Hallo vragen toocontinue Hallo aanmelding in een browser met een Microsoft-account op met uw Azure-abonnement.

3. Hallo implementatie gebruikersgroep in te stellen voor App Service. U gaat later code implementeren met behulp van deze referenties.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) met een naam. Voor deze zelfstudie over Node.js hoeft u niet zeker tooknow wat is.

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee welke mogelijke waarden u kunt gebruiken voor `<location>`, gebruik Hallo `az appservice list-locations` CLI-opdracht.

3. Maken van een 'gratis' [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) met een naam. Deze zelfstudie over Node.js, net weten dat u voor web-apps geen in dit abonnement afgeschreven.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. Maak een nieuwe web-app met een unieke naam in `<app_name>`.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Stap 3: Configureer en implementeer uw app Sails.js

1. Lokale Git-implementatie voor uw nieuwe web-app te configureren met Hallo volgende opdracht:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    U ontvangt een JSON-uitvoer als volgt, wat betekent dat Hallo externe Git-opslagplaats is geconfigureerd:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Hallo-URL toevoegen in Hallo JSON als een externe Git voor uw lokale opslagplaats (aangeroepen `azure` voor eenvoud).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Implementeer uw code voorbeeld toohello `azure` externe Git. Wanneer u wordt gevraagd, gebruikt u Hallo-implementatiereferenties die u eerder hebt geconfigureerd.

        git push azure master

7. Ten slotte uw live Azure-app in de browser Hallo NET starten:

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    U ziet nu Hallo dezelfde Sails.js-startpagina.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Problemen met uw implementatie oplossen
Als uw toepassing Sails.js voor een bepaalde reden in App Service mislukt, vinden Hallo stderr logboeken toohelp oplossen van dit probleem.
Zie voor meer informatie [hoe toodebug een Node.js web-app in Azure App Service](web-sites-nodejs-debug.md).
Als het Hallo-app is gestart, Hallo stdout logboek moet worden weergegeven u bekend het Hallo-bericht:

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

U kunt de granulatie van Hallo stdout Logboeken in Hallo beheren [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) bestand.

## <a name="connect-tooa-database-in-azure"></a>Verbinding maken met tooa database in Azure
tooconnect tooa database in Azure, Hallo-database van uw keuze maakt in Azure, zoals Azure SQL Database, MySQL, MongoDB, Azure (Redis)-Cache, enz., en gebruik Hallo overeenkomt [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit. Hallo stappen in deze sectie laten zien hoe u tooconnect tooMongoDB met behulp van een [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, die ondersteuning voor MongoDB-clientverbindingen bieden.

1. [Maakt een Cosmos-DB-account met protocolondersteuning voor MongoDB](../documentdb/documentdb-create-mongodb-account.md).
2. [Maak een Cosmos-DB-verzameling en de database](../documentdb/documentdb-create-collection.md). Hallo-naam van Hallo verzameling maakt niet uit, maar u moet Hallo-naam van Hallo-database wanneer u verbinding vanaf Sails.js maakt.
3. [Hallo verbindingsinformatie vinden voor uw database Cosmos DB](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Vanaf de opdrachtregel terminal Hallo MongoDB-adapter te installeren:

        npm install sails-mongo --save

3. Open config/connections.js en Hallo verbinding toohello objectenlijst volgende toevoegen:

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
    > Hallo `ssl: true` optie is belangrijk omdat [Cosmos DB vereist](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Voor elke omgevingsvariabele (`process.env.*`), moet u tooset in App Service. toodo deze, Voer Hallo volgende opdrachten uit uw terminal. Hallo-verbindingsgegevens voor de Cosmos-DB gebruiken.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Als uw instellingen in Azure app-instellingen, houdt u gevoelige gegevens buiten uw broncodebeheer (Git). Vervolgens configureert u uw development environment toouse Hallo dezelfde verbindingsgegevens.
5. Open config/local.js en Hallo na verbindingen object toevoegen:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Deze configuratie vervangt Hallo-instellingen in het bestand config/connections.js voor Hallo lokale omgeving. Dit bestand is uitgesloten door Hallo standaard .gitignore in uw project, zodat deze niet worden opgeslagen in Git. U bent nu, kunnen tooconnect tooyour Cosmos-DB (MongoDB)-database van uw Azure-web-app en van uw lokale ontwikkelingsomgeving.
6. Open config/env/production.js tooconfigure uw productieomgeving en voeg de volgende Hallo `models` object:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Open config/env/development.js tooconfigure uw ontwikkelomgeving en voeg de volgende Hallo `models` object:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`u kunt database migratie functies toocreate gebruiken en eenvoudig database verzamelingen of -tabellen bijwerken. Echter, `migrate: 'safe'` wordt gebruikt voor uw omgeving voor Azure (productie) omdat Sails.js niet toe u toouse dat staat `migrate: 'alter'` in een productieomgeving (Zie [Sails.js documentatie](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. Van Hallo terminal [genereren](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) een Sails.js [API blauwdruk](http://sailsjs.org/documentation/concepts/blueprints) zoals u normaal doet, voer `sails lift` Hallo database maakt met de migratie van Sails.js-database. Bijvoorbeeld:

         sails generate api mywidget
         sails lift

    Hallo `mywidget` die worden gegenereerd door deze opdracht inhoudsmodel is leeg, maar we tooshow of er verbinding met de database kunnen gebruiken.
    Bij het uitvoeren van `sails lift`, het Hallo ontbrekende verzamelingen maakt en tabellen voor Hallo modellen uw app gebruikt.
9. Toegang Hallo blauwdruk API u zojuist hebt gemaakt in de browser Hallo. Bijvoorbeeld:

        http://localhost:1337/mywidget/create

    Hallo API Hallo gemaakt vermelding back tooyou moet worden geretourneerd in browservenster hello, wat betekent dat uw verzameling is gemaakt.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Nu uw wijzigingen tooAzure push en tooyour app toomake ervoor werkt nog altijd bladeren.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Hallo blauwdruk API toegang van uw Azure-web-app. Bijvoorbeeld:

         http://<appname>.azurewebsites.net/mywidget/create

     Als Hallo API een andere nieuwe vermelding retourneert, praten uw Azure-web-app tooyour Cosmos-DB (MongoDB)-database.

## <a name="more-resources"></a>Meer bronnen
* [Aan de slag met Node.js-web-apps in Azure App Service](app-service-web-get-started-nodejs.md)
* [Node.js-modules gebruiken met Azure-toepassingen](../nodejs-use-node-modules-azure-apps.md)
