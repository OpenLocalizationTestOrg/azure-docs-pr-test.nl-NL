---
title: Ongeldige gateway aaaFix 502, 503 service niet beschikbaar fouten | Microsoft Docs
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
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="5f420-104">HTTP-fouten van '502 Slechte gateway' en '503 service niet beschikbaar' in uw Azure-web-apps</span><span class="sxs-lookup"><span data-stu-id="5f420-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="5f420-105">'502 Slechte gateway' en '503 service niet beschikbaar' zijn veelvoorkomende fouten in uw web-app gehost in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="5f420-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="5f420-106">In dit artikel helpt u bij deze fouten oplossen.</span><span class="sxs-lookup"><span data-stu-id="5f420-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="5f420-107">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [hello Azure MSDN en forums Stack Overflow Hallo](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5f420-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="5f420-108">U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand.</span><span class="sxs-lookup"><span data-stu-id="5f420-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="5f420-109">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en klik op **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="5f420-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="5f420-110">Symptoom</span><span class="sxs-lookup"><span data-stu-id="5f420-110">Symptom</span></span>
<span data-ttu-id="5f420-111">Wanneer u de web-app toohello bladert, wordt een HTTP '502 Slechte Gateway' fout of een HTTP-fout '503 Service niet beschikbaar'.</span><span class="sxs-lookup"><span data-stu-id="5f420-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="5f420-112">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="5f420-112">Cause</span></span>
<span data-ttu-id="5f420-113">Dit probleem wordt vaak veroorzaakt door problemen met toepassingen niveau, zoals:</span><span class="sxs-lookup"><span data-stu-id="5f420-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="5f420-114">aanvragen duurt lang</span><span class="sxs-lookup"><span data-stu-id="5f420-114">requests taking a long time</span></span>
* <span data-ttu-id="5f420-115">toepassing met hoge geheugen/CPU</span><span class="sxs-lookup"><span data-stu-id="5f420-115">application using high memory/CPU</span></span>
* <span data-ttu-id="5f420-116">de toepassing is gecrasht vanwege tooan uitzondering.</span><span class="sxs-lookup"><span data-stu-id="5f420-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="5f420-117">Het oplossen van stappen toosolve '502 Slechte gateway' en '503 service niet beschikbaar'-fouten</span><span class="sxs-lookup"><span data-stu-id="5f420-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="5f420-118">Het oplossen van problemen kan worden onderverdeeld in drie verschillende taken in opeenvolgende volgorde:</span><span class="sxs-lookup"><span data-stu-id="5f420-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="5f420-119">Bekijken en controleren van gedrag van toepassingen</span><span class="sxs-lookup"><span data-stu-id="5f420-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="5f420-120">Gegevens verzamelen</span><span class="sxs-lookup"><span data-stu-id="5f420-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="5f420-121">Hallo probleem verhelpen</span><span class="sxs-lookup"><span data-stu-id="5f420-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="5f420-122">[App Service Web Apps](/services/app-service/web/) biedt verschillende opties bij elke stap.</span><span class="sxs-lookup"><span data-stu-id="5f420-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="5f420-123">1. Bekijken en controleren van gedrag van toepassingen</span><span class="sxs-lookup"><span data-stu-id="5f420-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="5f420-124">Servicestatus bijhouden</span><span class="sxs-lookup"><span data-stu-id="5f420-124">Track Service health</span></span>
<span data-ttu-id="5f420-125">Microsoft Azure publicizes telkens wanneer er een service wordt onderbroken of de prestaties nadelig beïnvloeden is.</span><span class="sxs-lookup"><span data-stu-id="5f420-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="5f420-126">U kunt Hallo status van Hallo service bijhouden op Hallo [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5f420-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="5f420-127">Zie voor meer informatie [bijhouden servicestatus](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="5f420-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="5f420-128">Uw web-app bewaken</span><span class="sxs-lookup"><span data-stu-id="5f420-128">Monitor your web app</span></span>
<span data-ttu-id="5f420-129">Deze optie kunt u toofind uit als uw toepassing problemen ondervindt.</span><span class="sxs-lookup"><span data-stu-id="5f420-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="5f420-130">Klik in de blade van uw web-app op Hallo **aanvragen en fouten** tegel.</span><span class="sxs-lookup"><span data-stu-id="5f420-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="5f420-131">Hallo **metriek** blade ziet u alle Hallo metrische gegevens u kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5f420-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="5f420-132">Aantal Hallo metrische gegevens die u toomonitor voor uw web-app wilt mogelijk</span><span class="sxs-lookup"><span data-stu-id="5f420-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="5f420-133">Gemiddelde geheugen werkset</span><span class="sxs-lookup"><span data-stu-id="5f420-133">Average memory working set</span></span>
* <span data-ttu-id="5f420-134">Gemiddelde reactietijd</span><span class="sxs-lookup"><span data-stu-id="5f420-134">Average response time</span></span>
* <span data-ttu-id="5f420-135">CPU-tijd</span><span class="sxs-lookup"><span data-stu-id="5f420-135">CPU time</span></span>
* <span data-ttu-id="5f420-136">Geheugen-werkset</span><span class="sxs-lookup"><span data-stu-id="5f420-136">Memory working set</span></span>
* <span data-ttu-id="5f420-137">Aanvragen</span><span class="sxs-lookup"><span data-stu-id="5f420-137">Requests</span></span>

