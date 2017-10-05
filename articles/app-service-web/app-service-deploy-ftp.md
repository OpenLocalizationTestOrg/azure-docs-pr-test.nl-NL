---
title: Uw app implementeren in Azure App Service met behulp van FTP/S | Microsoft Docs
description: Informatie over het implementeren van uw app in Azure App Service met behulp van de FTP- of FTPS.
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
ms.openlocfilehash: 9078abbc4ed7eff6975201443992f7bbb84bf57c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="53c69-103">Uw app implementeren in Azure App Service met behulp van FTP/S</span><span class="sxs-lookup"><span data-stu-id="53c69-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="53c69-104">Dit artikel laat zien hoe u FTP- of FTPS voor het implementeren van uw web-app, back-end voor mobiele app of API-app [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="53c69-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="53c69-105">Het eindpunt van de FTP-/ S voor uw app is al actief.</span><span class="sxs-lookup"><span data-stu-id="53c69-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="53c69-106">Er is geen configuratie nodig zijn voor de FTP-/ S-implementatie in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="53c69-106">No configuration is necessary to enable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53c69-107">We zijn voortdurend stappen voor verbeterde beveiliging van Microsoft Azure-Platform.</span><span class="sxs-lookup"><span data-stu-id="53c69-107">We are continuously taking steps to improve Microsoft Azure Platform security.</span></span> <span data-ttu-id="53c69-108">Als onderdeel van deze continue inspanningen is een upgrade van webtoepassingen gepland voor Duitsland centraal en Duitsland noordoosten regio's.</span><span class="sxs-lookup"><span data-stu-id="53c69-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="53c69-109">Tijdens dit wordt het gebruik van tekst zonder opmaak FTP-protocol voor implementaties op Web-Apps worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="53c69-109">During this Web Apps will be disabling the use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="53c69-110">Onze aanbeveling voor onze klanten, is overschakelen naar FTPS voor implementaties.</span><span class="sxs-lookup"><span data-stu-id="53c69-110">Our recommendation to our customers is to switch to FTPS for deployments.</span></span> <span data-ttu-id="53c69-111">We niet van plan bent een onderbreking van uw service tijdens deze upgrade die is gepland voor 9/5.</span><span class="sxs-lookup"><span data-stu-id="53c69-111">We do not expect any disruption to your service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="53c69-112">Bedankt dat je hebt in deze inspanningen ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="53c69-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="53c69-113">Stap 1: Stel de referenties voor implementatie</span><span class="sxs-lookup"><span data-stu-id="53c69-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="53c69-114">Voor toegang tot de FTP-server voor uw app, moet u eerst referenties voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="53c69-114">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="53c69-115">Als u wilt instellen of opnieuw instellen van uw referenties voor implementatie, Zie [referenties voor de Azure App Service-implementatie](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="53c69-115">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="53c69-116">Deze zelfstudie laat zien dat het gebruik van beveiliging op gebruikersniveau referenties.</span><span class="sxs-lookup"><span data-stu-id="53c69-116">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="53c69-117">Stap 2: Gegevens van de FTP-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="53c69-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="53c69-118">In de [Azure-portal](https://portal.azure.com), opent u uw app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="53c69-118">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="53c69-119">Selecteer **overzicht** Noteer de waarden voor in het menu links **FTP-/ Implementatiegebruiker gebruiker**, **FTP-hostnaam**, en **FTPS hostnaam**.</span><span class="sxs-lookup"><span data-stu-id="53c69-119">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![FTP-verbindingsgegevens](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="53c69-121">De **FTP-/ Implementatiegebruiker gebruiker** gebruiker waarde zoals weergegeven door de Azure Portal, met inbegrip van de app-naam zodat de juiste context voor de FTP-server.</span><span class="sxs-lookup"><span data-stu-id="53c69-121">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="53c69-122">U vindt de dezelfde informatie wanneer u selecteert **eigenschappen** in het menu links.</span><span class="sxs-lookup"><span data-stu-id="53c69-122">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="53c69-123">Het wachtwoord voor de implementatie wordt nooit weergegeven.</span><span class="sxs-lookup"><span data-stu-id="53c69-123">Also, the deployment password is never shown.</span></span> <span data-ttu-id="53c69-124">Als u uw implementatie wachtwoord bent vergeten, gaat u terug naar [stap 1](#step1) en uw implementatie-wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="53c69-124">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="53c69-125">Stap 3: Bestanden implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="53c69-125">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="53c69-126">Van uw FTP-client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), enzovoort), de verbindingsgegevens die u hebt verzameld om verbinding met uw app te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="53c69-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="53c69-127">Kopieer uw bestanden en hun respectieve mapstructuur op de [ **/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (of de **/site/wwwroot/App_Data/taken/** map voor WebJobs).</span><span class="sxs-lookup"><span data-stu-id="53c69-127">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="53c69-128">Blader naar uw app-URL om te controleren of dat de app correct wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="53c69-128">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="53c69-129">In tegenstelling tot [implementaties op basis van Git](app-service-deploy-local-git.md), FTP-implementatie biedt geen ondersteuning voor de volgende implementatie automatische:</span><span class="sxs-lookup"><span data-stu-id="53c69-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="53c69-130">afhankelijkheid herstellen (zoals NuGet, NPM, PIP en Composer automatische)</span><span class="sxs-lookup"><span data-stu-id="53c69-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="53c69-131">compilatie van binaire bestanden voor .NET</span><span class="sxs-lookup"><span data-stu-id="53c69-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="53c69-132">generatie van web.config (dit is een [Node.js-voorbeeld](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="53c69-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="53c69-133">U moet herstellen, maken, en deze vereiste bestanden handmatig op uw lokale machine genereren en deze samen met uw app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="53c69-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="53c69-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="53c69-134">Next steps</span></span>

<span data-ttu-id="53c69-135">Probeer meer geavanceerde implementatiescenario's voor [implementeren naar Azure met Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="53c69-135">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="53c69-136">Implementatie op basis van GIT in Azure kunt versiebeheer, pakket herstellen en MSBuild.</span><span class="sxs-lookup"><span data-stu-id="53c69-136">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="53c69-137">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="53c69-137">More Resources</span></span>

* <span data-ttu-id="53c69-138">[Een PHP-MySQL web-app maken en implementeren met FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="53c69-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="53c69-139">Referenties voor Azure App Service-implementatie</span><span class="sxs-lookup"><span data-stu-id="53c69-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
