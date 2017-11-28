---
title: aaaTroubleshoot Application Insights in een Java-webproject
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
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="c08f3-103">Probleemoplossing voor en antwoorden op vragen over Application Insights voor Java</span><span class="sxs-lookup"><span data-stu-id="c08f3-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="c08f3-104">Vragen of problemen met [Azure Application Insights in Java][java]?</span><span class="sxs-lookup"><span data-stu-id="c08f3-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="c08f3-105">Hier volgen enkele tips.</span><span class="sxs-lookup"><span data-stu-id="c08f3-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="c08f3-106">Fouten bouwen</span><span class="sxs-lookup"><span data-stu-id="c08f3-106">Build errors</span></span>
<span data-ttu-id="c08f3-107">**In Eclipse wanneer toe te voegen Hallo Application Insights-SDK via Maven of Gradle, wordt er validatiefouten in build of controlesom.**</span><span class="sxs-lookup"><span data-stu-id="c08f3-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="c08f3-108">Als afhankelijkheid Hallo <version> element gebruikt een patroon met jokertekens (bijvoorbeeld (Maven) `<version>[1.0,)</version>` of (Gradle) `version:'1.0.+'`), kunt u een specifieke versie te gebruiken in plaats daarvan opgeven zoals `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="c08f3-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="c08f3-109">Zie Hallo [release-opmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) voor Hallo meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="c08f3-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="c08f3-110">Er zijn geen gegevens</span><span class="sxs-lookup"><span data-stu-id="c08f3-110">No data</span></span>
<span data-ttu-id="c08f3-111">**Ik heb Application Insights is toegevoegd en Mijn app uitgevoerd, maar ik gegevens in de portal Hallo nooit hebt gezien.**</span><span class="sxs-lookup"><span data-stu-id="c08f3-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="c08f3-112">Wacht even en klik op vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="c08f3-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="c08f3-113">Hallo grafieken worden regelmatig vernieuwd, maar u kunt ook handmatig vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="c08f3-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="c08f3-114">Hallo-interval voor vernieuwen is afhankelijk van tijdsbereik Hallo van Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="c08f3-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="c08f3-115">Controleer of u een instrumentatiesleutel die is gedefinieerd in Hallo ApplicationInsights.xml-bestand (in Hallo map van de bronnen in uw project hebt)</span><span class="sxs-lookup"><span data-stu-id="c08f3-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="c08f3-116">Controleer of er geen `<DisableTelemetry>true</DisableTelemetry>` knooppunt in Hallo XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="c08f3-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="c08f3-117">In de firewall wellicht tooopen TCP-poorten 80 en 443 voor het uitgaande verkeer toodc.services.visualstudio.com. Zie Hallo [volledige lijst met uitzonderingen voor firewall](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="c08f3-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="c08f3-118">In Microsoft Azure Hallo start board, bekijkt hello status Serviceoverzicht.</span><span class="sxs-lookup"><span data-stu-id="c08f3-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="c08f3-119">Als er een waarschuwing aanwijzingen zijn, wacht u totdat ze zijn tooOK geretourneerd en vervolgens sluiten en opnieuw de blade van het Application Insights-toepassing openen.</span><span class="sxs-lookup"><span data-stu-id="c08f3-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="c08f3-120">Schakelt logboekregistratie toohello IDE-consolevenster, door toe te voegen in een `<SDKLogger />` element onder het hoofdknooppunt Hallo in Hallo ApplicationInsights.xml-bestand (in Hallo map van de bronnen in uw project) en Controleer op vermeldingen die vooraf worden gegaan door [fout].</span><span class="sxs-lookup"><span data-stu-id="c08f3-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="c08f3-121">Zorg ervoor dat Hallo juiste ApplicationInsights.xml-bestand is geladen door Hallo Java SDK, door te kijken Hallo-console-Uitvoerberichten voor een 'configuratiebestand is gevonden'-instructie.</span><span class="sxs-lookup"><span data-stu-id="c08f3-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="c08f3-122">Als het Hallo-configuratiebestand is niet gevonden, Controleer Hallo uitvoer berichten toosee waar Hallo-configuratiebestand wordt gezocht en zorg ervoor dat Hallo die applicationinsights.xml bevindt zich in een van deze zoeklocaties.</span><span class="sxs-lookup"><span data-stu-id="c08f3-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="c08f3-123">Als vuistregel, kunt u Hallo configuratiebestand plaatsen in de buurt Hallo Application Insights SDK JARs.</span><span class="sxs-lookup"><span data-stu-id="c08f3-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="c08f3-124">Bijvoorbeeld: in Tomcat, dit zou betekenen Hallo WEB-INF/lib map.</span><span class="sxs-lookup"><span data-stu-id="c08f3-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="c08f3-125">Ik toosee gegevens gebruikt, maar deze is gestopt</span><span class="sxs-lookup"><span data-stu-id="c08f3-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="c08f3-126">Controleer de Hallo [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="c08f3-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="c08f3-127">Hebt u uw maandelijkse quotum van gegevenspunten bereikt?</span><span class="sxs-lookup"><span data-stu-id="c08f3-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="c08f3-128">Open instellingen/quotum en prijzen toofind uit. Als dit het geval is, kunt u uw abonnement upgraden of betalen voor extra capaciteit.</span><span class="sxs-lookup"><span data-stu-id="c08f3-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="c08f3-129">Zie Hallo [prijzen schema](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c08f3-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="c08f3-130">Alle Hallo gegevens die ik ben verwacht wordt niet weergegeven</span><span class="sxs-lookup"><span data-stu-id="c08f3-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="c08f3-131">Open Hallo quota's en prijzen blade en controleer of [steekproeven](app-insights-sampling.md) wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c08f3-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="c08f3-132">(de verzending van 100% betekent dat steekproeven in bewerking niet.) Hallo Application Insights-service kan worden ingesteld tooaccept slechts een fractie van Hallo telemetrie van uw app binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="c08f3-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="c08f3-133">Hiermee houdt u binnen uw maandelijkse quotum telemetrie.</span><span class="sxs-lookup"><span data-stu-id="c08f3-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="c08f3-134">Geen gebruiksgegevens</span><span class="sxs-lookup"><span data-stu-id="c08f3-134">No usage data</span></span>
<span data-ttu-id="c08f3-135">**Gegevens over aanvragen en reactietijden, maar er is geen paginaweergave, browser of gebruikersgegevens weergegeven.**</span><span class="sxs-lookup"><span data-stu-id="c08f3-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="c08f3-136">U ingesteld uw app toosend telemetrie van Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="c08f3-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="c08f3-137">Nu de volgende stap te is[instellen van uw webpagina's toosend telemetrie vanuit de webbrowser Hallo][usage].</span><span class="sxs-lookup"><span data-stu-id="c08f3-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="c08f3-138">U kunt ook als de client is een app in een [telefoon of ander apparaat][platforms], voor het verzenden van telemetrie vanaf daar.</span><span class="sxs-lookup"><span data-stu-id="c08f3-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="c08f3-139">Gebruik dezelfde Hallo instrumentation sleutel tooset up telemetrie van uw client en de server.</span><span class="sxs-lookup"><span data-stu-id="c08f3-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="c08f3-140">Hallo gegevens weergegeven dezelfde Application Insights-resource Hallo en u zult kunnen toocorrelate gebeurtenissen van de client en server.</span><span class="sxs-lookup"><span data-stu-id="c08f3-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="c08f3-141">Telemetrie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="c08f3-141">Disabling telemetry</span></span>
<span data-ttu-id="c08f3-142">**Hoe kan ik telemetrie verzameling uitschakelen?**</span><span class="sxs-lookup"><span data-stu-id="c08f3-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="c08f3-143">In de code:</span><span class="sxs-lookup"><span data-stu-id="c08f3-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="c08f3-144">**Of**</span><span class="sxs-lookup"><span data-stu-id="c08f3-144">**Or**</span></span> 

<span data-ttu-id="c08f3-145">Werk ApplicationInsights.xml (in Hallo map van de bronnen in uw project).</span><span class="sxs-lookup"><span data-stu-id="c08f3-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="c08f3-146">Voeg de volgende Hallo onder Hallo hoofdknooppunt:</span><span class="sxs-lookup"><span data-stu-id="c08f3-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="c08f3-147">Hallo XML-methode gebruikt, hebt u toorestart Hallo toepassing wanneer u Hallo waarde wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c08f3-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="c08f3-148">Hallo doel wijzigen</span><span class="sxs-lookup"><span data-stu-id="c08f3-148">Changing hello target</span></span>
<span data-ttu-id="c08f3-149">**Hoe kan ik welke Azure-resource mijn project gegevens worden verzonden wijzigen?**</span><span class="sxs-lookup"><span data-stu-id="c08f3-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="c08f3-150">[Hallo-instrumentatiesleutel van de nieuwe resource Hallo ophalen.][java]</span><span class="sxs-lookup"><span data-stu-id="c08f3-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="c08f3-151">Als u Application Insights tooyour project met hello Azure Toolkit voor Eclipse hebt toegevoegd, klik met de rechtermuisknop op uw webproject, selecteer **Azure**, **Configure Application Insights**, en wijzig Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="c08f3-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="c08f3-152">Anders werken Hallo-sleutel in ApplicationInsights.xml in de map van de Hallo bronnen in uw project.</span><span class="sxs-lookup"><span data-stu-id="c08f3-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="c08f3-153">Gegevens van Hallo SDK Debug</span><span class="sxs-lookup"><span data-stu-id="c08f3-153">Debug data from hello SDK</span></span>

<span data-ttu-id="c08f3-154">**Hoe vind ik welke Hallo SDK doet?**</span><span class="sxs-lookup"><span data-stu-id="c08f3-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="c08f3-155">tooget meer informatie over wat er gebeurt in Hallo-API toevoegen `<SDKLogger/>` onder het hoofdknooppunt Hallo van Hallo ApplicationInsights.xml-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="c08f3-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="c08f3-156">U kunt ook de opdracht geven Hallo berichtenlogboek toooutput tooa bestand:</span><span class="sxs-lookup"><span data-stu-id="c08f3-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="c08f3-157">Hallo-bestanden kunnen worden gevonden in het `%temp%\javasdklogs` of `java.io.tmpdir` in geval van Tomcat-server.</span><span class="sxs-lookup"><span data-stu-id="c08f3-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="c08f3-158">Hello Azure startscherm</span><span class="sxs-lookup"><span data-stu-id="c08f3-158">hello Azure start screen</span></span>
<span data-ttu-id="c08f3-159">**Ik ben kijken [hello Azure-portal](https://portal.azure.com). Hallo-kaart zegt iets over mijn app?**</span><span class="sxs-lookup"><span data-stu-id="c08f3-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="c08f3-160">Nee, het Hallo-status van de Azure-servers bevat Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="c08f3-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="c08f3-161">*Van hello Azure start board (startscherm), hoe vind ik gegevens over mijn app?*</span><span class="sxs-lookup"><span data-stu-id="c08f3-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="c08f3-162">Ervan uitgaande dat u [stelt u de app voor Application Insights][java], klik op Bladeren, selecteer Application Insights en selecteer Hallo app bron die u voor uw app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c08f3-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="c08f3-163">tooget er sneller in de toekomst, u kunt vastmaken uw app toohello start board.</span><span class="sxs-lookup"><span data-stu-id="c08f3-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="c08f3-164">Servers van intranet</span><span class="sxs-lookup"><span data-stu-id="c08f3-164">Intranet servers</span></span>
<span data-ttu-id="c08f3-165">**Kan ik een server bewaken op mijn intranet**</span><span class="sxs-lookup"><span data-stu-id="c08f3-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="c08f3-166">Ja, mits uw server kunt verzenden telemetrie toohello Application Insights-portal via openbaar internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="c08f3-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="c08f3-167">In de firewall wellicht tooopen TCP-poorten 80 en 443 voor het uitgaande verkeer toodc.services.visualstudio.com en f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="c08f3-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="c08f3-168">Bewaartijd van gegevens</span><span class="sxs-lookup"><span data-stu-id="c08f3-168">Data retention</span></span>
<span data-ttu-id="c08f3-169">**Hoe lang gegevens bewaard in de portal Hallo? Is het veilig?**</span><span class="sxs-lookup"><span data-stu-id="c08f3-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="c08f3-170">Zie [bewaren van gegevens en privacy][data].</span><span class="sxs-lookup"><span data-stu-id="c08f3-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c08f3-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c08f3-171">Next steps</span></span>
<span data-ttu-id="c08f3-172">**Ik instellen Application Insights voor de app my server Java. Wat kan ik doen?**</span><span class="sxs-lookup"><span data-stu-id="c08f3-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="c08f3-173">[Beschikbaarheid van uw webpagina's bewaken][availability]</span><span class="sxs-lookup"><span data-stu-id="c08f3-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="c08f3-174">[Webpagina-gebruik controleren][usage]</span><span class="sxs-lookup"><span data-stu-id="c08f3-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="c08f3-175">[Gebruik bijhouden en onderzoeken van problemen in uw apps op apparaten][platforms]</span><span class="sxs-lookup"><span data-stu-id="c08f3-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="c08f3-176">[Schrijven van code tootrack informatie over het gebruik van uw app][track]</span><span class="sxs-lookup"><span data-stu-id="c08f3-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="c08f3-177">[Logboeken met diagnostische gegevens vastleggen][javalogs]</span><span class="sxs-lookup"><span data-stu-id="c08f3-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="c08f3-178">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="c08f3-178">Get help</span></span>
* [<span data-ttu-id="c08f3-179">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="c08f3-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

