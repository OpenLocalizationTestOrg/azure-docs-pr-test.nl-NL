---
title: Azure Service Fabric-patch orchestration toepassing | Microsoft Docs
description: De toepassing te automatiseren besturingssysteem patchen op een Service Fabric-cluster.
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
ms.openlocfilehash: 2c5842822e347113e388d570f6ae603a313944d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="patch-the-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="027af-103">Patch voor het Windows-besturingssysteem in uw Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="027af-103">Patch the Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="027af-104">De patch orchestration-toepassing is een Azure Service Fabric-toepassing die op een Service Fabric-cluster in Azure zonder uitvaltijd patchen besturingssysteem automatiseert.</span><span class="sxs-lookup"><span data-stu-id="027af-104">The patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="027af-105">De patch orchestration-app biedt het volgende:</span><span class="sxs-lookup"><span data-stu-id="027af-105">The patch orchestration app provides the following:</span></span>

- <span data-ttu-id="027af-106">**Automatische update besturingssysteeminstallatie**.</span><span class="sxs-lookup"><span data-stu-id="027af-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="027af-107">Besturingssysteem-updates automatisch gedownload en geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="027af-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="027af-108">Clusterknooppunten worden opgestart naar behoefte zonder uitvaltijd van de cluster.</span><span class="sxs-lookup"><span data-stu-id="027af-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="027af-109">**Clusterbewust patchen en health integratie**.</span><span class="sxs-lookup"><span data-stu-id="027af-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="027af-110">Tijdens het toepassen van updates controleert de patch orchestration app de status van de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="027af-110">While applying updates, the patch orchestration app monitors the health of the cluster nodes.</span></span> <span data-ttu-id="027af-111">Clusterknooppunten worden één knooppunt of één upgradedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="027af-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="027af-112">Als de status van het cluster als gevolg van de patch-proces uitvalt, is patchen om te voorkomen dat het probleem toegenomen gestopt.</span><span class="sxs-lookup"><span data-stu-id="027af-112">If the health of the cluster goes down due to the patching process, patching is stopped to prevent aggravating the problem.</span></span>

## <a name="internal-details-of-the-app"></a><span data-ttu-id="027af-113">Interne details van de app.</span><span class="sxs-lookup"><span data-stu-id="027af-113">Internal details of the app</span></span>

<span data-ttu-id="027af-114">De patch orchestration app bestaat uit de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="027af-114">The patch orchestration app is composed of the following subcomponents:</span></span>

- <span data-ttu-id="027af-115">**Service Coordinator**: deze stateful service is verantwoordelijk voor:</span><span class="sxs-lookup"><span data-stu-id="027af-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="027af-116">Coördinatie van de Windows Update-taak op het hele cluster.</span><span class="sxs-lookup"><span data-stu-id="027af-116">Coordinating the Windows Update job on the entire cluster.</span></span>
    - <span data-ttu-id="027af-117">Het opslaan van het resultaat van de voltooide Windows Update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="027af-117">Storing the result of completed Windows Update operations.</span></span>
- <span data-ttu-id="027af-118">**Knooppunt-agentservice**: deze staatloze service wordt uitgevoerd op alle clusterknooppunten van de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="027af-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="027af-119">De service is verantwoordelijk voor:</span><span class="sxs-lookup"><span data-stu-id="027af-119">The service is responsible for:</span></span>
    - <span data-ttu-id="027af-120">De Agent knooppunt NTService uitvoeren van de bootstrap.</span><span class="sxs-lookup"><span data-stu-id="027af-120">Bootstrapping the Node Agent NTService.</span></span>
    - <span data-ttu-id="027af-121">Bewaken van de Agent knooppunt NTService.</span><span class="sxs-lookup"><span data-stu-id="027af-121">Monitoring the Node Agent NTService.</span></span>
- <span data-ttu-id="027af-122">**Knooppunt Agent NTService**: deze Windows NT-service wordt uitgevoerd op een hoger niveau van bevoegdheden (systeem).</span><span class="sxs-lookup"><span data-stu-id="027af-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="027af-123">Daarentegen de knooppunt Agent-Service en de coördinator-Service worden uitgevoerd op een lager niveau van bevoegdheden (NETWORK SERVICE).</span><span class="sxs-lookup"><span data-stu-id="027af-123">In contrast, the Node Agent Service and the Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="027af-124">De service is verantwoordelijk voor het uitvoeren van de volgende taken in de Windows Update op alle clusterknooppunten:</span><span class="sxs-lookup"><span data-stu-id="027af-124">The service is responsible for performing the following Windows Update jobs on all the cluster nodes:</span></span>
    - <span data-ttu-id="027af-125">Het uitschakelen van automatische Windows-updates op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="027af-125">Disabling automatic Windows Update on the node.</span></span>
    - <span data-ttu-id="027af-126">Downloaden en installeren van Windows Update volgens het beleid voor is de gebruiker opgegeven.</span><span class="sxs-lookup"><span data-stu-id="027af-126">Downloading and installing Windows Update according to the policy the user has provided.</span></span>
    - <span data-ttu-id="027af-127">Opnieuw starten van de computer na installatie van Windows Update.</span><span class="sxs-lookup"><span data-stu-id="027af-127">Restarting the machine post Windows Update installation.</span></span>
    - <span data-ttu-id="027af-128">De resultaten van Windows-updates naar de coördinator-Service geüpload.</span><span class="sxs-lookup"><span data-stu-id="027af-128">Uploading the results of Windows updates to the Coordinator Service.</span></span>
    - <span data-ttu-id="027af-129">Reporting systeemstatusrapporten voor het geval is mislukt na het toewijzen van alle nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="027af-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="027af-130">De patch orchestration-app gebruikmaakt van de Service Fabric reparatie manager service uitschakelen of het inschakelen van het knooppunt en het uitvoeren van statuscontroles.</span><span class="sxs-lookup"><span data-stu-id="027af-130">The patch orchestration app uses the Service Fabric repair manager system service to disable or enable the node and perform health checks.</span></span> <span data-ttu-id="027af-131">De hersteltaak gemaakt door de patch orchestration app houdt de voortgang van de Windows Update voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="027af-131">The repair task created by the patch orchestration app tracks the Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="027af-132">Vereisten</span><span class="sxs-lookup"><span data-stu-id="027af-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="027af-133">Minimaal ondersteunde versie van Service Fabric-runtime</span><span class="sxs-lookup"><span data-stu-id="027af-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="027af-134">Azure-clusters</span><span class="sxs-lookup"><span data-stu-id="027af-134">Azure clusters</span></span>
