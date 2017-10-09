---
title: aaaDebug uw toepassing in Visual Studio | Microsoft Docs
description: Hallo-betrouwbaarheid en prestaties van uw services verbeteren door te ontwikkelen en ze op een lokaal ontwikkelcluster foutopsporing in Visual Studio.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="adc8c-103">Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="adc8c-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="adc8c-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="adc8c-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="adc8c-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="adc8c-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="adc8c-106">Fouten opsporen in een lokale Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="adc8c-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="adc8c-107">U kunt tijd en geld besparen door te implementeren en foutopsporing van uw Azure Service Fabric-toepassing in een cluster van de ontwikkeling van lokale computer.</span><span class="sxs-lookup"><span data-stu-id="adc8c-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="adc8c-108">Visual Studio 2017 of Visual Studio 2015 Hallo toepassing toohello lokale cluster implementeren en automatisch verbinding Hallo foutopsporingsprogramma tooall exemplaren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="adc8c-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="adc8c-109">Een lokaal ontwikkelcluster starten door de stappen te volgen Hallo in [instellen van uw ontwikkelomgeving Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="adc8c-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="adc8c-110">Druk op **F5** of klik op **Debug** > **foutopsporing starten**.</span><span class="sxs-lookup"><span data-stu-id="adc8c-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Foutopsporing van een toepassing starten][startdebugging]
3. <span data-ttu-id="adc8c-112">Onderbrekingspunten instellen in uw code en de toepassing hello stap voor stap door te klikken op de opdrachten in Hallo **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="adc8c-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="adc8c-113">Visual Studio koppelt tooall exemplaren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="adc8c-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="adc8c-114">Terwijl u de code hebt doorlopen, kunnen onderbrekingspunten ophalen geraakt door meerdere processen, wat resulteert in gelijktijdige sessies.</span><span class="sxs-lookup"><span data-stu-id="adc8c-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="adc8c-115">Probeer Hallo onderbrekingspunten uitschakelen nadat ze zijn bereikt door middel van elke onderbrekingspunt voorwaardelijke op Hallo thread-ID of met behulp van diagnostische gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="adc8c-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="adc8c-116">Hallo **diagnostische gebeurtenissen** venster wordt automatisch geopend zodat u de diagnostische gebeurtenissen in realtime kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="adc8c-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Diagnostische gebeurtenissen in realtime weergeven][diagnosticevents]
5. <span data-ttu-id="adc8c-118">U kunt ook openen Hallo **diagnostische gebeurtenissen** venster in de Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="adc8c-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="adc8c-119">Onder **Service Fabric**, met de rechtermuisknop op een willekeurig knooppunt en kiest u **weergave Streaming traceringen**.</span><span class="sxs-lookup"><span data-stu-id="adc8c-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Open Hallo diagnostische gebeurtenissen venster][viewdiagnosticevents]
   
    <span data-ttu-id="adc8c-121">Als u toofilter uw traceringen tooa specifieke service of toepassing wilt, schakel gewoon streaming traces op die specifieke service of toepassing.</span><span class="sxs-lookup"><span data-stu-id="adc8c-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="adc8c-122">Hallo diagnostische gebeurtenissen worden weergegeven in Hallo automatisch gegenereerd **ServiceEventSource.cs** bestand en worden aangeroepen vanuit de toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="adc8c-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="adc8c-123">Hallo **diagnostische gebeurtenissen** venster biedt ondersteuning voor filteren, onderbreken en gebeurtenissen in realtime te bekijken.</span><span class="sxs-lookup"><span data-stu-id="adc8c-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="adc8c-124">Hallo-filter is een eenvoudige tekenreeks zoekactie van Hallo gebeurtenisbericht, met inbegrip van de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="adc8c-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![Filteren, onderbreken en hervatten of gebeurtenissen in realtime controleren][diagnosticeventsactions]
