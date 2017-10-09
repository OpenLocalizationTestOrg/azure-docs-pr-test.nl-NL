---
title: aaaDeploy uw app tooAzure met FTP/S-App Service | Microsoft Docs
description: Meer informatie over hoe toodeploy uw app tooAzure App Service met behulp van de FTP- of FTPS.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="d6087-103">Uw app tooAzure met FTP/S-App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="d6087-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="d6087-104">Dit artikel ziet u hoe toouse FTP of toodeploy uw web-app, back-end voor mobiele app of API-app te FTPS[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d6087-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="d6087-105">Hallo FTP-/ S-eindpunt voor uw app is al actief.</span><span class="sxs-lookup"><span data-stu-id="d6087-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="d6087-106">Implementatie van benodigde tooenable FTP-/ S, is geen configuratie.</span><span class="sxs-lookup"><span data-stu-id="d6087-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6087-107">We nemen continu stappen tooimprove beveiliging van Microsoft Azure-Platform.</span><span class="sxs-lookup"><span data-stu-id="d6087-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="d6087-108">Als onderdeel van deze continue inspanningen is een upgrade van webtoepassingen gepland voor Duitsland centraal en Duitsland noordoosten regio's.</span><span class="sxs-lookup"><span data-stu-id="d6087-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="d6087-109">Gedurende deze heeft Web-Apps uitschakelen Hallo gebruik van tekst zonder opmaak FTP-protocol voor implementaties.</span><span class="sxs-lookup"><span data-stu-id="d6087-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="d6087-110">Onze aanbeveling tooour klanten is tooswitch tooFTPS voor implementaties.</span><span class="sxs-lookup"><span data-stu-id="d6087-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="d6087-111">We verwachten niet elke tooyour-service wordt onderbroken tijdens deze upgrade die is gepland voor 9/5.</span><span class="sxs-lookup"><span data-stu-id="d6087-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="d6087-112">Bedankt dat je hebt in deze inspanningen ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="d6087-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="d6087-113">Stap 1: Stel de referenties voor implementatie</span><span class="sxs-lookup"><span data-stu-id="d6087-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="d6087-114">tooaccess hello FTP-server voor uw app, moet u eerst referenties voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="d6087-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="d6087-115">tooset of opnieuw instellen van de implementatiereferenties van uw, Zie [referenties voor de Azure App Service-implementatie](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="d6087-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="d6087-116">Deze zelfstudie wordt gedemonstreerd Hallo gebruik van beveiliging op gebruikersniveau referenties.</span><span class="sxs-lookup"><span data-stu-id="d6087-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="d6087-117">Stap 2: Gegevens van de FTP-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="d6087-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="d6087-118">In Hallo [Azure-portal](https://portal.azure.com), opent u uw app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="d6087-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="d6087-119">Selecteer **overzicht** in het linkermenu Hallo, bekijk Hallo waarden voor **FTP-/ Implementatiegebruiker gebruiker**, **FTP-hostnaam**, en **FTPS hostnaam**.</span><span class="sxs-lookup"><span data-stu-id="d6087-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![FTP-verbindingsgegevens](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="d6087-121">Hallo **FTP-/ Implementatiegebruiker gebruiker** waarde van de gebruiker, zoals weergegeven door hello Azure Portal, met inbegrip van app-naam Hallo in volgorde tooprovide juiste context voor Hallo FTP-server.</span><span class="sxs-lookup"><span data-stu-id="d6087-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="d6087-122">U vindt Hallo dezelfde informatie wanneer u selecteert **eigenschappen** in het linkermenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6087-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="d6087-123">Hallo implementatie wachtwoord wordt nooit weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6087-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="d6087-124">Als u uw implementatie wachtwoord bent vergeten, gaat u terug te[stap 1](#step1) en uw implementatie-wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="d6087-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="d6087-125">Stap 3: Bestanden tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="d6087-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="d6087-126">Van uw FTP-client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), enzovoort), Hallo verbindingsgegevens verzameld van tooconnect tooyour app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6087-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="d6087-127">Kopieer de bestanden en hun respectieve directory structuur toohello [ **/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (of Hallo **/site/wwwroot/App_Data/taken/** map voor WebJobs).</span><span class="sxs-lookup"><span data-stu-id="d6087-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="d6087-128">Bladeren tooyour app-URL tooverify Hallo app wordt correct uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d6087-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="d6087-129">In tegenstelling tot [implementaties op basis van Git](app-service-deploy-local-git.md), FTP-implementatie biedt geen ondersteuning voor hello automatische implementatie te volgen:</span><span class="sxs-lookup"><span data-stu-id="d6087-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="d6087-130">afhankelijkheid herstellen (zoals NuGet, NPM, PIP en Composer automatische)</span><span class="sxs-lookup"><span data-stu-id="d6087-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="d6087-131">compilatie van binaire bestanden voor .NET</span><span class="sxs-lookup"><span data-stu-id="d6087-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="d6087-132">generatie van web.config (dit is een [Node.js-voorbeeld](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="d6087-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="d6087-133">U moet herstellen, maken, en deze vereiste bestanden handmatig op uw lokale machine genereren en deze samen met uw app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="d6087-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d6087-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6087-134">Next steps</span></span>

<span data-ttu-id="d6087-135">Probeer meer geavanceerde implementatiescenario's voor [tooAzure met Git implementeren](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d6087-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="d6087-136">Implementatie op basis van GIT tooAzure kunt versiebeheer, pakket herstellen en MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d6087-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="d6087-137">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="d6087-137">More Resources</span></span>

* <span data-ttu-id="d6087-138">[Een PHP-MySQL web-app maken en implementeren met FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="d6087-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="d6087-139">Referenties voor Azure App Service-implementatie</span><span class="sxs-lookup"><span data-stu-id="d6087-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
