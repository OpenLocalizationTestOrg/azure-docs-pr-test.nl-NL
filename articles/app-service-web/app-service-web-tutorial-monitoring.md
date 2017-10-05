---
title: Een Web-App bewaken | Microsoft Docs
description: Meer informatie over het instellen van de controle op uw Web-App
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="434ff-103">App Service bewaken</span><span class="sxs-lookup"><span data-stu-id="434ff-103">Monitor App Service</span></span>
<span data-ttu-id="434ff-104">Deze zelfstudie wordt u via uw app voor bewaking en oplossen van problemen wanneer ze zich voordoen met behulp van de ingebouwde platformhulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="434ff-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="434ff-105">Elke sectie van dit document gaat over een specifieke functie.</span><span class="sxs-lookup"><span data-stu-id="434ff-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="434ff-106">Samen met behulp van de functies, kunt u:</span><span class="sxs-lookup"><span data-stu-id="434ff-106">Using the features together let you:</span></span>
- <span data-ttu-id="434ff-107">Identificeren van een probleem in uw app.</span><span class="sxs-lookup"><span data-stu-id="434ff-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="434ff-108">Bepalen wanneer het probleem wordt veroorzaakt door uw code of het platform.</span><span class="sxs-lookup"><span data-stu-id="434ff-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="434ff-109">Verfijn de bron van het probleem in uw code.</span><span class="sxs-lookup"><span data-stu-id="434ff-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="434ff-110">Foutopsporing en verhelpen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="434ff-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="434ff-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="434ff-111">Before you begin</span></span>
- <span data-ttu-id="434ff-112">U moet een Web-App om te controleren en volg de stappen beschreven.</span><span class="sxs-lookup"><span data-stu-id="434ff-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="434ff-113">Kunt u een toepassing die de stappen in de [een ASP.NET-app maken in Azure met SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="434ff-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="434ff-114">Als u wilt uitproberen **foutopsporing op afstand** van uw toepassing, moet u Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="434ff-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="434ff-115">Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken de gratis [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="434ff-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="434ff-116">Zorg ervoor dat u **Azure-ontwikkeling** inschakelt tijdens de installatie van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="434ff-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="434ff-117"><a name="metrics"></a>Stap 1 - metrische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="434ff-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="434ff-118">**Metrische gegevens** zijn handig om te begrijpen:</span><span class="sxs-lookup"><span data-stu-id="434ff-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="434ff-119">Toepassingsstatus</span><span class="sxs-lookup"><span data-stu-id="434ff-119">Application health</span></span>
- <span data-ttu-id="434ff-120">Appprestaties</span><span class="sxs-lookup"><span data-stu-id="434ff-120">App performance</span></span>
- <span data-ttu-id="434ff-121">Resourceverbruik</span><span class="sxs-lookup"><span data-stu-id="434ff-121">Resource consumption</span></span>

