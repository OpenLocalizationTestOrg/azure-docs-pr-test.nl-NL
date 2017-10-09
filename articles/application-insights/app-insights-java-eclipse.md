---
title: aaaGet slag met Azure Application Insights met behulp van Java in Eclipse | Microsoft docs
description: Hallo Eclipse invoegtoepassing tooadd prestaties en gebruik bewaking van Java-website met Application Insights tooyour gebruiken
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="facb6-103">Aan de slag met Application Insights met behulp van Java in Eclipse</span><span class="sxs-lookup"><span data-stu-id="facb6-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="facb6-104">Hallo Application Insights-SDK verzendt telemetrie van uw Java-webtoepassing, zodat u gebruik en prestaties kan analyseren.</span><span class="sxs-lookup"><span data-stu-id="facb6-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="facb6-105">Hallo Eclipse-invoegtoepassing voor Application Insights installeert automatisch Hallo SDK in uw project, zodat u buiten Hallo vak telemetrie, plus een API waarmee u kunt aangepaste telemetrie toowrite ophalen.</span><span class="sxs-lookup"><span data-stu-id="facb6-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="facb6-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="facb6-106">Prerequisites</span></span>
<span data-ttu-id="facb6-107">Hallo-invoegtoepassing werkt momenteel voor Maven-projecten en dynamische webprojecten in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="facb6-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="facb6-108">([Application Insights toevoegen tooother typen Java-project][java].)</span><span class="sxs-lookup"><span data-stu-id="facb6-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="facb6-109">U hebt het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="facb6-109">You'll need:</span></span>

