---
title: Een betrouwbare Azure Service Fabric-service maken met C#
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
ms.openlocfilehash: f93298e6483fd8c9dfda835964aeebd1a430af69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="bdd82-103">Uw eerste stateful betrouwbare Service Fabric-servicetoepassing maken met C#</span><span class="sxs-lookup"><span data-stu-id="bdd82-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="bdd82-104">Lees hoe u uw eerste Service Fabric-toepassing voor .NET in Windows in slechts een paar minuten kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="bdd82-104">Learn how to deploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="bdd82-105">Wanneer u klaar bent, hebt u een lokaal cluster uitgevoerd met een betrouwbare servicetoepassing.</span><span class="sxs-lookup"><span data-stu-id="bdd82-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdd82-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bdd82-106">Prerequisites</span></span>

<span data-ttu-id="bdd82-107">Voordat u begint, zorgt u ervoor dat u [uw ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bdd82-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="bdd82-108">Dit omvat het installeren van de Service Fabric SDK en Visual Studio 2017 of 2015.</span><span class="sxs-lookup"><span data-stu-id="bdd82-108">This includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="bdd82-109">De toepassing maken</span><span class="sxs-lookup"><span data-stu-id="bdd82-109">Create the application</span></span>

<span data-ttu-id="bdd82-110">Start Visual Studio als **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="bdd82-111">Maak een project met `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="bdd82-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="bdd82-112">Kies in het dialoogvenster **Nieuw Project** de optie **Cloud > Service Fabric-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-112">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="bdd82-113">Noem de toepassing **MyApplication** en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-113">Name the application **MyApplication** and press **OK**.</span></span>

   
![Dialoogvenster voor nieuw project in Visual Studio][1]

<span data-ttu-id="bdd82-115">In het volgende dialoogvenster kunt u elk type Service Fabric-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="bdd82-115">You can create any type of Service Fabric application from the next dialog.</span></span> <span data-ttu-id="bdd82-116">Kies voor deze snelstartgids **Stateful service**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="bdd82-117">Noem de service **MyStatefulService** en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-117">Name the service **MyStatefulService** and press **OK**.</span></span>

![Dialoogvenster voor nieuwe service in Visual Studio][2]


<span data-ttu-id="bdd82-119">Visual Studio maakt het toepassingsproject en het stateful service-project en geeft deze weer in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="bdd82-119">Visual Studio creates the application project and the stateful service project and displays them in Solution Explorer.</span></span>

![Solution Explorer na het maken van de stateful service-toepassing][3]

<span data-ttu-id="bdd82-121">Het toepassingsproject (**MyApplication**) bevat geen directe code.</span><span class="sxs-lookup"><span data-stu-id="bdd82-121">The application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="bdd82-122">Het verwijst naar een reeks serviceprojecten.</span><span class="sxs-lookup"><span data-stu-id="bdd82-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="bdd82-123">Daarnaast bevat het project drie andere typen inhoud:</span><span class="sxs-lookup"><span data-stu-id="bdd82-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="bdd82-124">**Profielen publiceren**</span><span class="sxs-lookup"><span data-stu-id="bdd82-124">**Publish profiles**</span></span>  
<span data-ttu-id="bdd82-125">Profielen voor het implementeren van verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="bdd82-125">Profiles for deploying to different environments.</span></span>

* <span data-ttu-id="bdd82-126">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="bdd82-126">**Scripts**</span></span>  
<span data-ttu-id="bdd82-127">PowerShell-script voor het implementeren/bijwerken van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="bdd82-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="bdd82-128">**Toepassingsdefinitie**</span><span class="sxs-lookup"><span data-stu-id="bdd82-128">**Application definition**</span></span>  
<span data-ttu-id="bdd82-129">Bevat het bestand ApplicationManifest.xml onder *ApplicationPackageRoot* waarin de samenstelling van uw toepassing wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="bdd82-129">Includes the ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="bdd82-130">Bijbehorende toepassingsparameterbestanden bevinden zich onder *ApplicationParameters*, dat kan worden gebruikt om omgevingsspecifieke parameters op te geven.</span><span class="sxs-lookup"><span data-stu-id="bdd82-130">Associated application parameter files are under *ApplicationParameters*, which can be used to specify environment-specific parameters.</span></span> <span data-ttu-id="bdd82-131">Visual Studio selecteert een toepassingsparameterbestand dat is opgegeven in het bijbehorende publicatieprofiel tijdens de implementatie in een specifieke omgeving.</span><span class="sxs-lookup"><span data-stu-id="bdd82-131">Visual Studio selects an application parameter file that's specified in the associated publish profile during deployment to a specific environment.</span></span>
    
<span data-ttu-id="bdd82-132">Zie [Aan de slag met Reliable Services](service-fabric-reliable-services-quick-start.md) voor een overzicht van de inhoud van het serviceproject.</span><span class="sxs-lookup"><span data-stu-id="bdd82-132">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-the-application"></a><span data-ttu-id="bdd82-133">De toepassing implementeren en fouten opsporen in de toepassing</span><span class="sxs-lookup"><span data-stu-id="bdd82-133">Deploy and debug the application</span></span>

<span data-ttu-id="bdd82-134">Nu u een toepassing hebt, kunt u deze uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bdd82-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="bdd82-135">Druk op `F5` in Visual Studio om de toepassing voor foutopsporing te implementeren.</span><span class="sxs-lookup"><span data-stu-id="bdd82-135">In Visual Studio, press `F5` to deploy the application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="bdd82-136">De eerste keer dat u de toepassing lokaal uitvoert en implementeert, wordt door Visual Studio een lokaal cluster voor foutopsporing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bdd82-136">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="bdd82-137">Dit kan enige tijd duren.</span><span class="sxs-lookup"><span data-stu-id="bdd82-137">This may take some time.</span></span> <span data-ttu-id="bdd82-138">De status van het maken van het cluster wordt weergegeven in het Visual Studio-uitvoervenster.</span><span class="sxs-lookup"><span data-stu-id="bdd82-138">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="bdd82-139">Als het cluster gereed is, ontvangt u een melding van de lokale toepassing die het systeemvak voor het cluster beheert en die in de SDK is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="bdd82-139">When the cluster is ready, you get a notification from the local cluster system tray manager application included with the SDK.</span></span>
   
![Melding van het systeemvak van het lokale cluster][4]

<span data-ttu-id="bdd82-141">Als de toepassing wordt gestart, geeft Visual Studio automatisch de **diagnostische logboeken met gebeurtenissen** weer, waarin u de traceringsuitvoer van uw services kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="bdd82-141">Once the application starts, Visual Studio automatically brings up the **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Diagnostische logboeken][5]

<span data-ttu-id="bdd82-143">De stateful servicesjabloon die wij hebben gebruikt, toont alleen de itemwaarde die wordt verhoogd in de methode `RunAsync` van **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-143">The stateful service template we used simply shows a counter value incrementing in the `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="bdd82-144">Vouw een van de gebeurtenissen uit voor meer informatie, zoals het knooppunt waarop de code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bdd82-144">Expand one of the events to see more details, including the node where the code is running.</span></span> <span data-ttu-id="bdd82-145">In dit geval is het \_Node\_2. Dit kan anders zijn op uw machine.</span><span class="sxs-lookup"><span data-stu-id="bdd82-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Details van de gebeurtenissenviewer][6]

