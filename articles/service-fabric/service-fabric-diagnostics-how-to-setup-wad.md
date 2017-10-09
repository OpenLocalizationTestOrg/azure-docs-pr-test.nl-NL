---
title: logboeken met behulp van Azure Diagnostics aaaCollect | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van Azure Diagnostics toocollect registreert van een Service Fabric-cluster in Azure wordt uitgevoerd.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="64ea2-103">Logboeken verzamelen met Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="64ea2-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64ea2-104">Windows</span><span class="sxs-lookup"><span data-stu-id="64ea2-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="64ea2-105">Linux</span><span class="sxs-lookup"><span data-stu-id="64ea2-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="64ea2-106">Wanneer u een Azure Service Fabric-cluster uitvoert, is het een goed idee toocollect Hallo Logboeken uit alle Hallo knooppunten in een centrale locatie.</span><span class="sxs-lookup"><span data-stu-id="64ea2-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="64ea2-107">Hallo-logboeken die in een centrale locatie, helpt u bij het analyseren en oplossen van problemen in het cluster of problemen in Hallo toepassingen en services die worden uitgevoerd in het cluster.</span><span class="sxs-lookup"><span data-stu-id="64ea2-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="64ea2-108">Een manier tooupload en verzamelen van Logboeken is toouse hello Azure extensie voor diagnostische gegevens, welke uploads logboeken tooAzure opslag, Azure Application Insights of Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="64ea2-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="64ea2-109">Er zijn geen Hallo logboeken die handig zijn in de opslag of in Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="64ea2-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="64ea2-110">Maar u kunt een extern proces tooread Hallo gebeurtenissen uit de opslag gebruiken en plaats deze in een product zoals [logboekanalyse](../log-analytics/log-analytics-service-fabric.md) of een andere oplossing voor het parseren van het logboek.</span><span class="sxs-lookup"><span data-stu-id="64ea2-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="64ea2-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) wordt geleverd met een uitgebreide zoeken en analytics logboekservice ingebouwde.</span><span class="sxs-lookup"><span data-stu-id="64ea2-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64ea2-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="64ea2-112">Prerequisites</span></span>
<span data-ttu-id="64ea2-113">Gebruik van deze hulpprogramma's voor tooperform aantal Hallo-bewerkingen in dit document:</span><span class="sxs-lookup"><span data-stu-id="64ea2-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="64ea2-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (gerelateerde tooAzure Cloudservices met een goede informatie over en voorbeelden)</span><span class="sxs-lookup"><span data-stu-id="64ea2-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="64ea2-115">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64ea2-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="64ea2-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="64ea2-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="64ea2-117">Azure Resource Manager-client</span><span class="sxs-lookup"><span data-stu-id="64ea2-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="64ea2-118">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="64ea2-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="64ea2-119">Meld u bronnen die u wilt misschien toocollect</span><span class="sxs-lookup"><span data-stu-id="64ea2-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="64ea2-120">**Service Fabric-logboeken**: van Hallo platform toostandard Event Tracing voor Windows (ETW) en EventSource kanalen verzonden.</span><span class="sxs-lookup"><span data-stu-id="64ea2-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="64ea2-121">Logboeken kunnen een van de verschillende typen zijn:</span><span class="sxs-lookup"><span data-stu-id="64ea2-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="64ea2-122">Operationele gebeurtenissen: logboeken voor bewerkingen waarvoor Hallo Service Fabric-platform wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="64ea2-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="64ea2-123">Voorbeelden zijn onder meer het maken van toepassingen en services, knooppunt statuswijzigingen en informatie over de upgrade.</span><span class="sxs-lookup"><span data-stu-id="64ea2-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="64ea2-124">Reliable Actors programming model gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="64ea2-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="64ea2-125">Reliable Services programming model gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="64ea2-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="64ea2-126">**Toepassingsgebeurtenissen**: gebeurtenissen verzonden vanuit de code van uw service en met behulp van de klasse van Help voor Hallo EventSource opgegeven in de Visual Studio-sjablonen Hallo uitgeschreven.</span><span class="sxs-lookup"><span data-stu-id="64ea2-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="64ea2-127">Zie voor meer informatie over hoe toowrite vanuit uw App registreert, [bewaken en onderzoeken van services in de instellingen voor een lokale computer ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="64ea2-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="64ea2-128">Hallo-extensie voor diagnostische gegevens implementeren</span><span class="sxs-lookup"><span data-stu-id="64ea2-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="64ea2-129">Hallo eerste stap bij het verzamelen van Logboeken is toodeploy Hallo-extensie voor diagnostische gegevens op elk van de VM Hallo in Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="64ea2-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="64ea2-130">Hallo-extensie voor diagnostische gegevens verzamelt logboeken op elke virtuele machine en geüpload toohello storage-account die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="64ea2-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="64ea2-131">Hallo stappen verschillen enigszins op basis van of u hello Azure-portal of Azure Resource Manager gebruiken.</span><span class="sxs-lookup"><span data-stu-id="64ea2-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="64ea2-132">Hallo stappen ook variëren, afhankelijk van of Hallo implementatie maakt deel uit van het maken van het cluster of voor een cluster dat al bestaat.</span><span class="sxs-lookup"><span data-stu-id="64ea2-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="64ea2-133">Bekijk Hallo stappen voor elk scenario.</span><span class="sxs-lookup"><span data-stu-id="64ea2-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="64ea2-134">Hallo-extensie voor diagnostische gegevens als onderdeel van het maken van het cluster via Hallo portal implementeren</span><span class="sxs-lookup"><span data-stu-id="64ea2-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="64ea2-135">toodeploy hello Diagnostics extensie toohello virtuele machines in de cluster Hallo als onderdeel van het maken van het cluster, u Hallo Diagnostics paneel met toepassingsinstellingen in Hallo volgende afbeelding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="64ea2-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="64ea2-136">tooenable Reliable Actors of Reliable Services gebeurtenissen verzamelen, moet het diagnostische gegevens te instellen**op** (Hallo standaardinstelling).</span><span class="sxs-lookup"><span data-stu-id="64ea2-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="64ea2-137">Nadat u Hallo-cluster maakt, kunt u deze instellingen niet wijzigen met behulp van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="64ea2-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Azure Diagnostics-instellingen in Hallo-portal voor het maken van het cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="64ea2-139">Hallo ondersteuningsteam van Azure *vereist* ondersteuning logboeken toohelp los ondersteuningsaanvragen die u maakt.</span><span class="sxs-lookup"><span data-stu-id="64ea2-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="64ea2-140">Deze logboeken worden in realtime verzameld en worden opgeslagen in een van de storage-accounts Hallo gemaakt in resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="64ea2-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="64ea2-141">Hallo diagnostische instellingen configureren op toepassingsniveau gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="64ea2-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="64ea2-142">Deze gebeurtenissen opnemen [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) gebeurtenissen, [Reliable Services](service-fabric-reliable-services-diagnostics.md) gebeurtenissen en sommige systeemniveau Service Fabric gebeurtenissen toobe opgeslagen in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="64ea2-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="64ea2-143">Producten zoals [Elasticsearch](https://www.elastic.co/guide/index.html) of uw eigen proces Hallo gebeurtenissen kan worden opgehaald van Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="64ea2-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="64ea2-144">Er is momenteel geen manier toofilter of opschoondagen Hallo gebeurtenissen die worden verzonden toohello tabel.</span><span class="sxs-lookup"><span data-stu-id="64ea2-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="64ea2-145">Als u een proces tooremove gebeurtenissen uit de tabel Hallo niet implementeert, blijven Hallo tabel toogrow.</span><span class="sxs-lookup"><span data-stu-id="64ea2-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="64ea2-146">Wanneer u een cluster met behulp van Hallo portal maakt, wordt ten zeerste aanbevolen dat u het Hallo-sjabloon downloaden **voordat u op OK** toocreate Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="64ea2-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="64ea2-147">Voor meer informatie, Raadpleeg te[een Service Fabric-cluster instellen met behulp van een Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="64ea2-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="64ea2-148">Omdat u geen enkele wijzigingen aanbrengen met behulp van de portal Hallo, hebt u de Sjabloonwijzigingen toomake hello later nodig.</span><span class="sxs-lookup"><span data-stu-id="64ea2-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="64ea2-149">U kunt sjablonen exporteren vanuit de portal Hallo met behulp van de volgende stappen uit Hallo.</span><span class="sxs-lookup"><span data-stu-id="64ea2-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="64ea2-150">Deze sjablonen kunnen echter moeilijker toouse zijn omdat ze wellicht hebben null-waarden die vereiste informatie ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="64ea2-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="64ea2-151">Open uw resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="64ea2-151">Open your resource group.</span></span>
2. <span data-ttu-id="64ea2-152">Selecteer **instellingen** toodisplay Hallo paneel met toepassingsinstellingen.</span><span class="sxs-lookup"><span data-stu-id="64ea2-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="64ea2-153">Selecteer **implementaties** deelvenster Historie toodisplay Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="64ea2-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="64ea2-154">Selecteer een implementatie toodisplay Hallo details van Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="64ea2-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="64ea2-155">Selecteer **exportsjabloon** toodisplay Hallo sjabloon Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="64ea2-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="64ea2-156">Selecteer **opslaan toofile** tooexport een ZIP-bestand dat Hallo-sjabloon, parameter en PowerShell-bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="64ea2-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="64ea2-157">Nadat u de bestanden Hallo exporteert, moet u toomake een wijziging.</span><span class="sxs-lookup"><span data-stu-id="64ea2-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="64ea2-158">Hallo parameters.json bestand bewerken en verwijderen van Hallo **adminPassword** element.</span><span class="sxs-lookup"><span data-stu-id="64ea2-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="64ea2-159">Hierdoor wordt een prompt voor wachtwoord Hallo wanneer Hallo implementatiescript wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="64ea2-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="64ea2-160">Wanneer u het implementatiescript Hallo uitvoert, hebt u mogelijk toofix null-parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="64ea2-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="64ea2-161">Hallo toouse gedownload sjabloon tooupdate een configuratie:</span><span class="sxs-lookup"><span data-stu-id="64ea2-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="64ea2-162">Pak Hallo inhoud tooa map op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="64ea2-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="64ea2-163">Hallo inhoud tooreflect Hallo nieuwe configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="64ea2-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="64ea2-164">Start PowerShell en wijzig toohello map waar u Hallo inhoud hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="64ea2-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="64ea2-165">Uitvoeren **deploy.ps1** en vul Hallo abonnements-ID, naam resourcegroep hello (gebruik Hallo dezelfde naam tooupdate Hallo configuratie), en de naam van een unieke implementatie.</span><span class="sxs-lookup"><span data-stu-id="64ea2-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="64ea2-166">Hallo-extensie voor diagnostische gegevens als onderdeel van het maken van het cluster implementeren met behulp van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64ea2-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="64ea2-167">toocreate een cluster met Resource Manager, moet u tooadd Hallo Diagnostics configuratie JSON toohello volledige cluster Resource Manager-sjabloon voordat u Hallo-cluster maakt.</span><span class="sxs-lookup"><span data-stu-id="64ea2-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="64ea2-168">We een voorbeeldsjabloon vijf VM-cluster Resource Manager voorzien van configuratie van diagnostische toegevoegd tooit als onderdeel van onze voorbeelden Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="64ea2-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="64ea2-169">Kunt u deze bekijken op deze locatie in de galerie met hello Azure Samples: [cluster met vijf knooppunten met diagnostische gegevens van Resource Manager-sjabloon voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="64ea2-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="64ea2-170">toosee hello diagnostische instelling in Hallo Resource Manager-sjabloon, open Hallo azuredeploy.json bestand en zoek naar **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="64ea2-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="64ea2-171">een cluster met behulp van deze sjabloon, selecteer Hallo toocreate **tooAzure implementeren** beschikbaar op de vorige koppeling Hallo knop.</span><span class="sxs-lookup"><span data-stu-id="64ea2-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="64ea2-172">U kunt ook u kunt Hallo Resource Manager voorbeeld downloaden, tooit wijzigingen aanbrengen en Hallo met een cluster maken met de gewijzigde sjabloon Hallo `New-AzureRmResourceGroupDeployment` opdracht in een Azure PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="64ea2-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="64ea2-173">Zie Hallo code voor Hallo-parameters die u in toohello opdracht doorgeeft te volgen.</span><span class="sxs-lookup"><span data-stu-id="64ea2-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="64ea2-174">Zie voor gedetailleerde informatie over hoe een resource toodeploy groeperen met behulp van PowerShell, Hallo artikel [een resourcegroep implementeren met Azure Resource Manager-sjabloon voor Hallo](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="64ea2-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="64ea2-175">Hallo Diagnostics extensie tooan bestaande cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="64ea2-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="64ea2-176">Als er een bestaand cluster dat geen diagnostische gegevens die zijn geïmplementeerd, of als u een bestaande configuratie toomodify wilt, kunt u deze kunt toevoegen of bijwerken.</span><span class="sxs-lookup"><span data-stu-id="64ea2-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="64ea2-177">Hallo Resource Manager-sjabloon die wordt gebruikt toocreate Hallo bestaand cluster wijzigen of Hallo sjabloon downloaden van Hallo beheerportal, zoals eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="64ea2-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="64ea2-178">Hallo template.json bestand wijzigen door het uitvoeren van Hallo taken te volgen.</span><span class="sxs-lookup"><span data-stu-id="64ea2-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="64ea2-179">Voeg een nieuwe opslag resource toohello sjabloon door toohello bronnensectie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="64ea2-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="64ea2-180">Vervolgens voegt u parameters toohello sectie direct na Hallo storage account definities tussen `supportLogStorageAccountName` en `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="64ea2-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="64ea2-181">Hallo tijdelijke aanduiding voor tekst vervangen *opslagaccountnaam hier* met de naam van het opslagaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="64ea2-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

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
<span data-ttu-id="64ea2-182">Werk vervolgens, Hallo `VirtualMachineProfile` sectie van Hallo template.json bestand door toe te voegen Hallo code binnen Hallo extensies matrix te volgen.</span><span class="sxs-lookup"><span data-stu-id="64ea2-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="64ea2-183">Niet zeker tooadd een komma aan Hallo begin of einde van de hello, afhankelijk van waar het ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="64ea2-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="64ea2-184">Nadat u gewijzigd Hallo template.json bestand, zoals wordt beschreven, opnieuw publiceren Hallo Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="64ea2-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="64ea2-185">Als Hallo-sjabloon is geëxporteerd, rapport uitvoeren Hallo deploy.ps1 van bestand opnieuw publiceert Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="64ea2-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="64ea2-186">Nadat u hebt geïmplementeerd, zorg ervoor dat **ProvisioningState** is **geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="64ea2-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="64ea2-187">Bijwerken van diagnostische gegevens toocollect status en load-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="64ea2-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="64ea2-188">Vanaf Hallo 5.4 versie van Service Fabric, zijn status en load metrische gebeurtenissen beschikbaar voor de verzameling.</span><span class="sxs-lookup"><span data-stu-id="64ea2-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="64ea2-189">Deze gebeurtenissen gebeurtenissen die zijn gegenereerd door Hallo systeem of uw code via Hallo health of rapportage-API's, zoals load [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) of [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="64ea2-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="64ea2-190">Hierdoor kan voor het aggregeren en weergeven van systeemstatus na verloop van tijd en voor waarschuwingen op basis van status- of load-gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="64ea2-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="64ea2-191">Deze gebeurtenissen in Visual Studio diagnostische logboeken toevoegen tooview ' Microsoft-ServiceFabric:4:0x4000000000000008 ' toohello lijst met ETW-providers.</span><span class="sxs-lookup"><span data-stu-id="64ea2-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="64ea2-192">toocollect hello gebeurtenissen, wijzigen Hallo resource manager-sjabloon tooinclude</span><span class="sxs-lookup"><span data-stu-id="64ea2-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="64ea2-193">Bijwerken van diagnostische gegevens toocollect en logboeken van de nieuwe EventSource kanalen uploaden</span><span class="sxs-lookup"><span data-stu-id="64ea2-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="64ea2-194">tooupdate Diagnostics toocollect logboeken van de nieuwe EventSource kanalen die een nieuwe toepassing die u over toodeploy, vertegenwoordigen voeren dezelfde stappen als in Hallo Hallo [vorige sectie](#deploywadarm) voor het instellen van diagnostische gegevens voor een bestaande cluster.</span><span class="sxs-lookup"><span data-stu-id="64ea2-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="64ea2-195">Hallo bijwerken `EtwEventSourceProviderConfiguration` sectie in Hallo template.json bestandsvermeldingen tooadd Hallo nieuwe EventSource kanalen voordat u Hallo configuratie toepassen met behulp van Hallo werk `New-AzureRmResourceGroupDeployment` PowerShell-opdracht.</span><span class="sxs-lookup"><span data-stu-id="64ea2-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="64ea2-196">Hallo-naam van de gebeurtenisbron Hallo is gedefinieerd als onderdeel van uw code in Hallo ServiceEventSource.cs Visual Studio gegenereerd bestand.</span><span class="sxs-lookup"><span data-stu-id="64ea2-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="64ea2-197">Als uw gebeurtenisbron mijn Eventsource heet, bijvoorbeeld Hallo volgende code tooplace Hallo gebeurtenissen uit mijn Eventsource in een tabel met de naam MyDestinationTableName toevoegen.</span><span class="sxs-lookup"><span data-stu-id="64ea2-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="64ea2-198">toocollect-prestatiemeteritems of gebeurtenislogboeken Hallo Resource Manager-sjabloon wijzigen met behulp van Hallo-voorbeelden vindt u in [virtuele Windows-machine maken met controle en diagnostische gegevens met behulp van een Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="64ea2-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="64ea2-199">Vervolgens opnieuw publiceren Hallo Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="64ea2-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64ea2-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64ea2-200">Next steps</span></span>
<span data-ttu-id="64ea2-201">toounderstand in meer detail welke gebeurtenissen u moet letten tijdens het oplossen van problemen, Zie Hallo diagnostische gebeurtenissen die worden verzonden voor [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) en [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="64ea2-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="64ea2-202">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="64ea2-202">Related articles</span></span>
* [<span data-ttu-id="64ea2-203">Meer informatie over hoe toocollect prestatiemeteritems of de logboeken met behulp van Hallo extensie voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="64ea2-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="64ea2-204">Service Fabric-oplossing in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="64ea2-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