![Monitor voor web-app voor het oplossen van HTTP-fouten van 502 Slechte gateway en 503 service niet beschikbaar](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="5f420-139">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="5f420-139">For more information, see:</span></span>

* [<span data-ttu-id="5f420-140">Web-Apps bewaken in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5f420-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="5f420-141">Waarschuwingen ontvangen</span><span class="sxs-lookup"><span data-stu-id="5f420-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="5f420-142">2. Gegevens verzamelen</span><span class="sxs-lookup"><span data-stu-id="5f420-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="5f420-143">Hello Azure App Service-ondersteuning Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="5f420-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="5f420-144">Web Apps biedt Hallo mogelijkheid tootroubleshoot problemen gerelateerde tooyour web-app door te kijken HTTP Logboeken, gebeurtenislogboeken proces dumpbestanden en meer.</span><span class="sxs-lookup"><span data-stu-id="5f420-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="5f420-145">U toegang hebt tot deze informatie met onze portal ondersteuning op **http://&lt;uw app-naam >.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="5f420-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="5f420-146">Hallo-portal voor ondersteuning van Azure App Service biedt drie afzonderlijke tabbladen toosupport Hallo drie stappen van een algemeen scenario voor het oplossen van problemen:</span><span class="sxs-lookup"><span data-stu-id="5f420-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="5f420-147">Huidige gedrag observeren</span><span class="sxs-lookup"><span data-stu-id="5f420-147">Observe current behavior</span></span>
2. <span data-ttu-id="5f420-148">Door het verzamelen van diagnostische gegevens en Hallo ingebouwde analyzers analyseren</span><span class="sxs-lookup"><span data-stu-id="5f420-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="5f420-149">Beperken</span><span class="sxs-lookup"><span data-stu-id="5f420-149">Mitigate</span></span>

<span data-ttu-id="5f420-150">Als het probleem Hallo nu zich voordoet, klikt u op **analyseren** > **Diagnostics** > **onderzoeken nu** toocreate een diagnostische sessie voor u verzamelt die HTTP zich aanmeldt, Logboeken, geheugen dumpbestanden, PHP-foutenlogboek en PHP-proces rapport.</span><span class="sxs-lookup"><span data-stu-id="5f420-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="5f420-151">Zodra het Hallo-gegevens worden verzameld, wordt ook een analyse uitgevoerd op Hallo gegevens en bieden u een HTML-rapport.</span><span class="sxs-lookup"><span data-stu-id="5f420-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="5f420-152">Als u wilt dat toodownload Hallo gegevens, standaard, zou dit worden opgeslagen in Hallo D:\home\data\DaaS map.</span><span class="sxs-lookup"><span data-stu-id="5f420-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="5f420-153">Zie voor meer informatie over de ondersteuning van Azure App Service-portal Hallo [nieuwe Updates tooSupport Site-uitbreiding voor Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="5f420-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="5f420-154">Hallo Kudu-Console voor foutopsporing gebruiken</span><span class="sxs-lookup"><span data-stu-id="5f420-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="5f420-155">Web-Apps wordt geleverd met een Foutopsporingsconsole die u gebruiken kunt voor foutopsporing, verkennen, het uploaden van bestanden, evenals de JSON-eindpunten voor het ophalen van informatie over uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="5f420-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="5f420-156">Dit wordt genoemd, Hallo *Kudu-Console* of Hallo *SCM Dashboard* voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="5f420-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="5f420-157">U kunt toegang krijgen tot dit dashboard toohello koppeling gaat **https://&lt;uw app-naam >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="5f420-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="5f420-158">Enkele van de Kudu verschaft Hallo zaken zijn:</span><span class="sxs-lookup"><span data-stu-id="5f420-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="5f420-159">omgevingsinstellingen voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="5f420-159">environment settings for your application</span></span>
* <span data-ttu-id="5f420-160">logboekstream</span><span class="sxs-lookup"><span data-stu-id="5f420-160">log stream</span></span>
* <span data-ttu-id="5f420-161">diagnostische dump</span><span class="sxs-lookup"><span data-stu-id="5f420-161">diagnostic dump</span></span>
* <span data-ttu-id="5f420-162">fouten opsporen console waarin u Powershell-cmdlets en basic DOS-opdrachten kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5f420-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="5f420-163">Een andere handige functie van Kudu is dat, als uw toepassing die eerste kans uitzonderingen, kunt u Kudu en Hallo SysInternals-hulpprogramma Procdump toocreate geheugendumps.</span><span class="sxs-lookup"><span data-stu-id="5f420-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="5f420-164">Deze geheugendumps momentopnamen van het Hallo-proces en vaak kunt u meer gecompliceerde problemen oplossen met uw web-app.</span><span class="sxs-lookup"><span data-stu-id="5f420-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="5f420-165">Zie voor meer informatie over functies die beschikbaar zijn in Kudu [Azure Websites on line hulpmiddelen die u moet weten over](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="5f420-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="5f420-166">3. Hallo probleem verhelpen</span><span class="sxs-lookup"><span data-stu-id="5f420-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="5f420-167">Schaal Hallo web-app</span><span class="sxs-lookup"><span data-stu-id="5f420-167">Scale hello web app</span></span>
<span data-ttu-id="5f420-168">In Azure App Service kunt voor betere prestaties en doorvoer, u aanpassen Hallo schaal waarmee u uw toepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="5f420-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="5f420-169">Schalen van een web-app omvat twee gerelateerde acties: uw App Service plan tooa hogere prijscategorie en bepaalde instellingen configureren nadat u hebt gekozen toohello hoger prijscategorie te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5f420-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="5f420-170">Zie voor meer informatie over het schalen [schalen van een web-app in Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="5f420-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="5f420-171">U kunt bovendien kiezen toorun uw toepassing op meer dan één exemplaar.</span><span class="sxs-lookup"><span data-stu-id="5f420-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="5f420-172">Dit niet alleen biedt u meer mogelijkheden voor verwerking, maar biedt u eveneens bepaalde hoeveelheid fouttolerantie.</span><span class="sxs-lookup"><span data-stu-id="5f420-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="5f420-173">Als hello proces uitgeschakeld op één exemplaar wordt, blijven hello andere exemplaar nog steeds voldoen aan aanvragen.</span><span class="sxs-lookup"><span data-stu-id="5f420-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="5f420-174">U kunt Hallo toobe handmatig of automatisch schalen instellen.</span><span class="sxs-lookup"><span data-stu-id="5f420-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="5f420-175">Gebruik AutoHeal</span><span class="sxs-lookup"><span data-stu-id="5f420-175">Use AutoHeal</span></span>
<span data-ttu-id="5f420-176">AutoHeal wordt gerecycled werkproces Hallo voor uw app op basis van de instellingen die u kiest (zoals wijzigingen in de configuratie, aanvragen, op basis van geheugen limieten of Hallo tijd nodig tooexecute een aanvraag).</span><span class="sxs-lookup"><span data-stu-id="5f420-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="5f420-177">Meestal Hallo is recyclen Hallo proces Hallo snelste manier toorecover van een probleem.</span><span class="sxs-lookup"><span data-stu-id="5f420-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="5f420-178">Hoewel u altijd opnieuw Hallo web-app uit rechtstreeks in Azure Portal hello opstarten kunt, wordt AutoHeal het automatisch voor u doen.</span><span class="sxs-lookup"><span data-stu-id="5f420-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="5f420-179">Toodo hoeft u sommige triggers in Hallo root web.config voor uw web-app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5f420-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="5f420-180">Opmerking dat deze instellingen zijn werk gaat in Hallo dezelfde manier zelfs als uw toepassing niet een .net een is.</span><span class="sxs-lookup"><span data-stu-id="5f420-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="5f420-181">Zie voor meer informatie [Azure websites automatisch herstel](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="5f420-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="5f420-182">Hallo-web-app starten</span><span class="sxs-lookup"><span data-stu-id="5f420-182">Restart hello web app</span></span>
<span data-ttu-id="5f420-183">Dit is vaak het eenvoudigste manier toorecover Hallo eenmalige problemen.</span><span class="sxs-lookup"><span data-stu-id="5f420-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="5f420-184">Op Hallo [Azure Portal](https://portal.azure.com/), op de blade van uw web-app en u hebt Hallo opties toostop of opnieuw opstarten van uw app.</span><span class="sxs-lookup"><span data-stu-id="5f420-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![opnieuw opstarten app toosolve HTTP-fouten van 502 Slechte gateway en 503 service niet beschikbaar](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="5f420-186">U kunt ook uw web-app met Azure Powershell beheren.</span><span class="sxs-lookup"><span data-stu-id="5f420-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="5f420-187">Zie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5f420-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