<span data-ttu-id="bdd82-147">Het lokale cluster bevat vijf knooppunten die worden gehost op een enkele computer.</span><span class="sxs-lookup"><span data-stu-id="bdd82-147">The local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="bdd82-148">In een productieomgeving wordt elk knooppunt gehost op een afzonderlijke fysieke of virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bdd82-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="bdd82-149">We bekijken een van de knooppunten op het lokale cluster om het verlies van gegevens van een machine te simuleren en tegelijkertijd te oefenen met de foutopsporingsfunctie.</span><span class="sxs-lookup"><span data-stu-id="bdd82-149">To simulate the loss of a machine while exercising the Visual Studio debugger at the same time, let's take down one of the nodes on the local cluster.</span></span>

<span data-ttu-id="bdd82-150">Open in de **Solution Explorer** **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-150">In the **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="bdd82-151">Zoek de `RunAsync`-methode op en stel een onderbrekingspunt in op de eerste regel van de methode.</span><span class="sxs-lookup"><span data-stu-id="bdd82-151">Find the `RunAsync` method and set a breakpoint on the first line of the method.</span></span>

![Onderbrekingspunt in de stateful service RunAsync-methode][7]

<span data-ttu-id="bdd82-153">Start **Service Fabric Explorer** door met de rechtermuisknop op het systeemvak **Lokaal clusterbeheer** te klikken en kies **Lokaal cluster beheren**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-153">Launch the **Service Fabric Explorer** tool by right-clicking on the **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Start Service Fabric Explorer vanuit Lokaal clusterbeheer][systray-launch-sfx]

<span data-ttu-id="bdd82-155">[**Service Fabric Explorer** ](service-fabric-visualizing-your-cluster.md) biedt een visuele weergave van een cluster.</span><span class="sxs-lookup"><span data-stu-id="bdd82-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="bdd82-156">Deze bevat de set toepassingen die erin zijn geïmplementeerd en de set van fysieke knooppunten waaruit het cluster bestaat.</span><span class="sxs-lookup"><span data-stu-id="bdd82-156">It includes the set of applications deployed to it and the set of physical nodes that make it up.</span></span>

