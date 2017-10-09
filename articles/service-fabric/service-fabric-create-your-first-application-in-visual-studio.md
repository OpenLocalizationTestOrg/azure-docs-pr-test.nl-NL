---
title: aaaCreate een betrouwbare Azure Service Fabric-service met C#
description: Een betrouwbare Service-toepassing die is gebouwd op Azure Service Fabric met Visual Studio maken, implementeren en er foutopsporing op toepassen.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="935fa-103">Uw eerste stateful betrouwbare Service Fabric-servicetoepassing maken met C#</span><span class="sxs-lookup"><span data-stu-id="935fa-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="935fa-104">Meer informatie over hoe toodeploy uw eerste Service Fabric-toepassing voor .NET in Windows over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="935fa-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="935fa-105">Wanneer u klaar bent, hebt u een lokaal cluster uitgevoerd met een betrouwbare servicetoepassing.</span><span class="sxs-lookup"><span data-stu-id="935fa-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="935fa-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="935fa-106">Prerequisites</span></span>

<span data-ttu-id="935fa-107">Voordat u begint, zorgt u ervoor dat u [uw ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="935fa-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="935fa-108">Dit omvat het installeren van Service Fabric SDK Hallo en Visual Studio 2017 of 2015.</span><span class="sxs-lookup"><span data-stu-id="935fa-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="935fa-109">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="935fa-109">Create hello application</span></span>

<span data-ttu-id="935fa-110">Start Visual Studio als **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="935fa-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="935fa-111">Maak een project met `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="935fa-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="935fa-112">In Hallo **nieuw Project** dialoogvenster kiezen **Cloud > Service Fabric-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="935fa-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="935fa-113">Naam van de toepassing hello **Mijntoepassing** en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="935fa-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Dialoogvenster voor nieuw project in Visual Studio][1]

<span data-ttu-id="935fa-115">U kunt elk type Service Fabric-toepassing uit het volgende dialoogvenster Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="935fa-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="935fa-116">Kies voor deze snelstartgids **Stateful service**.</span><span class="sxs-lookup"><span data-stu-id="935fa-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="935fa-117">Service voor Hallo **MyStatefulService** en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="935fa-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Dialoogvenster voor nieuwe service in Visual Studio][2]


<span data-ttu-id="935fa-119">Visual Studio maakt het toepassingsproject Hallo en Hallo stateful service-project en geeft deze weer in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="935fa-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![Solution Explorer na het maken van de stateful service-toepassing][3]

<span data-ttu-id="935fa-121">Hallo-toepassingsproject (**Mijntoepassing**) bevat geen code rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="935fa-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="935fa-122">Het verwijst naar een reeks serviceprojecten.</span><span class="sxs-lookup"><span data-stu-id="935fa-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="935fa-123">Daarnaast bevat het project drie andere typen inhoud:</span><span class="sxs-lookup"><span data-stu-id="935fa-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="935fa-124">**Profielen publiceren**</span><span class="sxs-lookup"><span data-stu-id="935fa-124">**Publish profiles**</span></span>  
<span data-ttu-id="935fa-125">Profielen voor het implementeren van toodifferent omgevingen.</span><span class="sxs-lookup"><span data-stu-id="935fa-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="935fa-126">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="935fa-126">**Scripts**</span></span>  
<span data-ttu-id="935fa-127">PowerShell-script voor het implementeren/bijwerken van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="935fa-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="935fa-128">**Toepassingsdefinitie**</span><span class="sxs-lookup"><span data-stu-id="935fa-128">**Application definition**</span></span>  
<span data-ttu-id="935fa-129">Hallo ApplicationManifest.xml bestand onder omvat *ApplicationPackageRoot* waarin wordt beschreven samenstelling van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="935fa-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="935fa-130">Bijbehorende parameter voor toepassingsbestanden onder zijn *ApplicationParameters*, welke gebruikte toospecify omgeving-specifieke parameters kan worden.</span><span class="sxs-lookup"><span data-stu-id="935fa-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="935fa-131">Visual Studio selecteert een parameterbestand toepassing die opgegeven in Hallo gekoppeld publicatieprofiel tijdens de implementatie tooa-specifieke omgeving.</span><span class="sxs-lookup"><span data-stu-id="935fa-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="935fa-132">Zie voor een overzicht van Hallo inhoud van het serviceproject Hallo [aan de slag met Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="935fa-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="935fa-133">Implementeren en fouten opsporen in de toepassing hello</span><span class="sxs-lookup"><span data-stu-id="935fa-133">Deploy and debug hello application</span></span>

<span data-ttu-id="935fa-134">Nu u een toepassing hebt, kunt u deze uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="935fa-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="935fa-135">Druk in Visual Studio op `F5` toodeploy Hallo-toepassing voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="935fa-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="935fa-136">Hallo maakt eerst u uitvoeren en implementeren van Hallo toepassing lokaal door Visual Studio een lokaal cluster voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="935fa-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="935fa-137">Dit kan enige tijd duren.</span><span class="sxs-lookup"><span data-stu-id="935fa-137">This may take some time.</span></span> <span data-ttu-id="935fa-138">status van het Hallo-cluster maken wordt weergegeven in Visual Studio-uitvoervenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="935fa-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="935fa-139">Wanneer Hallo cluster klaar is, kunt u een melding krijgt van Hallo lokale cluster system lade manager-toepassing Hello SDK is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="935fa-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![Melding van het systeemvak van het lokale cluster][4]

<span data-ttu-id="935fa-141">Eenmaal Hallo toepassing wordt gestart, Visual Studio automatisch wordt Hallo **diagnostische logboeken**, waar u de trace-uitvoer van uw services kunt zien.</span><span class="sxs-lookup"><span data-stu-id="935fa-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Diagnostische logboeken][5]

