---
title: aaaNode.js toepassing met Socket.io | Microsoft Docs
description: Meer informatie over hoe toouse socket.io in een node.js-toepassing wordt gehost op Azure.
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>Het bouwen van een Node.js-chattoepassing met Socket.IO op een Azure Cloudservice
Socket.IO biedt realtime-communicatie tussen tussen uw node.js-server en clients. Deze zelfstudie helpt u bij het hosten van een socket. I/o gebaseerd chatprogramma op Azure. Zie voor meer informatie over Socket.IO <http://socket.io/>.

Een schermopname van de toepassing hello voltooid lager is dan:

![Een browservenster met Hallo service die wordt gehost op Azure][completed-app]  

## <a name="prerequisites"></a>Vereisten
Zorg ervoor dat Hallo na producten en versies zijn geïnstalleerd toosuccessfully voltooid Hallo voorbeeld in dit artikel:

* [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) installeren
* [Node.js](https://nodejs.org/download/) installeren
* Installeer [Python versie 2.7.10](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>Een Cloud Service-Project maken
Hallo volgende stappen maakt u Hallo-cloudserviceproject die als host Hallo Socket.IO toepassing fungeert.

1. Van Hallo **startmenu** of **startscherm**, zoeken naar **Windows PowerShell**. Ten slotte de met de rechtermuisknop op **Windows PowerShell** en selecteer **als Administrator uitvoeren**.
   
    ![Azure PowerShell-pictogram][powershell-menu]
2. Maak een map met de naam **c:\\knooppunt**. 
   
        PS C:\> md node
3. Wijzig de mappen toohello **c:\\knooppunt** directory
   
        PS C:\> cd node
4. Voer Hallo na opdrachten toocreate een nieuwe oplossing met de naam **chatapp** en een werkrol toe met de naam **WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    Hier ziet u Hallo antwoord te volgen:
   
    ![Hallo-uitvoer van de nieuwe Hallo-azureservice en voeg azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>Hallo chatten voorbeeld downloaden
Voor dit project, gebruiken we Hallo chat voorbeeld uit Hallo [Socket.IO GitHub-opslagplaats]. Hallo te volgen stappen toodownload Hallo-voorbeeld uitvoeren en voeg deze toohello project dat u eerder hebt gemaakt.

1. Maken van een lokale kopie van het Hallo-opslagplaats met behulp van Hallo **kloon** knop. U kunt ook Hallo **ZIP** knop toodownload Hallo project.
   
   ![Een browservenster https://github.com/LearnBoost/socket.io/tree/master/examples/chat, weergeven met Hallo ZIP downloadpictogram gemarkeerd][chat-example-view]
2. Navigeer Hallo directorystructuur van de lokale opslagplaats Hallo totdat u bij Hallo aankomt **voorbeelden\\chat** directory. Kopieer Hallo inhoud van deze directory toothe **C:\\knooppunt\\chatapp\\WorkerRole1** directory eerder hebt gemaakt.
   
   ![Verkenner weergeven Hallo inhoud van Hallo voorbeelden\\chat-map opgehaald uit het Hallo-archief][chat-contents]
   
   Hallo gemarkeerde items in de bovenstaande Hallo Hallo bestanden zijn gekopieerd uit Hallo **voorbeelden\\chat** directory
3. In Hallo **C:\\knooppunt\\chatapp\\WorkerRole1** directory, delete Hallo **server.js** bestand en wijzig de naam Hallo **app.js**bestand te**server.js**. Hiermee verwijdert u de standaard Hallo **server.js** bestand dat eerder is gemaakt door Hallo **toevoegen AzureNodeWorkerRole** cmdlet en vervangt deze met de toepassing hello bestand van Hallo chat-voorbeeld.

### <a name="modify-serverjs-and-install-modules"></a>Wijzigen van Server.js en -Modules installeren
Voordat u testtoepassing Hallo in hello Azure-emulator maken we een aantal kleine wijzigingen. Voer Hallo stappen toothe server.js-bestand te volgen:

1. Open Hallo **server.js** -bestand in Visual Studio of een teksteditor.
2. Hallo zoeken **Module afhankelijkheden** sectie aan Hallo begin van server.js en wijzig Hallo regel die **sio require('.. = //.. lib//socket.IO')** te**sio require('socket.io') =** zoals hieronder wordt weergegeven:
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. tooensure hello toepassing luistert op de juiste poort hello, server.js geopend in Kladblok of uw favoriete editor en wijzigt u de volgende regel door te vervangen **3000** met **process.env.port** zoals wordt weergegeven hieronder:
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

Na het opslaan van wijzigingen hello te**server.js**Hallo stappen te volgen gebruiken voor het installeren van vereiste modules en vervolgens test Hallo toepassingen in de Azure-emulator:

1. Met behulp van **Azure PowerShell**, wijzig de mappen toohello **C:\\knooppunt\\chatapp\\WorkerRole1** directory en gebruik Hallo opdracht tooinstall Hallo na modules die zijn vereist voor deze toepassing:
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   Hiermee installeert u Hallo-modules die worden vermeld in Hallo package.json-bestand. Nadat het Hallo-opdracht is voltooid, ziet u uitvoer vergelijkbare toothe volgende:
   
   ![Hallo-uitvoer van Hallo npm installatieopdracht][The-output-of-the-npm-install-command]
2. Aangezien dit voorbeeld oorspronkelijk deel uit van Hallo Socket.IO GitHub-opslagplaats en rechtstreeks Hallo Socket.IO bibliotheek relatief pad verwijst naar, is niet Socket.IO verwezen in Hallo package.json-bestand, dus er moet worden geïnstalleerd door uitgifte van de volgende opdracht Hallo:
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>Testen en implementeren
1. Hallo-emulator door uitgifte van de volgende opdracht Hallo starten:
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > Als u problemen ondervindt met bijvoorbeeld emulator te starten.: begin AzureEmulator: Er is een onverwachte fout opgetreden.  Details: Aangetroffen een onverwachte fout Hallo communicatieobject, System.ServiceModel.Channels.ServiceChannel, kan niet worden gebruikt voor communicatie omdat het Hallo status Faulted heeft.
   
      Installeer AzureAuthoringTools v 2.7.1 en AzureComputeEmulator v 2.7: Zorg ervoor dat de versie die overeenkomt met.
   >
   >


2. Open een browser en te navigeren**http://127.0.0.1**.
3. Wanneer Hallo browservenster wordt geopend, voer een bijnaam en klik vervolgens op ENTER drukken.
   Hierdoor kunt u berichten toopost als een specifieke bijnaam. functionaliteit voor meerdere gebruikers tootest, extra browservensters met dezelfde URL te openen en voer verschillende bijnaam.
   
   ![Twee browservensters chatberichten van Gebruiker1 als Gebruiker2 weergeven](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. Stop na testtoepassing Hallo Hallo emulator door de volgende opdracht:
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. toodeploy hello toepassing tooAzure, gebruik de **Publish-AzureServiceProject** cmdlet. Bijvoorbeeld:
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > Ervoor toouse een unieke naam zijn, anders Hallo publicatieproces zal mislukken. Nadat het Hallo-implementatie is voltooid, wordt de Hallo browser openen en de Navigeer toohello geïmplementeerd service.
   > 
   > Als u ontvangt een foutbericht waarin wordt gemeld dat Hallo opgegeven naam van abonnement bestaat niet in Hallo geïmporteerd publicatieprofiel, moet u downloaden en importeren Hallo publicatieprofiel voor uw abonnement voordat u tooAzure implementeert. Zie Hallo **implementeren Hallo toepassing tooAzure** sectie van [bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![Een browservenster met Hallo service die wordt gehost op Azure][completed-app]
   
   > [!NOTE]
   > Als u ontvangt een foutbericht waarin wordt gemeld dat Hallo opgegeven naam van abonnement bestaat niet in Hallo geïmporteerd publicatieprofiel, moet u downloaden en importeren Hallo publicatieprofiel voor uw abonnement voordat u tooAzure implementeert. Zie Hallo **implementeren Hallo toepassing tooAzure** sectie van [bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

Uw toepassing wordt nu uitgevoerd in Azure, en kan chatberichten tussen verschillende clients met Socket.IO doorsturen.

> [!NOTE]
> Voor de eenvoud, dit voorbeeld is beperkt toochatting tussen gebruikers verbonden toohello hetzelfde exemplaar. Dit betekent dat als cloudservice Hallo twee exemplaren van worker-rol maakt, gebruikers is alleen mogelijk toochat met anderen verbonden toohello hetzelfde exemplaar van de worker-rol. tooscale hello toowork toepassing met meerdere rolexemplaren, u kunt een technologie zoals Socket.IO archiefstatus voor Service Bus tooshare Hallo over exemplaren. Zie voor voorbeelden Hallo Service Bus-wachtrijen en onderwerpen voorbeelden voor gebruik in Hallo [Azure SDK voor Node.js GitHub-opslagplaats](https://github.com/WindowsAzure/azure-sdk-for-node).
> 
> 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toocreate een basic-chattoepassing gehost in een Azure Cloud Service. toolearn hoe toohost deze toepassing in een Azure-Website zien [een Node.js-chattoepassing met Socket.IO op een Azure-website bouwen][chatwebsite].

Zie voor meer informatie, ook Hallo [Node.js Developer Center](/develop/nodejs/).

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Socket.IO GitHub-opslagplaats]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