<span data-ttu-id="bdd82-157">Vouw in het linkerdeelvenster **Cluster > Knooppunten** uit en zoek het knooppunt waarop uw code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bdd82-157">In the left pane, expand **Cluster > Nodes** and find the node where your code is running.</span></span>

<span data-ttu-id="bdd82-158">Klik op **Acties > uitschakelen (opnieuw opstarten)** simuleren een machine opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="bdd82-158">Click **Actions > Deactivate (Restart)** to simulate a machine restarting.</span></span>

![Een knooppunt in Service Fabric Explorer stoppen][sfx-stop-node]

<span data-ttu-id="bdd82-160">U ziet uw onderbrekingspunt in Visual Studio, terwijl de berekening die u uitvoerde op één knooppunt naadloos wordt overgenomen door een ander.</span><span class="sxs-lookup"><span data-stu-id="bdd82-160">Momentarily, you should see your breakpoint hit in Visual Studio as the computation you were doing on one node seamlessly fails over to another.</span></span>


<span data-ttu-id="bdd82-161">Ga nu terug naar de details van de gebeurtenisviewer en bekijk de berichten.</span><span class="sxs-lookup"><span data-stu-id="bdd82-161">Next, return to the Diagnostic Events Viewer and observe the messages.</span></span> <span data-ttu-id="bdd82-162">De teller blijft oplopen in stappen, zelfs als de gebeurtenissen daadwerkelijk afkomstig zijn uit een ander knooppunt.</span><span class="sxs-lookup"><span data-stu-id="bdd82-162">The counter has continued incrementing, even though the events are actually coming from a different node.</span></span>

![Details van de gebeurtenissenviewer na een failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-the-local-cluster-optional"></a><span data-ttu-id="bdd82-164">Het lokale cluster opschonen (optioneel)</span><span class="sxs-lookup"><span data-stu-id="bdd82-164">Cleaning up the local cluster (optional)</span></span>

<span data-ttu-id="bdd82-165">Vergeet niet dat dit lokale cluster echt bestaat.</span><span class="sxs-lookup"><span data-stu-id="bdd82-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="bdd82-166">Als u het foutopsporingsprogramma stopt, worden uw toepassingsexemplaar en de registratie van het toepassingstype verwijderd.</span><span class="sxs-lookup"><span data-stu-id="bdd82-166">Stopping the debugger removes your application instance and unregisters the application type.</span></span> <span data-ttu-id="bdd82-167">Het op de achtergrond uitvoeren van het cluster gaat echter gewoon door.</span><span class="sxs-lookup"><span data-stu-id="bdd82-167">However, the cluster continues to run in the background.</span></span> <span data-ttu-id="bdd82-168">Wanneer u klaar bent om het lokale cluster te stoppen, is er een aantal opties.</span><span class="sxs-lookup"><span data-stu-id="bdd82-168">When you're ready to stop the local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="bdd82-169">Toepassing behouden en gegevens traceren</span><span class="sxs-lookup"><span data-stu-id="bdd82-169">Keep application and trace data</span></span>

<span data-ttu-id="bdd82-170">Sluit het cluster af door met de rechtermuisknop op het systeemvak **Lokaal clusterbeheer** te klikken en kies vervolgens **Lokaal cluster stoppen**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-170">Shut down the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-the-cluster-and-all-data"></a><span data-ttu-id="bdd82-171">Het cluster en alle gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="bdd82-171">Delete the cluster and all data</span></span>

<span data-ttu-id="bdd82-172">Verwijder het cluster door met de rechtermuisknop op het systeemvak **Lokaal clusterbeheer** te klikken en kies vervolgens **Lokaal cluster verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="bdd82-172">Remove the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="bdd82-173">Als u deze optie kiest, implementeert Visual Studio het cluster de volgende keer dat u de toepassing uitvoert opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bdd82-173">If you choose this option, Visual Studio will redeploy the cluster the next time your run the application.</span></span> <span data-ttu-id="bdd82-174">Kies deze optie als u het lokale cluster een tijdje niet gaat gebruiken of als u resources moet vrijmaken.</span><span class="sxs-lookup"><span data-stu-id="bdd82-174">Choose this option if you don't intend to use the local cluster for some time or if you need to reclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdd82-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bdd82-175">Next steps</span></span>
<span data-ttu-id="bdd82-176">Meer informatie over [betrouwbare services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bdd82-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
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
