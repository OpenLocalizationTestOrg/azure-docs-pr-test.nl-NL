---
title: aaaTroubleshoot uw lokale installatie van de Service Fabric-cluster | Microsoft Docs
description: In dit artikel wordt een reeks suggesties voor het oplossen van uw lokaal ontwikkelcluster behandeld.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="949a9-103">Installatie van uw lokale ontwikkeling oplossen</span><span class="sxs-lookup"><span data-stu-id="949a9-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="949a9-104">Wanneer u een probleem tijdens interactie met uw lokale cluster van de Azure Service Fabric-ontwikkeling, controleert u Hallo suggesties voor mogelijke oplossingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="949a9-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="949a9-105">Setup van clusters</span><span class="sxs-lookup"><span data-stu-id="949a9-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="949a9-106">Kan niet opschonen van Service Fabric-Logboeken</span><span class="sxs-lookup"><span data-stu-id="949a9-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="949a9-107">Probleem</span><span class="sxs-lookup"><span data-stu-id="949a9-107">Problem</span></span>
<span data-ttu-id="949a9-108">Tijdens het Hallo DevClusterSetup script uitvoeren, ziet u een fout als volgt:</span><span class="sxs-lookup"><span data-stu-id="949a9-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="949a9-109">Oplossing</span><span class="sxs-lookup"><span data-stu-id="949a9-109">Solution</span></span>
<span data-ttu-id="949a9-110">Sluit Hallo huidige PowerShell-venster en opent u een nieuwe PowerShell-venster als beheerder.</span><span class="sxs-lookup"><span data-stu-id="949a9-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="949a9-111">Nu moet u kunnen toosuccessfully Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="949a9-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="949a9-112">Verbindingsfouten cluster</span><span class="sxs-lookup"><span data-stu-id="949a9-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="949a9-113">Service Fabric PowerShell-cmdlets worden niet herkend in Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="949a9-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="949a9-114">Probleem</span><span class="sxs-lookup"><span data-stu-id="949a9-114">Problem</span></span>
<span data-ttu-id="949a9-115">Als u toorun Hallo Service Fabric PowerShell-cmdlets, zoals gaat `Connect-ServiceFabricCluster` in een Azure PowerShell-venster het mislukt, vermeld die Hallo-cmdlet wordt niet herkend.</span><span class="sxs-lookup"><span data-stu-id="949a9-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="949a9-116">Hallo reden hiervoor is dat gebruikmaakt van Azure PowerShell Hallo 32-bits versie van Windows PowerShell (zelfs op 64-bits OS-versies), terwijl Hallo Service Fabric-cmdlets alleen werken in 64-bits-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="949a9-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="949a9-117">Oplossing</span><span class="sxs-lookup"><span data-stu-id="949a9-117">Solution</span></span>
<span data-ttu-id="949a9-118">Service Fabric-cmdlets worden altijd uitgevoerd rechtstreeks vanuit Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="949a9-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="949a9-119">meest recente versie van Azure PowerShell Hallo maakt geen een speciale snelkoppeling zodat dit niet langer moet gebeuren.</span><span class="sxs-lookup"><span data-stu-id="949a9-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="949a9-120">Type initialisatie van de uitzondering</span><span class="sxs-lookup"><span data-stu-id="949a9-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="949a9-121">Probleem</span><span class="sxs-lookup"><span data-stu-id="949a9-121">Problem</span></span>
<span data-ttu-id="949a9-122">Wanneer u verbinding toohello cluster in PowerShell maakt, ziet u fout Hallo TypeInitializationException voor System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="949a9-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="949a9-123">Oplossing</span><span class="sxs-lookup"><span data-stu-id="949a9-123">Solution</span></span>
<span data-ttu-id="949a9-124">De variabele path is niet correct ingesteld tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="949a9-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="949a9-125">Afmelden bij Windows en meld u opnieuw aan.</span><span class="sxs-lookup"><span data-stu-id="949a9-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="949a9-126">Dit vernieuwt pad naar uw.</span><span class="sxs-lookup"><span data-stu-id="949a9-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="949a9-127">Cluster-verbinding is mislukt met '-Object is gesloten'</span><span class="sxs-lookup"><span data-stu-id="949a9-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="949a9-128">Probleem</span><span class="sxs-lookup"><span data-stu-id="949a9-128">Problem</span></span>
<span data-ttu-id="949a9-129">Een aanroep van tooConnect-ServiceFabricCluster mislukt met een fout als volgt:</span><span class="sxs-lookup"><span data-stu-id="949a9-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="949a9-130">Oplossing</span><span class="sxs-lookup"><span data-stu-id="949a9-130">Solution</span></span>
<span data-ttu-id="949a9-131">Sluit Hallo huidige PowerShell-venster en opent u een nieuwe PowerShell-venster als beheerder.</span><span class="sxs-lookup"><span data-stu-id="949a9-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="949a9-132">Nu moet u kunnen toosuccessfully verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="949a9-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="949a9-133">Verbinding geweigerd fabric-uitzondering</span><span class="sxs-lookup"><span data-stu-id="949a9-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="949a9-134">Probleem</span><span class="sxs-lookup"><span data-stu-id="949a9-134">Problem</span></span>
<span data-ttu-id="949a9-135">Als u foutopsporing van Visual Studio, krijgt u een FabricConnectionDeniedException-fout.</span><span class="sxs-lookup"><span data-stu-id="949a9-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="949a9-136">Oplossing</span><span class="sxs-lookup"><span data-stu-id="949a9-136">Solution</span></span>
<span data-ttu-id="949a9-137">Deze fout treedt meestal op wanneer u toostart een hostproces van de service handmatig, probeert in plaats van Hallo Service Fabric-runtime toostart zodat het voor u.</span><span class="sxs-lookup"><span data-stu-id="949a9-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="949a9-138">Zorg ervoor dat er geen serviceprojecten die zijn ingesteld als opstartprojecten in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="949a9-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="949a9-139">Alleen de projecten van Service Fabric-toepassing moeten worden ingesteld als opstartprojecten.</span><span class="sxs-lookup"><span data-stu-id="949a9-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="949a9-140">Als na de installatie, uw lokale cluster toobehave abnormaal begint, kunt u het opnieuw met behulp van Hallo lokale cluster manager system lade-toepassing instellen.</span><span class="sxs-lookup"><span data-stu-id="949a9-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="949a9-141">Hiermee verwijdert u Hallo bestaand cluster en een nieuw wachtwoord instellen.</span><span class="sxs-lookup"><span data-stu-id="949a9-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="949a9-142">Houd er rekening mee dat alle toepassingen geïmplementeerde en bijbehorende gegevens worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="949a9-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="949a9-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="949a9-143">Next steps</span></span>
* [<span data-ttu-id="949a9-144">Begrijpen en oplossen van het cluster met systeemstatusrapporten</span><span class="sxs-lookup"><span data-stu-id="949a9-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="949a9-145">Een cluster visualiseren met Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="949a9-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

