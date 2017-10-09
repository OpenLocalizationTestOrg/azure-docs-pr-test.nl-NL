---
title: Aggregatie van Service Fabric-gebeurtenis met Windows Azure Diagnostics aaaAzure | Microsoft Docs
description: Meer informatie over het aggregeren en het verzamelen van gebeurtenissen met af voor controle en diagnostische gegevens van Azure Service Fabric-clusters.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="e8c4c-103">Gebeurtenis-aggregatie en verzameling op basis van Windows Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="e8c4c-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8c4c-104">Windows</span><span class="sxs-lookup"><span data-stu-id="e8c4c-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="e8c4c-105">Linux</span><span class="sxs-lookup"><span data-stu-id="e8c4c-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="e8c4c-106">Wanneer u een Azure Service Fabric-cluster uitvoert, is het een goed idee toocollect Hallo Logboeken uit alle Hallo knooppunten in een centrale locatie.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="e8c4c-107">Hallo-logboeken die in een centrale locatie, helpt u bij het analyseren en oplossen van problemen in het cluster of problemen in Hallo toepassingen en services die worden uitgevoerd in het cluster.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="e8c4c-108">Een manier tooupload en verzamelen van Logboeken is toouse Hallo Windows Azure Diagnostics (af) extensie, die u uploadt logboeken tooAzure opslag, en heeft ook Hallo optie toosend logboeken tooAzure Application Insights of Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-108">One way tooupload and collect logs is toouse hello Windows Azure Diagnostics (WAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="e8c4c-109">U kunt ook gebruikt een extern proces tooread Hallo gebeurtenissen uit de opslag en plaats deze in een analyse platform-product, zoals [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) of een andere oplossing voor het parseren van het logboek.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8c4c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e8c4c-110">Prerequisites</span></span>
<span data-ttu-id="e8c4c-111">Deze hulpprogramma's zijn gebruikte tooperform aantal Hallo-bewerkingen in dit document:</span><span class="sxs-lookup"><span data-stu-id="e8c4c-111">These tools are used tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="e8c4c-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (gerelateerde tooAzure Cloudservices met een goede informatie over en voorbeelden)</span><span class="sxs-lookup"><span data-stu-id="e8c4c-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="e8c4c-113">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8c4c-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="e8c4c-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8c4c-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="e8c4c-115">Azure Resource Manager-client</span><span class="sxs-lookup"><span data-stu-id="e8c4c-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="e8c4c-116">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="e8c4c-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="e8c4c-117">Logboekbestand en de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="e8c4c-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="e8c4c-118">Gebeurtenissen voor service Fabric-platform</span><span class="sxs-lookup"><span data-stu-id="e8c4c-118">Service Fabric platform events</span></span>
<span data-ttu-id="e8c4c-119">Zoals beschreven in [in dit artikel](service-fabric-diagnostics-event-generation-infra.md), Service Fabric stelt u met enkele out-of-the-box-logboekregistratie kanalen, van die Hallo eenvoudig volgende kanalen zijn geconfigureerd met af toosend controle en diagnostische gegevens tooa opslag gegevenstabel of elders:</span><span class="sxs-lookup"><span data-stu-id="e8c4c-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which hello following channels are easily configured with WAD toosend monitoring and diagnostics data tooa storage table or elsewhere:</span></span>
  * <span data-ttu-id="e8c4c-120">Operationele gebeurtenissen: een hoger niveau bewerkingen die Hallo Service Fabric-platform wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-120">Operational events: higher-level operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="e8c4c-121">Voorbeelden zijn onder meer het maken van toepassingen en services, knooppunt statuswijzigingen en informatie over de upgrade.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="e8c4c-122">Deze worden verzonden als Logboeken Event Tracing voor Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="e8c4c-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="e8c4c-123">Reliable Actors programming model gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="e8c4c-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="e8c4c-124">Reliable Services programming model gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="e8c4c-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="e8c4c-125">Toepassingsgebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="e8c4c-125">Application events</span></span>
 <span data-ttu-id="e8c4c-126">Gebeurtenissen van uw toepassingen en services code verzonden en geschreven met behulp van Hallo EventSource helper-klasse die is opgegeven in Hallo Visual Studio-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-126">Events emitted from your applications' and services' code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="e8c4c-127">Zie voor meer informatie over hoe toowrite EventSource vanuit uw App registreert, [bewaken en onderzoeken van services in de instellingen voor een lokale computer ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="e8c4c-127">For more information on how toowrite EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="e8c4c-128">Hallo-extensie voor diagnostische gegevens implementeren</span><span class="sxs-lookup"><span data-stu-id="e8c4c-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="e8c4c-129">Hallo eerste stap bij het verzamelen van Logboeken is toodeploy Hallo-extensie voor diagnostische gegevens op elk van de VM Hallo in Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="e8c4c-130">Hallo-extensie voor diagnostische gegevens verzamelt logboeken op elke virtuele machine en geüpload toohello storage-account die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="e8c4c-131">Hallo stappen verschillen enigszins op basis van of u hello Azure-portal of Azure Resource Manager gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="e8c4c-132">Hallo stappen ook variëren, afhankelijk van of Hallo implementatie maakt deel uit van het maken van het cluster of voor een cluster dat al bestaat.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="e8c4c-133">Bekijk Hallo stappen voor elk scenario.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="e8c4c-134">Hallo-extensie voor diagnostische gegevens als onderdeel van het maken van het cluster via Azure portal implementeren</span><span class="sxs-lookup"><span data-stu-id="e8c4c-134">Deploy hello Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="e8c4c-135">toodeploy hello Diagnostics extensie toohello virtuele machines in de cluster Hallo als onderdeel van het maken van het cluster, u Hallo Diagnostics paneel met toepassingsinstellingen weergegeven in de volgende Hallo afbeelding: Controleer of de diagnostische gegevens te is ingesteld**op** (Hallo standaardinstelling) .</span><span class="sxs-lookup"><span data-stu-id="e8c4c-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image - ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="e8c4c-136">Nadat u Hallo-cluster maakt, kunt u deze instellingen niet wijzigen met behulp van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-136">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Azure Diagnostics-instellingen in Hallo-portal voor het maken van het cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="e8c4c-138">Wanneer u een cluster met behulp van Hallo portal maakt, wordt ten zeerste aanbevolen dat u het Hallo-sjabloon downloaden **voordat u op OK** toocreate Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-138">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="e8c4c-139">Voor meer informatie, Raadpleeg te[een Service Fabric-cluster instellen met behulp van een Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e8c4c-139">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="e8c4c-140">Omdat u geen enkele wijzigingen aanbrengen met behulp van de portal Hallo, hebt u de Sjabloonwijzigingen toomake hello later nodig.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-140">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="e8c4c-141">Hallo-extensie voor diagnostische gegevens als onderdeel van het maken van het cluster implementeren met behulp van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8c4c-141">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="e8c4c-142">toocreate een cluster met Resource Manager, moet u tooadd Hallo Diagnostics configuratie JSON toohello volledige cluster Resource Manager-sjabloon voordat u Hallo-cluster maakt.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-142">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="e8c4c-143">We een voorbeeldsjabloon vijf VM-cluster Resource Manager voorzien van configuratie van diagnostische toegevoegd tooit als onderdeel van onze voorbeelden Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="e8c4c-144">Kunt u deze bekijken op deze locatie in de galerie met hello Azure Samples: [cluster met vijf knooppunten met diagnostische gegevens van Resource Manager-sjabloon voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="e8c4c-144">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="e8c4c-145">toosee hello diagnostische instelling in Hallo Resource Manager-sjabloon, open Hallo azuredeploy.json bestand en zoek naar **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-145">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="e8c4c-146">een cluster met behulp van deze sjabloon, selecteer Hallo toocreate **tooAzure implementeren** beschikbaar op de vorige koppeling Hallo knop.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-146">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="e8c4c-147">U kunt ook u kunt Hallo Resource Manager voorbeeld downloaden, tooit wijzigingen aanbrengen en Hallo met een cluster maken met de gewijzigde sjabloon Hallo `New-AzureRmResourceGroupDeployment` opdracht in een Azure PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-147">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="e8c4c-148">Zie Hallo code voor Hallo-parameters die u in toohello opdracht doorgeeft te volgen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-148">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="e8c4c-149">Zie voor gedetailleerde informatie over hoe een resource toodeploy groeperen met behulp van PowerShell, Hallo artikel [een resourcegroep implementeren met Azure Resource Manager-sjabloon voor Hallo](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e8c4c-149">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="e8c4c-150">Hallo Diagnostics extensie tooan bestaande cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="e8c4c-150">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="e8c4c-151">Als er een bestaand cluster dat geen diagnostische gegevens die zijn geïmplementeerd, of als u een bestaande configuratie toomodify wilt, kunt u deze kunt toevoegen of bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="e8c4c-152">Hallo Resource Manager-sjabloon die wordt gebruikt toocreate Hallo bestaand cluster wijzigen of Hallo sjabloon downloaden van Hallo beheerportal, zoals eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-152">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="e8c4c-153">Hallo template.json bestand wijzigen door het uitvoeren van Hallo taken te volgen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-153">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="e8c4c-154">Voeg een nieuwe opslag resource toohello sjabloon door toohello bronnensectie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-154">Add a new storage resource toohello template by adding toohello resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="e8c4c-155">Vervolgens voegt u parameters toohello sectie direct na Hallo storage account definities tussen `supportLogStorageAccountName` en `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-155">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="e8c4c-156">Hallo tijdelijke aanduiding voor tekst vervangen *opslagaccountnaam hier* met de naam van het opslagaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-156">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="e8c4c-157">Werk vervolgens, Hallo `VirtualMachineProfile` sectie van Hallo template.json bestand door toe te voegen Hallo code binnen Hallo extensies matrix te volgen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-157">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="e8c4c-158">Niet zeker tooadd een komma aan Hallo begin of einde van de hello, afhankelijk van waar het ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-158">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="e8c4c-159">Nadat u gewijzigd Hallo template.json bestand, zoals wordt beschreven, opnieuw publiceren Hallo Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-159">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="e8c4c-160">Als Hallo-sjabloon is geëxporteerd, rapport uitvoeren Hallo deploy.ps1 van bestand opnieuw publiceert Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-160">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="e8c4c-161">Nadat u hebt geïmplementeerd, zorg ervoor dat **ProvisioningState** is **geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="e8c4c-162">Health verzamelen en laden van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="e8c4c-162">Collect health and load events</span></span>