8. <span data-ttu-id="adc8c-126">Services-foutopsporing is vergelijkbaar met een andere toepassing voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="adc8c-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="adc8c-127">U wordt normaal gesproken onderbrekingspunten met Visual Studio voor het opsporen van eenvoudige instellen.</span><span class="sxs-lookup"><span data-stu-id="adc8c-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="adc8c-128">Hoewel betrouwbare verzamelingen over meerdere knooppunten repliceren, ze nog steeds IEnumerable is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="adc8c-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="adc8c-129">Dit betekent dat u Hallo resultaten weergeven in Visual Studio gebruiken kunt tijdens het opsporen van toosee wat u hebt opgeslagen in.</span><span class="sxs-lookup"><span data-stu-id="adc8c-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="adc8c-130">Gewoon een onderbrekingspunt instellen overal in uw code.</span><span class="sxs-lookup"><span data-stu-id="adc8c-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Foutopsporing van een toepassing starten][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="adc8c-132">Fouten opsporen in een externe Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="adc8c-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="adc8c-133">Als uw Service Fabric-toepassingen worden uitgevoerd op een Service Fabric-cluster in Azure, u zich tooremotely fouten opsporen in deze rechtstreeks vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="adc8c-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="adc8c-134">Hallo-onderdeel vereist [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) en [Azure SDK voor .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="adc8c-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="adc8c-135">Foutopsporing op afstand is bedoeld voor ontwikkel-/ Testscenario's en niet toobe gebruikt in een productieomgeving vanwege Hallo impact op Hallo uitvoeren van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="adc8c-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="adc8c-136">Navigeer tooyour cluster in **Cloud Explorer**, klik met de rechtermuisknop en kies **foutopsporing inschakelen**</span><span class="sxs-lookup"><span data-stu-id="adc8c-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Foutopsporing op afstand inschakelen][enableremotedebugging]
   
    <span data-ttu-id="adc8c-138">Dit wordt ere van Hallo proces van het Hallo-extensie op uw clusterknooppunten foutopsporing op afstand inschakelen, evenals netwerkconfiguraties vereist.</span><span class="sxs-lookup"><span data-stu-id="adc8c-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="adc8c-139">Klik met de rechtermuisknop Hallo clusterknooppunt in **Cloud Explorer**, en kies **foutopsporingsprogramma koppelen**</span><span class="sxs-lookup"><span data-stu-id="adc8c-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Foutopsporingsprogramma koppelen][attachdebugger]
