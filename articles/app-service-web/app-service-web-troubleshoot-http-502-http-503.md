---
title: 502 Slechte gateway oplossen, 503 service niet beschikbaar fouten | Microsoft Docs
description: Problemen oplossen met 502 Slechte gateway en 503 service niet beschikbaar fouten in uw web-app in Azure App Service wordt gehost.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: 502 Slechte gateway 503 service niet beschikbaar, 503-fout, fout 502
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 397a6aaf7dc27adfa0fc0e722b8a2be5cc1d75f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="e990b-104">HTTP-fouten van '502 Slechte gateway' en '503 service niet beschikbaar' in uw Azure-web-apps</span><span class="sxs-lookup"><span data-stu-id="e990b-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="e990b-105">'502 Slechte gateway' en '503 service niet beschikbaar' zijn veelvoorkomende fouten in uw web-app gehost in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e990b-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="e990b-106">In dit artikel helpt u bij deze fouten oplossen.</span><span class="sxs-lookup"><span data-stu-id="e990b-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="e990b-107">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts raadplegen op [de Azure MSDN en de Stack Overflow-forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e990b-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e990b-108">U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand.</span><span class="sxs-lookup"><span data-stu-id="e990b-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="e990b-109">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en klik op **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="e990b-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="e990b-110">Symptoom</span><span class="sxs-lookup"><span data-stu-id="e990b-110">Symptom</span></span>
<span data-ttu-id="e990b-111">Wanneer u de web-app bladert, wordt een HTTP '502 Slechte Gateway' fout of een HTTP-fout '503 Service niet beschikbaar'.</span><span class="sxs-lookup"><span data-stu-id="e990b-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="e990b-112">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="e990b-112">Cause</span></span>
<span data-ttu-id="e990b-113">Dit probleem wordt vaak veroorzaakt door problemen met toepassingen niveau, zoals:</span><span class="sxs-lookup"><span data-stu-id="e990b-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="e990b-114">aanvragen duurt lang</span><span class="sxs-lookup"><span data-stu-id="e990b-114">requests taking a long time</span></span>
* <span data-ttu-id="e990b-115">toepassing met hoge geheugen/CPU</span><span class="sxs-lookup"><span data-stu-id="e990b-115">application using high memory/CPU</span></span>
* <span data-ttu-id="e990b-116">de toepassing is gecrasht vanwege een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="e990b-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="e990b-117">Stappen voor probleemoplossing om op te lossen '502 Slechte gateway' en '503 service niet beschikbaar'-fouten</span><span class="sxs-lookup"><span data-stu-id="e990b-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="e990b-118">Het oplossen van problemen kan worden onderverdeeld in drie verschillende taken in opeenvolgende volgorde:</span><span class="sxs-lookup"><span data-stu-id="e990b-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="e990b-119">Bekijken en controleren van gedrag van toepassingen</span><span class="sxs-lookup"><span data-stu-id="e990b-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="e990b-120">Gegevens verzamelen</span><span class="sxs-lookup"><span data-stu-id="e990b-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="e990b-121">Het probleem te verhelpen</span><span class="sxs-lookup"><span data-stu-id="e990b-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="e990b-122">[App Service Web Apps](/services/app-service/web/) biedt verschillende opties bij elke stap.</span><span class="sxs-lookup"><span data-stu-id="e990b-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="e990b-123">1. Bekijken en controleren van gedrag van toepassingen</span><span class="sxs-lookup"><span data-stu-id="e990b-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="e990b-124">Servicestatus bijhouden</span><span class="sxs-lookup"><span data-stu-id="e990b-124">Track Service health</span></span>
<span data-ttu-id="e990b-125">Microsoft Azure publicizes telkens wanneer er een service wordt onderbroken of de prestaties nadelig beïnvloeden is.</span><span class="sxs-lookup"><span data-stu-id="e990b-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="e990b-126">U kunt de status van de service bijhouden op het [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e990b-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="e990b-127">Zie voor meer informatie [bijhouden servicestatus](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="e990b-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="e990b-128">Uw web-app bewaken</span><span class="sxs-lookup"><span data-stu-id="e990b-128">Monitor your web app</span></span>
<span data-ttu-id="e990b-129">Deze optie kunt u achterhalen als uw toepassing problemen ondervindt.</span><span class="sxs-lookup"><span data-stu-id="e990b-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="e990b-130">Klik op de blade van uw web-app de **aanvragen en fouten** tegel.</span><span class="sxs-lookup"><span data-stu-id="e990b-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="e990b-131">De **metriek** blade ziet u alle metrische gegevens die u kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e990b-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="e990b-132">Sommige van de metrische gegevens die u voor uw web-app kunt bewaken</span><span class="sxs-lookup"><span data-stu-id="e990b-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="e990b-133">Gemiddelde geheugen werkset</span><span class="sxs-lookup"><span data-stu-id="e990b-133">Average memory working set</span></span>
* <span data-ttu-id="e990b-134">Gemiddelde reactietijd</span><span class="sxs-lookup"><span data-stu-id="e990b-134">Average response time</span></span>
* <span data-ttu-id="e990b-135">CPU-tijd</span><span class="sxs-lookup"><span data-stu-id="e990b-135">CPU time</span></span>
* <span data-ttu-id="e990b-136">Geheugen-werkset</span><span class="sxs-lookup"><span data-stu-id="e990b-136">Memory working set</span></span>
* <span data-ttu-id="e990b-137">Aanvragen</span><span class="sxs-lookup"><span data-stu-id="e990b-137">Requests</span></span>

![Monitor voor web-app voor het oplossen van HTTP-fouten van 502 Slechte gateway en 503 service niet beschikbaar](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="e990b-139">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="e990b-139">For more information, see:</span></span>

* [<span data-ttu-id="e990b-140">Web-Apps bewaken in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e990b-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="e990b-141">Waarschuwingen ontvangen</span><span class="sxs-lookup"><span data-stu-id="e990b-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="e990b-142">2. Gegevens verzamelen</span><span class="sxs-lookup"><span data-stu-id="e990b-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="e990b-143">Gebruik de Portal-Azure App Service-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="e990b-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="e990b-144">Web Apps biedt u de mogelijkheid om op te lossen problemen met betrekking tot uw web-app door te kijken HTTP Logboeken, gebeurtenislogboeken proces dumpbestanden en meer.</span><span class="sxs-lookup"><span data-stu-id="e990b-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="e990b-145">U toegang hebt tot deze informatie met onze portal ondersteuning op **http://&lt;uw app-naam >.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="e990b-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="e990b-146">De portal voor ondersteuning van Azure App Service biedt drie afzonderlijke tabbladen ter ondersteuning van de drie stappen van een algemeen scenario voor het oplossen van problemen:</span><span class="sxs-lookup"><span data-stu-id="e990b-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="e990b-147">Huidige gedrag observeren</span><span class="sxs-lookup"><span data-stu-id="e990b-147">Observe current behavior</span></span>
2. <span data-ttu-id="e990b-148">Door het verzamelen van diagnostische gegevens en uitvoeren van de ingebouwde analyzers analyseren</span><span class="sxs-lookup"><span data-stu-id="e990b-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="e990b-149">Beperken</span><span class="sxs-lookup"><span data-stu-id="e990b-149">Mitigate</span></span>

<span data-ttu-id="e990b-150">Als het probleem nu voordoet zich, klikt u op **analyseren** > **Diagnostics** > **onderzoeken nu** een diagnostische sessie voor u te maken, die HTTP-Logboeken, Logboeken, geheugen dumpbestanden, PHP-foutenlogboek en PHP-proces rapport verzamelt.</span><span class="sxs-lookup"><span data-stu-id="e990b-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="e990b-151">Nadat de gegevens worden verzameld, wordt ook een analyse uitgevoerd op de gegevens en bieden u een HTML-rapport.</span><span class="sxs-lookup"><span data-stu-id="e990b-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="e990b-152">Als u downloaden van de gegevens standaard wilt, zou deze opgeslagen in de map D:\home\data\DaaS.</span><span class="sxs-lookup"><span data-stu-id="e990b-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="e990b-153">Zie voor meer informatie over de ondersteuning van Azure App Service-portal [nieuwe Updates naar de Site-extensie ondersteuning voor Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="e990b-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="e990b-154">Gebruik de Kudu-Console voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="e990b-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="e990b-155">Web-Apps wordt geleverd met een Foutopsporingsconsole die u gebruiken kunt voor foutopsporing, verkennen, het uploaden van bestanden, evenals de JSON-eindpunten voor het ophalen van informatie over uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="e990b-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="e990b-156">Dit heet de *Kudu-Console* of de *SCM Dashboard* voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="e990b-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="e990b-157">U kunt dit dashboard openen door op de koppeling **https://&lt;uw app-naam >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="e990b-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="e990b-158">Enkele van de Kudu verschaft zaken zijn:</span><span class="sxs-lookup"><span data-stu-id="e990b-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="e990b-159">omgevingsinstellingen voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="e990b-159">environment settings for your application</span></span>
* <span data-ttu-id="e990b-160">logboekstream</span><span class="sxs-lookup"><span data-stu-id="e990b-160">log stream</span></span>
* <span data-ttu-id="e990b-161">diagnostische dump</span><span class="sxs-lookup"><span data-stu-id="e990b-161">diagnostic dump</span></span>
* <span data-ttu-id="e990b-162">fouten opsporen console waarin u Powershell-cmdlets en basic DOS-opdrachten kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e990b-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="e990b-163">Een andere handige functie van Kudu is dat, als uw toepassing die eerste kans uitzonderingen, kunt u Kudu en dumpbestanden voor het SysInternals-hulpprogramma Procdump geheugen maken.</span><span class="sxs-lookup"><span data-stu-id="e990b-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="e990b-164">Deze geheugendumps momentopnamen van het proces zijn en vaak kunt u meer gecompliceerde problemen oplossen met uw web-app.</span><span class="sxs-lookup"><span data-stu-id="e990b-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="e990b-165">Zie voor meer informatie over functies die beschikbaar zijn in Kudu [Azure Websites on line hulpmiddelen die u moet weten over](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="e990b-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="e990b-166">3. Het probleem te verhelpen</span><span class="sxs-lookup"><span data-stu-id="e990b-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="e990b-167">De web-app schalen</span><span class="sxs-lookup"><span data-stu-id="e990b-167">Scale the web app</span></span>
<span data-ttu-id="e990b-168">In Azure App Service kunt voor betere prestaties en doorvoer, u de schaal waarmee u uw toepassing uitvoert aanpassen.</span><span class="sxs-lookup"><span data-stu-id="e990b-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="e990b-169">Schalen van een web-app omvat twee gerelateerde acties: uw App Service-abonnement wijzigen in een hogere prijscategorie en bepaalde instellingen configureren nadat u hebt overgeschakeld naar de hogere prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="e990b-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="e990b-170">Zie voor meer informatie over het schalen [schalen van een web-app in Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="e990b-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="e990b-171">U kunt bovendien uw toepassing uitvoeren in meer dan één exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e990b-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="e990b-172">Dit niet alleen biedt u meer mogelijkheden voor verwerking, maar biedt u eveneens bepaalde hoeveelheid fouttolerantie.</span><span class="sxs-lookup"><span data-stu-id="e990b-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="e990b-173">Als het proces uitgeschakeld op één exemplaar wordt, wordt in het andere exemplaar echter blijven voldoen aan aanvragen.</span><span class="sxs-lookup"><span data-stu-id="e990b-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="e990b-174">U kunt instellen om de schaal worden handmatig of automatisch.</span><span class="sxs-lookup"><span data-stu-id="e990b-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="e990b-175">Gebruik AutoHeal</span><span class="sxs-lookup"><span data-stu-id="e990b-175">Use AutoHeal</span></span>
<span data-ttu-id="e990b-176">AutoHeal wordt gerecycled het werkproces voor uw app op basis van de instellingen die u (zoals wijzigingen in de configuratie, aanvragen, limieten op basis van geheugen of de benodigde tijd kiest voor het uitvoeren van een aanvraag).</span><span class="sxs-lookup"><span data-stu-id="e990b-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="e990b-177">De meeste gevallen, is recyclen van het proces de snelste manier om te herstellen van een probleem.</span><span class="sxs-lookup"><span data-stu-id="e990b-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="e990b-178">Hoewel u altijd opnieuw van de web-app rechtstreeks in de Azure Portal opstarten kunt, wordt AutoHeal het automatisch voor u doen.</span><span class="sxs-lookup"><span data-stu-id="e990b-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="e990b-179">Hoeft u sommige triggers toevoegen in web.config voor de hoofdmap voor uw web-app is.</span><span class="sxs-lookup"><span data-stu-id="e990b-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="e990b-180">Houd er rekening mee dat deze instellingen op dezelfde manier werken zou, zelfs als uw toepassing niet een .net een is.</span><span class="sxs-lookup"><span data-stu-id="e990b-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="e990b-181">Zie voor meer informatie [Azure websites automatisch herstel](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="e990b-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="e990b-182">Opnieuw opstarten van de web-app</span><span class="sxs-lookup"><span data-stu-id="e990b-182">Restart the web app</span></span>
<span data-ttu-id="e990b-183">Dit is vaak de eenvoudigste manier om eenmalige problemen herstellen.</span><span class="sxs-lookup"><span data-stu-id="e990b-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="e990b-184">Op de [Azure Portal](https://portal.azure.com/), op de blade van uw web-app, hebt u de opties te stoppen of opnieuw opstarten van uw app.</span><span class="sxs-lookup"><span data-stu-id="e990b-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![opnieuw opstarten van de app om op te lossen HTTP-fouten van 502 Slechte gateway en 503 service niet beschikbaar](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="e990b-186">U kunt ook uw web-app met Azure Powershell beheren.</span><span class="sxs-lookup"><span data-stu-id="e990b-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="e990b-187">Zie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e990b-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

