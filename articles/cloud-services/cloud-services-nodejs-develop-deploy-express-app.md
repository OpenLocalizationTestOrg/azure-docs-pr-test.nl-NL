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
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="b221b-103">Een Node.js-webtoepassing met een snelle op een Azure Cloud Service bouwen</span><span class="sxs-lookup"><span data-stu-id="b221b-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="b221b-104">Node.js bevat een minimale set van de functionaliteit in Hallo core runtime.</span><span class="sxs-lookup"><span data-stu-id="b221b-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="b221b-105">Ontwikkelaars vaak 3e partij modules tooprovide aanvullende functionaliteit gebruiken bij het ontwikkelen van een Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b221b-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="b221b-106">In deze zelfstudie maakt u een nieuwe toepassing met behulp van Hallo [Express] [ Express] module waarmee een MVC-framework biedt voor het maken van Node.js-webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="b221b-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="b221b-107">Een schermopname van de toepassing hello voltooid lager is dan:</span><span class="sxs-lookup"><span data-stu-id="b221b-107">A screenshot of hello completed application is below:</span></span>

![Een webbrowser waarin Welkom tooExpress in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="b221b-109">Een Cloud Service-Project maken</span><span class="sxs-lookup"><span data-stu-id="b221b-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="b221b-110">Uitvoeren van de volgende Hallo toocreate stappen een nieuwe cloudserviceproject met de naam 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="b221b-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="b221b-111">Van Hallo **startmenu** of **startscherm**, zoeken naar **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b221b-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="b221b-112">Ten slotte de met de rechtermuisknop op **Windows PowerShell** en selecteer **als Administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="b221b-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell-pictogram](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="b221b-114">Wijzig de mappen toohello **c:\\knooppunt** directory en voer vervolgens de volgende opdrachten toocreate een nieuwe oplossing met de naam Hallo **expressapp** en een Webrol met de naam **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="b221b-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="b221b-115">Standaard **Add-AzureNodeWebRole** maakt gebruik van een oudere versie van Node.js.</span><span class="sxs-lookup"><span data-stu-id="b221b-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="b221b-116">Hallo **Set AzureServiceProjectRole** instructie hiervoor Hiermee geeft u Azure toouse v0.10.21 van knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b221b-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="b221b-117">Houd er rekening mee Hallo parameters zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="b221b-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="b221b-118">U kunt controleren of de juiste versie Hallo van Node.js is geselecteerd door te controleren Hallo **engines** eigenschap in **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="b221b-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="b221b-119">Express installeren</span><span class="sxs-lookup"><span data-stu-id="b221b-119">Install Express</span></span>
1. <span data-ttu-id="b221b-120">Hallo Express-generator door uitgifte van Hallo volgende opdracht installeren:</span><span class="sxs-lookup"><span data-stu-id="b221b-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="b221b-121">Hallo-uitvoer van Hallo npm opdracht ziet er vergelijkbaar toohello resultaat hieronder.</span><span class="sxs-lookup"><span data-stu-id="b221b-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Windows PowerShell weergeven Hallo uitvoer van Hallo npm snelle opdracht installeren.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="b221b-123">Wijzig de mappen toohello **WebRole1** directory en gebruik Hallo snelle opdracht toogenerate een nieuwe toepassing:</span><span class="sxs-lookup"><span data-stu-id="b221b-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="b221b-124">U na vragen aan gebruiker toooverwrite uw eerdere toepassing zijn.</span><span class="sxs-lookup"><span data-stu-id="b221b-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="b221b-125">Voer **y** of **Ja** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b221b-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="b221b-126">Express wordt gegenereerd Hallo app.js bestands- en de mappenstructuur van een voor het bouwen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b221b-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![Hallo-uitvoer van Hallo snelle opdracht](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="b221b-128">tooinstall extra afhankelijkheden gedefinieerd in Hallo package.json-bestand, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b221b-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Hallo-uitvoer van Hallo npm installatieopdracht](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="b221b-130">Gebruik Hallo volgende opdracht toocopy hello **bin/www** bestand te**server.js**.</span><span class="sxs-lookup"><span data-stu-id="b221b-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="b221b-131">Dit is dus cloudservice Hallo Hallo toegangspunt voor deze toepassing kunt vinden.</span><span class="sxs-lookup"><span data-stu-id="b221b-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="b221b-132">Nadat u deze opdracht is voltooid, hebt u een **server.js** bestand in map Hallo WebRole1.</span><span class="sxs-lookup"><span data-stu-id="b221b-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="b221b-133">Hallo wijzigen **server.js** tooremove een Hallo '.' tekens bevatten uit Hallo volgt regel.</span><span class="sxs-lookup"><span data-stu-id="b221b-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="b221b-134">Na deze wijziging, Hallo regel moet worden weergegeven als volgt.</span><span class="sxs-lookup"><span data-stu-id="b221b-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="b221b-135">Deze wijziging is vereist omdat we Hallo-bestand is verplaatst (voorheen **bin/www**,) toohello dezelfde directory als Hallo app-bestand wordt vereist.</span><span class="sxs-lookup"><span data-stu-id="b221b-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="b221b-136">Nadat u deze wijziging, opslaan Hallo **server.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="b221b-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="b221b-137">Gebruik Hallo opdracht toorun Hallo toepassing in hello Azure-emulator te volgen:</span><span class="sxs-lookup"><span data-stu-id="b221b-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Een webpagina met Welkom tooexpress.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="b221b-139">Hallo weergave wijzigen</span><span class="sxs-lookup"><span data-stu-id="b221b-139">Modifying hello View</span></span>
<span data-ttu-id="b221b-140">Nu wijzigen Hallo weergave toodisplay Hallo-bericht 'Welkom tooExpress in Azure'.</span><span class="sxs-lookup"><span data-stu-id="b221b-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="b221b-141">Voer Hallo opdrachtbestand tooopen hello index.jade te volgen:</span><span class="sxs-lookup"><span data-stu-id="b221b-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Hallo-inhoud van Hallo index.jade bestand.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="b221b-143">Jade is Hallo standaard weergave-engine wordt gebruikt door toepassingen van Express.</span><span class="sxs-lookup"><span data-stu-id="b221b-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="b221b-144">Zie voor meer informatie over Jade weergave-engine Hallo [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="b221b-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="b221b-145">Hallo laatste regel van tekst wijzigen door toe te voegen **in Azure**.</span><span class="sxs-lookup"><span data-stu-id="b221b-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![Hallo index.jade bestand, de laatste regel Hallo leest: p Welkom te\#{title} in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="b221b-147">Hallo-bestand opslaan en sluit u Kladblok af.</span><span class="sxs-lookup"><span data-stu-id="b221b-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="b221b-148">Vernieuw de browser en ziet u uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="b221b-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Een browservenster Hallo pagina bevat Welkom tooExpress in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="b221b-150">Gebruik na testtoepassing Hallo Hallo **Stop AzureEmulator** cmdlet toostop Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="b221b-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="b221b-151">Publishing Hallo toepassing tooAzure</span><span class="sxs-lookup"><span data-stu-id="b221b-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="b221b-152">Gebruik in hello Azure PowerShell-venster Hallo **Publish-AzureServiceProject** cmdlet toodeploy hello tooa cloud toepassingsservice</span><span class="sxs-lookup"><span data-stu-id="b221b-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="b221b-153">Zodra het Hallo-implementatie is voltooid, wordt uw browser openen en Hallo webpagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b221b-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![Een webbrowser om Hallo Express pagina weer te geven.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="b221b-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b221b-156">Next steps</span></span>
<span data-ttu-id="b221b-157">Zie voor meer informatie, Hallo [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="b221b-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


