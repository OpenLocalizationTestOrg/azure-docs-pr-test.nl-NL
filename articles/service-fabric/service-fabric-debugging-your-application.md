---
title: Fouten opsporen in uw toepassing in Visual Studio | Microsoft Docs
description: De betrouwbaarheid en prestaties van uw services verbeteren door te ontwikkelen en ze op een lokaal ontwikkelcluster foutopsporing in Visual Studio.
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
ms.openlocfilehash: 2459025899a7f5ffebf44fa104ed112c0eb99dfa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="34129-103">Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34129-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34129-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="34129-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="34129-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="34129-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="34129-106">Fouten opsporen in een lokale Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="34129-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="34129-107">U kunt tijd en geld besparen door te implementeren en foutopsporing van uw Azure Service Fabric-toepassing in een cluster van de ontwikkeling van lokale computer.</span><span class="sxs-lookup"><span data-stu-id="34129-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="34129-108">Visual Studio 2017 of Visual Studio 2015 kunt implementeren van de toepassing met het lokale cluster en het foutopsporingsprogramma wordt automatisch verbinding maken met alle exemplaren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="34129-108">Visual Studio 2017 or Visual Studio 2015 can deploy the application to the local cluster and automatically connect the debugger to all instances of your application.</span></span>

1. <span data-ttu-id="34129-109">Een lokaal ontwikkelcluster starten door de stappen in [instellen van uw ontwikkelomgeving Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="34129-109">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="34129-110">Druk op **F5** of klik op **Debug** > **foutopsporing starten**.</span><span class="sxs-lookup"><span data-stu-id="34129-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Foutopsporing van een toepassing starten][startdebugging]
3. <span data-ttu-id="34129-112">Onderbrekingspunten instellen in uw code en de stap door de toepassing door te klikken op de opdrachten in de **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="34129-112">Set breakpoints in your code and step through the application by clicking commands in the **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="34129-113">Visual Studio koppelt aan alle exemplaren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="34129-113">Visual Studio attaches to all instances of your application.</span></span> <span data-ttu-id="34129-114">Terwijl u de code hebt doorlopen, kunnen onderbrekingspunten ophalen geraakt door meerdere processen, wat resulteert in gelijktijdige sessies.</span><span class="sxs-lookup"><span data-stu-id="34129-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="34129-115">Probeer de onderbrekingspunten uitschakelen nadat ze zijn bereikt door middel van elke onderbrekingspunt afhankelijk van de thread-ID of met behulp van diagnostische gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="34129-115">Try disabling the breakpoints after they're hit, by making each breakpoint conditional on the thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="34129-116">De **diagnostische gebeurtenissen** venster wordt automatisch geopend zodat u de diagnostische gebeurtenissen in realtime kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="34129-116">The **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Diagnostische gebeurtenissen in realtime weergeven][diagnosticevents]
5. <span data-ttu-id="34129-118">U kunt ook openen de **diagnostische gebeurtenissen** venster in de Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="34129-118">You can also open the **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="34129-119">Onder **Service Fabric**, met de rechtermuisknop op een willekeurig knooppunt en kiest u **weergave Streaming traceringen**.</span><span class="sxs-lookup"><span data-stu-id="34129-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Open het venster diagnostische gebeurtenissen][viewdiagnosticevents]
   
    <span data-ttu-id="34129-121">Als u filteren van uw traceringen voor een bepaalde service of toepassing wilt, schakelt u gewoon streaming traces op die specifieke service of toepassing.</span><span class="sxs-lookup"><span data-stu-id="34129-121">If you want to filter your traces to a specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="34129-122">De diagnostische gebeurtenissen kunnen worden weergegeven in de automatisch gegenereerde **ServiceEventSource.cs** bestand en worden aangeroepen vanuit de toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="34129-122">The diagnostic events can be seen in the automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="34129-123">De **diagnostische gebeurtenissen** venster biedt ondersteuning voor filteren, onderbreken en gebeurtenissen in realtime te bekijken.</span><span class="sxs-lookup"><span data-stu-id="34129-123">The **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="34129-124">Het filter is een eenvoudige tekenreeks zoeken in het gebeurtenisbericht, met inbegrip van de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="34129-124">The filter is a simple string search of the event message, including its contents.</span></span>
   
    ![Filteren, onderbreken en hervatten of gebeurtenissen in realtime controleren][diagnosticeventsactions]
8. <span data-ttu-id="34129-126">Services-foutopsporing is vergelijkbaar met een andere toepassing voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="34129-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="34129-127">U wordt normaal gesproken onderbrekingspunten met Visual Studio voor het opsporen van eenvoudige instellen.</span><span class="sxs-lookup"><span data-stu-id="34129-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="34129-128">Hoewel betrouwbare verzamelingen over meerdere knooppunten repliceren, ze nog steeds IEnumerable is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="34129-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="34129-129">Dit betekent dat kunt u het resultaatvenster in Visual Studio tijdens foutopsporing om te zien wat u hebt opgeslagen in.</span><span class="sxs-lookup"><span data-stu-id="34129-129">This means that you can use the Results View in Visual Studio while debugging to see what you've stored inside.</span></span> <span data-ttu-id="34129-130">Gewoon een onderbrekingspunt instellen overal in uw code.</span><span class="sxs-lookup"><span data-stu-id="34129-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Foutopsporing van een toepassing starten][breakpoint]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="34129-132">Fouten opsporen in een externe Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="34129-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="34129-133">Als uw Service Fabric-toepassingen worden uitgevoerd op een Service Fabric-cluster in Azure, zich u op afstand fouten opsporen in deze rechtstreeks vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34129-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able to remotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="34129-134">Vereist de functie [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) en [Azure SDK voor .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="34129-134">The feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="34129-135">Foutopsporing op afstand is bedoeld voor ontwikkel-/ Testscenario's en niet moet worden gebruikt in een productieomgeving vanwege de gevolgen voor de actieve toepassingen.</span><span class="sxs-lookup"><span data-stu-id="34129-135">Remote debugging is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> 
> 