* <span data-ttu-id="facb6-110">Oracle JRE 1.6 of hoger</span><span class="sxs-lookup"><span data-stu-id="facb6-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="facb6-111">Een abonnement te[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="facb6-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="facb6-112">[Eclipse IDE voor Java EE-ontwikkelaars](http://www.eclipse.org/downloads/), Indigo of hoger.</span><span class="sxs-lookup"><span data-stu-id="facb6-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="facb6-113">Windows 7 of hoger, of WindowsServer 2008 of hoger</span><span class="sxs-lookup"><span data-stu-id="facb6-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="facb6-114">Hallo SDK installeren op Eclipse (eenmaal)</span><span class="sxs-lookup"><span data-stu-id="facb6-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="facb6-115">U hoeft alleen toodo dit één keer per computer.</span><span class="sxs-lookup"><span data-stu-id="facb6-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="facb6-116">Deze stap installeert een werkset waarmee Hallo SDK tooeach dynamisch webproject vervolgens kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="facb6-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="facb6-117">Klik op Help, nieuwe Software installeren in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="facb6-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Help, installeert u nieuwe Software](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="facb6-119">Hallo SDK wordt http://dl.microsoft.com/eclipse onder Azure Toolkit.</span><span class="sxs-lookup"><span data-stu-id="facb6-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="facb6-120">Schakel het selectievakje **Neem contact op met alle updatewebsites...**</span><span class="sxs-lookup"><span data-stu-id="facb6-120">Uncheck **Contact all update sites...**</span></span>

    ![Voor Application Insights-SDK, schakelt u contact op met bijwerken alle sites](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="facb6-122">Ga als volgt Hallo resterende stappen voor elk Java-project.</span><span class="sxs-lookup"><span data-stu-id="facb6-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="facb6-123">Een Application Insights-resource maken in Azure</span><span class="sxs-lookup"><span data-stu-id="facb6-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="facb6-124">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="facb6-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="facb6-125">Maak een nieuwe Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="facb6-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="facb6-126">Hallo toepassing type tooJava-webtoepassing instellen.</span><span class="sxs-lookup"><span data-stu-id="facb6-126">Set hello application type tooJava web application.</span></span>  

    ![Op + klikken en Application Insights kiezen](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="facb6-128">Hallo-instrumentatiesleutel van Hallo nieuwe bron vinden.</span><span class="sxs-lookup"><span data-stu-id="facb6-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="facb6-129">U moet toopaste dit in uw CodeProject binnenkort.</span><span class="sxs-lookup"><span data-stu-id="facb6-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="facb6-131">Application Insights tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="facb6-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="facb6-132">Application Insights toevoegen in het contextmenu Hallo van uw Java-webproject.</span><span class="sxs-lookup"><span data-stu-id="facb6-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="facb6-134">Plak Hallo instrumentatiesleutel die u hebt gekregen hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="facb6-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="facb6-136">Hallo sleutel samen met elk telemetrie-item is verzonden en instrueert Application Insights toodisplay in de resource.</span><span class="sxs-lookup"><span data-stu-id="facb6-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="facb6-137">Voer de toepassing hello en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="facb6-137">Run hello application and see metrics</span></span>
<span data-ttu-id="facb6-138">Voer uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="facb6-138">Run your application.</span></span>

<span data-ttu-id="facb6-139">Tooyour Application Insights-resource in Microsoft Azure retourneren.</span><span class="sxs-lookup"><span data-stu-id="facb6-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="facb6-140">HTTP-aanvragen gegevens worden weergegeven op de overzichtsblade Hallo.</span><span class="sxs-lookup"><span data-stu-id="facb6-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="facb6-141">(Als dit niet het geval is, wacht u een paar seconden en klikt u vervolgens op Vernieuwen.)</span><span class="sxs-lookup"><span data-stu-id="facb6-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="facb6-142">Reactie van server, telt het aantal aanvragen en fouten</span><span class="sxs-lookup"><span data-stu-id="facb6-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="facb6-143">Klik op via een grafiek toosee gedetailleerdere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="facb6-143">Click through any chart toosee more detailed metrics.</span></span>

![Het aantal aanvragen met de naam](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="facb6-145">[Meer informatie over metrische gegevens.][metrics]</span><span class="sxs-lookup"><span data-stu-id="facb6-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="facb6-146">En wanneer u bekijkt hello eigenschappen van een aanvraag, ziet u Hallo telemetrische gebeurtenissen gekoppeld zoals aanvragen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="facb6-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![Alle traces voor deze aanvraag](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="facb6-148">Telemetrie-clientzijde</span><span class="sxs-lookup"><span data-stu-id="facb6-148">Client-side telemetry</span></span>
<span data-ttu-id="facb6-149">Hallo Quick Start-blade, klik op Get code toomonitor mijn webpagina's:</span><span class="sxs-lookup"><span data-stu-id="facb6-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![Op de overzichtsblade van uw app, kiest u snel starten, kunt u code toomonitor mijn webpagina's.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="facb6-152">Hallo-codefragment invoegen in Hallo-head van uw HTML-bestanden.</span><span class="sxs-lookup"><span data-stu-id="facb6-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="facb6-153">Client-side '-gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="facb6-153">View client-side data</span></span>
<span data-ttu-id="facb6-154">Open uw bijgewerkte webpagina's en ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="facb6-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="facb6-155">Wacht een minuut of twee en tooApplication Insights en open Hallo gebruik blade geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="facb6-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="facb6-156">(Overzichtsblade hello, schuif naar beneden en klik op informatie over het gebruik.)</span><span class="sxs-lookup"><span data-stu-id="facb6-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="facb6-157">Pagina metrische gegevens weergeven, de gebruiker en de sessie wordt weergegeven op Hallo gebruik blade:</span><span class="sxs-lookup"><span data-stu-id="facb6-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![Sessies, gebruikers en paginaweergaven](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="facb6-159">[Meer informatie over het instellen van de client-side telemetrie.][usage]</span><span class="sxs-lookup"><span data-stu-id="facb6-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="facb6-160">Uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="facb6-160">Publish your application</span></span>
<span data-ttu-id="facb6-161">Publiceer nu uw app toohello-server, kunnen gebruikers worden gebruikt en bekijkt hello telemetrie op Hallo portal weergegeven.</span><span class="sxs-lookup"><span data-stu-id="facb6-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="facb6-162">Zorg ervoor dat uw firewall kunt uw toepassing toosend telemetrie toothese poorten:</span><span class="sxs-lookup"><span data-stu-id="facb6-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="facb6-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="facb6-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="facb6-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="facb6-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="facb6-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="facb6-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="facb6-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="facb6-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="facb6-167">Installeer op Windows-servers:</span><span class="sxs-lookup"><span data-stu-id="facb6-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="facb6-168">Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="facb6-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="facb6-169">(Hiermee kunt u prestatiemeteritems instellen.)</span><span class="sxs-lookup"><span data-stu-id="facb6-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="facb6-170">Uitzonderingen en mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="facb6-170">Exceptions and request failures</span></span>
<span data-ttu-id="facb6-171">Onverwerkte uitzonderingen worden automatisch verzameld:</span><span class="sxs-lookup"><span data-stu-id="facb6-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="facb6-172">toocollect gegevens over andere uitzonderingen, hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="facb6-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="facb6-173">[INSERT tooTrackException in uw code roept](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="facb6-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="facb6-174">[Hallo Java-Agent installeren op uw server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="facb6-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="facb6-175">U opgeven Hallo-methoden die u wilt dat toowatch.</span><span class="sxs-lookup"><span data-stu-id="facb6-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="facb6-176">Methodeaanroepen en externe afhankelijkheden bewaken</span><span class="sxs-lookup"><span data-stu-id="facb6-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="facb6-177">[Hallo Java-Agent installeren](app-insights-java-agent.md) toolog opgegeven interne methoden en oproepen via JDBC vast, inclusief timinggegevens.</span><span class="sxs-lookup"><span data-stu-id="facb6-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="facb6-178">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="facb6-178">Performance counters</span></span>
<span data-ttu-id="facb6-179">Op de overzichtsblade Schuif naar beneden en klikt u op Hallo **Servers** tegel.</span><span class="sxs-lookup"><span data-stu-id="facb6-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="facb6-180">Hier ziet u een groot aantal prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="facb6-180">You'll see a range of performance counters.</span></span>

![Schuif naar beneden tooclick Hallo Servers tegel](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="facb6-182">Het verzamelen van prestatiemeteritems aanpassen</span><span class="sxs-lookup"><span data-stu-id="facb6-182">Customize performance counter collection</span></span>
<span data-ttu-id="facb6-183">toodisable verzameling Hallo standaardset prestatiemeteritems toevoegen Hallo code onder de hoofdknooppunt Hallo van Hallo ApplicationInsights.xml-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="facb6-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="facb6-184">Verzamelen van aanvullende prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="facb6-184">Collect additional performance counters</span></span>
<span data-ttu-id="facb6-185">U kunt aanvullende prestatie-items toobe verzamelde opgeven.</span><span class="sxs-lookup"><span data-stu-id="facb6-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="facb6-186">JMX-tellers (weergegeven door Hallo virtuele Java-Machine)</span><span class="sxs-lookup"><span data-stu-id="facb6-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="facb6-187">`displayName`– Hallo naam die wordt weergegeven in Hallo Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="facb6-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="facb6-188">`objectName`– hello JMX-objectnaam.</span><span class="sxs-lookup"><span data-stu-id="facb6-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="facb6-189">`attribute`– Hallo-kenmerk van Hallo JMX-object naam toofetch</span><span class="sxs-lookup"><span data-stu-id="facb6-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="facb6-190">`type`(optioneel) - Hallo type van kenmerk JMX-object:</span><span class="sxs-lookup"><span data-stu-id="facb6-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="facb6-191">Standaard: een eenvoudig type, zoals int of long.</span><span class="sxs-lookup"><span data-stu-id="facb6-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="facb6-192">`composite`: Hallo prestatiemetergegevens is Hallo indeling 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="facb6-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="facb6-193">`tabular`: Hallo prestatiemetergegevens heeft Hallo-indeling van de rij in een tabel</span><span class="sxs-lookup"><span data-stu-id="facb6-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="facb6-194">Windows-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="facb6-194">Windows performance counters</span></span>
<span data-ttu-id="facb6-195">Elke [Windows-prestatiemeteritem](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) lid is van een categorie (in Hallo dezelfde manier als een veld deel uitmaakt van een klasse).</span><span class="sxs-lookup"><span data-stu-id="facb6-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="facb6-196">Categorieën kunnen globaal zijn, maar ook genummerde of benoemde exemplaren hebben.</span><span class="sxs-lookup"><span data-stu-id="facb6-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="facb6-197">displayName: Hallo naam weergegeven in Hallo Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="facb6-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="facb6-198">Categorynaam: Hallo prestatiemeteritemcategorie (prestatie-object) waaraan dit prestatiemeteritem gekoppeld is.</span><span class="sxs-lookup"><span data-stu-id="facb6-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="facb6-199">counterName: de naam van het prestatiemeteritem Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="facb6-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="facb6-200">instanceName: de naam van exemplaar categorie Hallo van prestatiemeteritem hello of een lege tekenreeks (""), als Hallo categorie slechts één exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="facb6-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="facb6-201">Als Hallo categorienaam Process, en Hallo prestatiemeteritem gewenst toocollect is uit de huidige JVM-proces Hallo op waarop uw app wordt uitgevoerd, specificeert `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="facb6-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="facb6-202">De prestatiemeteritems zijn zichtbaar als aangepaste metrische gegevens in [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="facb6-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="facb6-203">Unix-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="facb6-203">Unix performance counters</span></span>
* <span data-ttu-id="facb6-204">[Installeer collectd met Application Insights-invoegtoepassing Hallo](app-insights-java-collectd.md) tooget een scala aan systeem- en netwerkbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="facb6-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="facb6-205">Webtests voor beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="facb6-205">Availability web tests</span></span>
<span data-ttu-id="facb6-206">Application Insights kunnen testen uw website op regelmatige intervallen toocheck of deze actief is en goed reageert.</span><span class="sxs-lookup"><span data-stu-id="facb6-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="facb6-207">[tooset up][availability], schuif omlaag tooclick beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="facb6-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![Omlaag schuiven, op Beschikbaarheid klikken en vervolgens op Webtest toevoegen klikken](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="facb6-209">Er worden grafieken weergegeven met reactietijden en u ontvangt e-mailmeldingen als uw site uitvalt.</span><span class="sxs-lookup"><span data-stu-id="facb6-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Voorbeeld van een webtest](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="facb6-211">[Meer informatie over de webtests voor beschikbaarheid.][availability]</span><span class="sxs-lookup"><span data-stu-id="facb6-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="facb6-212">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="facb6-212">Diagnostic logs</span></span>
<span data-ttu-id="facb6-213">Als u Logback en Log4J (versie 1.2 of 2.0) voor voor tracering, hebt u uw traceerlogboeken tooApplication Insights waar u kunt verkennen en zoeken op deze automatisch verzonden.</span><span class="sxs-lookup"><span data-stu-id="facb6-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="facb6-214">[Meer informatie over diagnostische logboeken][javalogs]</span><span class="sxs-lookup"><span data-stu-id="facb6-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="facb6-215">Aangepaste telemetrie</span><span class="sxs-lookup"><span data-stu-id="facb6-215">Custom telemetry</span></span>
<span data-ttu-id="facb6-216">Een paar regels code in uw Java web application toofind uit wat gebruikers met het doen invoegen of toohelp analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="facb6-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="facb6-217">U kunt de code kunt invoegen in webpagina's, JavaScript en in Hallo serverzijde Java.</span><span class="sxs-lookup"><span data-stu-id="facb6-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="facb6-218">[Meer informatie over aangepaste telemetrie][track]</span><span class="sxs-lookup"><span data-stu-id="facb6-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="facb6-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="facb6-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="facb6-220">Detecteren en onderzoeken van problemen</span><span class="sxs-lookup"><span data-stu-id="facb6-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="facb6-221">[Voeg telemetrie van de webclient] [ usage] tooget prestatietelemetrie van de webclient Hallo.</span><span class="sxs-lookup"><span data-stu-id="facb6-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="facb6-222">[Webtests instellen] [ availability] toomake zorgen dat uw toepassing live en responsief blijft.</span><span class="sxs-lookup"><span data-stu-id="facb6-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="facb6-223">[Zoek naar gebeurtenissen en logboeken] [ diagnostic] toohelp analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="facb6-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="facb6-224">[Vastleggen van traces Log4J of Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="facb6-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="facb6-225">Bijhouden van gebruik</span><span class="sxs-lookup"><span data-stu-id="facb6-225">Track usage</span></span>
* <span data-ttu-id="facb6-226">[Voeg telemetrie van de webclient] [ usage] toomonitor pagina weergaven en basisgebruiker metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="facb6-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="facb6-227">[Aangepaste gebeurtenissen en metrische gegevens bijhouden](app-insights-web-track-usage.md) toolearn over hoe uw toepassing wordt gebruikt, zowel op Hallo-client en server Hallo.</span><span class="sxs-lookup"><span data-stu-id="facb6-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
