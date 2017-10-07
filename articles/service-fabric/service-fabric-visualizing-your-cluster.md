---
title: aaaVisualizing uw cluster met behulp van Service Fabric Explorer | Microsoft Docs
description: Service Fabric Explorer is een Webhulpprogramma voor te bekijken en beheren van cloudtoepassingen en -knooppunten in een Microsoft Azure Service Fabric-cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="e80fd-103">Visualisern van uw cluster met Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="e80fd-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="e80fd-104">Service Fabric Explorer is een Webhulpprogramma voor te bekijken en beheren van toepassingen en de knooppunten in een Azure Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="e80fd-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="e80fd-105">Service Fabric Explorer wordt gehost rechtstreeks in het Hallo-cluster, zodat deze altijd beschikbaar is, ongeacht waar uw cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e80fd-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="e80fd-106">Zelfstudievideo</span><span class="sxs-lookup"><span data-stu-id="e80fd-106">Video tutorial</span></span>

<span data-ttu-id="e80fd-107">toolearn hoe toouse Service Fabric Explorer bekijkt hello Microsoft Virtual Academy video te volgen:</span><span class="sxs-lookup"><span data-stu-id="e80fd-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="e80fd-108">Verbinding maken met tooService Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="e80fd-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="e80fd-109">Als u te Hallo instructies hebt gevolgd[uw ontwikkelingsomgeving voorbereiden](service-fabric-get-started.md), kunt u de Service Fabric Explorer starten op uw lokale cluster door te navigeren toohttp://localhost:19080 / Explorer.</span><span class="sxs-lookup"><span data-stu-id="e80fd-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="e80fd-110">Hallo Service Fabric Explorer indeling begrijpen</span><span class="sxs-lookup"><span data-stu-id="e80fd-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="e80fd-111">U kunt via Service Fabric Explorer navigeren met behulp van Hallo structuur op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="e80fd-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="e80fd-112">In de hoofdmap van de Hallo van Hallo structuur overzicht Hallo cluster-dashboard van uw cluster, inclusief een overzicht van de toepassing en het knooppunt status.</span><span class="sxs-lookup"><span data-stu-id="e80fd-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Service Fabric Explorer cluster-dashboard][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="e80fd-114">Indeling van het cluster Hallo weergeven</span><span class="sxs-lookup"><span data-stu-id="e80fd-114">View hello cluster's layout</span></span>
<span data-ttu-id="e80fd-115">Knooppunten in een Service Fabric-cluster worden geplaatst in een tweedimensionale raster van domeinen met fouten en upgradedomeinen.</span><span class="sxs-lookup"><span data-stu-id="e80fd-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="e80fd-116">Deze plaatsing zorgt ervoor dat uw toepassingen beschikbaar in Hallo aanwezigheid van hardwarefouten en toepassingsupgrades blijven.</span><span class="sxs-lookup"><span data-stu-id="e80fd-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="e80fd-117">U kunt bekijken hoe Hallo huidig cluster met behulp van de clustertoewijzing Hallo worden verspreid.</span><span class="sxs-lookup"><span data-stu-id="e80fd-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![Service Fabric Explorer clustertoewijzing][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="e80fd-119">Weergave-toepassingen en services</span><span class="sxs-lookup"><span data-stu-id="e80fd-119">View applications and services</span></span>
<span data-ttu-id="e80fd-120">Hallo-cluster bevat twee substructuren: één voor toepassingen en andere voor knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e80fd-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="e80fd-121">U kunt Hallo toepassing weergave toonavigate via Service Fabric van logische hiërarchie: toepassingen, services, partities en replica's.</span><span class="sxs-lookup"><span data-stu-id="e80fd-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="e80fd-122">In onderstaande Hallo voorbeeld, Hallo toepassing **MyApp** bestaat uit twee services **MyStatefulService** en **WebService**.</span><span class="sxs-lookup"><span data-stu-id="e80fd-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="e80fd-123">Aangezien **MyStatefulService** stateful is, bevat een partitie met een primaire en twee secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="e80fd-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="e80fd-124">Daarentegen is WebSvcService staatloze en slechts één exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="e80fd-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Service Fabric Explorer toepassing weergeven][sfx-application-tree]

<span data-ttu-id="e80fd-126">Op elk niveau van Hallo-structuur bevat Hallo hoofdvenster relevante informatie over het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="e80fd-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="e80fd-127">Bijvoorbeeld, ziet u Hallo gezondheidsstatus en versie voor een bepaalde service.</span><span class="sxs-lookup"><span data-stu-id="e80fd-127">For example, you can see hello health status and version for a particular service.</span></span>