<span data-ttu-id="935fa-143">Hallo stateful servicesjabloon we gebruikt gewoon toont een teller waarde en oplopend in stappen in Hallo `RunAsync` methode van **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="935fa-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="935fa-144">Vouw een van de Hallo gebeurtenissen toosee meer informatie, zoals Hallo knooppunt waarop Hallo code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="935fa-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="935fa-145">In dit geval is het \_Node\_2. Dit kan anders zijn op uw machine.</span><span class="sxs-lookup"><span data-stu-id="935fa-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Details van de gebeurtenissenviewer][6]

<span data-ttu-id="935fa-147">Hallo lokale cluster bevat vijf knooppunten die worden gehost op een enkele computer.</span><span class="sxs-lookup"><span data-stu-id="935fa-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="935fa-148">In een productieomgeving wordt elk knooppunt gehost op een afzonderlijke fysieke of virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="935fa-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="935fa-149">foutopsporing toosimulate Hallo verlies van een machine tijdens het Hallo Visual Studio uitoefenen op Hallo dezelfde tijd, laten we bekijken een van de knooppunten op het lokale cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="935fa-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="935fa-150">In Hallo **Solution Explorer** venster open **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="935fa-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="935fa-151">Hallo zoeken `RunAsync` methode en stel een onderbrekingspunt in op de eerste regel Hallo van Hallo-methode.</span><span class="sxs-lookup"><span data-stu-id="935fa-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![Onderbrekingspunt in de stateful service RunAsync-methode][7]

<span data-ttu-id="935fa-153">Hallo starten **Service Fabric Explorer** hulpprogramma door met de rechtermuisknop op Hallo **lokaal Clusterbeheer** lade systeemtoepassing en kies **lokaal Cluster beheren**.</span><span class="sxs-lookup"><span data-stu-id="935fa-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Start Service Fabric Explorer vanuit lokaal Clusterbeheer Hallo][systray-launch-sfx]

<span data-ttu-id="935fa-155">[**Service Fabric Explorer** ](service-fabric-visualizing-your-cluster.md) biedt een visuele weergave van een cluster.</span><span class="sxs-lookup"><span data-stu-id="935fa-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="935fa-156">Dit omvat Hallo set toepassingen die zijn geïmplementeerd tooit en Hallo set van fysieke knooppunten waaruit het bestaat.</span><span class="sxs-lookup"><span data-stu-id="935fa-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="935fa-157">Vouw in het linkerdeelvenster hello, **Cluster > knooppunten** en zoeken Hallo knooppunt waarop uw code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="935fa-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="935fa-158">Klik op **Acties > uitschakelen (opnieuw opstarten)** toosimulate een machine opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="935fa-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![Een knooppunt in Service Fabric Explorer stoppen][sfx-stop-node]

<span data-ttu-id="935fa-160">Tijdelijk worden, ziet u uw onderbrekingspunt in Visual Studio bereikt, zoals Hallo berekening u op één knooppunt naadloos uitvoerde overgenomen tooanother wordt.</span><span class="sxs-lookup"><span data-stu-id="935fa-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="935fa-161">Vervolgens retourneert toohello diagnostische logboeken en Hallo-berichten te zien.</span><span class="sxs-lookup"><span data-stu-id="935fa-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="935fa-162">Hallo item is voortgezet en oplopend in stappen, zelfs als Hallo gebeurtenissen daadwerkelijk afkomstig zijn uit een ander knooppunt.</span><span class="sxs-lookup"><span data-stu-id="935fa-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![Details van de gebeurtenissenviewer na een failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="935fa-164">Opruimen van de lokale cluster hello (optioneel)</span><span class="sxs-lookup"><span data-stu-id="935fa-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="935fa-165">Vergeet niet dat dit lokale cluster echt bestaat.</span><span class="sxs-lookup"><span data-stu-id="935fa-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="935fa-166">Hallo debugger wordt gestopt, verwijdert het toepassingsexemplaar van uw en heft de registratie van toepassingstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="935fa-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="935fa-167">Hallo cluster blijft echter toorun op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="935fa-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="935fa-168">Wanneer u klaar toostop Hallo lokale cluster bent, zijn er een aantal opties.</span><span class="sxs-lookup"><span data-stu-id="935fa-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="935fa-169">Toepassing behouden en gegevens traceren</span><span class="sxs-lookup"><span data-stu-id="935fa-169">Keep application and trace data</span></span>

<span data-ttu-id="935fa-170">Hallo cluster afgesloten door met de rechtermuisknop op Hallo **lokaal Clusterbeheer** lade systeemtoepassing en kies vervolgens **lokaal Cluster stoppen**.</span><span class="sxs-lookup"><span data-stu-id="935fa-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="935fa-171">Hallo-cluster en alle gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="935fa-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="935fa-172">Hallo-cluster verwijderen door met de rechtermuisknop op Hallo **lokaal Clusterbeheer** lade systeemtoepassing en kies vervolgens **lokaal Cluster verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="935fa-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="935fa-173">Als u deze optie kiest, Visual Studio wordt opnieuw implementeren Hallo cluster Hallo zodra uw uitvoeren Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="935fa-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="935fa-174">Selecteer deze optie als u niet van plan toouse Hallo lokale cluster gedurende een bepaalde periode bent of als u tooreclaim bronnen nodig.</span><span class="sxs-lookup"><span data-stu-id="935fa-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="935fa-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="935fa-175">Next steps</span></span>
<span data-ttu-id="935fa-176">Meer informatie over [betrouwbare services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="935fa-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