1. <span data-ttu-id="34129-136">Navigeer naar uw cluster in **Cloud Explorer**, klik met de rechtermuisknop en kies **foutopsporing inschakelen**</span><span class="sxs-lookup"><span data-stu-id="34129-136">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Foutopsporing op afstand inschakelen][enableremotedebugging]
   
    <span data-ttu-id="34129-138">Hiermee wordt het proces voor het inschakelen van de externe foutopsporing extensie op uw clusterknooppunten, evenals de vereiste netwerkconfiguraties starten.</span><span class="sxs-lookup"><span data-stu-id="34129-138">This will kick off the process of enabling the remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="34129-139">Met de rechtermuisknop op het clusterknooppunt in **Cloud Explorer**, en kies **foutopsporingsprogramma koppelen**</span><span class="sxs-lookup"><span data-stu-id="34129-139">Right-click the cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Foutopsporingsprogramma koppelen][attachdebugger]
3. <span data-ttu-id="34129-141">In de **koppelen aan proces** dialoogvenster, kiest u het proces dat u wilt opsporen in en klik op **koppelen**</span><span class="sxs-lookup"><span data-stu-id="34129-141">In the **Attach to process** dialog, choose the process you want to debug, and click **Attach**</span></span>
   
    ![Kies proces][chooseprocess]
   
    <span data-ttu-id="34129-143">De naam van het proces dat u koppelen wilt, is gelijk aan de naam van het assembly-naam van uw service-project.</span><span class="sxs-lookup"><span data-stu-id="34129-143">The name of the process you want to attach to, equals the name of your service project assembly name.</span></span>
   
    <span data-ttu-id="34129-144">Het foutopsporingsprogramma zal worden gekoppeld aan alle knooppunten in het proces wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34129-144">The debugger will attach to all nodes running the process.</span></span>
   
   * <span data-ttu-id="34129-145">In het geval waar u fouten een stateless service opspoort, uitmaken alle exemplaren van de service op alle knooppunten deel van de foutopsporingssessie.</span><span class="sxs-lookup"><span data-stu-id="34129-145">In the case where you are debugging a stateless service, all instances of the service on all nodes are part of the debug session.</span></span>
   * <span data-ttu-id="34129-146">Als u fouten een stateful service opspoort, worden alleen de primaire replica van een partitie actief en daarom bijgewerkt door het foutopsporingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="34129-146">If you are debugging a stateful service, only the primary replica of any partition will be active and therefore caught by the debugger.</span></span> <span data-ttu-id="34129-147">Als de primaire replica tijdens de foutopsporingssessie wordt, wordt de verwerking van die replica nog steeds deel uitmaken van de foutopsporingssessie.</span><span class="sxs-lookup"><span data-stu-id="34129-147">If the primary replica moves during the debug session, the processing of that replica will still be part of the debug session.</span></span>
   * <span data-ttu-id="34129-148">Om te kunnen vangen alleen relevante partities of verschillende exemplaren van een bepaalde service, kunt u voorwaardelijke onderbrekingspunten om alleen een specifieke partitie of het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="34129-148">In order to only catch relevant partitions or instances of a given service, you can use conditional breakpoints to only break a specific partition or instance.</span></span>
     
     ![Voorwaardelijke onderbrekingspunt][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="34129-150">We bieden momenteel geen ondersteuning foutopsporing van een Service Fabric-cluster met meerdere exemplaren van dezelfde uitvoerbare servicenaam.</span><span class="sxs-lookup"><span data-stu-id="34129-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of the same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="34129-151">Nadat u fouten opspoort in uw toepassing hebt, kunt u de externe foutopsporing uitbreiding uitschakelen met de rechtermuisknop op het cluster in **Cloud Explorer** en kies **foutopsporing uitschakelen**</span><span class="sxs-lookup"><span data-stu-id="34129-151">Once you finish debugging your application, you can disable the remote debugging extension by right-clicking the cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Foutopsporing op afstand uitschakelen][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="34129-153">Streaming traceringen vanaf een externe clusterknooppunt</span><span class="sxs-lookup"><span data-stu-id="34129-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="34129-154">U staat ook kunnen stroom traceringen rechtstreeks vanaf een externe clusterknooppunt als Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34129-154">You are also able to stream traces directly from a remote cluster node to Visual Studio.</span></span> <span data-ttu-id="34129-155">Deze functie kunt u stroom ETW-traceringsgebeurtenissen, op het knooppunt van een Service Fabric-cluster geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="34129-155">This feature allows you to stream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="34129-156">Dit onderdeel vereist [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) en [Azure SDK voor .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="34129-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="34129-157">Deze functie ondersteunt alleen clusters die worden uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="34129-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="34129-158">Streaming traceringen is bedoeld voor ontwikkel-/ Testscenario's en niet moet worden gebruikt in een productieomgeving vanwege de gevolgen voor de actieve toepassingen.</span><span class="sxs-lookup"><span data-stu-id="34129-158">Streaming traces is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> <span data-ttu-id="34129-159">In een productiescenario verstandig doorsturen van gebeurtenissen met behulp van Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="34129-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="34129-160">Navigeer naar uw cluster in **Cloud Explorer**, klik met de rechtermuisknop en kies **Streaming traceringen inschakelen**</span><span class="sxs-lookup"><span data-stu-id="34129-160">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Externe streaming traceringen inschakelen][enablestreamingtraces]
   
    <span data-ttu-id="34129-162">Hiermee wordt het proces voor het inschakelen van de streaming traceringen-extensie op uw clusterknooppunten, evenals de vereiste netwerkconfiguraties starten.</span><span class="sxs-lookup"><span data-stu-id="34129-162">This will kick off the process of enabling the streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="34129-163">Vouw de **knooppunten** -element in **Cloud Explorer**, met de rechtermuisknop op het knooppunt dat u wilt streamen traceringen uit en kies **weergave Streaming traceringen**</span><span class="sxs-lookup"><span data-stu-id="34129-163">Expand the **Nodes** element in **Cloud Explorer**, right-click the node you want to stream traces from and choose **View Streaming Traces**</span></span>
   
    ![Externe streaming traceringen weergeven][viewremotestreamingtraces]
   
    <span data-ttu-id="34129-165">Herhaal stap 2 voor zoveel knooppunten als u wilt zien van traceringen uit.</span><span class="sxs-lookup"><span data-stu-id="34129-165">Repeat step 2 for as many nodes as you want to see traces from.</span></span> <span data-ttu-id="34129-166">Elke stroom knooppunten wordt in een speciale venster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="34129-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="34129-167">U bent nu kunnen zien de traceringen verzonden door het Service Fabric en uw services.</span><span class="sxs-lookup"><span data-stu-id="34129-167">You are now able to see the traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="34129-168">Als u filteren van de gebeurtenissen wilt zodat alleen een specifieke toepassing worden weergegeven, gewoon Typ de naam van de toepassing in het filter.</span><span class="sxs-lookup"><span data-stu-id="34129-168">If you want to filter the events to only show a specific application, simply type in the name of the application in the filter.</span></span>
   
    ![Streaming traceringen weergeven][viewingstreamingtraces]
3. <span data-ttu-id="34129-170">Wanneer u klaar bent streaming traceringen van uw cluster, kunt u externe streaming traceringen, uitschakelen met de rechtermuisknop op het cluster in **Cloud Explorer** en kies **Streaming traceringen uitschakelen**</span><span class="sxs-lookup"><span data-stu-id="34129-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking the cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Externe streaming traceringen uitschakelen][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="34129-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34129-172">Next steps</span></span>
* <span data-ttu-id="34129-173">[Een Service Fabric-service testen](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34129-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="34129-174">[Beheren van uw Service Fabric-toepassingen in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="34129-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

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
