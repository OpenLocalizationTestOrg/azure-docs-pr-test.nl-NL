---
title: aaaManage een web-app in Azure App Service
description: Koppelingen tooresources voor het beheren van een web-app in Azure App Service.
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="7d840-103">Een web-app in Azure App Service beheren</span><span class="sxs-lookup"><span data-stu-id="7d840-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="7d840-104">Dit onderwerp vindt u koppelingen tooresources voor het beheren van een web-app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="7d840-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="7d840-105">Beheer omvat alle Hallo-taken die uw web-app probleemloos houden.</span><span class="sxs-lookup"><span data-stu-id="7d840-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="7d840-106">Gedurende de levensduur van de Hallo van een web-app, wordt u verschillende beheertaken uitvoeren tijdens het verplaatsen van de initiële implementatie toonormal bewerking, onderhoud en updates.</span><span class="sxs-lookup"><span data-stu-id="7d840-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="7d840-107">Veel beheertaken voor web-app kunnen worden uitgevoerd in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="7d840-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="7d840-108">Voordat u uw web-app tooproduction implementeren</span><span class="sxs-lookup"><span data-stu-id="7d840-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="7d840-109">Kies een laag</span><span class="sxs-lookup"><span data-stu-id="7d840-109">Choose a tier</span></span>
<span data-ttu-id="7d840-110">Azure App Service wordt aangeboden in vijf categorieën: vrijmaken, gedeelde, Basic, Standard en Premium.</span><span class="sxs-lookup"><span data-stu-id="7d840-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="7d840-111">Zie voor meer informatie over het Hallo-functies en prijzen voor elke laag [prijsinformatie](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="7d840-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="7d840-112">[App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) kunt u meerdere web-apps onder Hallo groep dezelfde categorie.</span><span class="sxs-lookup"><span data-stu-id="7d840-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="7d840-113">U kunt altijd [overschakelen lagen](web-sites-scale.md) nadat u uw web-app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7d840-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="7d840-114">Configuratie</span><span class="sxs-lookup"><span data-stu-id="7d840-114">Configuration</span></span>
<span data-ttu-id="7d840-115">Gebruik Hallo [Azure Portal](https://portal.azure.com/) tooset verschillende configuratieopties.</span><span class="sxs-lookup"><span data-stu-id="7d840-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="7d840-116">Zie voor meer informatie [web-apps configureren in Azure App Service](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7d840-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="7d840-117">Dit is een snelle Controlelijst:</span><span class="sxs-lookup"><span data-stu-id="7d840-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="7d840-118">Selecteer **runtime versies** voor .NET, PHP, Java of Python, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="7d840-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="7d840-119">Schakel **WebSockets** als Hallo WebSocket-protocol maakt gebruik van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7d840-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="7d840-120">(Dit omvat apps die gebruikmaken van [ASP.NET SignalR](http://www.asp.net/signalr) of [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="7d840-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="7d840-121">Voert u doorlopende webtaken?</span><span class="sxs-lookup"><span data-stu-id="7d840-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="7d840-122">Zo ja, inschakelen **altijd op**.</span><span class="sxs-lookup"><span data-stu-id="7d840-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="7d840-123">Set Hallo **standaarddocument**, zoals index.html.</span><span class="sxs-lookup"><span data-stu-id="7d840-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="7d840-124">U kunt in toevoeging toothese basic configuratie-instellingen, tooconfigure Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="7d840-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="7d840-125">**Secure Socket Layer (SSL)** versleuteling.</span><span class="sxs-lookup"><span data-stu-id="7d840-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="7d840-126">toouse SSL met een aangepaste domeinnaam, moet u een SSL-certificaat en het configureren van uw web-app toouse deze.</span><span class="sxs-lookup"><span data-stu-id="7d840-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="7d840-127">Zie [HTTPS inschakelen voor een web-app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="7d840-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="7d840-128">**Aangepaste domeinnaam.**</span><span class="sxs-lookup"><span data-stu-id="7d840-128">**Custom domain name.**</span></span> <span data-ttu-id="7d840-129">Uw web-app wordt automatisch een subdomein onder azurewebsites.net heeft.</span><span class="sxs-lookup"><span data-stu-id="7d840-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="7d840-130">U kunt een aangepaste domeinnaam bijvoorbeeld contoso.com koppelen. Zie [een aangepaste domeinnaam configureren in Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="7d840-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="7d840-131">Taalspecifieke configuratie:</span><span class="sxs-lookup"><span data-stu-id="7d840-131">Language-specific configuration:</span></span>

* <span data-ttu-id="7d840-132">**PHP**: [PHP configureren in Azure App Service WebApps](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7d840-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="7d840-133">**Python**: [Python configureren met Azure App Service Web-Apps](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="7d840-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="7d840-134">Terwijl uw web-app wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="7d840-134">While your web app is running</span></span>
<span data-ttu-id="7d840-135">Terwijl uw web-app wordt uitgevoerd, wilt u ervoor dat deze beschikbaar is en dat het gebruikersverkeer toomeet schalen toomake.</span><span class="sxs-lookup"><span data-stu-id="7d840-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="7d840-136">U moet mogelijk ook tootroubleshoot fouten.</span><span class="sxs-lookup"><span data-stu-id="7d840-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="7d840-137">Bewaking</span><span class="sxs-lookup"><span data-stu-id="7d840-137">Monitoring</span></span>
* <span data-ttu-id="7d840-138">Met hello Azure Portal, kunt u [toevoegen maatstaven voor prestaties](web-sites-monitor.md) zoals CPU-gebruik en het aantal aanvragen van clients.</span><span class="sxs-lookup"><span data-stu-id="7d840-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="7d840-139">[Schalen van uw web-app](web-sites-scale.md) in antwoord tootraffic.</span><span class="sxs-lookup"><span data-stu-id="7d840-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="7d840-140">Afhankelijk van de laag, kunt u Hallo aantal VM's en/of Hallo grootte van de VM-instanties Hallo schalen.</span><span class="sxs-lookup"><span data-stu-id="7d840-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="7d840-141">In Hallo Standard en Premium-categorieën, kunt u ook instellen automatisch schalen, zodat uw web-app automatisch wordt geschaald op basis van een vaste planning, of in antwoord tooload.</span><span class="sxs-lookup"><span data-stu-id="7d840-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="7d840-142">Back-ups</span><span class="sxs-lookup"><span data-stu-id="7d840-142">Backups</span></span>
* <span data-ttu-id="7d840-143">Stel [automatische back-ups](web-sites-backup.md) van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7d840-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="7d840-144">Meer informatie over back-ups in [in deze video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="7d840-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="7d840-145">Meer informatie over opties voor Hallo [databases herstellen](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7d840-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="7d840-146">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7d840-146">Troubleshooting</span></span>
* <span data-ttu-id="7d840-147">Als er iets mis gaat, kunt u [in Visual Studio oplossen](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), met behulp van diagnostische logboeken en foutopsporing in de cloud Hallo live.</span><span class="sxs-lookup"><span data-stu-id="7d840-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="7d840-148">Buiten Visual Studio zijn er verschillende manieren toocollect diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="7d840-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="7d840-149">Zie [logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="7d840-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="7d840-150">Zie voor Node.js-toepassingen [hoe toodebug een Node.js web-app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="7d840-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="7d840-151">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="7d840-151">Restoring Data</span></span>
* <span data-ttu-id="7d840-152">[Herstellen](web-sites-restore.md) een web-app die u eerder een back-up.</span><span class="sxs-lookup"><span data-stu-id="7d840-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="7d840-153">Wanneer u uw web-app bijwerken</span><span class="sxs-lookup"><span data-stu-id="7d840-153">When you update your web app</span></span>
<span data-ttu-id="7d840-154">Als u automatische back-ups niet hebt ingeschakeld, kunt u een [handmatige back-up](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="7d840-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="7d840-155">Overweeg het gebruik van [gefaseerde implementatie](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="7d840-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="7d840-156">Deze optie kunt u updates tooa staging-implementatie die naast elkaar uitvoert publiceren met uw productie-implementatie.</span><span class="sxs-lookup"><span data-stu-id="7d840-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


