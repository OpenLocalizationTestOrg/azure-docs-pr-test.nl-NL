---
title: Aan de slag met Azure Application Insights met behulp van Java in Eclipse | Microsoft docs
description: Gebruik de Eclipse-invoegtoepassing prestaties en bewaking van het gebruik aan uw Java-website met Application Insights toevoegen
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
ms.openlocfilehash: f2f696a3bbe7893c1f521a3e5588f4f93805d6a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="2dd49-103">Aan de slag met Application Insights met behulp van Java in Eclipse</span><span class="sxs-lookup"><span data-stu-id="2dd49-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="2dd49-104">De Application Insights-SDK verzendt telemetrie van uw Java-webtoepassing, zodat u gebruik en prestaties kan analyseren.</span><span class="sxs-lookup"><span data-stu-id="2dd49-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="2dd49-105">De Eclipse-invoegtoepassing voor Application Insights installeert automatisch de SDK in uw project, zodat u zich buiten de telemetrie vak, plus een API die u kunt aangepaste telemetrie schrijven.</span><span class="sxs-lookup"><span data-stu-id="2dd49-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="2dd49-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2dd49-106">Prerequisites</span></span>
<span data-ttu-id="2dd49-107">Op dit moment de invoegtoepassing werkt voor Maven-projecten en dynamische webprojecten in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2dd49-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="2dd49-108">([Application Insights toevoegen aan andere typen van Java-project][java].)</span><span class="sxs-lookup"><span data-stu-id="2dd49-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="2dd49-109">U hebt het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="2dd49-109">You'll need:</span></span>

