---
title: een Web-App aaaMonitor | Microsoft Docs
description: Meer informatie over hoe tooset van controle op uw Web-App
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="81b30-103">App Service bewaken</span><span class="sxs-lookup"><span data-stu-id="81b30-103">Monitor App Service</span></span>
<span data-ttu-id="81b30-104">Deze zelfstudie wordt u via uw app voor bewaking en het gebruik van Hallo ingebouwde platform extra toosolve problemen wanneer deze optreden.</span><span class="sxs-lookup"><span data-stu-id="81b30-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="81b30-105">Elke sectie van dit document gaat over een specifieke functie.</span><span class="sxs-lookup"><span data-stu-id="81b30-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="81b30-106">Hallo functies samen gebruikt, kunt u:</span><span class="sxs-lookup"><span data-stu-id="81b30-106">Using hello features together let you:</span></span>
- <span data-ttu-id="81b30-107">Identificeren van een probleem in uw app.</span><span class="sxs-lookup"><span data-stu-id="81b30-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="81b30-108">Bepalen wanneer Hallo probleem wordt veroorzaakt door uw code of het Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="81b30-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="81b30-109">Verfijn Hallo bron van Hallo probleem in uw code.</span><span class="sxs-lookup"><span data-stu-id="81b30-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="81b30-110">Foutopsporing en het verhelpen Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="81b30-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="81b30-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="81b30-111">Before you begin</span></span>
- <span data-ttu-id="81b30-112">U moet een toomonitor Web-App en Hallo volgen die worden beschreven stappen.</span><span class="sxs-lookup"><span data-stu-id="81b30-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="81b30-113">U kunt een toepassing hello stappen in Hallo maken [een ASP.NET-app maken in Azure met SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="81b30-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="81b30-114">Als u wilt dat tootry uit **foutopsporing op afstand** van uw toepassing, moet u Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81b30-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="81b30-115">Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo gratis [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="81b30-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="81b30-116">Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.</span><span class="sxs-lookup"><span data-stu-id="81b30-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="81b30-117"><a name="metrics"></a>Stap 1 - metrische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="81b30-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="81b30-118">**Metrische gegevens** zijn nuttig toounderstand:</span><span class="sxs-lookup"><span data-stu-id="81b30-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="81b30-119">Toepassingsstatus</span><span class="sxs-lookup"><span data-stu-id="81b30-119">Application health</span></span>
- <span data-ttu-id="81b30-120">Appprestaties</span><span class="sxs-lookup"><span data-stu-id="81b30-120">App performance</span></span>
- <span data-ttu-id="81b30-121">Resourceverbruik</span><span class="sxs-lookup"><span data-stu-id="81b30-121">Resource consumption</span></span>

<span data-ttu-id="81b30-122">Bij het onderzoeken van een toepassingsprobleem is metrische gegevens controleren een goede plaats toostart.</span><span class="sxs-lookup"><span data-stu-id="81b30-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="81b30-123">Azure-portal is een snelle manier toovisually inspecteren Hallo metrische gegevens van uw app met **Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="81b30-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="81b30-124">Metrische gegevens bestaan uit een historisch overzicht over diverse belangrijke aggregaties voor uw app.</span><span class="sxs-lookup"><span data-stu-id="81b30-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="81b30-125">Voor elke app die wordt gehost in app service, moet u zowel Hallo Web-App en Hallo App Service-abonnement controleren.</span><span class="sxs-lookup"><span data-stu-id="81b30-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="81b30-126">Een App Service-plan vertegenwoordigt de verzameling Hallo van fysieke resources gebruikt toohost uw apps.</span><span class="sxs-lookup"><span data-stu-id="81b30-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="81b30-127">Alle toepassingen toegewezen tooan App Service plan Hallo resources delen door deze zodat u toosave kosten bij het hosten van meerdere apps gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="81b30-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="81b30-128">In App Service-plannen wordt het volgende gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="81b30-128">App Service plans define:</span></span>
> * <span data-ttu-id="81b30-129">Regio: Noord-Europa, VS-Oost, Zuidoost-Azië, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="81b30-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="81b30-130">Exemplaargrootte: Klein, normaal, groot, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="81b30-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="81b30-131">Aantal van de schaal: een, twee of drie exemplaren, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="81b30-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="81b30-132">SKU: Vrij gedeeld, Basic, Standard, Premium, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="81b30-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="81b30-133">tooreview metrische gegevens voor uw Web-App, Ga toohello **overzicht** blade Hallo app dat u wilt dat toomonitor.</span><span class="sxs-lookup"><span data-stu-id="81b30-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="81b30-134">Hier vindt u een grafiek voor metrische gegevens van uw app als een **bewaking tegel**.</span><span class="sxs-lookup"><span data-stu-id="81b30-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="81b30-135">Klik op Hallo tegel tooedit configureren welke tooview metrische gegevens en Hallo tijd bereik toodisplay.</span><span class="sxs-lookup"><span data-stu-id="81b30-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="81b30-136">Standaard Hallo resourceblade biedt een weergave voor Hallo aanvragen en fouten voor Hallo afgelopen uur.</span><span class="sxs-lookup"><span data-stu-id="81b30-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="81b30-137">![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="81b30-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="81b30-138">Zoals u in voorbeeld hello ziet, we hebben een toepassing die veel genereert **HTTP-Server-fouten**.</span><span class="sxs-lookup"><span data-stu-id="81b30-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="81b30-139">Hallo groot aantal fouten is de eerste vermelding Hallo tooinvestigate deze toepassing moet.</span><span class="sxs-lookup"><span data-stu-id="81b30-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="81b30-140">Meer informatie over Azure-Monitor met Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="81b30-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="81b30-141">Aan de slag met Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="81b30-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="81b30-142">Azure metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="81b30-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="81b30-143">Ondersteunde metrische gegevens met Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="81b30-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="81b30-144">Azure Dashboards</span><span class="sxs-lookup"><span data-stu-id="81b30-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="81b30-145"><a name="alerts"></a>Stap 2: waarschuwingen configureren</span><span class="sxs-lookup"><span data-stu-id="81b30-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="81b30-146">**Waarschuwingen** geconfigureerde tootrigger op bepaalde voorwaarden voor uw app kunt worden.</span><span class="sxs-lookup"><span data-stu-id="81b30-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="81b30-147">In [stap 1 - metrische gegevens weergeven](#metrics), hebt gezien dat Hallo-toepassing een groot aantal fouten heeft.</span><span class="sxs-lookup"><span data-stu-id="81b30-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="81b30-148">Een waarschuwing configureren kunt tooautomatically Blijf op de hoogte wanneer er fouten optreden.</span><span class="sxs-lookup"><span data-stu-id="81b30-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="81b30-149">In dit geval we wilt Hallo waarschuwing toosend en e-telkens wanneer het aantal HTTP-50 X fouten Hallo over een bepaalde drempelwaarde komt gaat.</span><span class="sxs-lookup"><span data-stu-id="81b30-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="81b30-150">toocreate een waarschuwing, te navigeren**bewaking** > **waarschuwingen** en klik op **[+] Waarschuwing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="81b30-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Waarschuwingen](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="81b30-152">Geef waarden op voor de configuratie van de waarschuwing Hallo:</span><span class="sxs-lookup"><span data-stu-id="81b30-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="81b30-153">**Bron:** Hallo site toomonitor met Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="81b30-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="81b30-154">**Naam:** een naam voor de waarschuwing, in dit geval: *hoge HTTP 50 X*.</span><span class="sxs-lookup"><span data-stu-id="81b30-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="81b30-155">**Beschrijving:** tekst zonder opmaak uitleg van wat deze waarschuwing kijken is.</span><span class="sxs-lookup"><span data-stu-id="81b30-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="81b30-156">**Waarschuwen bij:** waarschuwingen kunnen raadplegen metrische gegevens of gebeurtenissen, in dit voorbeeld wordt de metrische gegevens kijken.</span><span class="sxs-lookup"><span data-stu-id="81b30-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="81b30-157">**Metrische gegevens:** welke metrische toomonitor, in dit geval: *HTTP-Server-fouten*.</span><span class="sxs-lookup"><span data-stu-id="81b30-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="81b30-158">**Voorwaarde:** wanneer tooalert, in dit geval selecteert Hallo *groter is dan* optie.</span><span class="sxs-lookup"><span data-stu-id="81b30-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="81b30-159">**Drempelwaarde:** wat toolook waarde, in dit geval is: *400*.</span><span class="sxs-lookup"><span data-stu-id="81b30-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="81b30-160">**Periode:** waarschuwingen bepalen het verloop Hallo gemiddelde waarde van een metriek.</span><span class="sxs-lookup"><span data-stu-id="81b30-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="81b30-161">Kleinere perioden yield gevoeliger waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="81b30-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="81b30-162">in dit geval we kijkt *5 minuten*.</span><span class="sxs-lookup"><span data-stu-id="81b30-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="81b30-163">**E-eigenaars en bijdragers:** in dit geval: *ingeschakeld*.</span><span class="sxs-lookup"><span data-stu-id="81b30-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="81b30-164">Nu dat hello waarschuwing wordt gemaakt een e-mailbericht wordt verzonden zodra hello app boven de drempelwaarde Hallo geconfigureerd gaat.</span><span class="sxs-lookup"><span data-stu-id="81b30-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="81b30-165">Actieve waarschuwingen kunnen ook worden gecontroleerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="81b30-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![Geactiveerde waarschuwingen](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="81b30-167">Meer informatie over Azure-waarschuwingen Hello koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="81b30-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="81b30-168">Wat zijn de waarschuwingen in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="81b30-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="81b30-169">Metrische gegevens van actie ondernemen</span><span class="sxs-lookup"><span data-stu-id="81b30-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="81b30-170">Metrische waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="81b30-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="81b30-171"><a name="companion"></a>Stap 3 - Companion-App Service</span><span class="sxs-lookup"><span data-stu-id="81b30-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="81b30-172">**App Service companion** biedt een handige manier toomonitor uw app met een systeemeigen ervaring in uw mobiele apparaat (iOS of Android).</span><span class="sxs-lookup"><span data-stu-id="81b30-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="81b30-173">App Service-Companion te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="81b30-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="81b30-174">Toepassing metrische gegevens controleren</span><span class="sxs-lookup"><span data-stu-id="81b30-174">Review application metrics</span></span>
- <span data-ttu-id="81b30-175">Bekijken en reageren op waarschuwingen toepassingsfouten en aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="81b30-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="81b30-176">Oplossen (bladeren, starten, stoppen, opnieuw opstarten Hallo app)</span><span class="sxs-lookup"><span data-stu-id="81b30-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="81b30-177">Pushmeldingen voor kritieke gebeurtenissen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="81b30-177">Get push notifications for critical events.</span></span>

![Companion-App Service](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="81b30-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Companion Google Play-App Service](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="81b30-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="81b30-180">U kunt aanvullende App Service installeren vanaf Hallo [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) of [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="81b30-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="81b30-181"><a name="diagnose"></a>Stap 4: diagnosticeren en oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="81b30-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="81b30-182">**Diagnosticeren en oplossen van problemen met** helpt u problemen met toepassingen verschillende vormen problemen met het platform.</span><span class="sxs-lookup"><span data-stu-id="81b30-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="81b30-183">Deze kunt mogelijke oplossingen tooget ook uw Web-App back toohealthy voorstellen.</span><span class="sxs-lookup"><span data-stu-id="81b30-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![Diagnosticeren en oplossen van problemen](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="81b30-185">Hallo voorbeeld formulier vorige stappen voortzet, ziet u dat de toepassing hello heeft zijn er wanneer problemen.</span><span class="sxs-lookup"><span data-stu-id="81b30-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="81b30-186">Hallo Platformbeschikbaarheid is daarentegen geen verplaatst van 100%.</span><span class="sxs-lookup"><span data-stu-id="81b30-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="81b30-187">Wanneer Hallo app heeft met het probleem en hello platform blijft up, is een duidelijke aanwijzing dat we zijn een toepassingsprobleem betreft.</span><span class="sxs-lookup"><span data-stu-id="81b30-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="81b30-188"><a name="logging"></a>Stap 5 - logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="81b30-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="81b30-189">Nu dat we hebben Hallo fouten tooan toepassingsprobleem domeinpartitie, kunnen we kijken Hallo toepassings- en logboeken tooget meer informatie.</span><span class="sxs-lookup"><span data-stu-id="81b30-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="81b30-190">Logboekregistratie kunt u beide toocollect **Application Diagnostics** en **Web Server Diagnostische** logboeken voor uw Web-App.</span><span class="sxs-lookup"><span data-stu-id="81b30-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="81b30-191">Application Diagnostics</span><span class="sxs-lookup"><span data-stu-id="81b30-191">Application Diagnostics</span></span>
<span data-ttu-id="81b30-192">Application diagnostics kunt u toocapture traceringen geproduceerd door de toepassing hello tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="81b30-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="81b30-193">Toe te voegen tracering tooyour verbetert toepassing aanzienlijk de mogelijkheid toodebug en speldenpunt problemen.</span><span class="sxs-lookup"><span data-stu-id="81b30-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="81b30-194">In ASP.NET, kunt u zich aanmelden met behulp van toepassingstraceringen [System.Diagnostics.Trace klasse](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate gebeurtenissen die worden vastgelegd door Hallo logboek-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="81b30-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="81b30-195">U kunt ook Hallo ernst van Hallo tracering voor het filteren van eenvoudiger opgeven.</span><span class="sxs-lookup"><span data-stu-id="81b30-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="81b30-196">toepassingslogboeken tooenable te gaan**bewaking** > **diagnostische logboeken** en toepassing logboekregistratie inschakelen met behulp van Hallo Schakelknoppen.</span><span class="sxs-lookup"><span data-stu-id="81b30-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="81b30-198">Toepassingslogboeken kunnen bestandssysteem opgeslagen tooyour van Web-App of tooblob opslag gepusht.</span><span class="sxs-lookup"><span data-stu-id="81b30-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="81b30-199">Voor productiescenario's is het aanbevolen toouse blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="81b30-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81b30-200">Logboekregistratie inschakelen, heeft een invloed op de prestatie- en gebruik van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="81b30-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="81b30-201">Foutenlogboeken worden aanbevolen voor productiescenario's.</span><span class="sxs-lookup"><span data-stu-id="81b30-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="81b30-202">Alleen meer uitgebreide logboekregistratie inschakelen bij het onderzoeken van problemen.</span><span class="sxs-lookup"><span data-stu-id="81b30-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="81b30-203">Web Server Diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="81b30-203">Web Server Diagnostics</span></span>
<span data-ttu-id="81b30-204">Webserverlogboeken zijn gegenereerd, zelfs als uw app is niet geïnstrumenteerd.</span><span class="sxs-lookup"><span data-stu-id="81b30-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="81b30-205">App Service kunt drie soorten server-logboeken verzamelen:</span><span class="sxs-lookup"><span data-stu-id="81b30-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="81b30-206">**Web Server-logboekregistratie**</span><span class="sxs-lookup"><span data-stu-id="81b30-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="81b30-207">Informatie over HTTP transacties met Hallo [uitgebreide W3C-logboekbestandsindeling](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b30-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="81b30-208">Dit is handig bij het bepalen van de algemene site metrische gegevens zoals het aantal aanvragen dat is verwerkt Hallo of hoeveel aanvragen van een specifiek IP-adres zijn.</span><span class="sxs-lookup"><span data-stu-id="81b30-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="81b30-209">**Gedetailleerde fouten vastleggen**</span><span class="sxs-lookup"><span data-stu-id="81b30-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="81b30-210">Gedetailleerde informatie over de fout voor HTTP-statuscodes die wijzen op mislukte (statuscode 400 of hoger).</span><span class="sxs-lookup"><span data-stu-id="81b30-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="81b30-211">Meer informatie over logboekregistratie van gedetailleerde fout</span><span class="sxs-lookup"><span data-stu-id="81b30-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="81b30-212">**Tracering van mislukte aanvragen**</span><span class="sxs-lookup"><span data-stu-id="81b30-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="81b30-213">Gedetailleerde informatie over mislukte verzoeken, met inbegrip van een tracering van Hallo IIS componenten gebruikt tooprocess Hallo-aanvraag en Hallo tijd benodigd in elk onderdeel.</span><span class="sxs-lookup"><span data-stu-id="81b30-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="81b30-214">Logboeken voor mislukte aanvragen zijn nuttig wanneer u probeert tooisolate wat de oorzaak van een specifieke HTTP-fout.</span><span class="sxs-lookup"><span data-stu-id="81b30-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="81b30-215">Meer informatie over de tracering van mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="81b30-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="81b30-216">logboekregistratie van tooenable-Server:</span><span class="sxs-lookup"><span data-stu-id="81b30-216">tooenable Server logging:</span></span>
- <span data-ttu-id="81b30-217">Ga te**bewaking** > **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="81b30-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="81b30-218">Verschillende soorten Web Server van diagnostische gegevens met Hallo Schakelknoppen Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="81b30-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="81b30-220">Logboekregistratie inschakelen, heeft een invloed op de prestatie- en gebruik van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="81b30-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="81b30-221">Voor productiescenario's worden foutenlogboeken aanbevolen, wordt alleen inschakelen uitgebreide logboekregistratie bij het onderzoeken van problemen.</span><span class="sxs-lookup"><span data-stu-id="81b30-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="81b30-222">Toegang tot logboeken</span><span class="sxs-lookup"><span data-stu-id="81b30-222">Accessing Logs</span></span>
<span data-ttu-id="81b30-223">Logboeken die zijn opgeslagen in blob storage worden geopend met behulp van Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="81b30-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="81b30-224">Logboeken die zijn opgeslagen in het bestandssysteem Hallo van Web-App toegankelijk zijn via FTP onder Hallo paden te volgen:</span><span class="sxs-lookup"><span data-stu-id="81b30-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="81b30-225">**Toepassingslogboeken** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="81b30-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="81b30-226">Deze map bevat een of meer tekstbestanden met informatie die wordt geproduceerd door logboekregistratie van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="81b30-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="81b30-227">**Kan aanvraag traceringen** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="81b30-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="81b30-228">Deze map bevat een XSL-bestand en een of meer XML-bestanden.</span><span class="sxs-lookup"><span data-stu-id="81b30-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="81b30-229">**Gedetailleerde foutenlogboeken** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="81b30-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="81b30-230">Deze map bevat een of meer htm-bestanden met uitgebreide informatie over HTTP-fouten die zijn gegenereerd door uw app.</span><span class="sxs-lookup"><span data-stu-id="81b30-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="81b30-231">**Web Server-logboeken** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="81b30-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="81b30-232">Deze map bevat een of meer tekstbestanden die zijn geformatteerd met uitgebreide Hallo W3C-logboekindeling.</span><span class="sxs-lookup"><span data-stu-id="81b30-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="81b30-233"><a name="streaming"></a>Stap 6 - Streaming-logboek</span><span class="sxs-lookup"><span data-stu-id="81b30-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="81b30-234">Streaminglogboeken zijn handig als u fouten opspoort van een toepassing omdat bespaart u tijd te vergeleken[Hallo Logboeken openen](#Accessing-Logs) via FTP.</span><span class="sxs-lookup"><span data-stu-id="81b30-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="81b30-235">App Service kan worden gestreamd **toepassingslogboeken** en **Webserverlogboeken** nadat ze zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="81b30-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="81b30-236">Voordat u zich aanmeldt toostream, zorg ervoor dat u kunt het verzamelen van Logboeken hebt ingeschakeld, zoals beschreven in Hallo [logboekregistratie](#logging) sectie.</span><span class="sxs-lookup"><span data-stu-id="81b30-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="81b30-237">toostream-logboeken te gaan**bewaking**> **Logboekstream**.</span><span class="sxs-lookup"><span data-stu-id="81b30-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="81b30-238">Selecteer **toepassingslogboeken** of **Web server-logboeken** afhankelijk van welke informatie u zoekt.</span><span class="sxs-lookup"><span data-stu-id="81b30-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="81b30-239">Hier kunt u ook onderbreken, opnieuw opstarten en Hallo buffer wissen.</span><span class="sxs-lookup"><span data-stu-id="81b30-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![Streaminglogboeken](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="81b30-241">Logboeken worden alleen gemaakt wanneer er verkeer op Hallo app, u kunt ook Hallo uitgebreidheid van Logboeken tooget vergroten meer gebeurtenissen of informatie.</span><span class="sxs-lookup"><span data-stu-id="81b30-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="81b30-242"><a name="remote"></a>Stap 7 - foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="81b30-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="81b30-243">Zodra u de pincode-waarnaar wordt verwezen Hallo bron van Hallo toepassingen problemen hebt, gebruikt **foutopsporing op afstand** toowalk via Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="81b30-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="81b30-244">Externe foutopsporing kunt u koppelt een foutopsporingsprogramma tooyour Web-App uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="81b30-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="81b30-245">U kunt onderbrekingspunten instellen, geheugen rechtstreeks te manipuleren, analyseer code en zelfs wijzigen Hallo codepad net zoals u zou doen voor een app die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="81b30-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="81b30-246">tooattach hello foutopsporingsprogramma tooyour app uitgevoerd in de cloud Hallo:</span><span class="sxs-lookup"><span data-stu-id="81b30-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="81b30-247">Met behulp van Visual Studio 2017 open Hallo-oplossing voor het Hallo-app wilt toodebug</span><span class="sxs-lookup"><span data-stu-id="81b30-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="81b30-248">Enkele punten bedient net zoals u zou voor lokale ontwikkeling doen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="81b30-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="81b30-249">Open **cloud explorer** (ctr + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="81b30-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="81b30-250">Aanmelden met uw azure-referenties indien nodig.</span><span class="sxs-lookup"><span data-stu-id="81b30-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="81b30-251">Zoeken naar Hallo app gewenste toodebug</span><span class="sxs-lookup"><span data-stu-id="81b30-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="81b30-252">Selecteer **foutopsporingsprogramma koppelen** formulier Hallo **acties** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="81b30-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![Foutopsporing op afstand](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="81b30-254">Visual Studio, configureert u uw toepassing voor foutopsporing op afstand en opent een browservenster dat tooyour app navigeert.</span><span class="sxs-lookup"><span data-stu-id="81b30-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="81b30-255">Blader door de onderbreking van uw app-tootrigger en analyseer Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="81b30-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="81b30-256">Uitgevoerd in de foutopsporingsmodus in productie wordt niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="81b30-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="81b30-257">Als uw productie-app is toomultiple server-exemplaren niet worden uitgebreid, foutopsporing Hallo-webserver niet reageert tooother aanvragen voorkomen.</span><span class="sxs-lookup"><span data-stu-id="81b30-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="81b30-258">Voor het oplossen van problemen, is de beste bron te[logboekregistratie configureren](#logging) en [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="81b30-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="81b30-259"><a name="explorer"></a>Stap 8 - Procesverkenner</span><span class="sxs-lookup"><span data-stu-id="81b30-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="81b30-260">Wanneer uw toepassing uit toomore dan één exemplaar wordt geschaald **procesverkenner** kunt u exemplaar specifieke problemen te identificeren.</span><span class="sxs-lookup"><span data-stu-id="81b30-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="81b30-261">Gebruik **Explorer verwerken** naar:</span><span class="sxs-lookup"><span data-stu-id="81b30-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="81b30-262">Het inventariseren van alle Hallo-processen tussen verschillende exemplaren van uw App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="81b30-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="81b30-263">Inzoomen en Hallo-ingangen en modules die zijn gekoppeld aan elk proces weergeven.</span><span class="sxs-lookup"><span data-stu-id="81b30-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="81b30-264">Weergave CPU, werkset en Thread aantal bij Hallo verwerken niveau toohelp u buitensporige processen identificeren</span><span class="sxs-lookup"><span data-stu-id="81b30-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="81b30-265">Geopende bestandsingangen vinden en zelfs voor afsluiten van een specifiek proces-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="81b30-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="81b30-266">Proces Explorer kunt u vinden onder **bewaking** > **Procesverkenner**.</span><span class="sxs-lookup"><span data-stu-id="81b30-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Procesverkenner](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="81b30-268"><a name="insights"></a>Stap 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="81b30-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="81b30-269">**Application Insights** toepassingen en geavanceerde mogelijkheden voor bewaking biedt voor uw app.</span><span class="sxs-lookup"><span data-stu-id="81b30-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="81b30-270">Gebruik Application Insights toodetect en onderzoeken van uitzonderingen en prestatieproblemen in uw Web-App.</span><span class="sxs-lookup"><span data-stu-id="81b30-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="81b30-271">U kunt Application Insights inschakelen voor uw Web-App onder **bewaking** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="81b30-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="81b30-272">Application Insights mogelijk wordt u gevraagd tooinstall Hallo Application Insights-site-uitbreiding toostart verzamelen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="81b30-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="81b30-273">Installeren van site-extensie Hallo zorgt ervoor dat een toepassing opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="81b30-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="81b30-275">Application Insights is een geavanceerde functie stelt toolearn meer Hallo koppelingen volgen opgenomen in Hallo [Vervolgstappen](#next) sectie.</span><span class="sxs-lookup"><span data-stu-id="81b30-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="81b30-276"><a name="next"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81b30-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="81b30-277">Wat is Application Insights</span><span class="sxs-lookup"><span data-stu-id="81b30-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="81b30-278">Bewaking van prestaties van de Azure-web-app met Application Insights</span><span class="sxs-lookup"><span data-stu-id="81b30-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="81b30-279">Beschikbaarheid en reactiesnelheid van een website met Application Insights bewaken</span><span class="sxs-lookup"><span data-stu-id="81b30-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
