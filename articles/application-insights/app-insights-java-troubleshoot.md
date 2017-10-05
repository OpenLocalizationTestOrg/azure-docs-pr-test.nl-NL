---
title: Application Insights in een Java-webproject oplossen
description: Problemen oplossen met - bewaking live Java-apps met Application Insights.
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="89e4f-103">Probleemoplossing voor en antwoorden op vragen over Application Insights voor Java</span><span class="sxs-lookup"><span data-stu-id="89e4f-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="89e4f-104">Vragen of problemen met [Azure Application Insights in Java][java]?</span><span class="sxs-lookup"><span data-stu-id="89e4f-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="89e4f-105">Hier volgen enkele tips.</span><span class="sxs-lookup"><span data-stu-id="89e4f-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="89e4f-106">Fouten bouwen</span><span class="sxs-lookup"><span data-stu-id="89e4f-106">Build errors</span></span>
<span data-ttu-id="89e4f-107">**In Eclipse bij het toevoegen van de Application Insights-SDK via Maven of Gradle, krijg ik validatiefouten in build of controlesom.**</span><span class="sxs-lookup"><span data-stu-id="89e4f-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="89e4f-108">Als de afhankelijkheid <version> element gebruikt een patroon met jokertekens (bijvoorbeeld (Maven) `<version>[1.0,)</version>` of (Gradle) `version:'1.0.+'`), kunt u een specifieke versie te gebruiken in plaats daarvan opgeven zoals `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="89e4f-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="89e4f-109">Zie de [release-opmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) voor de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="89e4f-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="89e4f-110">Er zijn geen gegevens</span><span class="sxs-lookup"><span data-stu-id="89e4f-110">No data</span></span>
<span data-ttu-id="89e4f-111">**Ik heb Application Insights is toegevoegd en Mijn app uitgevoerd, maar ik nooit gegevens in de portal hebt gezien.**</span><span class="sxs-lookup"><span data-stu-id="89e4f-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="89e4f-112">Wacht even en klik op vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="89e4f-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="89e4f-113">De grafieken worden regelmatig vernieuwd, maar u kunt ook handmatig vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="89e4f-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="89e4f-114">Het interval voor vernieuwen is afhankelijk van het tijdsbereik van de grafiek.</span><span class="sxs-lookup"><span data-stu-id="89e4f-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="89e4f-115">Controleer of u een instrumentatiesleutel die is gedefinieerd in het ApplicationInsights.xml-bestand (in de map bronnen in uw project hebt)</span><span class="sxs-lookup"><span data-stu-id="89e4f-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="89e4f-116">Controleer of er geen `<DisableTelemetry>true</DisableTelemetry>` knooppunt in het xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="89e4f-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="89e4f-117">In de firewall, moet u wellicht open TCP-poorten 80 en 443 voor uitgaand verkeer naar dc.services.visualstudio.com. Zie de [volledige lijst met uitzonderingen voor firewall](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="89e4f-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com. See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="89e4f-118">In de Microsoft Azure start board, kijkt u naar het Serviceoverzicht status.</span><span class="sxs-lookup"><span data-stu-id="89e4f-118">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="89e4f-119">Als er een waarschuwing aanwijzingen zijn, wacht u totdat ze zijn geretourneerd op OK en klik vervolgens sluiten en opnieuw de blade van het Application Insights-toepassing openen.</span><span class="sxs-lookup"><span data-stu-id="89e4f-119">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="89e4f-120">Registratie in het consolevenster IDE inschakelen door toe te voegen een `<SDKLogger />` element onder het hoofdknooppunt in het ApplicationInsights.xml-bestand (in de map bronnen in uw project) en Controleer vooraf worden gegaan door [fout] vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="89e4f-120">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="89e4f-121">Zorg ervoor dat het juiste ApplicationInsights.xml-bestand is geladen door de Java SDK en door te kijken naar berichten van de console-uitvoer voor een 'configuratiebestand is gevonden'-instructie.</span><span class="sxs-lookup"><span data-stu-id="89e4f-121">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="89e4f-122">Als het configuratiebestand niet wordt gevonden, Controleer de Uitvoerberichten zien waar het configuratiebestand wordt gezocht en zorg ervoor dat de ApplicationInsights.xml in een van deze locaties bevinden zich.</span><span class="sxs-lookup"><span data-stu-id="89e4f-122">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="89e4f-123">Als vuistregel, kunt u het configuratiebestand plaatsen in de buurt van de Application Insights SDK JARs.</span><span class="sxs-lookup"><span data-stu-id="89e4f-123">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="89e4f-124">Bijvoorbeeld: in Tomcat, zou dit betekenen dat de WEB-INF/lib-map.</span><span class="sxs-lookup"><span data-stu-id="89e4f-124">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="89e4f-125">Ik gebruikt om gegevens te bekijken, maar deze is gestopt</span><span class="sxs-lookup"><span data-stu-id="89e4f-125">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="89e4f-126">Controleer de [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="89e4f-126">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="89e4f-127">Hebt u uw maandelijkse quotum van gegevenspunten bereikt?</span><span class="sxs-lookup"><span data-stu-id="89e4f-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="89e4f-128">Open instellingen/quotum en prijzen om erachter te komen. Als dit het geval is, kunt u uw abonnement upgraden of betalen voor extra capaciteit.</span><span class="sxs-lookup"><span data-stu-id="89e4f-128">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="89e4f-129">Zie de [prijzen schema](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="89e4f-129">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="89e4f-130">Ik zie niet alle gegevens die ik ben verwacht</span><span class="sxs-lookup"><span data-stu-id="89e4f-130">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="89e4f-131">Open de quota en prijzen blade en controleer of [steekproeven](app-insights-sampling.md) wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="89e4f-131">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="89e4f-132">(de verzending van 100% betekent dat steekproeven in bewerking niet.) De Application Insights-service kan worden ingesteld op accepteert alleen een fractie van de telemetrie van uw app binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="89e4f-132">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="89e4f-133">Hiermee houdt u binnen uw maandelijkse quotum telemetrie.</span><span class="sxs-lookup"><span data-stu-id="89e4f-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="89e4f-134">Geen gebruiksgegevens</span><span class="sxs-lookup"><span data-stu-id="89e4f-134">No usage data</span></span>
<span data-ttu-id="89e4f-135">**Gegevens over aanvragen en reactietijden, maar er is geen paginaweergave, browser of gebruikersgegevens weergegeven.**</span><span class="sxs-lookup"><span data-stu-id="89e4f-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="89e4f-136">U ingesteld uw app telemetrie verzenden van de server.</span><span class="sxs-lookup"><span data-stu-id="89e4f-136">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="89e4f-137">Nu de volgende stap het is [uw webpagina's instellen voor het verzenden van telemetrie vanuit de webbrowser][usage].</span><span class="sxs-lookup"><span data-stu-id="89e4f-137">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="89e4f-138">U kunt ook als de client is een app in een [telefoon of ander apparaat][platforms], voor het verzenden van telemetrie vanaf daar.</span><span class="sxs-lookup"><span data-stu-id="89e4f-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="89e4f-139">Gebruik de dezelfde instrumentatiesleutel voor het instellen van uw client- en telemetrie.</span><span class="sxs-lookup"><span data-stu-id="89e4f-139">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="89e4f-140">De gegevens in dezelfde Application Insights-resource wordt weergegeven en kunt gebeurtenissen van client en server met elkaar correleren.</span><span class="sxs-lookup"><span data-stu-id="89e4f-140">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="89e4f-141">Telemetrie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="89e4f-141">Disabling telemetry</span></span>
<span data-ttu-id="89e4f-142">**Hoe kan ik telemetrie verzameling uitschakelen?**</span><span class="sxs-lookup"><span data-stu-id="89e4f-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="89e4f-143">In de code:</span><span class="sxs-lookup"><span data-stu-id="89e4f-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="89e4f-144">**Of**</span><span class="sxs-lookup"><span data-stu-id="89e4f-144">**Or**</span></span> 

<span data-ttu-id="89e4f-145">Werk ApplicationInsights.xml (in de map bronnen in uw project).</span><span class="sxs-lookup"><span data-stu-id="89e4f-145">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="89e4f-146">Voeg de volgende onder het hoofdknooppunt:</span><span class="sxs-lookup"><span data-stu-id="89e4f-146">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="89e4f-147">Met de XML-methode die u moet de toepassing opnieuw te starten wanneer u de waarde wijzigen.</span><span class="sxs-lookup"><span data-stu-id="89e4f-147">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="89e4f-148">Het wijzigen van het doel</span><span class="sxs-lookup"><span data-stu-id="89e4f-148">Changing the target</span></span>
<span data-ttu-id="89e4f-149">**Hoe kan ik welke Azure-resource mijn project gegevens worden verzonden wijzigen?**</span><span class="sxs-lookup"><span data-stu-id="89e4f-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="89e4f-150">[De instrumentatiesleutel van de nieuwe resource ophalen.][java]</span><span class="sxs-lookup"><span data-stu-id="89e4f-150">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="89e4f-151">Als u Application Insights hebt toegevoegd aan uw project met de Azure-Toolkit voor Eclipse, klik met de rechtermuisknop op uw webproject, selecteer **Azure**, **Configure Application Insights**, en de sleutel te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="89e4f-151">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="89e4f-152">Anders wordt de sleutel in ApplicationInsights.xml in de map bronnen in uw project wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="89e4f-152">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="89e4f-153">Gegevens uit de SDK voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="89e4f-153">Debug data from the SDK</span></span>

<span data-ttu-id="89e4f-154">**Hoe vind ik wat de SDK doet?**</span><span class="sxs-lookup"><span data-stu-id="89e4f-154">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="89e4f-155">Als u meer informatie over wat er in de API gebeurt, toevoegen `<SDKLogger/>` onder het hoofdknooppunt van het ApplicationInsights.xml-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="89e4f-155">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="89e4f-156">U kunt ook opgeven dat het logboek voor uitvoer naar een bestand:</span><span class="sxs-lookup"><span data-stu-id="89e4f-156">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="89e4f-157">De bestanden kunnen worden gevonden in het `%temp%\javasdklogs` of `java.io.tmpdir` in geval van Tomcat-server.</span><span class="sxs-lookup"><span data-stu-id="89e4f-157">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="89e4f-158">Het Azure startscherm</span><span class="sxs-lookup"><span data-stu-id="89e4f-158">The Azure start screen</span></span>
<span data-ttu-id="89e4f-159">**Ik ben kijken [de Azure-portal](https://portal.azure.com). De kaart zegt iets over mijn app?**</span><span class="sxs-lookup"><span data-stu-id="89e4f-159">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="89e4f-160">Nee, wordt de status van de Azure-servers over de hele wereld.</span><span class="sxs-lookup"><span data-stu-id="89e4f-160">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="89e4f-161">*Van de Azure start board (startscherm) hoe vind ik gegevens over mijn app?*</span><span class="sxs-lookup"><span data-stu-id="89e4f-161">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="89e4f-162">Ervan uitgaande dat u [stelt u de app voor Application Insights][java], klik op Bladeren, selecteer Application Insights en selecteer de bron van de app die u voor uw app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="89e4f-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="89e4f-163">Als u kunt er sneller in de toekomst, u vastmaken uw app op het mededelingenbord start.</span><span class="sxs-lookup"><span data-stu-id="89e4f-163">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="89e4f-164">Servers van intranet</span><span class="sxs-lookup"><span data-stu-id="89e4f-164">Intranet servers</span></span>
<span data-ttu-id="89e4f-165">**Kan ik een server bewaken op mijn intranet**</span><span class="sxs-lookup"><span data-stu-id="89e4f-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="89e4f-166">Ja, verstrekt dat uw server kunt verzenden van telemetrie naar de Application Insights-portal via het openbare internet.</span><span class="sxs-lookup"><span data-stu-id="89e4f-166">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="89e4f-167">Mogelijk moet u TCP-poorten 80 en 443 voor het uitgaande verkeer naar dc.services.visualstudio.com en f5.services.visualstudio.com openen in uw firewall.</span><span class="sxs-lookup"><span data-stu-id="89e4f-167">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="89e4f-168">Bewaartijd van gegevens</span><span class="sxs-lookup"><span data-stu-id="89e4f-168">Data retention</span></span>
<span data-ttu-id="89e4f-169">**Hoe lang gegevens bewaard in de portal? Is het veilig?**</span><span class="sxs-lookup"><span data-stu-id="89e4f-169">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="89e4f-170">Zie [bewaren van gegevens en privacy][data].</span><span class="sxs-lookup"><span data-stu-id="89e4f-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="89e4f-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="89e4f-171">Next steps</span></span>
<span data-ttu-id="89e4f-172">**Ik instellen Application Insights voor de app my server Java. Wat kan ik doen?**</span><span class="sxs-lookup"><span data-stu-id="89e4f-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="89e4f-173">[Beschikbaarheid van uw webpagina's bewaken][availability]</span><span class="sxs-lookup"><span data-stu-id="89e4f-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="89e4f-174">[Webpagina-gebruik controleren][usage]</span><span class="sxs-lookup"><span data-stu-id="89e4f-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="89e4f-175">[Gebruik bijhouden en onderzoeken van problemen in uw apps op apparaten][platforms]</span><span class="sxs-lookup"><span data-stu-id="89e4f-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="89e4f-176">[Code schrijven voor het bijhouden van gebruik van uw app][track]</span><span class="sxs-lookup"><span data-stu-id="89e4f-176">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="89e4f-177">[Logboeken met diagnostische gegevens vastleggen][javalogs]</span><span class="sxs-lookup"><span data-stu-id="89e4f-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="89e4f-178">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="89e4f-178">Get help</span></span>
* [<span data-ttu-id="89e4f-179">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="89e4f-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

