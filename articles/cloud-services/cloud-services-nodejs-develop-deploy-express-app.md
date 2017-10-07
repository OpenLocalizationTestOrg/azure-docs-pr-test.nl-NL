---
title: aaaWeb App snelle (Node.js) | Microsoft Docs
description: Een zelfstudie die is gebaseerd op Hallo cloud service zelfstudie en laat zien hoe toouse Hallo Express-module.
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>Een Node.js-webtoepassing met een snelle op een Azure Cloud Service bouwen
Node.js bevat een minimale set van de functionaliteit in Hallo core runtime.
Ontwikkelaars vaak 3e partij modules tooprovide aanvullende functionaliteit gebruiken bij het ontwikkelen van een Node.js-toepassing. In deze zelfstudie maakt u een nieuwe toepassing met behulp van Hallo [Express] [ Express] module waarmee een MVC-framework biedt voor het maken van Node.js-webtoepassingen.

Een schermopname van de toepassing hello voltooid lager is dan:

![Een webbrowser waarin Welkom tooExpress in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>Een Cloud Service-Project maken
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

Uitvoeren van de volgende Hallo toocreate stappen een nieuwe cloudserviceproject met de naam 'expressapp':

1. Van Hallo **startmenu** of **startscherm**, zoeken naar **Windows PowerShell**. Ten slotte de met de rechtermuisknop op **Windows PowerShell** en selecteer **als Administrator uitvoeren**.
   
    ![Azure PowerShell-pictogram](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. Wijzig de mappen toohello **c:\\knooppunt** directory en voer vervolgens de volgende opdrachten toocreate een nieuwe oplossing met de naam Hallo **expressapp** en een Webrol met de naam **WebRole1** :
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > Standaard **Add-AzureNodeWebRole** maakt gebruik van een oudere versie van Node.js. Hallo **Set AzureServiceProjectRole** instructie hiervoor Hiermee geeft u Azure toouse v0.10.21 van knooppunt.  Houd er rekening mee Hallo parameters zijn hoofdlettergevoelig.  U kunt controleren of de juiste versie Hallo van Node.js is geselecteerd door te controleren Hallo **engines** eigenschap in **WebRole1\package.json**.
    > 
    > 

## <a name="install-express"></a>Express installeren
1. Hallo Express-generator door uitgifte van Hallo volgende opdracht installeren:
   
        PS C:\node\expressapp> npm install express-generator -g
   
    Hallo-uitvoer van Hallo npm opdracht ziet er vergelijkbaar toohello resultaat hieronder. 
   
    ![Windows PowerShell weergeven Hallo uitvoer van Hallo npm snelle opdracht installeren.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. Wijzig de mappen toohello **WebRole1** directory en gebruik Hallo snelle opdracht toogenerate een nieuwe toepassing:
   
        PS C:\node\expressapp\WebRole1> express
   
    U na vragen aan gebruiker toooverwrite uw eerdere toepassing zijn. Voer **y** of **Ja** toocontinue. Express wordt gegenereerd Hallo app.js bestands- en de mappenstructuur van een voor het bouwen van uw toepassing.
   
    ![Hallo-uitvoer van Hallo snelle opdracht](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. tooinstall extra afhankelijkheden gedefinieerd in Hallo package.json-bestand, Voer Hallo volgende opdracht:
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Hallo-uitvoer van Hallo npm installatieopdracht](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. Gebruik Hallo volgende opdracht toocopy hello **bin/www** bestand te**server.js**. Dit is dus cloudservice Hallo Hallo toegangspunt voor deze toepassing kunt vinden.
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   Nadat u deze opdracht is voltooid, hebt u een **server.js** bestand in map Hallo WebRole1.
5. Hallo wijzigen **server.js** tooremove een Hallo '.' tekens bevatten uit Hallo volgt regel.
   
       var app = require('../app');
   
   Na deze wijziging, Hallo regel moet worden weergegeven als volgt.
   
       var app = require('./app');
   
   Deze wijziging is vereist omdat we Hallo-bestand is verplaatst (voorheen **bin/www**,) toohello dezelfde directory als Hallo app-bestand wordt vereist. Nadat u deze wijziging, opslaan Hallo **server.js** bestand.
6. Gebruik Hallo opdracht toorun Hallo toepassing in hello Azure-emulator te volgen:
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Een webpagina met Welkom tooexpress.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>Hallo weergave wijzigen
Nu wijzigen Hallo weergave toodisplay Hallo-bericht 'Welkom tooExpress in Azure'.

1. Voer Hallo opdrachtbestand tooopen hello index.jade te volgen:
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Hallo-inhoud van Hallo index.jade bestand.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade is Hallo standaard weergave-engine wordt gebruikt door toepassingen van Express. Zie voor meer informatie over Jade weergave-engine Hallo [http://jade-lang.com][http://jade-lang.com].
2. Hallo laatste regel van tekst wijzigen door toe te voegen **in Azure**.
   
   ![Hallo index.jade bestand, de laatste regel Hallo leest: p Welkom te\#{title} in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. Hallo-bestand opslaan en sluit u Kladblok af.
4. Vernieuw de browser en ziet u uw wijzigingen.
   
   ![Een browservenster Hallo pagina bevat Welkom tooExpress in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

Gebruik na testtoepassing Hallo Hallo **Stop AzureEmulator** cmdlet toostop Hallo-emulator.

## <a name="publishing-hello-application-tooazure"></a>Publishing Hallo toepassing tooAzure
Gebruik in hello Azure PowerShell-venster Hallo **Publish-AzureServiceProject** cmdlet toodeploy hello tooa cloud toepassingsservice

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

Zodra het Hallo-implementatie is voltooid, wordt uw browser openen en Hallo webpagina weergegeven.

![Een webbrowser om Hallo Express pagina weer te geven. Hallo URL geeft dat het nu wordt gehost op Azure.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [Node.js Developer Center](/develop/nodejs/).

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


