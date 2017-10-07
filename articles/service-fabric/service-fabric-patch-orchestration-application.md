---
title: Service Fabric-toepassing voor patch orchestration aaaAzure | Microsoft Docs
description: Toepassing tooautomate operationele systeem herstellen op een Service Fabric-cluster.
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="0ac32-103">Patch Hallo Windows-besturingssysteem in uw Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="0ac32-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="0ac32-104">Hallo patch orchestration toepassing is een Azure Service Fabric-toepassing die op een Service Fabric-cluster in Azure zonder uitvaltijd patchen besturingssysteem automatiseert.</span><span class="sxs-lookup"><span data-stu-id="0ac32-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="0ac32-105">Hallo patch orchestration app biedt Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="0ac32-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="0ac32-106">**Automatische update besturingssysteeminstallatie**.</span><span class="sxs-lookup"><span data-stu-id="0ac32-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="0ac32-107">Besturingssysteem-updates automatisch gedownload en geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0ac32-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="0ac32-108">Clusterknooppunten worden opgestart naar behoefte zonder uitvaltijd van de cluster.</span><span class="sxs-lookup"><span data-stu-id="0ac32-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="0ac32-109">**Clusterbewust patchen en health integratie**.</span><span class="sxs-lookup"><span data-stu-id="0ac32-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="0ac32-110">Tijdens het toepassen van updates controleert Hallo patch orchestration app Hallo status van de clusterknooppunten Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ac32-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="0ac32-111">Clusterknooppunten worden één knooppunt of één upgradedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="0ac32-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="0ac32-112">Als Hallo status van de cluster hello uitgeschakeld vanwege toohello patch-proces wordt, is patchen gestopt tooprevent toegenomen Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="0ac32-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="0ac32-113">Interne details van Hallo-app</span><span class="sxs-lookup"><span data-stu-id="0ac32-113">Internal details of hello app</span></span>

<span data-ttu-id="0ac32-114">Hallo patch orchestration app bestaat uit Hallo subonderdelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0ac32-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="0ac32-115">**Service Coordinator**: deze stateful service is verantwoordelijk voor:</span><span class="sxs-lookup"><span data-stu-id="0ac32-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="0ac32-116">Windows Update-taak van de coördinerende Hallo op Hallo gehele cluster.</span><span class="sxs-lookup"><span data-stu-id="0ac32-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="0ac32-117">Het opslaan van Hallo resultaat van de voltooide Windows Update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="0ac32-118">**Knooppunt-agentservice**: deze staatloze service wordt uitgevoerd op alle clusterknooppunten van de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0ac32-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="0ac32-119">Hallo-service is verantwoordelijk voor:</span><span class="sxs-lookup"><span data-stu-id="0ac32-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="0ac32-120">Uitvoeren van de bootstrap Hallo knooppunt Agent NTService.</span><span class="sxs-lookup"><span data-stu-id="0ac32-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="0ac32-121">Hallo knooppunt Agent NTService bewaken.</span><span class="sxs-lookup"><span data-stu-id="0ac32-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="0ac32-122">**Knooppunt Agent NTService**: deze Windows NT-service wordt uitgevoerd op een hoger niveau van bevoegdheden (systeem).</span><span class="sxs-lookup"><span data-stu-id="0ac32-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="0ac32-123">Daarentegen Hallo knooppunt Agent-Service en Hallo Coordinator-Service worden uitgevoerd op een lager niveau van bevoegdheden (NETWORK SERVICE).</span><span class="sxs-lookup"><span data-stu-id="0ac32-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="0ac32-124">Hallo-service is verantwoordelijk voor het uitvoeren van Windows Update-taken te volgen op alle clusterknooppunten van Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="0ac32-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="0ac32-125">Het uitschakelen van automatische updates van Windows op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0ac32-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="0ac32-126">Downloaden en installeren van Windows Update is volgens toohello beleid Hallo gebruiker opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0ac32-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="0ac32-127">Opnieuw starten van Hallo machine na installatie van Windows Update.</span><span class="sxs-lookup"><span data-stu-id="0ac32-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="0ac32-128">Hallo-resultaten van Windows updates toohello Coordinator-Service worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="0ac32-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="0ac32-129">Reporting systeemstatusrapporten voor het geval is mislukt na het toewijzen van alle nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="0ac32-130">Hallo patch orchestration app gebruikt Hallo Service Fabric manager system service toodisable herstellen of Hallo knooppunt inschakelen en statuscontroles uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0ac32-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="0ac32-131">Hallo hersteltaak gemaakt door Hallo patch orchestration app houdt Hallo Windows Update uitgevoerd voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0ac32-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ac32-132">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0ac32-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="0ac32-133">Minimaal ondersteunde versie van Service Fabric-runtime</span><span class="sxs-lookup"><span data-stu-id="0ac32-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="0ac32-134">Azure-clusters</span><span class="sxs-lookup"><span data-stu-id="0ac32-134">Azure clusters</span></span>
<span data-ttu-id="0ac32-135">Hallo patch orchestration app moet worden uitgevoerd op Azure clusters met Service Fabric-runtime versie v5.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="0ac32-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="0ac32-136">Zelfstandige on-premises Clusters</span><span class="sxs-lookup"><span data-stu-id="0ac32-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="0ac32-137">Hallo patch orchestration app moet worden uitgevoerd op zelfstandige clusters met Service Fabric-runtime versie v5.6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="0ac32-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="0ac32-138">Hallo reparatie manager-service inschakelen (indien deze niet al actief)</span><span class="sxs-lookup"><span data-stu-id="0ac32-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="0ac32-139">Hallo patch orchestration app vereist Hallo reparatie manager system service toobe is ingeschakeld op het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0ac32-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="0ac32-140">Azure-clusters</span><span class="sxs-lookup"><span data-stu-id="0ac32-140">Azure clusters</span></span>

