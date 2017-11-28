---
title: aaaHow toouse io.js met Azure App Service Web Apps
description: Meer informatie over hoe een web-app in Azure App Service met io.js toouse.
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
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="497f7-103">Hoe toouse io.js met Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="497f7-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="497f7-104">Hallo populaire knooppunt fork [io.js] biedt verschillende verschillen-tooJoyent Node.js-project, inclusief een meer geopende governance-model, een snellere releasecyclus en een sneller acceptatie van nieuwe en experimentele JavaScript-functies.</span><span class="sxs-lookup"><span data-stu-id="497f7-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="497f7-105">Terwijl [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps heeft veel Node.js-versies die vooraf is geïnstalleerd, kunt u ook voor een gebruiker opgegeven Node.js-binair bestand.</span><span class="sxs-lookup"><span data-stu-id="497f7-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="497f7-106">Dit artikel bevat twee methoden mogelijk hello gebruiken io.js op App Service Web Apps: gebruik van een script voor uitgebreide implementatie, die configureert automatisch de meest recente beschikbare io.js versie van Azure toouse hello, evenals Hallo handmatig uploaden van een binair io.js Hallo.</span><span class="sxs-lookup"><span data-stu-id="497f7-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="497f7-107">Met behulp van een Script voor implementatie</span><span class="sxs-lookup"><span data-stu-id="497f7-107">Using a Deployment Script</span></span>
<span data-ttu-id="497f7-108">App Service Web Apps uitgevoerd na de implementatie van een Node.js-app, een aantal kleine opdrachten tooensure die omgeving Hallo juist is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="497f7-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="497f7-109">Met een implementatiescript, kan dit proces worden aangepaste tooinclude Hallo downloaden en de configuratie van io.js.</span><span class="sxs-lookup"><span data-stu-id="497f7-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="497f7-110">Hallo [io.js implementatiescript](https://github.com/felixrieseberg/iojs-azure) is beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="497f7-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="497f7-111">Kopieer in tooenable io.js op uw web-app **.deployment**, **deploy.cmd** en **IISNode.yml** toohello hoofdmap van de toepassingsmap tooWeb Apps en implementeren.</span><span class="sxs-lookup"><span data-stu-id="497f7-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="497f7-112">het eerste bestand Hello, **.deployment**, Hiermee geeft u Web-Apps toorun **deploy.cmd** van implementatie.</span><span class="sxs-lookup"><span data-stu-id="497f7-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="497f7-113">Dit script alle Hallo gebruikelijke stappen voor een Node.js-toepassing wordt uitgevoerd, maar ook de meest recente versie Hallo van io.js gedownload.</span><span class="sxs-lookup"><span data-stu-id="497f7-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="497f7-114">Ten slotte **IISNode.yml** Web-Apps toouse alleen Hallo gedownload io.js binaire in plaats van een vooraf geïnstalleerde Node.js binair configureert.</span><span class="sxs-lookup"><span data-stu-id="497f7-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="497f7-115">tooupdate hello io.js binair gebruikt, alleen uw toepassing opnieuw distribueren - Hallo script downloaden een nieuwe versie van io.js die elke één keer Hallo-toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="497f7-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="497f7-116">Met behulp van handmatige installatie</span><span class="sxs-lookup"><span data-stu-id="497f7-116">Using Manual Installation</span></span>
<span data-ttu-id="497f7-117">Hallo handmatige installatie van een aangepaste io.js versie bevat slechts twee stappen.</span><span class="sxs-lookup"><span data-stu-id="497f7-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="497f7-118">Eerst downloaden Hallo **win x64** binaire rechtstreeks vanuit Hallo [io.js distributie].</span><span class="sxs-lookup"><span data-stu-id="497f7-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="497f7-119">Vereist zijn twee bestanden - **iojs.exe** en **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="497f7-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="497f7-120">Opslaan beide bestanden tooa map in uw web-app, bijvoorbeeld in **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="497f7-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="497f7-121">tooconfigure Web-Apps toouse **iojs.exe** in plaats van een vooraf geïnstalleerde versie van de knooppunt maken een **IISNode.yml** -bestand op basis van uw toepassing hello en Hallo volgt regel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="497f7-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="497f7-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="497f7-122">Next Steps</span></span>
<span data-ttu-id="497f7-123">In dit artikel hebt u geleerd hoe toouse io.js met App Service Web Apps met zowel opgegeven voor de implementatiescripts, evenals een handmatige installatie.</span><span class="sxs-lookup"><span data-stu-id="497f7-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="497f7-124">IO.js wordt zwaar ontwikkeling en vaker bijgewerkt dan Node.js.</span><span class="sxs-lookup"><span data-stu-id="497f7-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="497f7-125">Een aantal Node.js-modules werkt mogelijk niet op io.js - Neem Raadpleeg [io.js op GitHub] voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="497f7-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="497f7-126">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="497f7-126">What's changed</span></span>
* <span data-ttu-id="497f7-127">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="497f7-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="497f7-128">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="497f7-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="497f7-129">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="497f7-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js distributie]: https://iojs.org/dist/
[io.js op GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