* <span data-ttu-id="2dd49-110">Oracle JRE 1.6 of hoger</span><span class="sxs-lookup"><span data-stu-id="2dd49-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="2dd49-111">Een abonnement op [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2dd49-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="2dd49-112">[Eclipse IDE voor Java EE-ontwikkelaars](http://www.eclipse.org/downloads/), Indigo of hoger.</span><span class="sxs-lookup"><span data-stu-id="2dd49-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="2dd49-113">Windows 7 of hoger, of WindowsServer 2008 of hoger</span><span class="sxs-lookup"><span data-stu-id="2dd49-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="2dd49-114">De SDK niet installeren op Eclipse (eenmaal)</span><span class="sxs-lookup"><span data-stu-id="2dd49-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="2dd49-115">U hoeft alleen te doen dit één keer per computer.</span><span class="sxs-lookup"><span data-stu-id="2dd49-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="2dd49-116">Deze stap installeert een werkset waarmee vervolgens de SDK aan elke dynamisch webproject toevoegen kunt.</span><span class="sxs-lookup"><span data-stu-id="2dd49-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="2dd49-117">Klik op Help, nieuwe Software installeren in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2dd49-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Help, installeert u nieuwe Software](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="2dd49-119">De SDK is in http://dl.microsoft.com/eclipse onder Azure Toolkit.</span><span class="sxs-lookup"><span data-stu-id="2dd49-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="2dd49-120">Schakel het selectievakje **Neem contact op met alle updatewebsites...**</span><span class="sxs-lookup"><span data-stu-id="2dd49-120">Uncheck **Contact all update sites...**</span></span>

    ![Voor Application Insights-SDK, schakelt u contact op met bijwerken alle sites](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="2dd49-122">De resterende stappen voor elk Java-project.</span><span class="sxs-lookup"><span data-stu-id="2dd49-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="2dd49-123">Een Application Insights-resource maken in Azure</span><span class="sxs-lookup"><span data-stu-id="2dd49-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="2dd49-124">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2dd49-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2dd49-125">Maak een nieuwe Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="2dd49-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="2dd49-126">Stel het toepassingstype in op Java-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="2dd49-126">Set the application type to Java web application.</span></span>  

    ![Op + klikken en Application Insights kiezen](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="2dd49-128">Zoek de instrumentatiesleutel van de nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="2dd49-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="2dd49-129">U moet deze zo dadelijk in de code van uw project plakken.</span><span class="sxs-lookup"><span data-stu-id="2dd49-129">You'll need to paste this into your code project shortly.</span></span>  

    ![Op Eigenschappen klikken in het overzicht van de nieuwe resource en de instrumentatiesleutel kopiëren](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="2dd49-131">Application Insights toevoegen aan uw project</span><span class="sxs-lookup"><span data-stu-id="2dd49-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="2dd49-132">Application Insights toevoegen in het contextmenu van uw Java-webproject.</span><span class="sxs-lookup"><span data-stu-id="2dd49-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![Op Eigenschappen klikken in het overzicht van de nieuwe resource en de instrumentatiesleutel kopiëren](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="2dd49-134">Plak de instrumentatiesleutel die u hebt verkregen via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2dd49-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![Op Eigenschappen klikken in het overzicht van de nieuwe resource en de instrumentatiesleutel kopiëren](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="2dd49-136">De sleutel samen met elk telemetrie-item is verzonden en instrueert Application Insights weer te geven in de resource.</span><span class="sxs-lookup"><span data-stu-id="2dd49-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="2dd49-137">Voer de toepassing en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="2dd49-137">Run the application and see metrics</span></span>
<span data-ttu-id="2dd49-138">Voer uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2dd49-138">Run your application.</span></span>

<span data-ttu-id="2dd49-139">Ga terug naar uw Application Insights-resource in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2dd49-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="2dd49-140">Gegevens van HTTP-aanvragen worden weergegeven op de overzichtsblade.</span><span class="sxs-lookup"><span data-stu-id="2dd49-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="2dd49-141">(Als dit niet het geval is, wacht u een paar seconden en klikt u vervolgens op Vernieuwen.)</span><span class="sxs-lookup"><span data-stu-id="2dd49-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="2dd49-142">Reactie van server, telt het aantal aanvragen en fouten</span><span class="sxs-lookup"><span data-stu-id="2dd49-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="2dd49-143">Klik in een grafiek voor gedetailleerdere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="2dd49-143">Click through any chart to see more detailed metrics.</span></span>

![Het aantal aanvragen met de naam](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="2dd49-145">[Meer informatie over metrische gegevens.][metrics]</span><span class="sxs-lookup"><span data-stu-id="2dd49-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="2dd49-146">En wanneer u de eigenschappen van een aanvraag bekijkt, ziet u de telemetriegebeurtenissen die zijn gekoppeld aan deze zoals aanvragen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="2dd49-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![Alle traces voor deze aanvraag](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="2dd49-148">Telemetrie-clientzijde</span><span class="sxs-lookup"><span data-stu-id="2dd49-148">Client-side telemetry</span></span>
<span data-ttu-id="2dd49-149">Klik op code ophalen voor het bewaken van mijn webpagina's op de blade snel aan de slag:</span><span class="sxs-lookup"><span data-stu-id="2dd49-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![Kies op de overzichtsblade van uw app de optie Snel starten, Code ophalen voor het bewaken van mijn webpagina’s.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="2dd49-152">Voeg het volgende codefragment in de kop van de HTML-bestanden.</span><span class="sxs-lookup"><span data-stu-id="2dd49-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="2dd49-153">Client-side '-gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="2dd49-153">View client-side data</span></span>
<span data-ttu-id="2dd49-154">Open uw bijgewerkte webpagina's en ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2dd49-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="2dd49-155">Wacht een minuut of twee, en vervolgens terug naar Application Insights en open de blade informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="2dd49-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="2dd49-156">(De blade overzicht Schuif naar beneden en klik op informatie over het gebruik.)</span><span class="sxs-lookup"><span data-stu-id="2dd49-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="2dd49-157">Pagina metrische gegevens weergeven, de gebruiker en de sessie wordt weergegeven op de blade gebruik:</span><span class="sxs-lookup"><span data-stu-id="2dd49-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![Sessies, gebruikers en paginaweergaven](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="2dd49-159">[Meer informatie over het instellen van de client-side telemetrie.][usage]</span><span class="sxs-lookup"><span data-stu-id="2dd49-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="2dd49-160">Uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="2dd49-160">Publish your application</span></span>
<span data-ttu-id="2dd49-161">Publiceer nu uw app op de server, geef de app vrij voor gebruik en bekijk de telemetrische gegevens die in de portal binnenkomen.</span><span class="sxs-lookup"><span data-stu-id="2dd49-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="2dd49-162">Controleer of de firewall het verzenden van telemetrie door uw app naar deze poorten toestaat:</span><span class="sxs-lookup"><span data-stu-id="2dd49-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="2dd49-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="2dd49-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="2dd49-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="2dd49-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="2dd49-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="2dd49-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="2dd49-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="2dd49-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="2dd49-167">Installeer op Windows-servers:</span><span class="sxs-lookup"><span data-stu-id="2dd49-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="2dd49-168">Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="2dd49-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="2dd49-169">(Hiermee kunt u prestatiemeteritems instellen.)</span><span class="sxs-lookup"><span data-stu-id="2dd49-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="2dd49-170">Uitzonderingen en mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="2dd49-170">Exceptions and request failures</span></span>
<span data-ttu-id="2dd49-171">Onverwerkte uitzonderingen worden automatisch verzameld:</span><span class="sxs-lookup"><span data-stu-id="2dd49-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="2dd49-172">Voor het verzamelen van gegevens over andere uitzonderingen hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="2dd49-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="2dd49-173">[Aanroepen naar TrackException invoegen in uw code](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="2dd49-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="2dd49-174">[De Java-agent installeren op uw server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="2dd49-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="2dd49-175">U specificeert de methoden die u wilt bekijken.</span><span class="sxs-lookup"><span data-stu-id="2dd49-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="2dd49-176">Methodeaanroepen en externe afhankelijkheden bewaken</span><span class="sxs-lookup"><span data-stu-id="2dd49-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="2dd49-177">[Installeer de Java-agent](app-insights-java-agent.md) om gespecificeerde interne methoden en oproepen via JDBC vast te leggen, inclusief timinggegevens.</span><span class="sxs-lookup"><span data-stu-id="2dd49-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="2dd49-178">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="2dd49-178">Performance counters</span></span>
<span data-ttu-id="2dd49-179">Op de overzichtsblade Schuif naar beneden en klik op de **Servers** tegel.</span><span class="sxs-lookup"><span data-stu-id="2dd49-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="2dd49-180">Hier ziet u een groot aantal prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="2dd49-180">You'll see a range of performance counters.</span></span>

![Schuif helemaal naar klikt u op die de Servers tegel](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="2dd49-182">Het verzamelen van prestatiemeteritems aanpassen</span><span class="sxs-lookup"><span data-stu-id="2dd49-182">Customize performance counter collection</span></span>
<span data-ttu-id="2dd49-183">Als u het verzamelen van de standaardset prestatiemeteritems wilt uitschakelen, voegt u de volgende code toe onder het hoofdknooppunt van het ApplicationInsights.xml-bestand:</span><span class="sxs-lookup"><span data-stu-id="2dd49-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="2dd49-184">Verzamelen van aanvullende prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="2dd49-184">Collect additional performance counters</span></span>
<span data-ttu-id="2dd49-185">U kunt opgeven dat er aanvullende prestatiemeteritems moeten worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="2dd49-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="2dd49-186">JMX-tellers (weergegeven door de virtuele Java-machine)</span><span class="sxs-lookup"><span data-stu-id="2dd49-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="2dd49-187">`displayName` - De naam die wordt weergegeven in de Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="2dd49-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="2dd49-188">`objectName` - De JMX-objectnaam.</span><span class="sxs-lookup"><span data-stu-id="2dd49-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="2dd49-189">`attribute` - Het kenmerk van de JMX-objectnaam dat moet worden opgehaald</span><span class="sxs-lookup"><span data-stu-id="2dd49-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="2dd49-190">`type` (optioneel) - Het type kenmerk van het JMX-object:</span><span class="sxs-lookup"><span data-stu-id="2dd49-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="2dd49-191">Standaard: een eenvoudig type, zoals int of long.</span><span class="sxs-lookup"><span data-stu-id="2dd49-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="2dd49-192">`composite`: de gegevens van de prestatiemeteritems hebben de indeling 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="2dd49-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="2dd49-193">`tabular`: de gegevens van de prestatiemeteritems hebben de vorm van een rij in een tabel</span><span class="sxs-lookup"><span data-stu-id="2dd49-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="2dd49-194">Windows-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="2dd49-194">Windows performance counters</span></span>
<span data-ttu-id="2dd49-195">Elk [Windows-prestatiemeteritem](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) maakt deel uit van een categorie (net zoals een veld deel uitmaakt van een klasse).</span><span class="sxs-lookup"><span data-stu-id="2dd49-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="2dd49-196">Categorieën kunnen globaal zijn, maar ook genummerde of benoemde exemplaren hebben.</span><span class="sxs-lookup"><span data-stu-id="2dd49-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="2dd49-197">displayName: de naam die wordt weergegeven in de Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="2dd49-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="2dd49-198">categorynaam: de prestatiemeteritemcategorie (prestatie-object) waaraan dit prestatiemeteritem is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2dd49-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="2dd49-199">counterName: de naam van het prestatiemeteritem.</span><span class="sxs-lookup"><span data-stu-id="2dd49-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="2dd49-200">instanceName: de naam van het exemplaar van de prestatiemeteritemcategorie, of een lege tekenreeks ("") als de categorie slechts één exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="2dd49-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="2dd49-201">Als de categorienaam Process is en het prestatiemeteritem dat u wilt verzamelen, afkomstig is uit het huidige JVM-proces waarop uw app wordt uitgevoerd, specificeert u `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="2dd49-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="2dd49-202">De prestatiemeteritems zijn zichtbaar als aangepaste metrische gegevens in [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="2dd49-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="2dd49-203">Unix-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="2dd49-203">Unix performance counters</span></span>
* <span data-ttu-id="2dd49-204">[Installeer collectd met de Application Insights-invoegtoepassing](app-insights-java-collectd.md) om een scala aan systeem- en netwerkgegevens op te halen.</span><span class="sxs-lookup"><span data-stu-id="2dd49-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="2dd49-205">Webtests voor beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="2dd49-205">Availability web tests</span></span>
<span data-ttu-id="2dd49-206">Application Insights kan uw website regelmatig testen om te controleren of deze actief is en goed reageert.</span><span class="sxs-lookup"><span data-stu-id="2dd49-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="2dd49-207">[Voor het instellen van][availability], schuift u omlaag en klikt u op beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2dd49-207">[To set up][availability], scroll down to click Availability.</span></span>

![Omlaag schuiven, op Beschikbaarheid klikken en vervolgens op Webtest toevoegen klikken](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="2dd49-209">Er worden grafieken weergegeven met reactietijden en u ontvangt e-mailmeldingen als uw site uitvalt.</span><span class="sxs-lookup"><span data-stu-id="2dd49-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Voorbeeld van een webtest](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="2dd49-211">[Meer informatie over de webtests voor beschikbaarheid.][availability]</span><span class="sxs-lookup"><span data-stu-id="2dd49-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="2dd49-212">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="2dd49-212">Diagnostic logs</span></span>
<span data-ttu-id="2dd49-213">Als u Logback en Log4J (versie 1.2 of 2.0) voor voor tracering, hebt u uw traceerlogboeken automatisch verzonden naar Application Insights waar u kunt verkennen en op te zoeken.</span><span class="sxs-lookup"><span data-stu-id="2dd49-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="2dd49-214">[Meer informatie over diagnostische logboeken][javalogs]</span><span class="sxs-lookup"><span data-stu-id="2dd49-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="2dd49-215">Aangepaste telemetrie</span><span class="sxs-lookup"><span data-stu-id="2dd49-215">Custom telemetry</span></span>
<span data-ttu-id="2dd49-216">Voeg een paar regels code in uw Java-webtoepassing om erachter te komen wat gebruikers met het doen of om u te helpen bij het analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="2dd49-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="2dd49-217">U kunt de code kunt invoegen in webpagina's, JavaScript en in de Java-serverzijde.</span><span class="sxs-lookup"><span data-stu-id="2dd49-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="2dd49-218">[Meer informatie over aangepaste telemetrie][track]</span><span class="sxs-lookup"><span data-stu-id="2dd49-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dd49-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2dd49-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="2dd49-220">Detecteren en onderzoeken van problemen</span><span class="sxs-lookup"><span data-stu-id="2dd49-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="2dd49-221">[Voeg telemetrie van de webclient] [ usage] prestatietelemetrie van de webclient ophalen.</span><span class="sxs-lookup"><span data-stu-id="2dd49-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="2dd49-222">[Stel webtests in][availability] om te controleren of de toepassing live en responsief blijft.</span><span class="sxs-lookup"><span data-stu-id="2dd49-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="2dd49-223">[Doorzoek gebeurtenissen en logboeken][diagnostic] om problemen beter te kunnen analyseren.</span><span class="sxs-lookup"><span data-stu-id="2dd49-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="2dd49-224">[Vastleggen van traces Log4J of Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="2dd49-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="2dd49-225">Bijhouden van gebruik</span><span class="sxs-lookup"><span data-stu-id="2dd49-225">Track usage</span></span>
* <span data-ttu-id="2dd49-226">[Voeg telemetrie van de webclient] [ usage] bewaken van paginaweergaven en metrische gegevens over basic-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2dd49-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="2dd49-227">[Aangepaste gebeurtenissen en metrische gegevens bijhouden](app-insights-web-track-usage.md) voor meer informatie over hoe uw toepassing wordt gebruikt, zowel op de client en de server.</span><span class="sxs-lookup"><span data-stu-id="2dd49-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