<span data-ttu-id="e8c4c-163">Vanaf Hallo 5.4 versie van Service Fabric, zijn status en load metrische gebeurtenissen beschikbaar voor de verzameling.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-163">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="e8c4c-164">Deze gebeurtenissen gebeurtenissen die zijn gegenereerd door Hallo systeem of uw code via Hallo health of rapportage-API's, zoals load [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) of [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8c4c-164">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="e8c4c-165">Hierdoor kan voor het aggregeren en weergeven van systeemstatus na verloop van tijd en voor waarschuwingen op basis van status- of load-gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="e8c4c-166">Deze gebeurtenissen in Visual Studio diagnostische logboeken toevoegen tooview ' Microsoft-ServiceFabric:4:0x4000000000000008 ' toohello lijst met ETW-providers.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-166">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="e8c4c-167">toocollect hello gebeurtenissen, wijzigen Hallo Resource Manager-sjabloon tooinclude</span><span class="sxs-lookup"><span data-stu-id="e8c4c-167">toocollect hello events, modify hello Resource Manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="e8c4c-168">Omgekeerde proxy-gebeurtenissen verzamelen</span><span class="sxs-lookup"><span data-stu-id="e8c4c-168">Collect reverse proxy events</span></span>

<span data-ttu-id="e8c4c-169">Vanaf versie van Service Fabric Hallo 5.7 [omgekeerde proxy](service-fabric-reverseproxy.md) gebeurtenissen zijn beschikbaar voor de verzameling.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-169">Starting with hello 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="e8c4c-170">Omgekeerde proxy verzendt gebeurtenissen naar twee kanalen, één met fout gebeurtenissen opgetreden bij het weergeven mislukte verwerkingen aanvragen en andere uitgebreide gebeurtenissen over alle Hallo-aanvragen op Hallo omgekeerde proxy verwerkt met een Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and hello other one containing verbose events about all hello requests processed at hello reverse proxy.</span></span> 