<span data-ttu-id="0ac32-141">Azure clusters in Hallo zilver duurzaamheid laag hebben Hallo herstellen manager-service is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0ac32-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="0ac32-142">Azure-clusters in Hallo gold duurzaamheid laag mogelijk of mogelijk geen Hallo manager-service voor herstel is ingeschakeld, afhankelijk van wanneer deze clusters zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0ac32-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="0ac32-143">Azure-clusters in de laag Brons duurzaamheid hello, standaard geen Hallo herstellen manager-service is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0ac32-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="0ac32-144">Als het Hallo-service al is ingeschakeld, ziet u draait in Hallo system services gedeelte op Hallo Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="0ac32-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="0ac32-145">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0ac32-145">Azure portal</span></span>
<span data-ttu-id="0ac32-146">U kunt herstel manager vanuit Azure-portal op Hallo tijd voor het instellen van van cluster inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="0ac32-147">Selecteer `Include Repair Manager` onder de optie `Add on features` op Hallo tijdstip van de configuratie van het Cluster.</span><span class="sxs-lookup"><span data-stu-id="0ac32-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="0ac32-148">![Afbeelding van inschakelen van herstel-Manager vanuit Azure-portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="0ac32-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="0ac32-149">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0ac32-149">Azure Resource Manager template</span></span>
<span data-ttu-id="0ac32-150">U kunt ook hello gebruiken [Azure Resource Manager-sjabloon](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable Hallo reparatie manager-service op de nieuwe en bestaande Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="0ac32-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="0ac32-151">Hallo sjabloon ophalen voor Hallo-cluster dat u wilt dat toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0ac32-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="0ac32-152">U kunt voorbeeldsjablonen hello gebruiken of een aangepaste Resource Manager-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="0ac32-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="0ac32-153">tooenable hello reparatie manager service met behulp van [Azure Resource Manager-sjabloon](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="0ac32-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="0ac32-154">Controleer eerst of Hallo `apiversion` te is ingesteld,`2017-07-01-preview` voor Hallo `Microsoft.ServiceFabric/clusters` resource, zoals wordt weergegeven in het volgende codefragment Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ac32-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="0ac32-155">Als dit afwijkt, moet u tooupdate hello `apiVersion` toohello waarde `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="0ac32-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="0ac32-156">Nu Hallo reparatie manager-service inschakelen door toe te voegen Hallo volgende `addonFeatures` sectie na Hallo `fabricSettings` sectie:</span><span class="sxs-lookup"><span data-stu-id="0ac32-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="0ac32-157">Nadat u de sjabloon voor het cluster hebt bijgewerkt met deze wijzigingen, ze toepassen en laten Hallo upgrade voltooien.</span><span class="sxs-lookup"><span data-stu-id="0ac32-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="0ac32-158">U ziet nu Hallo reparatie manager system-service in uw cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0ac32-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="0ac32-159">Wordt aangeroepen `fabric:/System/RepairManagerService` in Hallo system services gedeelte op Hallo Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="0ac32-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="0ac32-160">Zelfstandige lokale clusters</span><span class="sxs-lookup"><span data-stu-id="0ac32-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="0ac32-161">U kunt Hallo [configuratie-instellingen voor Windows-cluster zelfstandige](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable Hallo reparatie manager-service op de nieuwe en bestaande Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="0ac32-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="0ac32-162">tooenable hello reparatie manager-service:</span><span class="sxs-lookup"><span data-stu-id="0ac32-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="0ac32-163">Controleer eerst of Hallo `apiversion` in [algemene clusterconfiguraties](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) te is ingesteld,`04-2017` of hoger:</span><span class="sxs-lookup"><span data-stu-id="0ac32-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="0ac32-164">Nu reparatie manager-service inschakelen door toe te voegen Hallo volgende `addonFeaturres` sectie na Hallo `fabricSettings` sectie zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="0ac32-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="0ac32-165">Uw clustermanifest bijwerken met deze wijzigingen, met behulp van het clustermanifest Hallo bijgewerkt [Maak een nieuw cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) of [upgrade Hallo clusterconfiguratie](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="0ac32-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="0ac32-166">Zodra het Hallo-cluster wordt uitgevoerd met bijgewerkte clustermanifest, nu ziet u Hallo reparatie manager systeemservice in uw cluster, heet `fabric:/System/RepairManagerService`onder sectie in Hallo Service Fabric explorer van systeemservices.</span><span class="sxs-lookup"><span data-stu-id="0ac32-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="0ac32-167">Automatische Update van Windows op alle knooppunten uitschakelen</span><span class="sxs-lookup"><span data-stu-id="0ac32-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="0ac32-168">Automatische updates voor Windows tooavailability gegevensverlies kunnen leiden omdat meerdere clusterknooppunten op Hallo dezelfde opstarten kunnen tijd.</span><span class="sxs-lookup"><span data-stu-id="0ac32-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="0ac32-169">Hallo patch orchestration app standaard pogingen toodisable Hallo automatische Windows-updates op elk clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="0ac32-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="0ac32-170">Als het Hallo-instellingen worden beheerd door een beheerder of Groepsbeleid, raden wij echter instelling Hallo Windows Update-beleid te 'waarschuwen voordat downloaden' expliciet.</span><span class="sxs-lookup"><span data-stu-id="0ac32-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="0ac32-171">Optioneel: Azure diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="0ac32-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="0ac32-172">Clusters met Service Fabric-runtime-versie `5.6.220.9494` en registreert hierboven verzamelen patch orchestration app Logboeken als onderdeel van Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0ac32-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="0ac32-173">U kunt deze stap overslaan als het cluster wordt uitgevoerd op de Service Fabric-runtime-versie `5.6.220.9494` en hoger.</span><span class="sxs-lookup"><span data-stu-id="0ac32-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="0ac32-174">Voor clusters met Service Fabric-runtime-versie lager dan `5.6.220.9494`, logboeken voor Hallo patch orchestration app lokaal op elk van de clusterknooppunten Hallo zijn verzameld.</span><span class="sxs-lookup"><span data-stu-id="0ac32-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="0ac32-175">Het is raadzaam dat u Azure Diagnostics tooupload logboeken van alle knooppunten tooa centrale locatie configureren.</span><span class="sxs-lookup"><span data-stu-id="0ac32-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="0ac32-176">Zie voor meer informatie over het inschakelen van Azure Diagnostics [logboeken verzamelen met behulp van Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="0ac32-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="0ac32-177">Logboeken voor Hallo patch orchestration app worden gegenereerd op Hallo vaste provider id's te volgen:</span><span class="sxs-lookup"><span data-stu-id="0ac32-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="0ac32-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="0ac32-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="0ac32-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="0ac32-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="0ac32-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="0ac32-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="0ac32-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="0ac32-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="0ac32-182">In het Resource Manager-sjabloon goto `EtwEventSourceProviderConfiguration` onder sectie `WadCfg` en Hallo volgende vermeldingen toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="0ac32-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="0ac32-183">Als uw Service Fabric-cluster typen met meerdere knooppunten heeft, wordt de vorige sectie Hallo moet worden toegevoegd voor alle Hallo `WadCfg` secties.</span><span class="sxs-lookup"><span data-stu-id="0ac32-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="0ac32-184">Hallo-app downloaden</span><span class="sxs-lookup"><span data-stu-id="0ac32-184">Download hello app package</span></span>

<span data-ttu-id="0ac32-185">Hallo-toepassing downloaden van Hallo [downloadkoppeling](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="0ac32-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="0ac32-186">Hallo-app configureren</span><span class="sxs-lookup"><span data-stu-id="0ac32-186">Configure hello app</span></span>

<span data-ttu-id="0ac32-187">gedrag van Hallo patch orchestration app Hallo geconfigureerde toomeet uw behoeften kunt worden.</span><span class="sxs-lookup"><span data-stu-id="0ac32-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="0ac32-188">Hallo-standaardwaarden overschrijven door door te geven in de parameter toepassing hello tijdens het maken van de toepassing of update.</span><span class="sxs-lookup"><span data-stu-id="0ac32-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="0ac32-189">Parameters voor de toepassing kunnen worden opgegeven door te geven `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` of `New-ServiceFabricApplication` cmdlets.</span><span class="sxs-lookup"><span data-stu-id="0ac32-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="0ac32-190">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="0ac32-190">**Parameter**</span></span>        |<span data-ttu-id="0ac32-191">**Type**</span><span class="sxs-lookup"><span data-stu-id="0ac32-191">**Type**</span></span>                          | <span data-ttu-id="0ac32-192">**Details**</span><span class="sxs-lookup"><span data-stu-id="0ac32-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="0ac32-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="0ac32-193">MaxResultsToCache</span></span>    |<span data-ttu-id="0ac32-194">Lang</span><span class="sxs-lookup"><span data-stu-id="0ac32-194">Long</span></span>                              | <span data-ttu-id="0ac32-195">Maximum aantal resultaten van de Windows Update, die in de cache moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="0ac32-196">Standaardwaarde is 3000 ervan uitgaande dat de:</span><span class="sxs-lookup"><span data-stu-id="0ac32-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="0ac32-197">-Het aantal knooppunten is 20.</span><span class="sxs-lookup"><span data-stu-id="0ac32-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="0ac32-198">-Het aantal updates dat op een knooppunt per maand gebeurt is vijf.</span><span class="sxs-lookup"><span data-stu-id="0ac32-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="0ac32-199">-Het aantal resultaten per bewerking is 10.</span><span class="sxs-lookup"><span data-stu-id="0ac32-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="0ac32-200">-Resultaten voor de afgelopen drie maanden Hallo moeten worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="0ac32-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="0ac32-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="0ac32-202">Enum</span><span class="sxs-lookup"><span data-stu-id="0ac32-202">Enum</span></span> <br> <span data-ttu-id="0ac32-203">{NodeWise, UpgradeDomainWise}</span><span class="sxs-lookup"><span data-stu-id="0ac32-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="0ac32-204">TaskApprovalPolicy geeft Hallo-beleid dat wordt gebruikt door Hallo Service Coordinator tooinstall Windows-updates via Service Fabric-clusterknooppunten Hallo toobe.</span><span class="sxs-lookup"><span data-stu-id="0ac32-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="0ac32-205">Toegestane waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="0ac32-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="0ac32-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="0ac32-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="0ac32-207">Windows Update is geïnstalleerd, één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="0ac32-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="0ac32-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="0ac32-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="0ac32-209">Windows Update is geïnstalleerd, één upgradedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="0ac32-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="0ac32-210">(Op Hallo maximale, alle Hallo knooppunten die behoren tooan upgradedomein gaan voor Windows Update.)</span><span class="sxs-lookup"><span data-stu-id="0ac32-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="0ac32-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="0ac32-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="0ac32-212">Lang</span><span class="sxs-lookup"><span data-stu-id="0ac32-212">Long</span></span>  <br> <span data-ttu-id="0ac32-213">(Standaard: 1024)</span><span class="sxs-lookup"><span data-stu-id="0ac32-213">(Default: 1024)</span></span>               |<span data-ttu-id="0ac32-214">Maximale grootte van de patch orchestration app registreert in MB, hetgeen kan lokaal op knooppunten worden gehandhaafd.</span><span class="sxs-lookup"><span data-stu-id="0ac32-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="0ac32-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="0ac32-215">WUQuery</span></span>               | <span data-ttu-id="0ac32-216">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0ac32-216">string</span></span><br><span data-ttu-id="0ac32-217">(Standaard: ' IsInstalled = 0 ")</span><span class="sxs-lookup"><span data-stu-id="0ac32-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="0ac32-218">Query tooget Windows-updates.</span><span class="sxs-lookup"><span data-stu-id="0ac32-218">Query tooget Windows updates.</span></span> <span data-ttu-id="0ac32-219">Zie voor meer informatie [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="0ac32-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="0ac32-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="0ac32-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="0ac32-221">BOOL</span><span class="sxs-lookup"><span data-stu-id="0ac32-221">Bool</span></span> <br> <span data-ttu-id="0ac32-222">(standaard: True)</span><span class="sxs-lookup"><span data-stu-id="0ac32-222">(default: True)</span></span>                 | <span data-ttu-id="0ac32-223">Deze vlag kan Windows-besturingssysteem system updates toobe geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0ac32-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="0ac32-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="0ac32-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="0ac32-225">int</span><span class="sxs-lookup"><span data-stu-id="0ac32-225">Int</span></span> <br><span data-ttu-id="0ac32-226">(Standaard: 90).</span><span class="sxs-lookup"><span data-stu-id="0ac32-226">(Default: 90)</span></span>                   | <span data-ttu-id="0ac32-227">Hiermee geeft u Hallo de time-out voor alle Windows Update-bewerking (zoeken of downloaden of installeren).</span><span class="sxs-lookup"><span data-stu-id="0ac32-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="0ac32-228">Als het Hallo-bewerking is niet voltooid in Hallo opgegeven time-out, deze wordt afgebroken.</span><span class="sxs-lookup"><span data-stu-id="0ac32-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="0ac32-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="0ac32-229">WURescheduleCount</span></span>     | <span data-ttu-id="0ac32-230">int</span><span class="sxs-lookup"><span data-stu-id="0ac32-230">Int</span></span> <br> <span data-ttu-id="0ac32-231">(Standaard: 5).</span><span class="sxs-lookup"><span data-stu-id="0ac32-231">(Default: 5)</span></span>                  | <span data-ttu-id="0ac32-232">Hallo kunt u het maximum aantal keren Hallo-service wordt automatisch opnieuw gepland Hallo Windows update als een bewerking blijft mislukken.</span><span class="sxs-lookup"><span data-stu-id="0ac32-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="0ac32-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="0ac32-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="0ac32-234">int</span><span class="sxs-lookup"><span data-stu-id="0ac32-234">Int</span></span> <br><span data-ttu-id="0ac32-235">(Standaard: 30).</span><span class="sxs-lookup"><span data-stu-id="0ac32-235">(Default: 30)</span></span> | <span data-ttu-id="0ac32-236">Hallo-interval op welke Hallo service wordt automatisch opnieuw gepland Hallo Windows update als de fout zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="0ac32-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="0ac32-237">WUFrequency</span></span>           | <span data-ttu-id="0ac32-238">Door komma's gescheiden tekenreeks (standaard: "Wekelijks, woensdag, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="0ac32-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="0ac32-239">Hallo-frequentie voor het installeren van Windows Update.</span><span class="sxs-lookup"><span data-stu-id="0ac32-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="0ac32-240">Hallo-indeling en de mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="0ac32-240">hello format and possible values are:</span></span> <br><span data-ttu-id="0ac32-241">-Maandelijks, DD: mm: ss, bijvoorbeeld, maandelijks, 5, 12: 22:32.</span><span class="sxs-lookup"><span data-stu-id="0ac32-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="0ac32-242">-Per week, dag,: mm: ss, voor bijvoorbeeld wekelijks, dinsdag, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="0ac32-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="0ac32-243">-Dagelijks: mm: ss, bijvoorbeeld dagelijks, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="0ac32-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="0ac32-244">-Geen geeft aan dat de Windows Update mag niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0ac32-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="0ac32-245">Houd er rekening mee dat alle Hallo tijden in UTC zijn.</span><span class="sxs-lookup"><span data-stu-id="0ac32-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="0ac32-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="0ac32-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="0ac32-247">BOOL</span><span class="sxs-lookup"><span data-stu-id="0ac32-247">Bool</span></span> <br><span data-ttu-id="0ac32-248">(Standaard: true)</span><span class="sxs-lookup"><span data-stu-id="0ac32-248">(Default: true)</span></span> | <span data-ttu-id="0ac32-249">Deze vlag instelt, accepteert Hallo toepassing hello eindgebruiker licentie overeenkomst voor Windows Update namens Hallo-eigenaar van het Hallo-machine.</span><span class="sxs-lookup"><span data-stu-id="0ac32-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="0ac32-250">Als u Windows Update toohappen onmiddellijk wilt, stelt `WUFrequency` implementatietijd relatieve toohello-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ac32-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="0ac32-251">Stel bijvoorbeeld dat u hebt een vijf knooppunten test-cluster en plan toodeploy Hallo-app op ongeveer 5:00 uur UTC.</span><span class="sxs-lookup"><span data-stu-id="0ac32-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="0ac32-252">Als u wordt ervan uitgegaan dat de upgrade van de toepassing hello of implementatie duurt voordat 30 minuten op Hallo maximale, stel Hallo WUFrequency als "Dagelijks, 17:30:00."</span><span class="sxs-lookup"><span data-stu-id="0ac32-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="0ac32-253">Hallo-app implementeren</span><span class="sxs-lookup"><span data-stu-id="0ac32-253">Deploy hello app</span></span>

1. <span data-ttu-id="0ac32-254">Voltooi alle Hallo vereiste stappen tooprepare Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0ac32-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="0ac32-255">Hallo patch orchestration app als elke andere Service Fabric-app implementeren.</span><span class="sxs-lookup"><span data-stu-id="0ac32-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="0ac32-256">U kunt het Hallo-app implementeren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ac32-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="0ac32-257">Volg de stappen Hallo in [implementeren en verwijderen van toepassingen via PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="0ac32-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="0ac32-258">tooconfigure hello toepassing tijdens het Hallo van implementatie en pass Hallo `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0ac32-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="0ac32-259">We bieden Hallo script Deploy.ps1 samen met de Hallo-toepassing voor uw gemak.</span><span class="sxs-lookup"><span data-stu-id="0ac32-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="0ac32-260">toouse hello script:</span><span class="sxs-lookup"><span data-stu-id="0ac32-260">toouse hello script:</span></span>

    - <span data-ttu-id="0ac32-261">Verbinding maken met tooa Service Fabric-cluster met behulp van `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="0ac32-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="0ac32-262">Hallo PowerShell-script Deploy.ps1 Hello juiste uitvoeren `ApplicationParameter` waarde.</span><span class="sxs-lookup"><span data-stu-id="0ac32-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="0ac32-263">Houd Hallo script en de map van de toepassing hello PatchOrchestrationApplication Hallo dezelfde directory.</span><span class="sxs-lookup"><span data-stu-id="0ac32-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="0ac32-264">Hallo-app bijwerken</span><span class="sxs-lookup"><span data-stu-id="0ac32-264">Upgrade hello app</span></span>

<span data-ttu-id="0ac32-265">een bestaande patch orchestration-app met behulp van PowerShell, tooupgrade Hallo stappen in [upgrade van de Service Fabric-toepassing met behulp van PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="0ac32-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="0ac32-266">Hallo-app verwijderen</span><span class="sxs-lookup"><span data-stu-id="0ac32-266">Remove hello app</span></span>

<span data-ttu-id="0ac32-267">Volg de stappen Hallo in-toepassing hello tooremove [implementeren en verwijderen van toepassingen via PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="0ac32-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="0ac32-268">We bieden Hallo script Undeploy.ps1 samen met de Hallo-toepassing voor uw gemak.</span><span class="sxs-lookup"><span data-stu-id="0ac32-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="0ac32-269">toouse hello script:</span><span class="sxs-lookup"><span data-stu-id="0ac32-269">toouse hello script:</span></span>

  - <span data-ttu-id="0ac32-270">Verbinding maken met tooa Service Fabric-cluster met behulp van ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="0ac32-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="0ac32-271">Hallo PowerShell-script Undeploy.ps1 uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0ac32-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="0ac32-272">Houd Hallo script en de map van de toepassing hello PatchOrchestrationApplication Hallo dezelfde directory.</span><span class="sxs-lookup"><span data-stu-id="0ac32-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="0ac32-273">Hallo Windows Update-resultaten weergeven</span><span class="sxs-lookup"><span data-stu-id="0ac32-273">View hello Windows Update results</span></span>

<span data-ttu-id="0ac32-274">Hallo patch orchestration app beschrijft de REST-API's toodisplay Hallo historische resultaten toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0ac32-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="0ac32-275">Een voorbeeld van resultaat Hallo JSON:</span><span class="sxs-lookup"><span data-stu-id="0ac32-275">An example of hello result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="0ac32-276">Als er geen update nog is gepland, is Hallo resultaat JSON leeg.</span><span class="sxs-lookup"><span data-stu-id="0ac32-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="0ac32-277">Meld u bij toohello cluster tooquery Windows Update resultaten.</span><span class="sxs-lookup"><span data-stu-id="0ac32-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="0ac32-278">Vervolgens weten Hallo replica adres voor de primaire Hallo Hallo Coordinator-Service en Hallo URL vanuit de browser Hallo bereikt: http://&lt;REPLICA-IP-&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="0ac32-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="0ac32-279">Hallo REST-eindpunt voor Hallo Coordinator-Service heeft een dynamische poort.</span><span class="sxs-lookup"><span data-stu-id="0ac32-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="0ac32-280">toocheck exacte URL hello, raadpleeg dan toohello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="0ac32-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="0ac32-281">Bijvoorbeeld, Hallo resultaten zijn beschikbaar op `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="0ac32-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Afbeelding van REST-eindpunt](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="0ac32-283">Als omgekeerde proxy Hallo op Hallo-cluster is ingeschakeld, kunt u Hallo URL uit buiten Hallo cluster ook openen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="0ac32-284">Hallo-eindpunt dat toobe moet treffer is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="0ac32-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="0ac32-285">tooenable hello omgekeerde proxy op Hallo cluster Hallo stappen in [omgekeerde proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="0ac32-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="0ac32-286">Nadat Hallo omgekeerde proxy is geconfigureerd, kunnen alle micro services in Hallo cluster die een HTTP-eindpunt worden opgevraagd uit buiten Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0ac32-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="0ac32-287">Diagnostische gegevens/health-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="0ac32-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="0ac32-288">Collect patch orchestration applogboeken</span><span class="sxs-lookup"><span data-stu-id="0ac32-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="0ac32-289">Patch orchestration app logboeken worden verzameld als onderdeel van Service Fabric-logboeken van de runtimeversie `5.6.220.9494` en hoger.</span><span class="sxs-lookup"><span data-stu-id="0ac32-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="0ac32-290">Voor clusters met Service Fabric-runtime-versie lager dan `5.6.220.9494`, logboeken kunnen worden verzameld met behulp van een van de volgende methoden Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ac32-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="0ac32-291">Lokaal op elk knooppunt</span><span class="sxs-lookup"><span data-stu-id="0ac32-291">Locally on each node</span></span>

<span data-ttu-id="0ac32-292">Logboeken worden verzameld lokaal op elk clusterknooppunt Service Fabric als Service Fabric-runtime-versie is minder dan `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="0ac32-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="0ac32-293">Hallo locatie tooaccess Hallo Logboeken is \[Service Fabric\_installatie\_station\]:\\PatchOrchestrationApplication\\Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0ac32-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="0ac32-294">Als Service Fabric is geïnstalleerd op station D, Hallo pad is bijvoorbeeld D:\\PatchOrchestrationApplication\\Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0ac32-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="0ac32-295">Centrale locatie</span><span class="sxs-lookup"><span data-stu-id="0ac32-295">Central location</span></span>

<span data-ttu-id="0ac32-296">Als Azure Diagnostics is geconfigureerd als onderdeel van de vereiste stappen, zijn logboeken voor Hallo patch orchestration app beschikbaar in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0ac32-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="0ac32-297">Statusrapporten</span><span class="sxs-lookup"><span data-stu-id="0ac32-297">Health reports</span></span>

<span data-ttu-id="0ac32-298">Hallo patch orchestration app publiceert ook statusrapporten tegen Hallo Service Coordinator of Hallo knooppunt Agent-Service in de volgende gevallen Hallo:</span><span class="sxs-lookup"><span data-stu-id="0ac32-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="0ac32-299">Een Windows Update-bewerking is mislukt</span><span class="sxs-lookup"><span data-stu-id="0ac32-299">A Windows Update operation failed</span></span>

<span data-ttu-id="0ac32-300">Als een Windows Update-bewerking is mislukt op een knooppunt, wordt een statusrapport gegenereerd op basis van Hallo knooppunt Agent-Service.</span><span class="sxs-lookup"><span data-stu-id="0ac32-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="0ac32-301">Details van het statusrapport Hallo bevatten Hallo problematisch knooppuntnaam.</span><span class="sxs-lookup"><span data-stu-id="0ac32-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="0ac32-302">Nadat patching is voltooid op Hallo problematisch knooppunt, wordt Hallo rapport automatisch gewist.</span><span class="sxs-lookup"><span data-stu-id="0ac32-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="0ac32-303">Hallo knooppunt Agent NTService is niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="0ac32-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="0ac32-304">Als Hallo knooppunt Agent NTService niet actief op een knooppunt is, wordt een waarschuwing het niveau statusrapport gegenereerd tegen Hallo knooppunt Agent-Service.</span><span class="sxs-lookup"><span data-stu-id="0ac32-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="0ac32-305">Hallo reparatie manager-service is niet ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="0ac32-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="0ac32-306">Als Hallo reparatie manager-service niet op cluster hello gevonden is, wordt een waarschuwing het niveau statusrapport gegenereerd voor Hallo Coordinator-Service.</span><span class="sxs-lookup"><span data-stu-id="0ac32-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="0ac32-307">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="0ac32-307">Frequently asked questions</span></span>

<span data-ttu-id="0ac32-308">Q.</span><span class="sxs-lookup"><span data-stu-id="0ac32-308">Q.</span></span> <span data-ttu-id="0ac32-309">**Waarom zie ik mijn cluster in een foutstatus wanneer Hallo patch orchestration app wordt uitgevoerd?**</span><span class="sxs-lookup"><span data-stu-id="0ac32-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="0ac32-310">A.</span><span class="sxs-lookup"><span data-stu-id="0ac32-310">A.</span></span> <span data-ttu-id="0ac32-311">Tijdens het installatieproces Hallo Hallo patch orchestration app wordt uitgeschakeld of opnieuw wordt opgestart knooppunten, die tijdelijk leiden tot Hallo status van Hallo cluster tijdelijk niet kunnen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="0ac32-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="0ac32-312">Op basis van beleid voor de toepassing hello hello, ofwel een knooppunt kan uitvallen tijdens een bewerking van de toepassing van patches *of* een hele upgradedomein tegelijkertijd kan uitvallen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="0ac32-313">Hallo knooppunten zijn ingeschakeld boeken door Hallo van Hallo Windows Update-installatie, opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="0ac32-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="0ac32-314">In de Hallo voorbeeld te volgen, Hallo-cluster is gegaan tooan foutstatus tijdelijk omdat twee knooppunten niet actief zijn en Hallo MaxPercentageUnhealthNodes beleid is geschonden.</span><span class="sxs-lookup"><span data-stu-id="0ac32-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="0ac32-315">Hallo-fout is tijdelijk totdat Hallo patchen bewerking uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="0ac32-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![Afbeelding van slecht cluster](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="0ac32-317">Als Hallo probleem zich blijft voordoen, raadpleegt u de sectie Probleemoplossing toohello.</span><span class="sxs-lookup"><span data-stu-id="0ac32-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="0ac32-318">Q.</span><span class="sxs-lookup"><span data-stu-id="0ac32-318">Q.</span></span> <span data-ttu-id="0ac32-319">**Patch orchestration app heeft de waarschuwingsstatus**</span><span class="sxs-lookup"><span data-stu-id="0ac32-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="0ac32-320">A.</span><span class="sxs-lookup"><span data-stu-id="0ac32-320">A.</span></span> <span data-ttu-id="0ac32-321">Controleer de toosee als een statusrapport geboekt tegen Hallo toepassing hello hoofdoorzaak.</span><span class="sxs-lookup"><span data-stu-id="0ac32-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="0ac32-322">Hallo-waarschuwing bevat meestal, details van probleem Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ac32-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="0ac32-323">Als Hallo probleem tijdelijke is, is toepassing hello verwachte tooauto-herstellen van deze status.</span><span class="sxs-lookup"><span data-stu-id="0ac32-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="0ac32-324">Q.</span><span class="sxs-lookup"><span data-stu-id="0ac32-324">Q.</span></span> <span data-ttu-id="0ac32-325">**Wat moet ik doen als mijn cluster beschadigd is en ik toodo urgente besturingssysteem bijwerken moet?**</span><span class="sxs-lookup"><span data-stu-id="0ac32-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="0ac32-326">A.</span><span class="sxs-lookup"><span data-stu-id="0ac32-326">A.</span></span> <span data-ttu-id="0ac32-327">Hallo patch orchestration app installeert updates niet tijdens het Hallo-cluster is beschadigd.</span><span class="sxs-lookup"><span data-stu-id="0ac32-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="0ac32-328">Probeer toobring uw cluster tooa status in orde toounblock Hallo patch orchestration app werkstroom.</span><span class="sxs-lookup"><span data-stu-id="0ac32-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="0ac32-329">Q.</span><span class="sxs-lookup"><span data-stu-id="0ac32-329">Q.</span></span> <span data-ttu-id="0ac32-330">**Waarom patchen tussen verschillende clusters duurt te lang waardoor toorun?**</span><span class="sxs-lookup"><span data-stu-id="0ac32-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="0ac32-331">A.</span><span class="sxs-lookup"><span data-stu-id="0ac32-331">A.</span></span> <span data-ttu-id="0ac32-332">Hallo-tijd die nodig is door Hallo patch orchestration app is voornamelijk afhankelijk van de volgende factoren Hallo:</span><span class="sxs-lookup"><span data-stu-id="0ac32-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="0ac32-333">Hallo beleid Hallo Coordinator-Service.</span><span class="sxs-lookup"><span data-stu-id="0ac32-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="0ac32-334">het standaardbeleid Hallo `NodeWise`, resulteert in het patchen slechts één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="0ac32-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="0ac32-335">Met name in geval van grotere clusters hello wordt aangeraden dat u Hallo `UpgradeDomainWise` beleid tooachieve sneller patchen tussen verschillende clusters.</span><span class="sxs-lookup"><span data-stu-id="0ac32-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="0ac32-336">Hallo aantal updates beschikbaar voor download en installatie.</span><span class="sxs-lookup"><span data-stu-id="0ac32-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="0ac32-337">gemiddelde tijd die nodig is toodownload Hallo en installeren van een update, wat mag niet meer dan een paar uur.</span><span class="sxs-lookup"><span data-stu-id="0ac32-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="0ac32-338">Hallo-prestaties van de VM en netwerkbandbreedte Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ac32-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="0ac32-339">Q.</span><span class="sxs-lookup"><span data-stu-id="0ac32-339">Q.</span></span> <span data-ttu-id="0ac32-340">**Waarom zie ik bepaalde updates in Windows Update-resultaten die zijn verkregen via de REST-api, maar niet onder Hallo geschiedenis van Windows Update op de machine?**</span><span class="sxs-lookup"><span data-stu-id="0ac32-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="0ac32-341">A.</span><span class="sxs-lookup"><span data-stu-id="0ac32-341">A.</span></span> <span data-ttu-id="0ac32-342">Sommige productupdates moeten toobe in de geschiedenis van hun respectieve update/patch gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="0ac32-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="0ac32-343">Bijvoorbeeld: Windows Defender-updates worden niet weergegeven in de geschiedenis van Windows Update op Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0ac32-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="0ac32-344">Disclaimers</span><span class="sxs-lookup"><span data-stu-id="0ac32-344">Disclaimers</span></span>

- <span data-ttu-id="0ac32-345">Hallo patch orchestration app accepteert Hallo eindgebruiker License Agreement van Windows Update namens de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ac32-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="0ac32-346">In de configuratie van de toepassing hello Hallo kan eventueel Hallo-instelling is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0ac32-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="0ac32-347">Hallo patch orchestration app verzamelt telemetrie tootrack gebruik en prestaties.</span><span class="sxs-lookup"><span data-stu-id="0ac32-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="0ac32-348">Hallo toepassingstelemetrie volgt Hallo-instelling van Hallo Service Fabric-runtime van telemetrie (die standaard is ingeschakeld).</span><span class="sxs-lookup"><span data-stu-id="0ac32-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0ac32-349">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="0ac32-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="0ac32-350">Een knooppunt is niet terugkomen tooup status</span><span class="sxs-lookup"><span data-stu-id="0ac32-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="0ac32-351">**Hallo-knooppunt kan blijven steken in een status uitschakelen omdat**:</span><span class="sxs-lookup"><span data-stu-id="0ac32-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="0ac32-352">Er is een veiligheidscontrole in behandeling.</span><span class="sxs-lookup"><span data-stu-id="0ac32-352">A safety check is pending.</span></span> <span data-ttu-id="0ac32-353">tooremedy deze situatie Zorg dat er voldoende knooppunten beschikbaar in een foutloze toestand bevindt zijn.</span><span class="sxs-lookup"><span data-stu-id="0ac32-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="0ac32-354">**Hallo-knooppunt kan blijven steken uitgeschakeld omdat**:</span><span class="sxs-lookup"><span data-stu-id="0ac32-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="0ac32-355">Hallo knooppunt is handmatig uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0ac32-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="0ac32-356">Hallo-knooppunt is uitgeschakeld vanwege tooan lopende Azure-infrastructuur taak.</span><span class="sxs-lookup"><span data-stu-id="0ac32-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="0ac32-357">Hallo-knooppunt is tijdelijk uitgeschakeld door Hallo patch orchestration app toopatch Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0ac32-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="0ac32-358">**Hallo knooppunt kan blijven steken in een status Omlaag omdat**:</span><span class="sxs-lookup"><span data-stu-id="0ac32-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="0ac32-359">Hallo-knooppunt is geplaatst in een status Omlaag handmatig.</span><span class="sxs-lookup"><span data-stu-id="0ac32-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="0ac32-360">Hallo-knooppunt is momenteel door een herstart (die kan worden geactiveerd door Hallo patch orchestration app).</span><span class="sxs-lookup"><span data-stu-id="0ac32-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="0ac32-361">Hallo knooppunt vervalt tooa defecte VM of machine of het netwerk verbindingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="0ac32-362">Updates zijn op sommige knooppunten overgeslagen</span><span class="sxs-lookup"><span data-stu-id="0ac32-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="0ac32-363">Hallo patch orchestration app probeert tooinstall een Windows update volgens toohello nieuwe beleid.</span><span class="sxs-lookup"><span data-stu-id="0ac32-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="0ac32-364">Hallo-service probeert toorecover Hallo knooppunt en Hallo update volgens toohello toepassingsbeleid overslaan.</span><span class="sxs-lookup"><span data-stu-id="0ac32-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="0ac32-365">In dat geval wordt een waarschuwing het niveau statusrapport gegenereerd tegen Hallo knooppunt Agent-Service.</span><span class="sxs-lookup"><span data-stu-id="0ac32-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="0ac32-366">Hallo-resultaat voor Windows Update bevat tevens Hallo mogelijke reden voor het Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="0ac32-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="0ac32-367">Hallo-status van Hallo cluster gaat tooerror terwijl het Hallo-update installeert</span><span class="sxs-lookup"><span data-stu-id="0ac32-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="0ac32-368">Een defecte Windows update kunt naar beneden Hallo status van een toepassing of het cluster op een bepaald knooppunt of upgradedomein brengen.</span><span class="sxs-lookup"><span data-stu-id="0ac32-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="0ac32-369">Hallo patch orchestration app stoppen eventuele latere Windows Update-bewerking totdat Hallo cluster weer in orde is.</span><span class="sxs-lookup"><span data-stu-id="0ac32-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="0ac32-370">Moet een beheerder ingrijpen en bepalen waarom Hallo toepassing of het cluster is geworden vanwege onjuiste tooWindows Update.</span><span class="sxs-lookup"><span data-stu-id="0ac32-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="0ac32-371">Release-opmerkingen:</span><span class="sxs-lookup"><span data-stu-id="0ac32-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="0ac32-372">Versie 1.1.0</span><span class="sxs-lookup"><span data-stu-id="0ac32-372">Version 1.1.0</span></span>
- <span data-ttu-id="0ac32-373">Openbare versie</span><span class="sxs-lookup"><span data-stu-id="0ac32-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="0ac32-374">Versie 1.1.1</span><span class="sxs-lookup"><span data-stu-id="0ac32-374">Version 1.1.1</span></span>
- <span data-ttu-id="0ac32-375">Een bug vast entrypoint van NodeAgentService waardoor de installatie van NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="0ac32-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="0ac32-376">Versie 1.2.0 (laatste)</span><span class="sxs-lookup"><span data-stu-id="0ac32-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="0ac32-377">Werkstroom van oplossingen voor problemen rond systeem opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="0ac32-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="0ac32-378">Fix fout bij het maken van RM taken toowhich statuscontrole tijdens het voorbereiden herstellen taken is niet zoals verwacht gebeurt.</span><span class="sxs-lookup"><span data-stu-id="0ac32-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="0ac32-379">Gewijzigde Hallo opstartmodus voor windows-service POANodeSvc van automatische toodelayed-auto.</span><span class="sxs-lookup"><span data-stu-id="0ac32-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