3. <span data-ttu-id="adc8c-141">In Hallo **koppelen tooprocess** dialoogvenster Kies Hallo proces u toodebug wilt en klikt u op **koppelen**</span><span class="sxs-lookup"><span data-stu-id="adc8c-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![Kies proces][chooseprocess]
   
    <span data-ttu-id="adc8c-143">de naam van de Hallo Hallo proces dat u wilt dat tooattach aan, gelijk is aan de naam van het assembly-naam van uw service-project Hallo.</span><span class="sxs-lookup"><span data-stu-id="adc8c-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="adc8c-144">Hallo-foutopsporingsprogramma koppelt tooall knooppunten Hallo process uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="adc8c-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="adc8c-145">In geval van Hallo waar u fouten een stateless service opspoort, uitmaken alle exemplaren van Hallo-service op alle knooppunten deel van Hallo foutopsporingssessie.</span><span class="sxs-lookup"><span data-stu-id="adc8c-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="adc8c-146">Als u fouten een stateful service opspoort, worden alleen Hallo primaire replica van een partitie actief en daarom bijgewerkt door Hallo foutopsporingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="adc8c-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="adc8c-147">Als de primaire replica Hallo tijdens de foutopsporingssessie hello verplaatst, wordt Hallo verwerking van die replica nog steeds deel uitmaken van Hallo foutopsporingssessie.</span><span class="sxs-lookup"><span data-stu-id="adc8c-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="adc8c-148">In de volgorde tooonly catch relevante partities of verschillende exemplaren van een bepaalde service, kunt u voorwaardelijke onderbrekingspunten tooonly einde een specifieke partitie of het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="adc8c-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![Voorwaardelijke onderbrekingspunt][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="adc8c-150">Momenteel wij bieden geen ondersteuning voor foutopsporing van een Service Fabric-cluster met meerdere exemplaren van Hallo dezelfde uitvoerbare service-naam.</span><span class="sxs-lookup"><span data-stu-id="adc8c-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="adc8c-151">Nadat u fouten opspoort in uw toepassing hebt, kunt u Hallo externe foutopsporing uitbreiding uitschakelen door met de rechtermuisknop op Hallo-cluster in **Cloud Explorer** en kies **foutopsporing uitschakelen**</span><span class="sxs-lookup"><span data-stu-id="adc8c-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Foutopsporing op afstand uitschakelen][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="adc8c-153">Streaming traceringen vanaf een externe clusterknooppunt</span><span class="sxs-lookup"><span data-stu-id="adc8c-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="adc8c-154">Bent u ook kunnen toostream traceringen rechtstreeks vanuit een externe cluster knooppunt tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="adc8c-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="adc8c-155">Deze functie kunt u toostream ETW-traceringsgebeurtenissen, op het knooppunt van een Service Fabric-cluster geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="adc8c-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="adc8c-156">Dit onderdeel vereist [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) en [Azure SDK voor .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="adc8c-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="adc8c-157">Deze functie ondersteunt alleen clusters die worden uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="adc8c-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="adc8c-158">Streaming traceringen is bedoeld voor ontwikkel-/ Testscenario's en niet toobe gebruikt in een productieomgeving vanwege Hallo impact op Hallo uitvoeren van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="adc8c-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="adc8c-159">In een productiescenario verstandig doorsturen van gebeurtenissen met behulp van Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="adc8c-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="adc8c-160">Navigeer tooyour cluster in **Cloud Explorer**, klik met de rechtermuisknop en kies **Streaming traceringen inschakelen**</span><span class="sxs-lookup"><span data-stu-id="adc8c-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Externe streaming traceringen inschakelen][enablestreamingtraces]
   
    <span data-ttu-id="adc8c-162">Dit wordt ere van Hallo proces van het inschakelen van Hallo streaming traceringen-extensie op uw clusterknooppunten, evenals netwerkconfiguraties vereist.</span><span class="sxs-lookup"><span data-stu-id="adc8c-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="adc8c-163">Vouw Hallo **knooppunten** -element in **Cloud Explorer**, klik met de rechtermuisknop Hallo knooppunt gewenste toostream traceringen uit en kies **weergave Streaming traceringen**</span><span class="sxs-lookup"><span data-stu-id="adc8c-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![Externe streaming traceringen weergeven][viewremotestreamingtraces]
   
    <span data-ttu-id="adc8c-165">Herhaal stap 2 voor zoveel knooppunten gewenste toosee traceringen uit.</span><span class="sxs-lookup"><span data-stu-id="adc8c-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="adc8c-166">Elke stroom knooppunten wordt in een speciale venster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="adc8c-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="adc8c-167">U bent nu kunnen toosee Hallo traceringen verzonden door het Service Fabric en uw services.</span><span class="sxs-lookup"><span data-stu-id="adc8c-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="adc8c-168">Als u een specifieke toepassing toofilter Hallo gebeurtenissen tooonly weergeven wilt, typ gewoon in Hallo-naam van de toepassing hello in Hallo filter.</span><span class="sxs-lookup"><span data-stu-id="adc8c-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![Streaming traceringen weergeven][viewingstreamingtraces]
3. <span data-ttu-id="adc8c-170">Wanneer u klaar bent streaming traceringen van uw cluster, kunt u externe streaming traceringen, uitschakelen met de rechtermuisknop op Hallo-cluster in **Cloud Explorer** en kies **Streaming traceringen uitschakelen**</span><span class="sxs-lookup"><span data-stu-id="adc8c-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Externe streaming traceringen uitschakelen][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="adc8c-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="adc8c-172">Next steps</span></span>
* <span data-ttu-id="adc8c-173">[Een Service Fabric-service testen](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="adc8c-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="adc8c-174">[Beheren van uw Service Fabric-toepassingen in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="adc8c-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
