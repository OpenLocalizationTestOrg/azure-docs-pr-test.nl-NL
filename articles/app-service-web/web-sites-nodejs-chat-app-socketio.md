---
title: aaaCreate een Node.js-chattoepassing met Socket.IO in Azure App Service
description: Een zelfstudie die u laat zien met socket.io in een node.js-web-app gehost op Azure.
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="2739e-103">In Azure App Service een Node.js-chattoepassing maken met Socket.IO</span><span class="sxs-lookup"><span data-stu-id="2739e-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="2739e-104">Socket.IO biedt realtime-communicatie tussen uw node.js-server en clients met behulp van WebSockets.</span><span class="sxs-lookup"><span data-stu-id="2739e-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="2739e-105">Het ondersteunt ook terugval tooother transporten (zoals lange polling) die met oudere browsers werken.</span><span class="sxs-lookup"><span data-stu-id="2739e-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="2739e-106">Deze zelfstudie wordt helpt u bij het hosten van een toepassing op basis van Socket.IO chat als een Azure-web-app en ziet u hoe tooscale Hallo gebruikt toepassing [Azure Redis-Cache].</span><span class="sxs-lookup"><span data-stu-id="2739e-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="2739e-107">Zie voor meer informatie over Socket.IO <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="2739e-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="2739e-108">Hallo procedures in deze taak te gelden[App Service Web Apps]; voor Cloud-Services, Zie [bouwen van een Node.js-chattoepassing met Socket.IO op een Azure Cloud Service].</span><span class="sxs-lookup"><span data-stu-id="2739e-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="2739e-109">Hallo chat voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="2739e-109">Download hello chat example</span></span>
<span data-ttu-id="2739e-110">Voor dit project, gebruiken we Hallo chat voorbeeld uit Hallo [Socket.IO GitHub-opslagplaats].</span><span class="sxs-lookup"><span data-stu-id="2739e-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="2739e-111">Hallo te volgen stappen toodownload Hallo-voorbeeld uitvoeren en voeg deze toohello project dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2739e-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="2739e-112">Download een [ZIP- of GZ gearchiveerd release] van Hallo Socket.IO project (versie 1.3.5 is gebruikt voor dit document)</span><span class="sxs-lookup"><span data-stu-id="2739e-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="2739e-113">Hallo archiveren en kopieer Hallo extraheren **voorbeelden\\chat** tooa nieuwe maplocatie.</span><span class="sxs-lookup"><span data-stu-id="2739e-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="2739e-114">Bijvoorbeeld:  **\\knooppunt\\chat**.</span><span class="sxs-lookup"><span data-stu-id="2739e-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="2739e-115">App.js wijzigen en -modules installeren</span><span class="sxs-lookup"><span data-stu-id="2739e-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="2739e-116">Wijzig de naam van Hallo **index.js** bestand te**app.js**.</span><span class="sxs-lookup"><span data-stu-id="2739e-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="2739e-117">Hierdoor kunnen Azure toodetect dat dit een Node.js-toepassing is.</span><span class="sxs-lookup"><span data-stu-id="2739e-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="2739e-118">Open Hallo **app.js** bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="2739e-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="2739e-119">Wijziging Hallo regel die `var io = require('../..')(server);` zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="2739e-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="2739e-120">Open Hallo **package.json** -bestand en voeg een verwijzing toosocket.io onder `dependencies`, zoals hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="2739e-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="2739e-121">Wijzig vanaf de opdrachtregel hello, toohello  **\\knooppunt\\chat** directory en gebruik npm tooinstall Hallo modules vereist door deze toepassing:</span><span class="sxs-lookup"><span data-stu-id="2739e-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="2739e-122">Hiermee installeert u Hallo modules in een submap met de naam **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="2739e-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="2739e-123">Een Azure-Web-App maken</span><span class="sxs-lookup"><span data-stu-id="2739e-123">Create an Azure Web App</span></span>
<span data-ttu-id="2739e-124">Volg deze stappen toocreate een Azure-web-app, Git-publicatie inschakelen en vervolgens WebSocket-ondersteuning voor web-app Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2739e-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="2739e-125">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2739e-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="2739e-126">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="2739e-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2739e-127">Zie <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Gratis proefversie van Azure</a> voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2739e-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="2739e-128">Installeer hello Azure-opdrachtregelinterface (Azure CLI) en verbinding maken met tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2739e-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="2739e-129">Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2739e-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="2739e-130">Als dit de eerste keer instellen van een opslagplaats in Azure, moet u de aanmeldingsreferenties toocreate.</span><span class="sxs-lookup"><span data-stu-id="2739e-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="2739e-131">Voer van hello Azure CLI, Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2739e-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="2739e-132">Wijzigen van toohello  **\\node\chat** directory en gebruik Hallo volgende toocreate opdracht een nieuwe Azure-web-app en een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="2739e-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="2739e-133">Met deze opdracht maakt ook een Git remote met de naam 'azure'.</span><span class="sxs-lookup"><span data-stu-id="2739e-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="2739e-134">U moet 'mysitename' vervangen door een unieke naam voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="2739e-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="2739e-135">Hallo bestaande bestanden toohello lokale opslagplaats met behulp van de volgende opdrachten Hallo doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="2739e-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="2739e-136">Hallo bestanden toohello Azure Web Apps opslagplaats pushen met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2739e-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="2739e-137">Wanneer u wordt gevraagd, typt u uw referenties uit stap 2.</span><span class="sxs-lookup"><span data-stu-id="2739e-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="2739e-138">U ontvangt statusberichten zoals modules geïmporteerd op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="2739e-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="2739e-139">Zodra dit proces is voltooid, wordt de toepassing hello worden gehost op uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="2739e-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2739e-140">Tijdens de installatie van de module, merkt u fouten die ' hello... geïmporteerde project is niet gevonden '.</span><span class="sxs-lookup"><span data-stu-id="2739e-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="2739e-141">Deze kunnen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="2739e-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="2739e-142">Socket.IO WebSockets die niet zijn ingeschakeld op Azure standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2739e-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="2739e-143">tooenable websockets, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2739e-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="2739e-144">Als u wordt gevraagd, geeft u Hallo-naam van Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="2739e-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2739e-145">Hallo-opdracht 'azure site set -w' wordt alleen met versie 0.7.4 werk- of hoger van hello Azure-opdrachtregelinterface.</span><span class="sxs-lookup"><span data-stu-id="2739e-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="2739e-146">U kunt ook inschakelen met behulp van Hallo WebSocket-ondersteuning [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2739e-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="2739e-147">WebSockets met behulp van tooenable hello Azure Portal, klik op Hallo web-app uit de Web-Apps-blade hello, **alle instellingen** > **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="2739e-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="2739e-148">Onder **Web Sockets**, klikt u op **op**.</span><span class="sxs-lookup"><span data-stu-id="2739e-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="2739e-149">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2739e-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="2739e-150">tooview hello web-app op Azure, gebruik Hallo volgende opdracht toolaunch uw webbrowser en navigeer toohello gehost web-app:</span><span class="sxs-lookup"><span data-stu-id="2739e-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="2739e-151">Uw app wordt nu uitgevoerd in Azure, en kan chatberichten tussen verschillende clients met Socket.IO doorsturen.</span><span class="sxs-lookup"><span data-stu-id="2739e-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="2739e-152">Uitschalen</span><span class="sxs-lookup"><span data-stu-id="2739e-152">Scale out</span></span>
<span data-ttu-id="2739e-153">Socket.IO toepassingen kunnen worden uitgebreid met behulp van een **adapter** toodistribute berichten en gebeurtenissen tussen meerdere exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="2739e-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="2739e-154">Hoewel er verschillende adapters beschikbaar zijn, Hallo [socket.io redis] adapter gemakkelijk kan worden gebruikt met hello Azure Redis-Cache-functie.</span><span class="sxs-lookup"><span data-stu-id="2739e-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="2739e-155">Een aanvullende vereiste voor het uitbreiden van een oplossing met Socket.IO is ondersteuning voor een tijdelijke sessies.</span><span class="sxs-lookup"><span data-stu-id="2739e-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="2739e-156">Een tijdelijke sessies zijn standaard ingeschakeld voor Azure-Web-Apps via Azure routering van toepassingsaanvragen.</span><span class="sxs-lookup"><span data-stu-id="2739e-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="2739e-157">Zie voor meer informatie [exemplaar affiniteit in Azure websites].</span><span class="sxs-lookup"><span data-stu-id="2739e-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="2739e-158">Een Redis-cache maken</span><span class="sxs-lookup"><span data-stu-id="2739e-158">Create a Redis cache</span></span>
<span data-ttu-id="2739e-159">Voer Hallo stappen uit in [maken van een cache in Azure Redis-Cache] toocreate een nieuwe cache.</span><span class="sxs-lookup"><span data-stu-id="2739e-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="2739e-160">Hallo opslaan **hostnaam** en **primaire sleutel** voor uw cache als deze nodig zijn de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="2739e-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="2739e-161">Hallo redis en socket.io redis modules toevoegen</span><span class="sxs-lookup"><span data-stu-id="2739e-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="2739e-162">Wijzig vanaf een opdrachtregel toohello  **\\knooppunt\\chat** directory en gebruik Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="2739e-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="2739e-163">Hallo-versies die zijn opgegeven in deze opdracht zijn Hallo-versies die zijn gebruikt bij het testen van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2739e-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="2739e-164">Hallo wijzigen **app.js** bestand tooadd Hallo volgende regels onmiddellijk na`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="2739e-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="2739e-165">Vervang **redishostname** en **rediskey** met Hallo-hostnaam en -sleutel voor de Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="2739e-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="2739e-166">Hiermee wordt een publiceren en abonneren client toohello Redis-cache eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2739e-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="2739e-167">Hallo-clients worden vervolgens gebruikt met Hallo adapter tooconfigure Socket.IO toouse hello Redis-cache voor het doorgeven van berichten en gebeurtenissen tussen exemplaren van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="2739e-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2739e-168">Tijdens het Hallo **socket.io redis** adapter kan communiceren rechtstreeks tooRedis, Hallo huidige versie ondersteunt geen Hallo-verificatie vereist voor Azure Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="2739e-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="2739e-169">Dus Hallo initiële verbinding wordt gemaakt met Hallo **redis** -module, klikt u vervolgens Hallo-client wordt doorgegeven toohello **socket.io redis** adapter.</span><span class="sxs-lookup"><span data-stu-id="2739e-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="2739e-170">Terwijl Azure Redis-Cache beveiligde verbindingen via poort 6380 ondersteunt, ondersteund Hallo-modules die worden gebruikt in dit voorbeeld beveiligde verbindingen vanaf 14-7-2014 niet.</span><span class="sxs-lookup"><span data-stu-id="2739e-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="2739e-171">Hallo bovenstaande code maakt gebruik van niet-beveiligde poort van 6379 Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="2739e-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="2739e-172">Opslaan Hallo gewijzigd **app.js**</span><span class="sxs-lookup"><span data-stu-id="2739e-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="2739e-173">Wijzigingen vastleggen en implementeren</span><span class="sxs-lookup"><span data-stu-id="2739e-173">Commit changes and redeploy</span></span>
<span data-ttu-id="2739e-174">Vanaf de opdrachtregel in Hallo Hallo  **\\knooppunt\\chat** directory, gebruiken de volgende opdrachten toocommit wijzigingen Hallo en toepassing hello opnieuw distribueren.</span><span class="sxs-lookup"><span data-stu-id="2739e-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="2739e-175">Wanneer wijzigingen Hallo pushbericht hebben ontvangen toohello server, kunt u uw site over meerdere exemplaren met behulp van de volgende opdracht Hallo schalen.</span><span class="sxs-lookup"><span data-stu-id="2739e-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="2739e-176">Waar  **#**  is het aantal exemplaren toocreate Hallo.</span><span class="sxs-lookup"><span data-stu-id="2739e-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="2739e-177">U kunt tooyour web-app uit meerdere tooverify browsers of computers die goed tooall clients berichten worden verbinden.</span><span class="sxs-lookup"><span data-stu-id="2739e-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2739e-178">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="2739e-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="2739e-179">Verbindingslimieten</span><span class="sxs-lookup"><span data-stu-id="2739e-179">Connection limits</span></span>
<span data-ttu-id="2739e-180">Azure-Web-Apps is beschikbaar in meerdere SKU's Hallo resources beschikbaar tooyour site vast te stellen.</span><span class="sxs-lookup"><span data-stu-id="2739e-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="2739e-181">Dit omvat Hallo aantal toegestane WebSocket-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="2739e-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="2739e-182">Zie voor meer informatie, Hallo [pagina met prijzen van Web-Apps].</span><span class="sxs-lookup"><span data-stu-id="2739e-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="2739e-183">Berichten worden niet verzonden met behulp van WebSockets</span><span class="sxs-lookup"><span data-stu-id="2739e-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="2739e-184">Als clientbrowsers toolong polling in plaats van WebSockets teruggevallen houden, mogelijk vanwege een van de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="2739e-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="2739e-185">**Probeer Hallo transport toojust WebSockets beperken**</span><span class="sxs-lookup"><span data-stu-id="2739e-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="2739e-186">Opdat Socket.IO toouse WebSockets als Hallo transport messaging, moeten zowel Hallo-server en client WebSockets ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="2739e-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="2739e-187">Als een of andere Hallo niet ondersteunt, zal de Socket.IO onderhandelen over een andere transport, zoals lange polling.</span><span class="sxs-lookup"><span data-stu-id="2739e-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="2739e-188">de standaardlijst Hallo van transporten gebruikt door Socket.IO ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="2739e-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="2739e-189">U kunt zorgen dat tooonly gebruik WebSockets door toe te voegen Hallo na code toohello **app.js** bestand, na het Hallo-regel die `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="2739e-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="2739e-190">Houd er rekening mee dat oudere browsers die bieden geen ondersteuning voor WebSockets niet kunnen tooconnect toohello site worden terwijl Hallo bovenstaande code actief en is als de communicatie tooWebSockets alleen wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="2739e-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="2739e-191">**SSL gebruiken**</span><span class="sxs-lookup"><span data-stu-id="2739e-191">**Use SSL**</span></span>
  
    <span data-ttu-id="2739e-192">WebSockets is afhankelijk van bepaalde minder gebruikte HTTP-headers, zoals Hallo **Upgrade** header.</span><span class="sxs-lookup"><span data-stu-id="2739e-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="2739e-193">Een aantal tussenliggende netwerkapparaten, zoals web proxy's, kunnen deze koppen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2739e-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="2739e-194">tooavoid dit probleem op door Hallo WebSocket verbinding kan worden gemaakt via SSL.</span><span class="sxs-lookup"><span data-stu-id="2739e-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="2739e-195">Een eenvoudige manier tooaccomplish is dit tooconfigure Socket.IO te`match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="2739e-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="2739e-196">Dit Socket.IO toosecure WebSockets communicatie Hallo gelijk zijn aan die afkomstig zijn HTTP/HTTPS Hallo voor de webpagina Hallo aanvragen geïnstrueerd.</span><span class="sxs-lookup"><span data-stu-id="2739e-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="2739e-197">Als een browser een toovisit HTTPS-URL voor uw website gebruikt, worden daaropvolgende WebSocket-communicatie via Socket.IO beveiligd via SSL.</span><span class="sxs-lookup"><span data-stu-id="2739e-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="2739e-198">toomodify in dit voorbeeld tooenable deze configuratie toevoegen na de code toohello Hallo **app.js** bestand na het Hallo-regel die `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="2739e-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="2739e-199">**Controleer of web.config-instellingen**</span><span class="sxs-lookup"><span data-stu-id="2739e-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="2739e-200">Azure-web-apps die als host Node.js-toepassingen fungeren gebruiken Hallo **web.config** bestand tooroute binnenkomende aanvragen toohello Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2739e-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="2739e-201">Hallo voor WebSockets toofunction correct met Node.js-toepassingen, **web.config** Hallo na datum moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="2739e-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="2739e-202">Hallo WebSockets IIS-module, waaronder een eigen implementatie van WebSockets en veroorzaakt een conflict met Node.js specifieke WebSocket-modules zoals Socket.IO wordt uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2739e-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="2739e-203">Als deze regel niet aanwezig is of is ingesteld te`true`, kan dit Hallo reden die Hallo WebSocket transport niet voor uw toepassing werkt.</span><span class="sxs-lookup"><span data-stu-id="2739e-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="2739e-204">Normaal gesproken Node.js-toepassingen bevatten geen een **web.config** -bestand, zodat Azure Websites wordt automatisch gegenereerd voor Node.js-toepassingen wanneer ze zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2739e-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="2739e-205">Omdat dit bestand wordt automatisch gegenereerd op Hallo-server, moet u Hallo FTP of FTPS-URL voor uw website tooview dit bestand.</span><span class="sxs-lookup"><span data-stu-id="2739e-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="2739e-206">U kunt zoeken Hallo FTP en FTPS-URL's voor uw site in de klassieke portal Hallo op uw web-app selecteren en vervolgens Hallo **Dashboard** koppeling.</span><span class="sxs-lookup"><span data-stu-id="2739e-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="2739e-207">Hallo URL's worden weergegeven in Hallo **snelle weergave** sectie.</span><span class="sxs-lookup"><span data-stu-id="2739e-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2739e-208">Hallo **web.config** bestand alleen wordt gegenereerd door Azure Websites als uw toepassing zorgt niet voor.</span><span class="sxs-lookup"><span data-stu-id="2739e-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="2739e-209">Als u een **web.config** bestand in de hoofdmap van uw toepassingsproject hello wordt gebruikt door Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="2739e-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="2739e-210">Hallo-vermelding is niet aanwezig of is ingesteld tooa waarde `true`, en vervolgens u maakt een **web.config** in de hoofdmap van uw Node.js-toepassing hello en geef een waarde van `false`.</span><span class="sxs-lookup"><span data-stu-id="2739e-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="2739e-211">Ter referentie: Hallo hieronder wordt een standaard **web.config** voor een toepassing die gebruikmaakt van **app.js** als Hallo toegangspunt.</span><span class="sxs-lookup"><span data-stu-id="2739e-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="2739e-212">Als uw toepassing gebruikmaakt van een toegangspunt dan **app.js**, moet u alle instanties van vervangen **app.js** Hello corrigeren toegangspunt.</span><span class="sxs-lookup"><span data-stu-id="2739e-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="2739e-213">Bijvoorbeeld, vervangen **app.js** met **server.js**.</span><span class="sxs-lookup"><span data-stu-id="2739e-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="2739e-214">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen], waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="2739e-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2739e-215">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="2739e-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2739e-216">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2739e-216">Next steps</span></span>
<span data-ttu-id="2739e-217">In deze zelfstudie hebt u geleerd hoe toocreate een chatprogramma gehost in een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="2739e-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="2739e-218">Ook kunt u deze toepassing als een Azure Cloud Service hosten.</span><span class="sxs-lookup"><span data-stu-id="2739e-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="2739e-219">Voor stapsgewijze instructies voor het tooaccomplish deze, Zie [bouwen van een Node.js-chattoepassing met Socket.IO op een Azure Cloud Service].</span><span class="sxs-lookup"><span data-stu-id="2739e-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="2739e-220">Zie voor meer informatie, ook Hallo [Node.js Developer Center].</span><span class="sxs-lookup"><span data-stu-id="2739e-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="2739e-221">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="2739e-221">What's changed</span></span>
* <span data-ttu-id="2739e-222">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services].</span><span class="sxs-lookup"><span data-stu-id="2739e-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[Azure Redis-Cache]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[pagina met prijzen van Web-Apps]: http://go.microsoft.com/fwlink/?LinkId=511643
[bouwen van een Node.js-chattoepassing met Socket.IO op een Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[Azure App Service en de invloed ervan op bestaande Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js Developer Center]: /develop/nodejs/
[App Service uitproberen]: https://azure.microsoft.com/try/app-service/
[exemplaar affiniteit in Azure websites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[maken van een cache in Azure Redis-Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub-opslagplaats]: https://github.com/socketio/socket.io
[ZIP- of GZ gearchiveerd release]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
