---
title: Web-App snelle (Node.js) | Microsoft Docs
description: Een zelfstudie die is gebaseerd op de cloud service-zelfstudie en laat zien hoe u de Express-module.
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
ms.openlocfilehash: 54b715695e24786ec4e8dfcabefc648d76179c8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="36f58-103">Een Node.js-webtoepassing met een snelle op een Azure Cloud Service bouwen</span><span class="sxs-lookup"><span data-stu-id="36f58-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="36f58-104">Node.js bevat een minimale set van de functionaliteit in de runtime core.</span><span class="sxs-lookup"><span data-stu-id="36f58-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="36f58-105">Ontwikkelaars gebruiken vaak 3e partij modules aanvullende functionaliteit kan bieden bij het ontwikkelen van een Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="36f58-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="36f58-106">In deze zelfstudie maakt u een nieuwe toepassing met de [Express] [ Express] module waarmee een MVC-framework biedt voor het maken van Node.js-webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="36f58-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="36f58-107">Een schermopname van de voltooide toepassing lager is dan:</span><span class="sxs-lookup"><span data-stu-id="36f58-107">A screenshot of the completed application is below:</span></span>

![Een webbrowser waarin Welkom in Express in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="36f58-109">Een Cloud Service-Project maken</span><span class="sxs-lookup"><span data-stu-id="36f58-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="36f58-110">Voer de volgende stappen voor het maken van een nieuw cloudserviceproject met de naam 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="36f58-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="36f58-111">Van de **startmenu** of **startscherm**, zoeken naar **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="36f58-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="36f58-112">Ten slotte de met de rechtermuisknop op **Windows PowerShell** en selecteer **als Administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="36f58-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell-pictogram](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="36f58-114">Wijzig de mappen op de **c:\\knooppunt** directory en voer de volgende opdrachten voor het maken van een nieuwe oplossing met de naam **expressapp** en een Webrol met de naam **WebRole1**:</span><span class="sxs-lookup"><span data-stu-id="36f58-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="36f58-115">Standaard **Add-AzureNodeWebRole** maakt gebruik van een oudere versie van Node.js.</span><span class="sxs-lookup"><span data-stu-id="36f58-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="36f58-116">De **Set AzureServiceProjectRole** instructie hiervoor Hiermee geeft u Azure v0.10.21 van knooppunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="36f58-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="36f58-117">Noteer dat de parameters zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="36f58-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="36f58-118">U kunt controleren of de juiste versie van Node.js is geselecteerd door het controleren van de **engines** eigenschap in **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="36f58-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="36f58-119">Express installeren</span><span class="sxs-lookup"><span data-stu-id="36f58-119">Install Express</span></span>
1. <span data-ttu-id="36f58-120">De Express-generator installeren door de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="36f58-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="36f58-121">De uitvoer van de npm-opdracht zijn vergelijkbaar met het onderstaande resultaat.</span><span class="sxs-lookup"><span data-stu-id="36f58-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![Windows PowerShell weergeven van de uitvoer van de npm installeren snelle opdracht.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="36f58-123">Wijzig de mappen op de **WebRole1** directory en gebruik de express-opdracht voor het genereren van een nieuwe toepassing:</span><span class="sxs-lookup"><span data-stu-id="36f58-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="36f58-124">U wordt gevraagd uw eerdere toepassing overschrijven.</span><span class="sxs-lookup"><span data-stu-id="36f58-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="36f58-125">Voer **y** of **Ja** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="36f58-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="36f58-126">Snelle genereert het bestand app.js en de mappenstructuur van een voor het bouwen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="36f58-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![De uitvoer van de snelle opdracht](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="36f58-128">Voer de volgende opdracht voor het installeren van extra afhankelijkheden die zijn gedefinieerd in het package.json-bestand:</span><span class="sxs-lookup"><span data-stu-id="36f58-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![De uitvoer van de npm-installatieopdracht](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="36f58-130">Gebruik de volgende opdracht om te kopiëren de **bin/www** van het bestand in **server.js**.</span><span class="sxs-lookup"><span data-stu-id="36f58-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="36f58-131">Dit is de service in de cloud vindt het toegangspunt dat voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="36f58-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="36f58-132">Nadat u deze opdracht is voltooid, hebt u een **server.js** bestand in de map WebRole1.</span><span class="sxs-lookup"><span data-stu-id="36f58-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="36f58-133">Wijzig de **server.js** verwijderen van een van de '.' tekens uit de volgende regel.</span><span class="sxs-lookup"><span data-stu-id="36f58-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="36f58-134">Na deze wijziging, de regel moet worden weergegeven als volgt.</span><span class="sxs-lookup"><span data-stu-id="36f58-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="36f58-135">Deze wijziging is vereist omdat het bestand is verplaatst (voorheen **bin/www**,) in dezelfde map als het appbestand dat vereist is.</span><span class="sxs-lookup"><span data-stu-id="36f58-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="36f58-136">Nadat u deze wijziging, sla de **server.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="36f58-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="36f58-137">Gebruik de volgende opdracht voor het uitvoeren van de toepassing in de Azure-emulator:</span><span class="sxs-lookup"><span data-stu-id="36f58-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Een webpagina met Welkom om uit te drukken.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="36f58-139">De weergave wijzigen</span><span class="sxs-lookup"><span data-stu-id="36f58-139">Modifying the View</span></span>
<span data-ttu-id="36f58-140">Wijzig nu de weergave om het bericht 'Welkom naar Express in Azure' weer te geven.</span><span class="sxs-lookup"><span data-stu-id="36f58-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="36f58-141">Voer de volgende opdracht om de index.jade-bestand te openen:</span><span class="sxs-lookup"><span data-stu-id="36f58-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![De inhoud van het bestand index.jade.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="36f58-143">Jade is de standaard weergave-engine wordt gebruikt door toepassingen van Express.</span><span class="sxs-lookup"><span data-stu-id="36f58-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="36f58-144">Zie voor meer informatie over Jade weergave-engine [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="36f58-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="36f58-145">De laatste regel van tekst wijzigen door toe te voegen **in Azure**.</span><span class="sxs-lookup"><span data-stu-id="36f58-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![Het bestand index.jade de laatste regel leest: p Welkom bij de \#{title} in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="36f58-147">Sla het bestand op en sluit u Kladblok af.</span><span class="sxs-lookup"><span data-stu-id="36f58-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="36f58-148">Vernieuw de browser en ziet u uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="36f58-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Een browservenster met de pagina bevat Welkom bij de snelle in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="36f58-150">Na de toepassing testen, gebruiken de **Stop AzureEmulator** cmdlet om te stoppen van de emulator.</span><span class="sxs-lookup"><span data-stu-id="36f58-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="36f58-151">Publiceren van de toepassing in Azure</span><span class="sxs-lookup"><span data-stu-id="36f58-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="36f58-152">In het venster Azure PowerShell gebruiken de **Publish-AzureServiceProject** cmdlet voor het implementeren van de toepassing naar een cloudservice</span><span class="sxs-lookup"><span data-stu-id="36f58-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="36f58-153">Zodra de implementatiebewerking is voltooid, wordt uw browser openen en de webpagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="36f58-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![Een webbrowser om de Express-pagina weer te geven.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="36f58-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36f58-156">Next steps</span></span>
<span data-ttu-id="36f58-157">Zie het [Node.js Developer Center](/develop/nodejs/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="36f58-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