<span data-ttu-id="434ff-122">Bij het onderzoeken van een toepassingsprobleem is metrische gegevens controleren een goede plaats om te starten.</span><span class="sxs-lookup"><span data-stu-id="434ff-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="434ff-123">Azure-portal is een snelle manier om visueel controleren en de metrische gegevens van uw app met **Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="434ff-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="434ff-124">Metrische gegevens bestaan uit een historisch overzicht over diverse belangrijke aggregaties voor uw app.</span><span class="sxs-lookup"><span data-stu-id="434ff-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="434ff-125">Voor elke app die wordt gehost in app service, moet u zowel de Web-App en de App Service-abonnement controleren.</span><span class="sxs-lookup"><span data-stu-id="434ff-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="434ff-126">Een App Service-plan bestaat uit een verzameling van fysieke resources die worden gebruikt voor het hosten van uw apps.</span><span class="sxs-lookup"><span data-stu-id="434ff-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="434ff-127">Alle toepassingen die zijn toegewezen aan een App Service-plan, delen de gedefinieerde resources, zodat u kosten kunt besparen als u meerdere apps host.</span><span class="sxs-lookup"><span data-stu-id="434ff-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="434ff-128">In App Service-plannen wordt het volgende gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="434ff-128">App Service plans define:</span></span>
> * <span data-ttu-id="434ff-129">Regio: Noord-Europa, VS-Oost, Zuidoost-Azië, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="434ff-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="434ff-130">Exemplaargrootte: Klein, normaal, groot, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="434ff-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="434ff-131">Aantal van de schaal: een, twee of drie exemplaren, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="434ff-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="434ff-132">SKU: Vrij gedeeld, Basic, Standard, Premium, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="434ff-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="434ff-133">Als u wilt controleren metrische gegevens voor uw Web-App, gaat u naar de **overzicht** blade van de app die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="434ff-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="434ff-134">Hier vindt u een grafiek voor metrische gegevens van uw app als een **bewaking tegel**.</span><span class="sxs-lookup"><span data-stu-id="434ff-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="434ff-135">Klik op de tegel om te bewerken en configureren welke metrische gegevens weergeven en het tijdsbereik om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="434ff-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="434ff-136">De resourceblade biedt standaard een weergave voor de toepassingsaanvragen en fouten voor het afgelopen uur.</span><span class="sxs-lookup"><span data-stu-id="434ff-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="434ff-137">![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="434ff-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="434ff-138">Zoals u in het voorbeeld zien kunt, hebben we een toepassing die veel genereert **HTTP-Server-fouten**.</span><span class="sxs-lookup"><span data-stu-id="434ff-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="434ff-139">Het grote aantal fouten is de eerste vermelding moet voor het onderzoeken van deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="434ff-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="434ff-140">Meer informatie over Azure-Monitor met de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="434ff-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="434ff-141">Aan de slag met Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="434ff-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="434ff-142">Azure metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="434ff-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="434ff-143">Ondersteunde metrische gegevens met Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="434ff-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="434ff-144">Azure Dashboards</span><span class="sxs-lookup"><span data-stu-id="434ff-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="434ff-145"><a name="alerts"></a>Stap 2: waarschuwingen configureren</span><span class="sxs-lookup"><span data-stu-id="434ff-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="434ff-146">**Waarschuwingen** kunnen worden geconfigureerd als reactie op bepaalde voorwaarden voor uw app.</span><span class="sxs-lookup"><span data-stu-id="434ff-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="434ff-147">In [stap 1 - metrische gegevens weergeven](#metrics), hebt gezien dat de toepassing een groot aantal fouten heeft.</span><span class="sxs-lookup"><span data-stu-id="434ff-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="434ff-148">U kunt configureren een waarschuwing automatisch Blijf op de hoogte wanneer er fouten optreden.</span><span class="sxs-lookup"><span data-stu-id="434ff-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="434ff-149">In dit geval willen we de waarschuwing te verzenden en e-telkens wanneer het aantal HTTP-50 X fouten over een bepaalde drempelwaarde komt gaat.</span><span class="sxs-lookup"><span data-stu-id="434ff-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="434ff-150">Voor het maken van een waarschuwing, gaat u naar **bewaking** > **waarschuwingen** en klik op **[+] Waarschuwing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="434ff-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Waarschuwingen](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="434ff-152">Geef waarden op voor de configuratie van de waarschuwing:</span><span class="sxs-lookup"><span data-stu-id="434ff-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="434ff-153">**Bron:** de site om te bewaken die de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="434ff-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="434ff-154">**Naam:** een naam voor de waarschuwing, in dit geval: *hoge HTTP 50 X*.</span><span class="sxs-lookup"><span data-stu-id="434ff-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="434ff-155">**Beschrijving:** tekst zonder opmaak uitleg van wat deze waarschuwing kijken is.</span><span class="sxs-lookup"><span data-stu-id="434ff-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="434ff-156">**Waarschuwen bij:** waarschuwingen kunnen raadplegen metrische gegevens of gebeurtenissen, in dit voorbeeld wordt de metrische gegevens kijken.</span><span class="sxs-lookup"><span data-stu-id="434ff-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="434ff-157">**Metrische gegevens:** welke metriek te bewaken, in dit geval: *HTTP-Server-fouten*.</span><span class="sxs-lookup"><span data-stu-id="434ff-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="434ff-158">**Voorwaarde:** wanneer op waarschuwing, in dit geval selecteert de *groter is dan* optie.</span><span class="sxs-lookup"><span data-stu-id="434ff-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="434ff-159">**Drempelwaarde:** wat is de waarde te zoeken, in dit geval: *400*.</span><span class="sxs-lookup"><span data-stu-id="434ff-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="434ff-160">**Periode:** waarschuwingen bepalen het verloop van de gemiddelde waarde van een metriek.</span><span class="sxs-lookup"><span data-stu-id="434ff-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="434ff-161">Kleinere perioden yield gevoeliger waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="434ff-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="434ff-162">in dit geval we kijkt *5 minuten*.</span><span class="sxs-lookup"><span data-stu-id="434ff-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="434ff-163">**E-eigenaars en bijdragers:** in dit geval: *ingeschakeld*.</span><span class="sxs-lookup"><span data-stu-id="434ff-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="434ff-164">Nu dat de waarschuwing is gemaakt wordt een e-mail verzonden telkens wanneer de app via de geconfigureerde drempelwaarde wordt.</span><span class="sxs-lookup"><span data-stu-id="434ff-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="434ff-165">Actieve waarschuwingen kunnen ook worden gecontroleerd in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="434ff-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![Geactiveerde waarschuwingen](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="434ff-167">Meer informatie over Azure-waarschuwingen met de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="434ff-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="434ff-168">Wat zijn de waarschuwingen in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="434ff-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="434ff-169">Metrische gegevens van actie ondernemen</span><span class="sxs-lookup"><span data-stu-id="434ff-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="434ff-170">Metrische waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="434ff-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="434ff-171"><a name="companion"></a>Stap 3 - Companion-App Service</span><span class="sxs-lookup"><span data-stu-id="434ff-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="434ff-172">**App Service companion** biedt een handige manier om het bewaken van uw app met een systeemeigen ervaring in uw mobiele apparaat (iOS of Android).</span><span class="sxs-lookup"><span data-stu-id="434ff-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="434ff-173">App Service-Companion te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="434ff-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="434ff-174">Toepassing metrische gegevens controleren</span><span class="sxs-lookup"><span data-stu-id="434ff-174">Review application metrics</span></span>
- <span data-ttu-id="434ff-175">Bekijken en reageren op waarschuwingen toepassingsfouten en aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="434ff-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="434ff-176">Oplossen (bladeren, starten, stoppen, start de app opnieuw)</span><span class="sxs-lookup"><span data-stu-id="434ff-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="434ff-177">Pushmeldingen voor kritieke gebeurtenissen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="434ff-177">Get push notifications for critical events.</span></span>

![Companion-App Service](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="434ff-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Companion Google Play-App Service](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="434ff-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="434ff-180">U kunt aanvullende van App Service installeren de [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) of [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="434ff-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="434ff-181"><a name="diagnose"></a>Stap 4: diagnosticeren en oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="434ff-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="434ff-182">**Diagnosticeren en oplossen van problemen met** helpt u problemen met toepassingen verschillende vormen problemen met het platform.</span><span class="sxs-lookup"><span data-stu-id="434ff-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="434ff-183">Het kan ook mogelijke oplossingen voor uw Web-App op in orde voorstellen.</span><span class="sxs-lookup"><span data-stu-id="434ff-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![Diagnosticeren en oplossen van problemen](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="434ff-185">U doorgaat met de vorige stappen van voorbeeld formulier, ziet u dat de toepassing heeft zijn er wanneer problemen.</span><span class="sxs-lookup"><span data-stu-id="434ff-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="434ff-186">Daarentegen is dat de Platformbeschikbaarheid niet heeft verplaatst van 100%.</span><span class="sxs-lookup"><span data-stu-id="434ff-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="434ff-187">Bij de app is een probleem en de blijft platform up, is een duidelijke aanwijzing dat we zijn een toepassingsprobleem betreft.</span><span class="sxs-lookup"><span data-stu-id="434ff-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="434ff-188"><a name="logging"></a>Stap 5 - logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="434ff-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="434ff-189">Nu dat we hebben de fouten voor een toepassingsprobleem domeinpartitie, kunnen we de toepassing en de server-logboeken voor meer informatie bekijken.</span><span class="sxs-lookup"><span data-stu-id="434ff-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="434ff-190">Logboekregistratie kunt u beide verzamelen **Application Diagnostics** en **Web Server Diagnostische** logboeken voor uw Web-App.</span><span class="sxs-lookup"><span data-stu-id="434ff-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="434ff-191">Application Diagnostics</span><span class="sxs-lookup"><span data-stu-id="434ff-191">Application Diagnostics</span></span>
<span data-ttu-id="434ff-192">Application diagnostics kunt u vastleggen van traces geproduceerd door de toepassing tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="434ff-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="434ff-193">Toe te voegen aanzienlijk tracering voor uw toepassing verbetert de mogelijkheid opsporen en speldenpunt problemen.</span><span class="sxs-lookup"><span data-stu-id="434ff-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="434ff-194">In ASP.NET, kunt u zich aanmelden met behulp van toepassingstraceringen [System.Diagnostics.Trace klasse](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) voor het genereren van gebeurtenissen die door de infrastructuur van het logboek worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="434ff-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="434ff-195">U kunt ook de ernst van de tracering voor het filteren van eenvoudiger opgeven.</span><span class="sxs-lookup"><span data-stu-id="434ff-195">You can also specify the severity of the trace for easier filtering.</span></span>

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
<span data-ttu-id="434ff-196">Schakel toepassingslogboeken in Ga naar de **bewaking** > **diagnostische logboeken** en toepassing logboekregistratie inschakelen met behulp van de in-of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="434ff-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="434ff-198">Toepassingslogboeken worden opgeslagen in uw Web-App-bestandssysteem of naar de blob storage wordt gepusht.</span><span class="sxs-lookup"><span data-stu-id="434ff-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="434ff-199">Het is raadzaam voor productiescenario's blob storage gebruiken.</span><span class="sxs-lookup"><span data-stu-id="434ff-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="434ff-200">Logboekregistratie inschakelen, heeft een invloed op de prestatie- en gebruik van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="434ff-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="434ff-201">Foutenlogboeken worden aanbevolen voor productiescenario's.</span><span class="sxs-lookup"><span data-stu-id="434ff-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="434ff-202">Alleen meer uitgebreide logboekregistratie inschakelen bij het onderzoeken van problemen.</span><span class="sxs-lookup"><span data-stu-id="434ff-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="434ff-203">Web Server Diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="434ff-203">Web Server Diagnostics</span></span>
<span data-ttu-id="434ff-204">Webserverlogboeken zijn gegenereerd, zelfs als uw app is niet geïnstrumenteerd.</span><span class="sxs-lookup"><span data-stu-id="434ff-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="434ff-205">App Service kunt drie soorten server-logboeken verzamelen:</span><span class="sxs-lookup"><span data-stu-id="434ff-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="434ff-206">**Web Server-logboekregistratie**</span><span class="sxs-lookup"><span data-stu-id="434ff-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="434ff-207">Informatie over HTTP transacties met behulp van de [uitgebreide W3C-logboekbestandsindeling](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="434ff-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="434ff-208">Dit is handig bij het bepalen van de algemene site metrische gegevens zoals het aantal aanvragen dat is verwerkt of hoeveel aanvragen van een specifiek IP-adres.</span><span class="sxs-lookup"><span data-stu-id="434ff-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="434ff-209">**Gedetailleerde fouten vastleggen**</span><span class="sxs-lookup"><span data-stu-id="434ff-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="434ff-210">Gedetailleerde informatie over de fout voor HTTP-statuscodes die wijzen op mislukte (statuscode 400 of hoger).</span><span class="sxs-lookup"><span data-stu-id="434ff-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="434ff-211">Meer informatie over logboekregistratie van gedetailleerde fout</span><span class="sxs-lookup"><span data-stu-id="434ff-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="434ff-212">**Tracering van mislukte aanvragen**</span><span class="sxs-lookup"><span data-stu-id="434ff-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="434ff-213">Gedetailleerde informatie over mislukte verzoeken, met inbegrip van een tracering van de IIS-onderdelen gebruikt voor het verwerken van de aanvraag en de tijd die in elk onderdeel.</span><span class="sxs-lookup"><span data-stu-id="434ff-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="434ff-214">Mislukte aanvragen logboeken handig zijn wanneer u probeert te isoleren wat wordt veroorzaakt door een specifieke HTTP-fout.</span><span class="sxs-lookup"><span data-stu-id="434ff-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="434ff-215">Meer informatie over de tracering van mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="434ff-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="434ff-216">Server-logboekregistratie inschakelen:</span><span class="sxs-lookup"><span data-stu-id="434ff-216">To enable Server logging:</span></span>
- <span data-ttu-id="434ff-217">Ga naar **bewaking** > **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="434ff-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="434ff-218">Schakel de verschillende soorten Web Server Diagnostische gegevens met behulp van de in-of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="434ff-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![App controleren](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="434ff-220">Logboekregistratie inschakelen, heeft een invloed op de prestatie- en gebruik van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="434ff-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="434ff-221">Voor productiescenario's worden foutenlogboeken aanbevolen, wordt alleen inschakelen uitgebreide logboekregistratie bij het onderzoeken van problemen.</span><span class="sxs-lookup"><span data-stu-id="434ff-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="434ff-222">Toegang tot logboeken</span><span class="sxs-lookup"><span data-stu-id="434ff-222">Accessing Logs</span></span>
<span data-ttu-id="434ff-223">Logboeken die zijn opgeslagen in blob storage worden geopend met behulp van Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="434ff-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="434ff-224">Logboeken die zijn opgeslagen in de Web-App bestandssysteem toegankelijk zijn via FTP onder de volgende paden:</span><span class="sxs-lookup"><span data-stu-id="434ff-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="434ff-225">**Toepassingslogboeken** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="434ff-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="434ff-226">Deze map bevat een of meer tekstbestanden met informatie die wordt geproduceerd door logboekregistratie van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="434ff-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="434ff-227">**Kan aanvraag traceringen** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="434ff-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="434ff-228">Deze map bevat een XSL-bestand en een of meer XML-bestanden.</span><span class="sxs-lookup"><span data-stu-id="434ff-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="434ff-229">**Gedetailleerde foutenlogboeken** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="434ff-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="434ff-230">Deze map bevat een of meer htm-bestanden met uitgebreide informatie over HTTP-fouten die zijn gegenereerd door uw app.</span><span class="sxs-lookup"><span data-stu-id="434ff-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="434ff-231">**Web Server-logboeken** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="434ff-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="434ff-232">Deze map bevat een of meer tekstbestanden die zijn geformatteerd met de indeling van het W3C-uitgebreide logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="434ff-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="434ff-233"><a name="streaming"></a>Stap 6 - Streaming-logboek</span><span class="sxs-lookup"><span data-stu-id="434ff-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="434ff-234">Streaminglogboeken zijn handig als u fouten opspoort van een toepassing omdat bespaart u tijd vergeleken met [toegang tot de logboeken](#Accessing-Logs) via FTP.</span><span class="sxs-lookup"><span data-stu-id="434ff-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="434ff-235">App Service kan worden gestreamd **toepassingslogboeken** en **Webserverlogboeken** nadat ze zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="434ff-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="434ff-236">Voordat u probeert te streamen van Logboeken, controleert u of u het verzamelen van Logboeken hebt ingeschakeld zoals beschreven in de [logboekregistratie](#logging) sectie.</span><span class="sxs-lookup"><span data-stu-id="434ff-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="434ff-237">Om te streamen van Logboeken, gaat u naar **bewaking**> **Logboekstream**.</span><span class="sxs-lookup"><span data-stu-id="434ff-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="434ff-238">Selecteer **toepassingslogboeken** of **Web server-logboeken** afhankelijk van welke informatie u zoekt.</span><span class="sxs-lookup"><span data-stu-id="434ff-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="434ff-239">Hier kunt u ook onderbreken, opnieuw opstarten en wissen van de buffer.</span><span class="sxs-lookup"><span data-stu-id="434ff-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![Streaminglogboeken](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="434ff-241">Logboeken worden alleen gemaakt wanneer er verkeer op de app, kunt u ook de uitgebreidheid van Logboeken meer gebeurtenissen of gegevens ophalen verhogen.</span><span class="sxs-lookup"><span data-stu-id="434ff-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="434ff-242"><a name="remote"></a>Stap 7 - foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="434ff-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="434ff-243">Zodra u pincode-in het vervolgmenu van de bron van de problemen met toepassingen, gebruikt u **foutopsporing op afstand** stapsgewijs door de code.</span><span class="sxs-lookup"><span data-stu-id="434ff-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="434ff-244">Externe foutopsporing kunt u een foutopsporingsprogramma koppelen aan uw Web-App uitgevoerd in de cloud.</span><span class="sxs-lookup"><span data-stu-id="434ff-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="434ff-245">U kunt onderbrekingspunten instellen, geheugen rechtstreeks te manipuleren, analyseer code en zelfs de codepad wijzigen, net zoals u zou doen voor een app die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="434ff-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="434ff-246">Het foutopsporingsprogramma koppelen aan uw app uitgevoerd in de cloud:</span><span class="sxs-lookup"><span data-stu-id="434ff-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="434ff-247">Visual Studio 2017, opent u de oplossing voor de app die u wilt opsporen</span><span class="sxs-lookup"><span data-stu-id="434ff-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="434ff-248">Enkele punten bedient net zoals u zou voor lokale ontwikkeling doen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="434ff-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="434ff-249">Open **cloud explorer** (ctr + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="434ff-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="434ff-250">Aanmelden met uw azure-referenties indien nodig.</span><span class="sxs-lookup"><span data-stu-id="434ff-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="434ff-251">De app die u wilt voor foutopsporing te zoeken</span><span class="sxs-lookup"><span data-stu-id="434ff-251">Find the app you want to debug</span></span>
- <span data-ttu-id="434ff-252">Selecteer **foutopsporingsprogramma koppelen** formulier de **acties** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="434ff-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![Foutopsporing op afstand](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="434ff-254">Visual Studio, configureert u uw toepassing voor foutopsporing op afstand en opent een browservenster dat naar uw app navigeren.</span><span class="sxs-lookup"><span data-stu-id="434ff-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="434ff-255">Blader door uw app voor het activeren van onderbreking en doorloop de code.</span><span class="sxs-lookup"><span data-stu-id="434ff-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="434ff-256">Uitgevoerd in de foutopsporingsmodus in productie wordt niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="434ff-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="434ff-257">Als uw productie-app niet naar meerdere exemplaren van server is uitgebreid, foutopsporing te voorkomen dat de webserver reageert op andere aanvragen.</span><span class="sxs-lookup"><span data-stu-id="434ff-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="434ff-258">Voor de productieproblemen wilt oplossen, is het de beste bron te [logboekregistratie configureren](#logging) en [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="434ff-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="434ff-259"><a name="explorer"></a>Stap 8 - Procesverkenner</span><span class="sxs-lookup"><span data-stu-id="434ff-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="434ff-260">Wanneer uw toepassing wordt uitgebreid naar meer dan één exemplaar **procesverkenner** kunt u exemplaar specifieke problemen te identificeren.</span><span class="sxs-lookup"><span data-stu-id="434ff-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="434ff-261">Gebruik **Explorer verwerken** naar:</span><span class="sxs-lookup"><span data-stu-id="434ff-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="434ff-262">Alle processen opsommen over verschillende exemplaren van uw App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="434ff-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="434ff-263">Inzoomen en weergeven van de ingangen en de modules die zijn gekoppeld aan elk proces.</span><span class="sxs-lookup"><span data-stu-id="434ff-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="434ff-264">CPU, werkset, weergeven en threads op het procesniveau van het om te identificeren voor overmatig processen</span><span class="sxs-lookup"><span data-stu-id="434ff-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="434ff-265">Geopende bestandsingangen vinden en zelfs voor afsluiten van een specifiek proces-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="434ff-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="434ff-266">Proces Explorer kunt u vinden onder **bewaking** > **Procesverkenner**.</span><span class="sxs-lookup"><span data-stu-id="434ff-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Procesverkenner](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="434ff-268"><a name="insights"></a>Stap 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="434ff-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="434ff-269">**Application Insights** toepassingen en geavanceerde mogelijkheden voor bewaking biedt voor uw app.</span><span class="sxs-lookup"><span data-stu-id="434ff-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="434ff-270">Application Insights gebruiken om te detecteren en onderzoeken van uitzonderingen en prestatieproblemen in uw Web-App.</span><span class="sxs-lookup"><span data-stu-id="434ff-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="434ff-271">U kunt Application Insights inschakelen voor uw Web-App onder **bewaking** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="434ff-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="434ff-272">Application Insights vragen u voor het installeren van de extensie Application Insights site om te beginnen met het verzamelen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="434ff-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="434ff-273">Installeren van de site-extensie zorgt ervoor dat een toepassing opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="434ff-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="434ff-275">Application Insights is een geavanceerde functie instellen, volgt u de opgenomen in koppelingen voor meer informatie de [Vervolgstappen](#next) sectie.</span><span class="sxs-lookup"><span data-stu-id="434ff-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="434ff-276"><a name="next"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="434ff-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="434ff-277">Wat is Application Insights</span><span class="sxs-lookup"><span data-stu-id="434ff-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="434ff-278">Bewaking van prestaties van de Azure-web-app met Application Insights</span><span class="sxs-lookup"><span data-stu-id="434ff-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="434ff-279">Beschikbaarheid en reactiesnelheid van een website met Application Insights bewaken</span><span class="sxs-lookup"><span data-stu-id="434ff-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