![Service Fabric Explorer essentials deelvenster][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="e80fd-129">Hallo clusterknooppunten weergeven</span><span class="sxs-lookup"><span data-stu-id="e80fd-129">View hello cluster's nodes</span></span>
<span data-ttu-id="e80fd-130">Hallo knooppunt weergave toont de fysieke indeling Hallo van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e80fd-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="e80fd-131">Voor elk knooppunt kunt u controleren voor welke toepassingen er op het knooppunt code is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e80fd-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="e80fd-132">Meer specifiek, kunt u zien welke replica er momenteel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e80fd-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="e80fd-133">Acties</span><span class="sxs-lookup"><span data-stu-id="e80fd-133">Actions</span></span>
<span data-ttu-id="e80fd-134">Service Fabric Explorer biedt een snelle manier tooinvoke acties op de knooppunten, toepassingen en services in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="e80fd-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="e80fd-135">Bijvoorbeeld: toodelete instantie van een toepassing hello toepassing kiezen uit Hallo structuur aan de linkerkant Hallo en kies vervolgens **acties** > **toepassing verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="e80fd-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![Verwijderen van een toepassing in Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="e80fd-137">U kunt uitvoeren Hallo dezelfde acties door te klikken op Hallo weglatingsteken volgende tooeach element.</span><span class="sxs-lookup"><span data-stu-id="e80fd-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="e80fd-138">Hallo bevat volgende tabel Hallo acties die beschikbaar zijn voor elke entiteit:</span><span class="sxs-lookup"><span data-stu-id="e80fd-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="e80fd-139">**Entiteit**</span><span class="sxs-lookup"><span data-stu-id="e80fd-139">**Entity**</span></span> | <span data-ttu-id="e80fd-140">**Actie**</span><span class="sxs-lookup"><span data-stu-id="e80fd-140">**Action**</span></span> | <span data-ttu-id="e80fd-141">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="e80fd-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e80fd-142">Toepassingstype</span><span class="sxs-lookup"><span data-stu-id="e80fd-142">Application type</span></span> |<span data-ttu-id="e80fd-143">Type inrichting</span><span class="sxs-lookup"><span data-stu-id="e80fd-143">Unprovision type</span></span> |<span data-ttu-id="e80fd-144">Hallo-toepassingspakket verwijdert uit de installatiekopieopslag Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e80fd-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="e80fd-145">Vereist dat alle toepassingen van dat type toobe eerst verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e80fd-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="e80fd-146">Toepassing</span><span class="sxs-lookup"><span data-stu-id="e80fd-146">Application</span></span> |<span data-ttu-id="e80fd-147">Toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="e80fd-147">Delete Application</span></span> |<span data-ttu-id="e80fd-148">Hallo-toepassing, met inbegrip van alle services en hun status (indien aanwezig) verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e80fd-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="e80fd-149">Service</span><span class="sxs-lookup"><span data-stu-id="e80fd-149">Service</span></span> |<span data-ttu-id="e80fd-150">Verwijderen van de Service</span><span class="sxs-lookup"><span data-stu-id="e80fd-150">Delete Service</span></span> |<span data-ttu-id="e80fd-151">Hallo-service en de status verwijderd (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="e80fd-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="e80fd-152">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="e80fd-152">Node</span></span> |<span data-ttu-id="e80fd-153">Activeren</span><span class="sxs-lookup"><span data-stu-id="e80fd-153">Activate</span></span> |<span data-ttu-id="e80fd-154">Hallo knooppunt activeren.</span><span class="sxs-lookup"><span data-stu-id="e80fd-154">Activate hello node.</span></span> |
| <span data-ttu-id="e80fd-155">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="e80fd-155">Node</span></span> | <span data-ttu-id="e80fd-156">Deactiveren (pause)</span><span class="sxs-lookup"><span data-stu-id="e80fd-156">Deactivate (pause)</span></span> | <span data-ttu-id="e80fd-157">Hallo-knooppunt onderbreken met de huidige status.</span><span class="sxs-lookup"><span data-stu-id="e80fd-157">Pause hello node in its current state.</span></span> <span data-ttu-id="e80fd-158">Services toorun doorgaan, maar Service Fabric proactief verplaatst geen alles naar of uit deze tenzij dit vereist tooprevent een storing of inconsistenties in de gegevens.</span><span class="sxs-lookup"><span data-stu-id="e80fd-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="e80fd-159">Deze actie is gewoonlijk gebruikte tooenable services op een specifiek knooppunt tooensure dat ze niet tijdens de inspectie verplaatsen foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="e80fd-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="e80fd-160">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="e80fd-160">Node</span></span> | <span data-ttu-id="e80fd-161">(Opnieuw opstarten) deactiveren</span><span class="sxs-lookup"><span data-stu-id="e80fd-161">Deactivate (restart)</span></span> | <span data-ttu-id="e80fd-162">Veilig Verplaats alle in het geheugen services een knooppunt uit en sluit permanente services.</span><span class="sxs-lookup"><span data-stu-id="e80fd-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="e80fd-163">Normaal gesproken gebruikt bij Hallo hostprocessen of machine nodig toobe opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="e80fd-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="e80fd-164">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="e80fd-164">Node</span></span> | <span data-ttu-id="e80fd-165">Deactiveren (gegevens verwijderen)</span><span class="sxs-lookup"><span data-stu-id="e80fd-165">Deactivate (remove data)</span></span> | <span data-ttu-id="e80fd-166">Alle services die worden uitgevoerd op Hallo knooppunt na het bouwen van voldoende spare replica's sluiten.</span><span class="sxs-lookup"><span data-stu-id="e80fd-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="e80fd-167">Doorgaans gebruikt wanneer een knooppunt (of ten minste bijbehorende opslag) is buiten het Commissie permanent genomen.</span><span class="sxs-lookup"><span data-stu-id="e80fd-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="e80fd-168">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="e80fd-168">Node</span></span> | <span data-ttu-id="e80fd-169">Status van knooppunt verwijderen</span><span class="sxs-lookup"><span data-stu-id="e80fd-169">Remove node state</span></span> | <span data-ttu-id="e80fd-170">Kennis van replica's van een knooppunt uit cluster Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e80fd-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="e80fd-171">Doorgaans gebruikt wanneer een knooppunt al onherstelbare wordt geacht.</span><span class="sxs-lookup"><span data-stu-id="e80fd-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="e80fd-172">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="e80fd-172">Node</span></span> | <span data-ttu-id="e80fd-173">Opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="e80fd-173">Restart</span></span> | <span data-ttu-id="e80fd-174">Een knooppuntfout simuleren door Hallo knooppunt opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="e80fd-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="e80fd-175">Meer informatie [hier](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="e80fd-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="e80fd-176">Aangezien veel acties destructieve, hebt u mogelijk gevraagd u tooconfirm uw bedoeling voordat Hallo actie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e80fd-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="e80fd-177">Elke actie die kan worden uitgevoerd via Service Fabric Explorer kan ook worden uitgevoerd via PowerShell of REST-API, tooenable automation.</span><span class="sxs-lookup"><span data-stu-id="e80fd-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="e80fd-178">U kunt ook een Service Fabric Explorer toocreate toepassingsexemplaren gebruiken voor een bepaalde toepassingstype en -versie.</span><span class="sxs-lookup"><span data-stu-id="e80fd-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="e80fd-179">Type van de toepassing hello kiezen in de structuurweergave hello, en klik vervolgens op Hallo **app-exemplaar maken** koppeling volgende toohello versie u in het rechterdeelvenster Hallo dat wilt.</span><span class="sxs-lookup"><span data-stu-id="e80fd-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![Instantie van een toepassing maken in Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="e80fd-181">Exemplaren van een toepassing gemaakt via Service Fabric Explorer kunnen niet op dit moment parameters worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e80fd-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="e80fd-182">Ze zijn gemaakt met behulp van de standaardwaarden voor parameters.</span><span class="sxs-lookup"><span data-stu-id="e80fd-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="e80fd-183">Verbinding maken met de externe Service Fabric-cluster tooa</span><span class="sxs-lookup"><span data-stu-id="e80fd-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="e80fd-184">Als u Hallo clustereindpunt kent en voldoende machtigingen hebt u toegang tot Service Fabric Explorer vanuit elke browser.</span><span class="sxs-lookup"><span data-stu-id="e80fd-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="e80fd-185">Dit komt doordat het Service Fabric Explorer is gewoon een service die wordt uitgevoerd in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e80fd-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="e80fd-186">Hallo Service Fabric Explorer-eindpunt voor een cluster met externe detecteren</span><span class="sxs-lookup"><span data-stu-id="e80fd-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="e80fd-187">tooreach Service Fabric Explorer voor een bepaald cluster punt uw browser:</span><span class="sxs-lookup"><span data-stu-id="e80fd-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="e80fd-188">http://&lt;uw cluster-eindpunt&gt;: 19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="e80fd-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="e80fd-189">Hallo volledige URL is voor Azure-clusters is ook beschikbaar in Hallo cluster essentials deelvenster Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e80fd-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="e80fd-190">Verbinding maken met de beveiligde cluster tooa</span><span class="sxs-lookup"><span data-stu-id="e80fd-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="e80fd-191">U kunt de client toegang tooyour Service Fabric-cluster met certificaten of met behulp van Azure Active Directory (AAD) beheren.</span><span class="sxs-lookup"><span data-stu-id="e80fd-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="e80fd-192">Als u tooconnect tooService Fabric Explorer op een beveiligde cluster probeert, vervolgens afhankelijk van Hallo clusterconfiguratie zult u worden toopresent vereist een clientcertificaat of meld u aan met AAD.</span><span class="sxs-lookup"><span data-stu-id="e80fd-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e80fd-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e80fd-193">Next steps</span></span>
* [<span data-ttu-id="e80fd-194">Overzicht van testbaarheid</span><span class="sxs-lookup"><span data-stu-id="e80fd-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="e80fd-195">Het beheren van uw Service Fabric-toepassingen in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e80fd-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="e80fd-196">Implementatie van de service Fabric-toepassing met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e80fd-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