<span data-ttu-id="027af-135">De patch orchestration-app moet worden uitgevoerd op Azure clusters met Service Fabric-runtime versie v5.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="027af-135">The patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="027af-136">Zelfstandige on-premises Clusters</span><span class="sxs-lookup"><span data-stu-id="027af-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="027af-137">De patch orchestration-app moet worden uitgevoerd op zelfstandige clusters met Service Fabric-runtime versie v5.6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="027af-137">The patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-the-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="027af-138">De reparatie manager-service inschakelen (indien deze niet al actief)</span><span class="sxs-lookup"><span data-stu-id="027af-138">Enable the repair manager service (if it's not running already)</span></span>

<span data-ttu-id="027af-139">De patch orchestration-app is vereist voor de service manager herstellen moet zijn ingeschakeld op het cluster.</span><span class="sxs-lookup"><span data-stu-id="027af-139">The patch orchestration app requires the repair manager system service to be enabled on the cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="027af-140">Azure-clusters</span><span class="sxs-lookup"><span data-stu-id="027af-140">Azure clusters</span></span>

<span data-ttu-id="027af-141">Azure clusters in de laag zilver duurzaamheid hebben de herstel-service manager standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="027af-141">Azure clusters in the silver durability tier have the repair manager service enabled by default.</span></span> <span data-ttu-id="027af-142">Azure-clusters in de laag goud duurzaamheid mogelijk of beschikt niet over de reparatie manager-service is ingeschakeld, afhankelijk van wanneer deze clusters zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="027af-142">Azure clusters in the gold durability tier might or might not have the repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="027af-143">Azure-clusters in de laag Brons duurzaamheid standaard beschikt niet over de reparatie manager service is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="027af-143">Azure clusters in the bronze durability tier, by default, do not have the repair manager service enabled.</span></span> <span data-ttu-id="027af-144">Als de service al is ingeschakeld, ziet u in het gedeelte van de services system op de Service Fabric Explorer draait.</span><span class="sxs-lookup"><span data-stu-id="027af-144">If the service is already enabled, you can see it running in the system services section in the Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="027af-145">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="027af-145">Azure portal</span></span>
<span data-ttu-id="027af-146">U kunt herstel manager vanuit Azure-portal inschakelen op het moment van het instellen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="027af-146">You can enable repair manager from Azure portal at the time of setting up of cluster.</span></span> <span data-ttu-id="027af-147">Selecteer `Include Repair Manager` onder de optie `Add on features` op het moment van de configuratie van het Cluster.</span><span class="sxs-lookup"><span data-stu-id="027af-147">Select `Include Repair Manager` option under `Add on features` at the time of Cluster configuration.</span></span>
<span data-ttu-id="027af-148">![Afbeelding van inschakelen van herstel-Manager vanuit Azure-portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="027af-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="027af-149">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="027af-149">Azure Resource Manager template</span></span>
<span data-ttu-id="027af-150">U kunt ook de [Azure Resource Manager-sjabloon](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) zodat de manager-service voor herstel op nieuwe en bestaande Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="027af-150">Alternatively you can use the [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) to enable the repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="027af-151">Haal de sjabloon voor het cluster dat u wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="027af-151">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="027af-152">U kunt de voorbeeldsjablonen gebruiken of een aangepaste Resource Manager-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="027af-152">You can either use the sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="027af-153">Om in te schakelen reparatie manager service gebruikmaakt [Azure Resource Manager-sjabloon](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="027af-153">To enable the repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="027af-154">Controleer eerst of de `apiversion` is ingesteld op `2017-07-01-preview` voor de `Microsoft.ServiceFabric/clusters` resource, zoals wordt weergegeven in het volgende fragment.</span><span class="sxs-lookup"><span data-stu-id="027af-154">First check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, as shown in the following snippet.</span></span> <span data-ttu-id="027af-155">Als dit afwijkt, moet u bijwerken de `apiVersion` op de waarde `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="027af-155">If it is different, then you need to update the `apiVersion` to the value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="027af-156">Nu de reparatie manager-service inschakelen door het volgende toe te voegen `addonFeatures` sectie na de `fabricSettings` sectie:</span><span class="sxs-lookup"><span data-stu-id="027af-156">Now enable the repair manager service by adding the following `addonFeatures` section after the `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="027af-157">Nadat u de sjabloon voor het cluster hebt bijgewerkt met deze wijzigingen, worden ze toepassen en kunt u de upgrade voltooien.</span><span class="sxs-lookup"><span data-stu-id="027af-157">After you have updated your cluster template with these changes, apply them and let the upgrade finish.</span></span> <span data-ttu-id="027af-158">U ziet nu de reparatie manager systeemservice in uw cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="027af-158">You can now see the repair manager system service running in your cluster.</span></span> <span data-ttu-id="027af-159">Wordt aangeroepen `fabric:/System/RepairManagerService` in het gedeelte van de services system op de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="027af-159">It is called `fabric:/System/RepairManagerService` in the system services section in the Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="027af-160">Zelfstandige lokale clusters</span><span class="sxs-lookup"><span data-stu-id="027af-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="027af-161">U kunt de [configuratie-instellingen voor Windows-cluster zelfstandige](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) zodat de reparatie manager-service op de nieuwe en bestaande Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="027af-161">You can use the [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) to enable the repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="027af-162">De reparatie manager-service inschakelen:</span><span class="sxs-lookup"><span data-stu-id="027af-162">To enable the repair manager service:</span></span>

1. <span data-ttu-id="027af-163">Controleer eerst of de `apiversion` in [algemene clusterconfiguraties](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is ingesteld op `04-2017` of hoger:</span><span class="sxs-lookup"><span data-stu-id="027af-163">First check that the `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set to `04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="027af-164">Nu reparatie manager-service inschakelen door het volgende toe te voegen `addonFeaturres` sectie na de `fabricSettings` sectie zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="027af-164">Now enable repair manager service by adding the following `addonFeaturres` section after the `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="027af-165">Uw clustermanifest bijwerken met deze wijzigingen, met behulp van de bijgewerkte clustermanifest [Maak een nieuw cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) of [upgrade van de clusterconfiguratie](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="027af-165">Update your cluster manifest with these changes, using the updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade the cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="027af-166">Zodra het cluster wordt uitgevoerd met bijgewerkte clustermanifest, zoals u ziet de reparatie manager systeemservice in het cluster die is aangeroepen met `fabric:/System/RepairManagerService`onder sectie in Service Fabric explorer van systeemservices.</span><span class="sxs-lookup"><span data-stu-id="027af-166">Once the cluster is running with updated cluster manifest, you can now see the repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in the Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="027af-167">Automatische Update van Windows op alle knooppunten uitschakelen</span><span class="sxs-lookup"><span data-stu-id="027af-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="027af-168">Automatische Windows-updates kunnen leiden tot verlies van beschikbaarheid omdat meerdere clusterknooppunten tegelijkertijd kunnen opnieuw worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="027af-168">Automatic Windows updates might lead to availability loss because multiple cluster nodes can restart at the same time.</span></span> <span data-ttu-id="027af-169">De patch orchestration-app probeert standaard, u de automatische Update van Windows op elk clusterknooppunt uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="027af-169">The patch orchestration app, by default, tries to disable the automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="027af-170">Echter, als de instellingen worden beheerd door een beheerder of Groepsbeleid, raden wij aan het beleid van Windows Update naar 'Waarschuwen voordat downloaden' expliciet instellen.</span><span class="sxs-lookup"><span data-stu-id="027af-170">However, if the settings are managed by an administrator or group policy, we recommend setting the Windows Update policy to “Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="027af-171">Optioneel: Azure diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="027af-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="027af-172">Clusters met Service Fabric-runtime-versie `5.6.220.9494` en registreert hierboven verzamelen patch orchestration app Logboeken als onderdeel van Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="027af-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="027af-173">U kunt deze stap overslaan als het cluster wordt uitgevoerd op de Service Fabric-runtime-versie `5.6.220.9494` en hoger.</span><span class="sxs-lookup"><span data-stu-id="027af-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="027af-174">Voor clusters met Service Fabric-runtime-versie lager dan `5.6.220.9494`, logboeken voor de orchestration patch app lokaal worden verzameld op elk van de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="027af-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for the patch orchestration app are collected locally on each of the cluster nodes.</span></span>
<span data-ttu-id="027af-175">Het is raadzaam dat u Azure Diagnostics om te uploaden van Logboeken van alle knooppunten op een centrale locatie configureren.</span><span class="sxs-lookup"><span data-stu-id="027af-175">We recommend that you configure Azure Diagnostics to upload logs from all nodes to a central location.</span></span>

<span data-ttu-id="027af-176">Zie voor meer informatie over het inschakelen van Azure Diagnostics [logboeken verzamelen met behulp van Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="027af-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="027af-177">Logboeken voor de orchestration-app patch worden gegenereerd op de volgende vaste provider id's:</span><span class="sxs-lookup"><span data-stu-id="027af-177">Logs for the patch orchestration app are generated on the following fixed provider IDs:</span></span>

- <span data-ttu-id="027af-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="027af-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="027af-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="027af-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="027af-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="027af-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="027af-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="027af-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="027af-182">In het Resource Manager-sjabloon goto `EtwEventSourceProviderConfiguration` onder sectie `WadCfg` en voeg de volgende items:</span><span class="sxs-lookup"><span data-stu-id="027af-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add the following entries:</span></span>

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
> <span data-ttu-id="027af-183">Als uw Service Fabric-cluster typen met meerdere knooppunten heeft, wordt de vorige sectie moet worden toegevoegd voor alle de `WadCfg` secties.</span><span class="sxs-lookup"><span data-stu-id="027af-183">If your Service Fabric cluster has multiple node types, then the previous section must be added for all the `WadCfg` sections.</span></span>

## <a name="download-the-app-package"></a><span data-ttu-id="027af-184">Download het apppakket</span><span class="sxs-lookup"><span data-stu-id="027af-184">Download the app package</span></span>

<span data-ttu-id="027af-185">Downloaden van de toepassing van de [downloadkoppeling](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="027af-185">Download the application from the [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-the-app"></a><span data-ttu-id="027af-186">De app configureren</span><span class="sxs-lookup"><span data-stu-id="027af-186">Configure the app</span></span>

<span data-ttu-id="027af-187">Het gedrag van de patch orchestration-app kan worden geconfigureerd om te voldoen aan uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="027af-187">The behavior of the patch orchestration app can be configured to meet your needs.</span></span> <span data-ttu-id="027af-188">De standaardwaarden overschrijven door door te geven in de parameter van de toepassing tijdens het maken van de toepassing of update.</span><span class="sxs-lookup"><span data-stu-id="027af-188">Override the default values by passing in the application parameter during application creation or update.</span></span> <span data-ttu-id="027af-189">Parameters voor de toepassing kunnen worden opgegeven door te geven `ApplicationParameter` naar de `Start-ServiceFabricApplicationUpgrade` of `New-ServiceFabricApplication` cmdlets.</span><span class="sxs-lookup"><span data-stu-id="027af-189">Application parameters can be provided by specifying `ApplicationParameter` to the `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="027af-190">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="027af-190">**Parameter**</span></span>        |<span data-ttu-id="027af-191">**Type**</span><span class="sxs-lookup"><span data-stu-id="027af-191">**Type**</span></span>                          | <span data-ttu-id="027af-192">**Details**</span><span class="sxs-lookup"><span data-stu-id="027af-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="027af-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="027af-193">MaxResultsToCache</span></span>    |<span data-ttu-id="027af-194">Lang</span><span class="sxs-lookup"><span data-stu-id="027af-194">Long</span></span>                              | <span data-ttu-id="027af-195">Maximum aantal resultaten van de Windows Update, die in de cache moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="027af-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="027af-196">Standaardwaarde is 3000 ervan uitgaande dat de:</span><span class="sxs-lookup"><span data-stu-id="027af-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="027af-197">-Het aantal knooppunten is 20.</span><span class="sxs-lookup"><span data-stu-id="027af-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="027af-198">-Het aantal updates dat op een knooppunt per maand gebeurt is vijf.</span><span class="sxs-lookup"><span data-stu-id="027af-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="027af-199">-Het aantal resultaten per bewerking is 10.</span><span class="sxs-lookup"><span data-stu-id="027af-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="027af-200">-Resultaten voor de afgelopen drie maanden moeten worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="027af-200">- Results for the past three months should be stored.</span></span> |
|<span data-ttu-id="027af-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="027af-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="027af-202">Enum</span><span class="sxs-lookup"><span data-stu-id="027af-202">Enum</span></span> <br> <span data-ttu-id="027af-203">{NodeWise, UpgradeDomainWise}</span><span class="sxs-lookup"><span data-stu-id="027af-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="027af-204">TaskApprovalPolicy geeft aan het beleid dat moet worden gebruikt door de coördinator-Service voor het installeren van Windows-updates over de clusterknooppunten Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="027af-204">TaskApprovalPolicy indicates the policy that is to be used by the Coordinator Service to install Windows updates across the Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="027af-205">Toegestane waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="027af-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="027af-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="027af-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="027af-207">Windows Update is geïnstalleerd, één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="027af-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="027af-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="027af-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="027af-209">Windows Update is geïnstalleerd, één upgradedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="027af-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="027af-210">(Het maximum is bereikt, alle knooppunten van een upgradedomein gaan voor Windows Update.)</span><span class="sxs-lookup"><span data-stu-id="027af-210">(At the maximum, all the nodes belonging to an upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="027af-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="027af-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="027af-212">Lang</span><span class="sxs-lookup"><span data-stu-id="027af-212">Long</span></span>  <br> <span data-ttu-id="027af-213">(Standaard: 1024)</span><span class="sxs-lookup"><span data-stu-id="027af-213">(Default: 1024)</span></span>               |<span data-ttu-id="027af-214">Maximale grootte van de patch orchestration app registreert in MB, hetgeen kan lokaal op knooppunten worden gehandhaafd.</span><span class="sxs-lookup"><span data-stu-id="027af-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="027af-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="027af-215">WUQuery</span></span>               | <span data-ttu-id="027af-216">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="027af-216">string</span></span><br><span data-ttu-id="027af-217">(Standaard: ' IsInstalled = 0 ")</span><span class="sxs-lookup"><span data-stu-id="027af-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="027af-218">De query voor het ophalen van Windows-updates.</span><span class="sxs-lookup"><span data-stu-id="027af-218">Query to get Windows updates.</span></span> <span data-ttu-id="027af-219">Zie voor meer informatie [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="027af-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="027af-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="027af-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="027af-221">BOOL</span><span class="sxs-lookup"><span data-stu-id="027af-221">Bool</span></span> <br> <span data-ttu-id="027af-222">(standaard: True)</span><span class="sxs-lookup"><span data-stu-id="027af-222">(default: True)</span></span>                 | <span data-ttu-id="027af-223">Deze vlag kan updates voor Windows-besturingssysteem moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="027af-223">This flag allows Windows operating system updates to be installed.</span></span>            |
| <span data-ttu-id="027af-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="027af-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="027af-225">int</span><span class="sxs-lookup"><span data-stu-id="027af-225">Int</span></span> <br><span data-ttu-id="027af-226">(Standaard: 90).</span><span class="sxs-lookup"><span data-stu-id="027af-226">(Default: 90)</span></span>                   | <span data-ttu-id="027af-227">Hiermee geeft u de time-out voor een Windows Update-bewerking (zoeken of downloaden of installeren).</span><span class="sxs-lookup"><span data-stu-id="027af-227">Specifies the timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="027af-228">Als de bewerking is niet voltooid binnen de opgegeven time-out, wordt het afgebroken.</span><span class="sxs-lookup"><span data-stu-id="027af-228">If the operation is not completed within the specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="027af-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="027af-229">WURescheduleCount</span></span>     | <span data-ttu-id="027af-230">int</span><span class="sxs-lookup"><span data-stu-id="027af-230">Int</span></span> <br> <span data-ttu-id="027af-231">(Standaard: 5).</span><span class="sxs-lookup"><span data-stu-id="027af-231">(Default: 5)</span></span>                  | <span data-ttu-id="027af-232">Het maximum aantal keren dat de service opnieuw gepland voor de Windows update als een bewerking blijft mislukken.</span><span class="sxs-lookup"><span data-stu-id="027af-232">The maximum number of times the service reschedules the Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="027af-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="027af-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="027af-234">int</span><span class="sxs-lookup"><span data-stu-id="027af-234">Int</span></span> <br><span data-ttu-id="027af-235">(Standaard: 30).</span><span class="sxs-lookup"><span data-stu-id="027af-235">(Default: 30)</span></span> | <span data-ttu-id="027af-236">Het interval waarmee de service wordt automatisch opnieuw gepland Windows update als de fout zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="027af-236">The interval at which the service reschedules the Windows update in case failure persists.</span></span> |
| <span data-ttu-id="027af-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="027af-237">WUFrequency</span></span>           | <span data-ttu-id="027af-238">Door komma's gescheiden tekenreeks (standaard: "Wekelijks, woensdag, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="027af-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="027af-239">De frequentie voor het installeren van Windows Update.</span><span class="sxs-lookup"><span data-stu-id="027af-239">The frequency for installing Windows Update.</span></span> <span data-ttu-id="027af-240">De indeling en de mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="027af-240">The format and possible values are:</span></span> <br><span data-ttu-id="027af-241">-Maandelijks, DD: mm: ss, bijvoorbeeld, maandelijks, 5, 12: 22:32.</span><span class="sxs-lookup"><span data-stu-id="027af-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="027af-242">-Per week, dag,: mm: ss, voor bijvoorbeeld wekelijks, dinsdag, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="027af-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="027af-243">-Dagelijks: mm: ss, bijvoorbeeld dagelijks, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="027af-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="027af-244">-Geen geeft aan dat de Windows Update mag niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="027af-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="027af-245">Houd er rekening mee dat alle tijden in UTC zijn.</span><span class="sxs-lookup"><span data-stu-id="027af-245">Note that all the times are in UTC.</span></span>|
| <span data-ttu-id="027af-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="027af-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="027af-247">BOOL</span><span class="sxs-lookup"><span data-stu-id="027af-247">Bool</span></span> <br><span data-ttu-id="027af-248">(Standaard: true)</span><span class="sxs-lookup"><span data-stu-id="027af-248">(Default: true)</span></span> | <span data-ttu-id="027af-249">Deze vlag instelt, wordt in de toepassing de eindgebruiker-licentie voor Windows Update accepteert namens de eigenaar van de machine.</span><span class="sxs-lookup"><span data-stu-id="027af-249">By setting this flag, the application accepts the End-User License Agreement for Windows Update on behalf of the owner of the machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="027af-250">Als u Windows Update gebeurt onmiddellijk wilt, stelt `WUFrequency` ten opzichte van de tijd van de implementatie van toepassing.</span><span class="sxs-lookup"><span data-stu-id="027af-250">If you want Windows Update to happen immediately, set `WUFrequency` relative to the application deployment time.</span></span> <span data-ttu-id="027af-251">Stel bijvoorbeeld dat u hebt een testcluster met vijf knooppunten en plan de implementatie van de app op ongeveer 5:00 uur UTC.</span><span class="sxs-lookup"><span data-stu-id="027af-251">For example, suppose that you have a five-node test cluster and plan to deploy the app at around 5:00 PM UTC.</span></span> <span data-ttu-id="027af-252">Als u wordt ervan uitgegaan dat de upgrade van de toepassing of implementatie 30 minuten maximaal duurt, ingesteld op de WUFrequency "Dagelijks, 17:30:00."</span><span class="sxs-lookup"><span data-stu-id="027af-252">If you assume that the application upgrade or deployment takes 30 minutes at the maximum, set the WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="027af-253">De app implementeren</span><span class="sxs-lookup"><span data-stu-id="027af-253">Deploy the app</span></span>

1. <span data-ttu-id="027af-254">Voltooi de vereiste stappen voor het voorbereiden van het cluster.</span><span class="sxs-lookup"><span data-stu-id="027af-254">Finish all the prerequisite steps to prepare the cluster.</span></span>
2. <span data-ttu-id="027af-255">Implementeer de patch orchestration-app als elke andere Service Fabric-app.</span><span class="sxs-lookup"><span data-stu-id="027af-255">Deploy the patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="027af-256">U kunt de app implementeren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="027af-256">You can deploy the app by using PowerShell.</span></span> <span data-ttu-id="027af-257">Volg de stappen in [implementeren en verwijderen van toepassingen via PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="027af-257">Follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="027af-258">De toepassing configureren op het moment van implementatie, de `ApplicationParamater` naar de `New-ServiceFabricApplication` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="027af-258">To configure the application at the time of deployment, pass the `ApplicationParamater` to the `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="027af-259">We bieden het script Deploy.ps1 samen met de toepassing voor uw gemak.</span><span class="sxs-lookup"><span data-stu-id="027af-259">For your convenience, we’ve provided the script Deploy.ps1 along with the application.</span></span> <span data-ttu-id="027af-260">Het script gebruiken:</span><span class="sxs-lookup"><span data-stu-id="027af-260">To use the script:</span></span>

    - <span data-ttu-id="027af-261">Verbinding maken met een Service Fabric-cluster met `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="027af-261">Connect to a Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="027af-262">Voer het PowerShell-script Deploy.ps1 met de juiste `ApplicationParameter` waarde.</span><span class="sxs-lookup"><span data-stu-id="027af-262">Execute the PowerShell script Deploy.ps1 with the appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="027af-263">Houd het script en de map application PatchOrchestrationApplication in dezelfde map.</span><span class="sxs-lookup"><span data-stu-id="027af-263">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="upgrade-the-app"></a><span data-ttu-id="027af-264">De app bijwerken</span><span class="sxs-lookup"><span data-stu-id="027af-264">Upgrade the app</span></span>

<span data-ttu-id="027af-265">Als u een bestaande app van de patch-orchestration upgraden met behulp van PowerShell, volg de stappen in [upgrade van de Service Fabric-toepassing met behulp van PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="027af-265">To upgrade an existing patch orchestration app by using PowerShell, follow the steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-the-app"></a><span data-ttu-id="027af-266">De app verwijderen</span><span class="sxs-lookup"><span data-stu-id="027af-266">Remove the app</span></span>

<span data-ttu-id="027af-267">Volg de stappen in de toepassing te verwijderen, [implementeren en verwijderen van toepassingen via PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="027af-267">To remove the application, follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="027af-268">We bieden het script Undeploy.ps1 samen met de toepassing voor uw gemak.</span><span class="sxs-lookup"><span data-stu-id="027af-268">For your convenience, we've provided the script Undeploy.ps1 along with the application.</span></span> <span data-ttu-id="027af-269">Het script gebruiken:</span><span class="sxs-lookup"><span data-stu-id="027af-269">To use the script:</span></span>

  - <span data-ttu-id="027af-270">Verbinding maken met een Service Fabric-cluster met ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="027af-270">Connect to a Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="027af-271">Voer het PowerShell-script Undeploy.ps1.</span><span class="sxs-lookup"><span data-stu-id="027af-271">Execute the PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="027af-272">Houd het script en de map application PatchOrchestrationApplication in dezelfde map.</span><span class="sxs-lookup"><span data-stu-id="027af-272">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="view-the-windows-update-results"></a><span data-ttu-id="027af-273">Bekijk de resultaten van Windows Update</span><span class="sxs-lookup"><span data-stu-id="027af-273">View the Windows Update results</span></span>

<span data-ttu-id="027af-274">De patch orchestration app beschrijft de REST-API's om de historische resultaten voor de gebruiker weer te geven.</span><span class="sxs-lookup"><span data-stu-id="027af-274">The patch orchestration app exposes REST APIs to display the historical results to the user.</span></span> <span data-ttu-id="027af-275">Een voorbeeld van het resultaat JSON:</span><span class="sxs-lookup"><span data-stu-id="027af-275">An example of the result JSON:</span></span>
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
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of the issues that are included in this update, see the associated Microsoft Knowledge Base article. After you install this update, you may have to restart your system.",
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
<span data-ttu-id="027af-276">Als er geen update nog is gepland, is het resultaat JSON is leeg.</span><span class="sxs-lookup"><span data-stu-id="027af-276">If no update is scheduled yet, the result JSON is empty.</span></span>

<span data-ttu-id="027af-277">Meld u aan bij het cluster om de query Windows Update resultaten.</span><span class="sxs-lookup"><span data-stu-id="027af-277">Log in to the cluster to query Windows Update results.</span></span> <span data-ttu-id="027af-278">Vervolgens weten het adres van de replica voor de primaire van de Service Coordinator en klik op de URL van de browser: http://&lt;REPLICA-IP-&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="027af-278">Then find out the replica address for the primary of the Coordinator Service, and hit the URL from the browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="027af-279">De REST-eindpunt voor de coördinator-Service heeft een dynamische poort.</span><span class="sxs-lookup"><span data-stu-id="027af-279">The REST endpoint for the Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="027af-280">Als u wilt de exacte URL controleren, raadpleegt u de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="027af-280">To check the exact URL, refer to the Service Fabric Explorer.</span></span> <span data-ttu-id="027af-281">Bijvoorbeeld, de resultaten zijn beschikbaar op `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="027af-281">For example, the results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Afbeelding van REST-eindpunt](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="027af-283">Als de omgekeerde proxy is ingeschakeld op het cluster, kunt u de URL van buiten het cluster ook openen.</span><span class="sxs-lookup"><span data-stu-id="027af-283">If the reverse proxy is enabled on the cluster, you can access the URL from outside of the cluster as well.</span></span>
<span data-ttu-id="027af-284">Het eindpunt dat moet worden bereikt is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="027af-284">The endpoint that needs to be hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="027af-285">Volg de stappen in zodat de omgekeerde proxy op het cluster [omgekeerde proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="027af-285">To enable the reverse proxy on the cluster, follow the steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="027af-286">Nadat de omgekeerde proxy is geconfigureerd, zijn alle micro services in het cluster die een HTTP-eindpunt adresseerbare van buiten het cluster.</span><span class="sxs-lookup"><span data-stu-id="027af-286">After the reverse proxy is configured, all micro services in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="027af-287">Diagnostische gegevens/health-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="027af-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="027af-288">Collect patch orchestration applogboeken</span><span class="sxs-lookup"><span data-stu-id="027af-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="027af-289">Patch orchestration app logboeken worden verzameld als onderdeel van Service Fabric-logboeken van de runtimeversie `5.6.220.9494` en hoger.</span><span class="sxs-lookup"><span data-stu-id="027af-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="027af-290">Voor clusters met Service Fabric-runtime-versie lager dan `5.6.220.9494`, logboeken kunnen worden verzameld met behulp van een van de volgende methoden.</span><span class="sxs-lookup"><span data-stu-id="027af-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of the following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="027af-291">Lokaal op elk knooppunt</span><span class="sxs-lookup"><span data-stu-id="027af-291">Locally on each node</span></span>

<span data-ttu-id="027af-292">Logboeken worden verzameld lokaal op elk clusterknooppunt Service Fabric als Service Fabric-runtime-versie is minder dan `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="027af-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="027af-293">De locatie voor toegang tot de logboeken is \[Service Fabric\_installatie\_station\]:\\PatchOrchestrationApplication\\Logboeken.</span><span class="sxs-lookup"><span data-stu-id="027af-293">The location to access the logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="027af-294">Als Service Fabric is geïnstalleerd op station D, het pad is bijvoorbeeld D:\\PatchOrchestrationApplication\\Logboeken.</span><span class="sxs-lookup"><span data-stu-id="027af-294">For example, if Service Fabric is installed on drive D, the path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="027af-295">Centrale locatie</span><span class="sxs-lookup"><span data-stu-id="027af-295">Central location</span></span>

<span data-ttu-id="027af-296">Als Azure Diagnostics is geconfigureerd als onderdeel van de vereiste stappen, zijn logboeken voor de orchestration-app patch beschikbaar in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="027af-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for the patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="027af-297">Statusrapporten</span><span class="sxs-lookup"><span data-stu-id="027af-297">Health reports</span></span>

<span data-ttu-id="027af-298">De patch orchestration-app publiceert ook statusrapporten op basis van de coördinator-Service of de Agent-Service van het knooppunt in de volgende gevallen:</span><span class="sxs-lookup"><span data-stu-id="027af-298">The patch orchestration app also publishes health reports against the Coordinator Service or the Node Agent Service in the following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="027af-299">Een Windows Update-bewerking is mislukt</span><span class="sxs-lookup"><span data-stu-id="027af-299">A Windows Update operation failed</span></span>

<span data-ttu-id="027af-300">Als een Windows Update-bewerking is mislukt op een knooppunt, wordt een statusrapport gegenereerd op basis van de Agent-Service van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="027af-300">If a Windows Update operation fails on a node, a health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="027af-301">Details van het statusrapport bevatten problematisch knooppuntnaam.</span><span class="sxs-lookup"><span data-stu-id="027af-301">Details of the health report contain the problematic node name.</span></span>

<span data-ttu-id="027af-302">Nadat patching is voltooid op het knooppunt problematisch, wordt het rapport automatisch gewist.</span><span class="sxs-lookup"><span data-stu-id="027af-302">After patching is successfully completed on the problematic node, the report is automatically cleared.</span></span>

#### <a name="the-node-agent-ntservice-is-down"></a><span data-ttu-id="027af-303">De Agent knooppunt NTService is niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="027af-303">The Node Agent NTService is down</span></span>

<span data-ttu-id="027af-304">Als de Agent knooppunt NTService niet actief op een knooppunt is, wordt een waarschuwing het niveau statusrapport gegenereerd op basis van de Agent-Service van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="027af-304">If the Node Agent NTService is down on a node, a warning-level health report is generated against the Node Agent Service.</span></span>

#### <a name="the-repair-manager-service-is-not-enabled"></a><span data-ttu-id="027af-305">De reparatie manager-service is niet ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="027af-305">The repair manager service is not enabled</span></span>

<span data-ttu-id="027af-306">Als de reparatie manager-service niet in het cluster gevonden is, wordt een waarschuwing het niveau statusrapport gegenereerd voor de coördinator-Service.</span><span class="sxs-lookup"><span data-stu-id="027af-306">If the repair manager service is not found on the cluster, a warning-level health report is generated for the Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="027af-307">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="027af-307">Frequently asked questions</span></span>

<span data-ttu-id="027af-308">Q.</span><span class="sxs-lookup"><span data-stu-id="027af-308">Q.</span></span> <span data-ttu-id="027af-309">**Waarom zie ik mijn cluster in een foutstatus wanneer de patch orchestration-app wordt uitgevoerd?**</span><span class="sxs-lookup"><span data-stu-id="027af-309">**Why do I see my cluster in an error state when the patch orchestration app is running?**</span></span>

<span data-ttu-id="027af-310">A.</span><span class="sxs-lookup"><span data-stu-id="027af-310">A.</span></span> <span data-ttu-id="027af-311">Tijdens het installatieproces de patch orchestration-app wordt uitgeschakeld of opnieuw wordt opgestart knooppunten, die tijdelijk leiden tot de status van het cluster tijdelijk niet kunnen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="027af-311">During the installation process, the patch orchestration app disables or restarts nodes, which can temporarily result in the health of the cluster going down.</span></span>

<span data-ttu-id="027af-312">Op basis van het beleid voor de toepassing, ofwel een knooppunt kan uitvallen tijdens een bewerking van de toepassing van patches *of* een hele upgradedomein tegelijkertijd kan uitvallen.</span><span class="sxs-lookup"><span data-stu-id="027af-312">Based on the policy for the application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="027af-313">Aan het einde van de Windows Update-installatie, de knooppunten zijn ingeschakeld boeken opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="027af-313">By the end of the Windows Update installation, the nodes are reenabled post restart.</span></span>

<span data-ttu-id="027af-314">In het volgende voorbeeld wordt het cluster is verzonden naar een foutstatus tijdelijk omdat twee knooppunten zijn en het beleid MaxPercentageUnhealthNodes is geschonden.</span><span class="sxs-lookup"><span data-stu-id="027af-314">In the following example, the cluster went to an error state temporarily because two nodes were down and the MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="027af-315">De fout is tijdelijk totdat de toepassing van patches bewerking uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="027af-315">The error is temporary until the patching operation is ongoing.</span></span>

![Afbeelding van slecht cluster](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="027af-317">Als het probleem zich blijft voordoen, raadpleegt u de sectie probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="027af-317">If the issue persists, refer to the Troubleshooting section.</span></span>

<span data-ttu-id="027af-318">Q.</span><span class="sxs-lookup"><span data-stu-id="027af-318">Q.</span></span> <span data-ttu-id="027af-319">**Patch orchestration app heeft de waarschuwingsstatus**</span><span class="sxs-lookup"><span data-stu-id="027af-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="027af-320">A.</span><span class="sxs-lookup"><span data-stu-id="027af-320">A.</span></span> <span data-ttu-id="027af-321">Controleer of een statusrapport geplaatst voor de toepassing de hoofdoorzaak is.</span><span class="sxs-lookup"><span data-stu-id="027af-321">Check to see if a health report posted against the application is the root cause.</span></span> <span data-ttu-id="027af-322">De waarschuwing bevat meestal, details van het probleem.</span><span class="sxs-lookup"><span data-stu-id="027af-322">Usually, the warning contains details of the problem.</span></span> <span data-ttu-id="027af-323">Als het probleem tijdelijke is, wordt de toepassing automatisch herstellen van deze status verwacht.</span><span class="sxs-lookup"><span data-stu-id="027af-323">If the issue is transient, the application is expected to auto-recover from this state.</span></span>

<span data-ttu-id="027af-324">Q.</span><span class="sxs-lookup"><span data-stu-id="027af-324">Q.</span></span> <span data-ttu-id="027af-325">**Wat moet ik doen als mijn cluster beschadigd is en moet ik doen urgente besturingssysteem bijwerken?**</span><span class="sxs-lookup"><span data-stu-id="027af-325">**What can I do if my cluster is unhealthy and I need to do an urgent operating system update?**</span></span>

<span data-ttu-id="027af-326">A.</span><span class="sxs-lookup"><span data-stu-id="027af-326">A.</span></span> <span data-ttu-id="027af-327">De patch orchestration app terwijl het cluster niet in orde is niet geïnstalleerd met updates.</span><span class="sxs-lookup"><span data-stu-id="027af-327">The patch orchestration app does not install updates while the cluster is unhealthy.</span></span> <span data-ttu-id="027af-328">Probeer uw cluster naar een goede status om de blokkering van de patch orchestration app werkstroom te brengen.</span><span class="sxs-lookup"><span data-stu-id="027af-328">Try to bring your cluster to a healthy state to unblock the patch orchestration app workflow.</span></span>

<span data-ttu-id="027af-329">Q.</span><span class="sxs-lookup"><span data-stu-id="027af-329">Q.</span></span> <span data-ttu-id="027af-330">**Waarom patchen tussen verschillende clusters duurt te lang om uit te voeren?**</span><span class="sxs-lookup"><span data-stu-id="027af-330">**Why does patching across clusters take so long to run?**</span></span>

<span data-ttu-id="027af-331">A.</span><span class="sxs-lookup"><span data-stu-id="027af-331">A.</span></span> <span data-ttu-id="027af-332">De tijd die nodig is door de patch orchestration-app is voornamelijk afhankelijk van de volgende factoren:</span><span class="sxs-lookup"><span data-stu-id="027af-332">The time needed by the patch orchestration app is mostly dependent on the following factors:</span></span>

- <span data-ttu-id="027af-333">Het beleid van de coördinator-Service.</span><span class="sxs-lookup"><span data-stu-id="027af-333">The policy of the Coordinator Service.</span></span> 
  - <span data-ttu-id="027af-334">Het standaardbeleid `NodeWise`, resulteert in het patchen slechts één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="027af-334">The default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="027af-335">Met name in het geval van grotere clusters, wordt aangeraden dat u de `UpgradeDomainWise` beleid sneller patchen tussen verschillende clusters.</span><span class="sxs-lookup"><span data-stu-id="027af-335">Especially in the case of bigger clusters, we recommend that you use the `UpgradeDomainWise` policy to achieve faster patching across clusters.</span></span>
- <span data-ttu-id="027af-336">Het aantal beschikbare updates voor het downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="027af-336">The number of updates available for download and installation.</span></span> 
- <span data-ttu-id="027af-337">De gemiddelde tijd die nodig zijn voor een update downloaden en installeren die mag niet meer dan een paar uur.</span><span class="sxs-lookup"><span data-stu-id="027af-337">The average time needed to download and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="027af-338">De prestaties van de virtuele machine en de netwerkbandbreedte.</span><span class="sxs-lookup"><span data-stu-id="027af-338">The performance of the VM and network bandwidth.</span></span>

<span data-ttu-id="027af-339">Q.</span><span class="sxs-lookup"><span data-stu-id="027af-339">Q.</span></span> <span data-ttu-id="027af-340">**Waarom zie ik bepaalde updates in de Windows Update-resultaten die zijn verkregen via de REST-api, maar niet onder de geschiedenis van Windows Update op de machine?**</span><span class="sxs-lookup"><span data-stu-id="027af-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under the Windows Update history on machine?**</span></span>

<span data-ttu-id="027af-341">A.</span><span class="sxs-lookup"><span data-stu-id="027af-341">A.</span></span> <span data-ttu-id="027af-342">Sommige productupdates moeten worden gecontroleerd in de geschiedenis van hun respectieve update/patch.</span><span class="sxs-lookup"><span data-stu-id="027af-342">Some product updates need to be checked in their respective update/patch history.</span></span> <span data-ttu-id="027af-343">Bijvoorbeeld: Windows Defender-updates worden niet weergegeven in de geschiedenis van Windows Update op Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="027af-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="027af-344">Disclaimers</span><span class="sxs-lookup"><span data-stu-id="027af-344">Disclaimers</span></span>

- <span data-ttu-id="027af-345">De patch orchestration app accepteert de eindgebruiker-licentie van Windows Update namens de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="027af-345">The patch orchestration app accepts the End-User License Agreement of Windows Update on behalf of the user.</span></span> <span data-ttu-id="027af-346">Eventueel kunt u de instelling ingeschakeld uitschakelen in de configuratie van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="027af-346">Optionally, the setting can be turned off in the configuration of the application.</span></span>

- <span data-ttu-id="027af-347">De patch orchestration app verzamelt telemetrie om informatie over het gebruik en prestaties te houden.</span><span class="sxs-lookup"><span data-stu-id="027af-347">The patch orchestration app collects telemetry to track usage and performance.</span></span> <span data-ttu-id="027af-348">De toepassing telemetrie volgt de instelling van de Service Fabric-runtime telemetrie (die standaard is ingeschakeld).</span><span class="sxs-lookup"><span data-stu-id="027af-348">The application’s telemetry follows the setting of the Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="027af-349">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="027af-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-to-up-state"></a><span data-ttu-id="027af-350">Een knooppunt afkomstig niet is back-up maken van status</span><span class="sxs-lookup"><span data-stu-id="027af-350">A node is not coming back to up state</span></span>

<span data-ttu-id="027af-351">**Het knooppunt kan blijven steken in een status uitschakelen omdat**:</span><span class="sxs-lookup"><span data-stu-id="027af-351">**The node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="027af-352">Er is een veiligheidscontrole in behandeling.</span><span class="sxs-lookup"><span data-stu-id="027af-352">A safety check is pending.</span></span> <span data-ttu-id="027af-353">U lost deze situatie, zorg ervoor dat er voldoende knooppunten beschikbaar in een foutloze toestand bevindt zijn.</span><span class="sxs-lookup"><span data-stu-id="027af-353">To remedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="027af-354">**Het knooppunt kan blijven steken uitgeschakeld omdat**:</span><span class="sxs-lookup"><span data-stu-id="027af-354">**The node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="027af-355">Het knooppunt is handmatig uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="027af-355">The node was disabled manually.</span></span>
- <span data-ttu-id="027af-356">Het knooppunt is uitgeschakeld vanwege een lopende Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="027af-356">The node was disabled due to an ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="027af-357">Het knooppunt is tijdelijk uitgeschakeld door de app patch orchestration patch van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="027af-357">The node was disabled temporarily by the patch orchestration app to patch the node.</span></span>

<span data-ttu-id="027af-358">**Het knooppunt kan blijven steken in een status Omlaag omdat**:</span><span class="sxs-lookup"><span data-stu-id="027af-358">**The node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="027af-359">Het knooppunt is geplaatst in een status Omlaag handmatig.</span><span class="sxs-lookup"><span data-stu-id="027af-359">The node was put in a down state manually.</span></span>
- <span data-ttu-id="027af-360">Het knooppunt is momenteel door een herstart (die kan worden geactiveerd door de patch orchestration app).</span><span class="sxs-lookup"><span data-stu-id="027af-360">The node is undergoing a restart (which might be triggered by the patch orchestration app).</span></span>
- <span data-ttu-id="027af-361">Het knooppunt is niet beschikbaar vanwege een defecte VM of verbindingsproblemen machine of het netwerk.</span><span class="sxs-lookup"><span data-stu-id="027af-361">The node is down due to a faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="027af-362">Updates zijn op sommige knooppunten overgeslagen</span><span class="sxs-lookup"><span data-stu-id="027af-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="027af-363">De patch orchestration app probeert te installeren van een Windows-update volgens het nieuwe beleid.</span><span class="sxs-lookup"><span data-stu-id="027af-363">The patch orchestration app tries to install a Windows update according to the rescheduling policy.</span></span> <span data-ttu-id="027af-364">De service probeert te herstellen van het knooppunt en overslaan van de update volgens het toepassingenbeleid.</span><span class="sxs-lookup"><span data-stu-id="027af-364">The service tries to recover the node and skip the update according to the application policy.</span></span>

<span data-ttu-id="027af-365">In dat geval wordt een waarschuwing het niveau statusrapport gegenereerd op basis van de Agent-Service van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="027af-365">In such a case, a warning-level health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="027af-366">Het resultaat voor Windows Update bevat ook de mogelijke reden voor de fout.</span><span class="sxs-lookup"><span data-stu-id="027af-366">The result for Windows Update also contains the possible reason for the failure.</span></span>

### <a name="the-health-of-the-cluster-goes-to-error-while-the-update-installs"></a><span data-ttu-id="027af-367">De status van het cluster overschakelt naar de fout tijdens de update is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="027af-367">The health of the cluster goes to error while the update installs</span></span>

<span data-ttu-id="027af-368">Een defecte Windows update kunt u de status van een toepassing of het cluster op een bepaald knooppunt of upgradedomein zetten.</span><span class="sxs-lookup"><span data-stu-id="027af-368">A faulty Windows update can bring down the health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="027af-369">De patch orchestration app stoppen eventuele latere Windows Update-bewerking totdat het cluster weer in orde is.</span><span class="sxs-lookup"><span data-stu-id="027af-369">The patch orchestration app discontinues any subsequent Windows Update operation until the cluster is healthy again.</span></span>

<span data-ttu-id="027af-370">Er moet een beheerder ingrijpen en bepalen waarom de toepassing of het cluster beschadigd vanwege Windows Update is.</span><span class="sxs-lookup"><span data-stu-id="027af-370">An administrator must intervene and determine why the application or cluster became unhealthy due to Windows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="027af-371">Release-opmerkingen:</span><span class="sxs-lookup"><span data-stu-id="027af-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="027af-372">Versie 1.1.0</span><span class="sxs-lookup"><span data-stu-id="027af-372">Version 1.1.0</span></span>
- <span data-ttu-id="027af-373">Openbare versie</span><span class="sxs-lookup"><span data-stu-id="027af-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="027af-374">Versie 1.1.1</span><span class="sxs-lookup"><span data-stu-id="027af-374">Version 1.1.1</span></span>
- <span data-ttu-id="027af-375">Een bug vast entrypoint van NodeAgentService waardoor de installatie van NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="027af-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="027af-376">Versie 1.2.0 (laatste)</span><span class="sxs-lookup"><span data-stu-id="027af-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="027af-377">Werkstroom van oplossingen voor problemen rond systeem opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="027af-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="027af-378">Fout te herstellen bij het maken van de RM-taken als gevolg van welke status selectievakje tijdens herstel taken voorbereiden is niet plaatsvinden, zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="027af-378">Bug fix in creation of RM tasks due to which health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="027af-379">De opstartmodus gewijzigd voor windows service POANodeSvc van automatische vertraagd automatisch.</span><span class="sxs-lookup"><span data-stu-id="027af-379">Changed the startup mode for windows service POANodeSvc from auto to delayed-auto.</span></span>