1. <span data-ttu-id="e8c4c-171">Verzamelen van foutgebeurtenissen: tooview deze gebeurtenissen in Visual Studio diagnostische logboeken toevoegen ' Microsoft-ServiceFabric:4:0x4000000000000010 ' toohello lijst met ETW-providers.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-171">Collect error events: tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" toohello list of ETW providers.</span></span>
<span data-ttu-id="e8c4c-172">toocollect hello gebeurtenissen van Azure clusters wijzigen Hallo Resource Manager-sjabloon tooinclude</span><span class="sxs-lookup"><span data-stu-id="e8c4c-172">toocollect hello events from Azure clusters, modify hello Resource Manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. <span data-ttu-id="e8c4c-173">Verzamelt alle verwerking van gebeurtenissen aanvragen: In Visual Studio van diagnostische logboeken update Hallo Microsoft ServiceFabric vermelding in de lijst voor ETW-provider te Hallo ' Microsoft-ServiceFabric:4:0x4000000000000020 '.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update hello Microsoft-ServiceFabric entry in hello ETW provider list too"Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="e8c4c-174">Voor de Azure Service Fabric-clusters, wijzigt u tooinclude Hallo resource manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="e8c4c-174">For Azure Service Fabric clusters, modify hello resource manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> <span data-ttu-id="e8c4c-175">Het verdient toojudiciously inschakelen verzamelen gebeurtenissen van dit kanaal omdat dit al het verkeer via de omgekeerde proxy Hallo verzamelt en opslagcapaciteit snel kan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-175">It is recommended toojudiciously enable collecting events from this channel as this collects all traffic through hello reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="e8c4c-176">Voor Azure Service Fabric-clusters Hallo gebeurtenissen van alle knooppunten van het Hallo verzameld en geaggregeerd in Hallo SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-176">For Azure Service Fabric clusters, hello events from all hello nodes are collected and aggregated in hello SystemEventTable.</span></span>
<span data-ttu-id="e8c4c-177">Voor gedetailleerde probleemoplossing van Hallo reverse proxy-gebeurtenissen, Raadpleeg Hallo [omgekeerde proxy diagnostics handleiding](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="e8c4c-177">For detailed troubleshooting of hello reverse proxy events, refer hello [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="e8c4c-178">Verzamelen van nieuwe EventSource kanalen</span><span class="sxs-lookup"><span data-stu-id="e8c4c-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="e8c4c-179">tooupdate Diagnostics toocollect logboeken van de nieuwe EventSource kanalen die een nieuwe toepassing die u over toodeploy, vertegenwoordigen uitvoeren Hallo dezelfde stappen als eerder beschreven voor het instellen van de Hallo van diagnostische gegevens voor een bestaand cluster.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-179">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as previously described for hello setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="e8c4c-180">Hallo bijwerken `EtwEventSourceProviderConfiguration` sectie in Hallo template.json bestandsvermeldingen tooadd Hallo nieuwe EventSource kanalen voordat u Hallo configuratie toepassen met behulp van Hallo werk `New-AzureRmResourceGroupDeployment` PowerShell-opdracht.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-180">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="e8c4c-181">Hallo-naam van de gebeurtenisbron Hallo is gedefinieerd als onderdeel van uw code in Hallo ServiceEventSource.cs Visual Studio gegenereerd bestand.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-181">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="e8c4c-182">Als uw gebeurtenisbron mijn Eventsource heet, bijvoorbeeld Hallo volgende code tooplace Hallo gebeurtenissen uit mijn Eventsource in een tabel met de naam MyDestinationTableName toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-182">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="e8c4c-183">toocollect-prestatiemeteritems of gebeurtenislogboeken Hallo Resource Manager-sjabloon wijzigen met behulp van Hallo-voorbeelden vindt u in [virtuele Windows-machine maken met controle en diagnostische gegevens met behulp van een Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8c4c-183">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e8c4c-184">Vervolgens opnieuw publiceren Hallo Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-184">Then, republish hello Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="e8c4c-185">Verzamelen van prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="e8c4c-185">Collect Performance Counters</span></span>

<span data-ttu-id="e8c4c-186">Hallo prestaties tellers tooyour 'WadCfg > DiagnosticMonitorConfiguration' toevoegen toocollect maatstaven voor prestaties van het cluster in Hallo Resource Manager-sjabloon voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-186">toocollect performance metrics from your cluster, add hello performance counters tooyour "WadCfg > DiagnosticMonitorConfiguration" in hello Resource Manager template for your cluster.</span></span> <span data-ttu-id="e8c4c-187">Zie [Service Fabric-prestatiemeteritems](service-fabric-diagnostics-event-generation-perf.md) voor prestatiemeteritems die wordt aangeraden verzamelen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="e8c4c-188">Bijvoorbeeld: Hier wordt een prestatiemeteritem dat elke 15 seconden instellen (dit kan worden gewijzigd en volgt de indeling van Hallo ' PT\<tijd >\<eenheid > ', bijvoorbeeld PT3M zou een steekproef nemen uit drie minuten durende intervallen), en toohello overgedragen de juiste opslag tabel om één minuut.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows hello format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred toohello appropriate storage table every one minute.</span></span>

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
<span data-ttu-id="e8c4c-189">Als u een Application Insights-sink gebruikt zoals beschreven in onderstaande sectie voor Hallo en deze metrische gegevens tooshow-up in Application Insights wilt, moet u ervoor tooadd Hallo sink-naam in Hallo 'put' sectie zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-189">If you are using an Application Insights sink, as described in hello section below, and want these metrics tooshow up in Application Insights, then make sure tooadd hello sink name in hello "sinks" section as shown above.</span></span> <span data-ttu-id="e8c4c-190">Bovendien kunt u een afzonderlijke tabel toosend uw prestatiemeteritems, zodat ze niet uit Hallo opnemen die afkomstig zijn van Hallo andere logboekkanalen die u hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-190">Additionally, consider creating a separate table toosend your Performance Counters to, so they don't crowd out hello data coming from hello other logging channels you have enabled.</span></span>


## <a name="send-logs-tooapplication-insights"></a><span data-ttu-id="e8c4c-191">Verzenden logboeken tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="e8c4c-191">Send logs tooApplication Insights</span></span>

<span data-ttu-id="e8c4c-192">Verzenden van controle en diagnostische gegevens tooApplication Insights (AI) kan worden uitgevoerd als onderdeel van Hallo af configuratie.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-192">Sending monitoring and diagnostics data tooApplication Insights (AI) can be done as part of hello WAD configuration.</span></span> <span data-ttu-id="e8c4c-193">Als u toouse AI voor analyse van gebeurtenis en visualisatie besluit, lezen [analyse van gebeurtenis en visualisatie met Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset van een AI Sink als onderdeel van uw 'WadCfg'.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-193">If you decide toouse AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8c4c-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8c4c-194">Next steps</span></span>

<span data-ttu-id="e8c4c-195">Nadat u Azure diagnostics correct hebt geconfigureerd, ziet u gegevens in de tabellen bij opslag van EventSource logboeken en Hallo ETW.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from hello ETW and EventSource logs.</span></span> <span data-ttu-id="e8c4c-196">Als u toouse OMS, moet Kibana of een andere gegevens analytics en visualisatie platform dat niet rechtstreeks in het Hallo-Resource Manager-sjabloon is geconfigureerd dat tooset Hallo platform van uw keuze tooread in Hallo gegevens uit deze opslagtabellen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-196">If you choose toouse OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in hello Resource Manager template, make sure tooset up hello platform of your choice tooread in hello data from these storage tables.</span></span> <span data-ttu-id="e8c4c-197">Hierdoor voor OMS is relatief eenvoudig en wordt uitgelegd in [analyse van gebeurtenis- en logboekbestanden via OMS](service-fabric-diagnostics-event-analysis-oms.md).</span><span class="sxs-lookup"><span data-stu-id="e8c4c-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="e8c4c-198">Application Insights is een bit van een speciaal geval in dit opzicht, omdat deze kan worden geconfigureerd als onderdeel van de configuratie van diagnostische gegevens uitbreiding hello, raadpleegt u dus toohello [juiste artikel](service-fabric-diagnostics-event-analysis-appinsights.md) als u ervoor toouse AI kiest.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of hello Diagnostics extension configuration, so refer toohello [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose toouse AI.</span></span>

>[!NOTE]
><span data-ttu-id="e8c4c-199">Er is momenteel geen manier toofilter of opschoondagen Hallo gebeurtenissen die worden verzonden toohello tabel.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-199">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="e8c4c-200">Als u een proces tooremove gebeurtenissen uit de tabel Hallo niet implementeert, blijven Hallo tabel toogrow.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-200">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span> <span data-ttu-id="e8c4c-201">Er is een voorbeeld van een gegevensservice opschonen uitgevoerd in de Hallo [Watchdog voorbeeld](https://github.com/Azure-Samples/service-fabric-watchdog-service), en wordt aanbevolen dat u één voor uzelf, schrijft tenzij er een goede reden voor u toostore Logboeken na een periode 30 of 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="e8c4c-201">Currently, there is an example of a data grooming service running in hello [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you toostore logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="e8c4c-202">Meer informatie over hoe toocollect prestatiemeteritems of de logboeken met behulp van Hallo extensie voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="e8c4c-202">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e8c4c-203">Analyse van gebeurtenis en visualisatie met Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8c4c-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="e8c4c-204">Analyse van gebeurtenis en visualisatie met OMS</span><span class="sxs-lookup"><span data-stu-id="e8c4c-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)