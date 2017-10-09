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
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="94832-103">Het bouwen van een Node.js-chattoepassing met Socket.IO op een Azure Cloudservice</span><span class="sxs-lookup"><span data-stu-id="94832-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="94832-104">Socket.IO biedt realtime-communicatie tussen tussen uw node.js-server en clients.</span><span class="sxs-lookup"><span data-stu-id="94832-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="94832-105">Deze zelfstudie helpt u bij het hosten van een socket. I/o gebaseerd chatprogramma op Azure.</span><span class="sxs-lookup"><span data-stu-id="94832-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="94832-106">Zie voor meer informatie over Socket.IO <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="94832-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="94832-107">Een schermopname van de toepassing hello voltooid lager is dan:</span><span class="sxs-lookup"><span data-stu-id="94832-107">A screenshot of hello completed application is below:</span></span>

![Een browservenster met Hallo service die wordt gehost op Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="94832-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="94832-109">Prerequisites</span></span>
<span data-ttu-id="94832-110">Zorg ervoor dat Hallo na producten en versies zijn geïnstalleerd toosuccessfully voltooid Hallo voorbeeld in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="94832-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="94832-111">[Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) installeren</span><span class="sxs-lookup"><span data-stu-id="94832-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="94832-112">[Node.js](https://nodejs.org/download/) installeren</span><span class="sxs-lookup"><span data-stu-id="94832-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="94832-113">Installeer [Python versie 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="94832-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="94832-114">Een Cloud Service-Project maken</span><span class="sxs-lookup"><span data-stu-id="94832-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="94832-115">Hallo volgende stappen maakt u Hallo-cloudserviceproject die als host Hallo Socket.IO toepassing fungeert.</span><span class="sxs-lookup"><span data-stu-id="94832-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="94832-116">Van Hallo **startmenu** of **startscherm**, zoeken naar **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="94832-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="94832-117">Ten slotte de met de rechtermuisknop op **Windows PowerShell** en selecteer **als Administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="94832-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell-pictogram][powershell-menu]
2. <span data-ttu-id="94832-119">Maak een map met de naam **c:\\knooppunt**.</span><span class="sxs-lookup"><span data-stu-id="94832-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="94832-120">Wijzig de mappen toohello **c:\\knooppunt** directory</span><span class="sxs-lookup"><span data-stu-id="94832-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="94832-121">Voer Hallo na opdrachten toocreate een nieuwe oplossing met de naam **chatapp** en een werkrol toe met de naam **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="94832-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="94832-122">Hier ziet u Hallo antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="94832-122">You will see hello following response:</span></span>
   
    ![Hallo-uitvoer van de nieuwe Hallo-azureservice en voeg azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="94832-124">Hallo chatten voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="94832-124">Download hello Chat Example</span></span>
<span data-ttu-id="94832-125">Voor dit project, gebruiken we Hallo chat voorbeeld uit Hallo [Socket.IO GitHub-opslagplaats].</span><span class="sxs-lookup"><span data-stu-id="94832-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="94832-126">Hallo te volgen stappen toodownload Hallo-voorbeeld uitvoeren en voeg deze toohello project dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="94832-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="94832-127">Maken van een lokale kopie van het Hallo-opslagplaats met behulp van Hallo **kloon** knop.</span><span class="sxs-lookup"><span data-stu-id="94832-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="94832-128">U kunt ook Hallo **ZIP** knop toodownload Hallo project.</span><span class="sxs-lookup"><span data-stu-id="94832-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![Een browservenster https://github.com/LearnBoost/socket.io/tree/master/examples/chat, weergeven met Hallo ZIP downloadpictogram gemarkeerd][chat-example-view]
2. <span data-ttu-id="94832-130">Navigeer Hallo directorystructuur van de lokale opslagplaats Hallo totdat u bij Hallo aankomt **voorbeelden\\chat** directory.</span><span class="sxs-lookup"><span data-stu-id="94832-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="94832-131">Kopieer Hallo inhoud van deze directory toothe **C:\\knooppunt\\chatapp\\WorkerRole1** directory eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="94832-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Verkenner weergeven Hallo inhoud van Hallo voorbeelden\\chat-map opgehaald uit het Hallo-archief][chat-contents]
   
   <span data-ttu-id="94832-133">Hallo gemarkeerde items in de bovenstaande Hallo Hallo bestanden zijn gekopieerd uit Hallo **voorbeelden\\chat** directory</span><span class="sxs-lookup"><span data-stu-id="94832-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="94832-134">In Hallo **C:\\knooppunt\\chatapp\\WorkerRole1** directory, delete Hallo **server.js** bestand en wijzig de naam Hallo **app.js**bestand te**server.js**.</span><span class="sxs-lookup"><span data-stu-id="94832-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="94832-135">Hiermee verwijdert u de standaard Hallo **server.js** bestand dat eerder is gemaakt door Hallo **toevoegen AzureNodeWorkerRole** cmdlet en vervangt deze met de toepassing hello bestand van Hallo chat-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="94832-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="94832-136">Wijzigen van Server.js en -Modules installeren</span><span class="sxs-lookup"><span data-stu-id="94832-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="94832-137">Voordat u testtoepassing Hallo in hello Azure-emulator maken we een aantal kleine wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="94832-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="94832-138">Voer Hallo stappen toothe server.js-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="94832-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="94832-139">Open Hallo **server.js** -bestand in Visual Studio of een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="94832-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="94832-140">Hallo zoeken **Module afhankelijkheden** sectie aan Hallo begin van server.js en wijzig Hallo regel die **sio require('.. = //.. lib//socket.IO')** te**sio require('socket.io') =** zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="94832-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="94832-141">tooensure hello toepassing luistert op de juiste poort hello, server.js geopend in Kladblok of uw favoriete editor en wijzigt u de volgende regel door te vervangen **3000** met **process.env.port** zoals wordt weergegeven hieronder:</span><span class="sxs-lookup"><span data-stu-id="94832-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="94832-142">Na het opslaan van wijzigingen hello te**server.js**Hallo stappen te volgen gebruiken voor het installeren van vereiste modules en vervolgens test Hallo toepassingen in de Azure-emulator:</span><span class="sxs-lookup"><span data-stu-id="94832-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="94832-143">Met behulp van **Azure PowerShell**, wijzig de mappen toohello **C:\\knooppunt\\chatapp\\WorkerRole1** directory en gebruik Hallo opdracht tooinstall Hallo na modules die zijn vereist voor deze toepassing:</span><span class="sxs-lookup"><span data-stu-id="94832-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="94832-144">Hiermee installeert u Hallo-modules die worden vermeld in Hallo package.json-bestand.</span><span class="sxs-lookup"><span data-stu-id="94832-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="94832-145">Nadat het Hallo-opdracht is voltooid, ziet u uitvoer vergelijkbare toothe volgende:</span><span class="sxs-lookup"><span data-stu-id="94832-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![Hallo-uitvoer van Hallo npm installatieopdracht][The-output-of-the-npm-install-command]
2. <span data-ttu-id="94832-147">Aangezien dit voorbeeld oorspronkelijk deel uit van Hallo Socket.IO GitHub-opslagplaats en rechtstreeks Hallo Socket.IO bibliotheek relatief pad verwijst naar, is niet Socket.IO verwezen in Hallo package.json-bestand, dus er moet worden geïnstalleerd door uitgifte van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="94832-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="94832-148">Testen en implementeren</span><span class="sxs-lookup"><span data-stu-id="94832-148">Test and Deploy</span></span>
1. <span data-ttu-id="94832-149">Hallo-emulator door uitgifte van de volgende opdracht Hallo starten:</span><span class="sxs-lookup"><span data-stu-id="94832-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="94832-150">Als u problemen ondervindt met bijvoorbeeld emulator te starten.: begin AzureEmulator: Er is een onverwachte fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="94832-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="94832-151">Details: Aangetroffen een onverwachte fout Hallo communicatieobject, System.ServiceModel.Channels.ServiceChannel, kan niet worden gebruikt voor communicatie omdat het Hallo status Faulted heeft.</span><span class="sxs-lookup"><span data-stu-id="94832-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="94832-152">Installeer AzureAuthoringTools v 2.7.1 en AzureComputeEmulator v 2.7: Zorg ervoor dat de versie die overeenkomt met.</span><span class="sxs-lookup"><span data-stu-id="94832-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="94832-153">Open een browser en te navigeren**http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="94832-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="94832-154">Wanneer Hallo browservenster wordt geopend, voer een bijnaam en klik vervolgens op ENTER drukken.</span><span class="sxs-lookup"><span data-stu-id="94832-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="94832-155">Hierdoor kunt u berichten toopost als een specifieke bijnaam.</span><span class="sxs-lookup"><span data-stu-id="94832-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="94832-156">functionaliteit voor meerdere gebruikers tootest, extra browservensters met dezelfde URL te openen en voer verschillende bijnaam.</span><span class="sxs-lookup"><span data-stu-id="94832-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Twee browservensters chatberichten van Gebruiker1 als Gebruiker2 weergeven](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="94832-158">Stop na testtoepassing Hallo Hallo emulator door de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="94832-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="94832-159">toodeploy hello toepassing tooAzure, gebruik de **Publish-AzureServiceProject** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="94832-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="94832-160">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="94832-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="94832-161">Ervoor toouse een unieke naam zijn, anders Hallo publicatieproces zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="94832-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="94832-162">Nadat het Hallo-implementatie is voltooid, wordt de Hallo browser openen en de Navigeer toohello geïmplementeerd service.</span><span class="sxs-lookup"><span data-stu-id="94832-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="94832-163">Als u ontvangt een foutbericht waarin wordt gemeld dat Hallo opgegeven naam van abonnement bestaat niet in Hallo geïmporteerd publicatieprofiel, moet u downloaden en importeren Hallo publicatieprofiel voor uw abonnement voordat u tooAzure implementeert.</span><span class="sxs-lookup"><span data-stu-id="94832-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="94832-164">Zie Hallo **implementeren Hallo toepassing tooAzure** sectie van [bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="94832-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Een browservenster met Hallo service die wordt gehost op Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="94832-166">Als u ontvangt een foutbericht waarin wordt gemeld dat Hallo opgegeven naam van abonnement bestaat niet in Hallo geïmporteerd publicatieprofiel, moet u downloaden en importeren Hallo publicatieprofiel voor uw abonnement voordat u tooAzure implementeert.</span><span class="sxs-lookup"><span data-stu-id="94832-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="94832-167">Zie Hallo **implementeren Hallo toepassing tooAzure** sectie van [bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="94832-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="94832-168">Uw toepassing wordt nu uitgevoerd in Azure, en kan chatberichten tussen verschillende clients met Socket.IO doorsturen.</span><span class="sxs-lookup"><span data-stu-id="94832-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="94832-169">Voor de eenvoud, dit voorbeeld is beperkt toochatting tussen gebruikers verbonden toohello hetzelfde exemplaar.</span><span class="sxs-lookup"><span data-stu-id="94832-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="94832-170">Dit betekent dat als cloudservice Hallo twee exemplaren van worker-rol maakt, gebruikers is alleen mogelijk toochat met anderen verbonden toohello hetzelfde exemplaar van de worker-rol.</span><span class="sxs-lookup"><span data-stu-id="94832-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="94832-171">tooscale hello toowork toepassing met meerdere rolexemplaren, u kunt een technologie zoals Socket.IO archiefstatus voor Service Bus tooshare Hallo over exemplaren.</span><span class="sxs-lookup"><span data-stu-id="94832-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="94832-172">Zie voor voorbeelden Hallo Service Bus-wachtrijen en onderwerpen voorbeelden voor gebruik in Hallo [Azure SDK voor Node.js GitHub-opslagplaats](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="94832-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="94832-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="94832-173">Next steps</span></span>
<span data-ttu-id="94832-174">In deze zelfstudie hebt u geleerd hoe toocreate een basic-chattoepassing gehost in een Azure Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="94832-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="94832-175">toolearn hoe toohost deze toepassing in een Azure-Website zien [een Node.js-chattoepassing met Socket.IO op een Azure-website bouwen][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="94832-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="94832-176">Zie voor meer informatie, ook Hallo [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="94832-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

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


