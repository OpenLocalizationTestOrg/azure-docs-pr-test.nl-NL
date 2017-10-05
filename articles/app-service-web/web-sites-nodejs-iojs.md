---
title: io.js gebruiken met Web Apps van Azure App Service
description: Informatie over het gebruik van een web-app in Azure App Service met io.js.
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="91c22-103">io.js gebruiken met Web Apps van Azure App Service</span><span class="sxs-lookup"><span data-stu-id="91c22-103">How to use io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="91c22-104">De populaire knooppunt fork [io.js] biedt verschillende verschillen van Joyent Node.js-project, inclusief een meer geopende governance-model, een snellere releasecyclus en een sneller acceptatie van nieuwe en experimentele JavaScript-functies.</span><span class="sxs-lookup"><span data-stu-id="91c22-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="91c22-105">Terwijl [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps heeft veel Node.js-versies die vooraf is geïnstalleerd, kunt u ook voor een gebruiker opgegeven Node.js-binair bestand.</span><span class="sxs-lookup"><span data-stu-id="91c22-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="91c22-106">Dit artikel bevat twee methoden om het gebruik van io.js op App Service Web Apps: het gebruik van een script voor uitgebreide implementatie, Azure voor het gebruik van de meest recente versie van de beschikbare io.js, evenals het handmatig uploaden van een binaire io.js automatisch te configureren.</span><span class="sxs-lookup"><span data-stu-id="91c22-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="91c22-107">Met behulp van een Script voor implementatie</span><span class="sxs-lookup"><span data-stu-id="91c22-107">Using a Deployment Script</span></span>
<span data-ttu-id="91c22-108">App Service Web Apps uitgevoerd na de implementatie van een Node.js-app, een aantal kleine opdrachten om ervoor te zorgen dat de omgeving juist is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="91c22-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span></span> <span data-ttu-id="91c22-109">Met een implementatiescript, kan dit proces zodanig dat het downloaden en de configuratie van io.js worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="91c22-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span></span>

<span data-ttu-id="91c22-110">De [io.js implementatiescript](https://github.com/felixrieseberg/iojs-azure) is beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="91c22-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="91c22-111">Kopieer zodat io.js op uw web-app **.deployment**, **deploy.cmd** en **IISNode.yml** naar de hoofdmap van de map van uw toepassing en implementeren voor Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="91c22-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span></span>  

<span data-ttu-id="91c22-112">Het eerste bestand **.deployment**, geeft u Web-Apps uit te voeren opdracht **deploy.cmd** van implementatie.</span><span class="sxs-lookup"><span data-stu-id="91c22-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="91c22-113">Dit script wordt uitgevoerd de gebruikelijke stappen voor een Node.js-toepassing, maar ook downloadt de nieuwste versie van io.js.</span><span class="sxs-lookup"><span data-stu-id="91c22-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span></span> <span data-ttu-id="91c22-114">Ten slotte **IISNode.yml** configureert voor het gebruik van alleen de gedownloade io.js binaire in plaats van een vooraf geïnstalleerde binair voor Node.js-Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="91c22-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="91c22-115">Het gebruikte io.js binaire bestand bijwerken, net opnieuw implementeren van uw toepassing - het script wordt een nieuwe versie downloaden van io.js telkens één wanneer die de toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="91c22-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="91c22-116">Met behulp van handmatige installatie</span><span class="sxs-lookup"><span data-stu-id="91c22-116">Using Manual Installation</span></span>
<span data-ttu-id="91c22-117">De handmatige installatie van een aangepaste io.js versie bevat slechts twee stappen.</span><span class="sxs-lookup"><span data-stu-id="91c22-117">The manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="91c22-118">Eerst, downloaden de **win x64** binaire rechtstreeks vanuit de [io.js distributie].</span><span class="sxs-lookup"><span data-stu-id="91c22-118">First, download the **win-x64** binary directly from the [io.js distribution].</span></span> <span data-ttu-id="91c22-119">Vereist zijn twee bestanden - **iojs.exe** en **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="91c22-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="91c22-120">Beide bestanden naar een map in uw web-app bijvoorbeeld opslaan in **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="91c22-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="91c22-121">Voor het configureren van Web-Apps gebruiken **iojs.exe** in plaats van een vooraf geïnstalleerde versie van de knooppunt maken een **IISNode.yml** -bestand in de hoofdmap van uw toepassing en voeg de volgende regel toe.</span><span class="sxs-lookup"><span data-stu-id="91c22-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="91c22-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91c22-122">Next Steps</span></span>
<span data-ttu-id="91c22-123">Io.js met App Service Web Apps met zowel opgegeven implementatiescripts ook als handmatige installatie in dit artikel die hebt u geleerd hoe moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="91c22-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="91c22-124">IO.js wordt zwaar ontwikkeling en vaker bijgewerkt dan Node.js.</span><span class="sxs-lookup"><span data-stu-id="91c22-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="91c22-125">Een aantal Node.js-modules werkt mogelijk niet op io.js - Neem Raadpleeg [io.js op GitHub] voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="91c22-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="91c22-126">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="91c22-126">What's changed</span></span>
* <span data-ttu-id="91c22-127">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="91c22-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="91c22-128">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="91c22-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="91c22-129">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="91c22-129">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="91c22-130">[io.js]: https://iojs.org</span><span class="sxs-lookup"><span data-stu-id="91c22-130">[io.js]: https://iojs.org</span></span>
<span data-ttu-id="91c22-131">[io.js distributie]: https://iojs.org/dist/</span><span class="sxs-lookup"><span data-stu-id="91c22-131">[io.js distribution]: https://iojs.org/dist/</span></span>
<span data-ttu-id="91c22-132">[io.js op GitHub]: https://github.com/iojs/io.js</span><span class="sxs-lookup"><span data-stu-id="91c22-132">[io.js on GitHub]: https://github.com/iojs/io.js</span></span>
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
