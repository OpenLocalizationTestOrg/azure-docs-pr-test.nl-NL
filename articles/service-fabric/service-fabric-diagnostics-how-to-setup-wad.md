---
title: Logboeken verzamelen met behulp van Azure Diagnostics | Microsoft Docs
description: Dit artikel wordt beschreven hoe u Azure Diagnostics instelt voor het verzamelen van Logboeken van een Service Fabric-cluster in Azure wordt uitgevoerd.
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
ms.openlocfilehash: 190a8a393f2e7d74a792db4efa81f94a18b02221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="81d18-103">Logboeken verzamelen met Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="81d18-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81d18-104">Windows</span><span class="sxs-lookup"><span data-stu-id="81d18-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="81d18-105">Linux</span><span class="sxs-lookup"><span data-stu-id="81d18-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="81d18-106">Wanneer u een Azure Service Fabric-cluster uitvoert, is het een goed idee de logboeken verzamelen van alle knooppunten in een centrale locatie.</span><span class="sxs-lookup"><span data-stu-id="81d18-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="81d18-107">De logboeken die in een centrale locatie, helpt u bij het analyseren en oplossen van problemen in het cluster of problemen in de toepassingen en services die worden uitgevoerd in het cluster.</span><span class="sxs-lookup"><span data-stu-id="81d18-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="81d18-108">Een manier om te uploaden en verzamelen van Logboeken is het gebruik van de extensie Azure Diagnostics, die logboeken naar Azure Storage of Azure Application Insights Azure Event Hubs uploadt.</span><span class="sxs-lookup"><span data-stu-id="81d18-108">One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="81d18-109">Er zijn geen de logboeken die handig zijn in de opslag of in Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="81d18-109">The logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="81d18-110">Maar u kunt een extern proces gebruiken om te lezen van de gebeurtenissen uit de opslag en plaats deze in een product zoals [logboekanalyse](../log-analytics/log-analytics-service-fabric.md) of een andere oplossing voor het parseren van het logboek.</span><span class="sxs-lookup"><span data-stu-id="81d18-110">But you can use an external process to read the events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="81d18-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) wordt geleverd met een uitgebreide zoeken en analytics logboekservice ingebouwde.</span><span class="sxs-lookup"><span data-stu-id="81d18-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81d18-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="81d18-112">Prerequisites</span></span>
<span data-ttu-id="81d18-113">U kunt deze hulpprogramma's gebruiken enkele bewerkingen uitvoeren in dit document:</span><span class="sxs-lookup"><span data-stu-id="81d18-113">You use these tools to perform some of the operations in this document:</span></span>

* <span data-ttu-id="81d18-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (gerelateerd aan Azure Cloud Services, maar heeft goede informatie over en voorbeelden)</span><span class="sxs-lookup"><span data-stu-id="81d18-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="81d18-115">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="81d18-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="81d18-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="81d18-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="81d18-117">Azure Resource Manager-client</span><span class="sxs-lookup"><span data-stu-id="81d18-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="81d18-118">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="81d18-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-to-collect"></a><span data-ttu-id="81d18-119">Logboek bronnen die u wilt verzamelen</span><span class="sxs-lookup"><span data-stu-id="81d18-119">Log sources that you might want to collect</span></span>
* <span data-ttu-id="81d18-120">**Service Fabric-logboeken**: van het platform standaard Event Tracing voor Windows (ETW) en EventSource kanalen verzonden.</span><span class="sxs-lookup"><span data-stu-id="81d18-120">**Service Fabric logs**: Emitted from the platform to standard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="81d18-121">Logboeken kunnen een van de verschillende typen zijn:</span><span class="sxs-lookup"><span data-stu-id="81d18-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="81d18-122">Operationele gebeurtenissen: logboeken voor bewerkingen waarmee de Service Fabric-platform.</span><span class="sxs-lookup"><span data-stu-id="81d18-122">Operational events: Logs for operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="81d18-123">Voorbeelden zijn onder meer het maken van toepassingen en services, knooppunt statuswijzigingen en informatie over de upgrade.</span><span class="sxs-lookup"><span data-stu-id="81d18-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="81d18-124">Reliable Actors programming model gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="81d18-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="81d18-125">Reliable Services programming model gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="81d18-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="81d18-126">**Toepassingsgebeurtenissen**: gebeurtenissen verzonden vanuit de code van uw service en geschreven met behulp van de EventSource helperklasse opgegeven in de Visual Studio-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="81d18-126">**Application events**: Events emitted from your service's code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="81d18-127">Zie voor meer informatie over het schrijven van Logboeken van uw toepassing [bewaken en onderzoeken van services in de instellingen voor een lokale computer ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="81d18-127">For more information on how to write logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="81d18-128">De extensie voor diagnostische gegevens implementeren</span><span class="sxs-lookup"><span data-stu-id="81d18-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="81d18-129">De eerste stap bij het verzamelen van Logboeken is voor het implementeren van de extensie voor diagnostische gegevens over elk van de virtuele machines in het Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="81d18-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="81d18-130">De extensie voor diagnostische gegevens verzamelt logboeken op elke virtuele machine en geüpload naar het opslagaccount dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="81d18-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="81d18-131">De stappen verschillen enigszins op basis van of u de Azure portal of Azure Resource Manager gebruiken.</span><span class="sxs-lookup"><span data-stu-id="81d18-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="81d18-132">De stappen ook variëren, afhankelijk van of de implementatie maakt deel uit van het maken van het cluster of voor een cluster dat al bestaat.</span><span class="sxs-lookup"><span data-stu-id="81d18-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="81d18-133">Bekijk de stappen voor elk scenario.</span><span class="sxs-lookup"><span data-stu-id="81d18-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-the-portal"></a><span data-ttu-id="81d18-134">De extensie voor diagnostische gegevens als onderdeel van het maken van het cluster via de portal implementeren</span><span class="sxs-lookup"><span data-stu-id="81d18-134">Deploy the Diagnostics extension as part of cluster creation through the portal</span></span>
<span data-ttu-id="81d18-135">Als u wilt implementeren de extensie voor diagnostische gegevens op de virtuele machines in het cluster als onderdeel van het maken van het cluster, moet u het instellingenpaneel voor diagnostische gegevens dat wordt weergegeven in de volgende afbeelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="81d18-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image.</span></span> <span data-ttu-id="81d18-136">Zorg ervoor dat Diagnostics is ingesteld op zodat Reliable Actors of Reliable Services gebeurtenisverzameling **op** (de standaardinstelling).</span><span class="sxs-lookup"><span data-stu-id="81d18-136">To enable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="81d18-137">Nadat u het cluster hebt gemaakt, kunt u deze instellingen niet wijzigen met behulp van de portal.</span><span class="sxs-lookup"><span data-stu-id="81d18-137">After you create the cluster, you can't change these settings by using the portal.</span></span>

![Azure Diagnostics-instellingen in de portal voor het maken van het cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="81d18-139">Het ondersteuningsteam van Azure *vereist* ondersteuning voor de logboeken om te helpen bij het oplossen van eventuele ondersteuningsaanvragen die u maakt.</span><span class="sxs-lookup"><span data-stu-id="81d18-139">The Azure support team *requires* support logs to help resolve any support requests that you create.</span></span> <span data-ttu-id="81d18-140">Deze logboeken worden in realtime verzameld en worden opgeslagen in een van de storage-accounts in de resourcegroep hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="81d18-140">These logs are collected in real time and are stored in one of the storage accounts created in the resource group.</span></span> <span data-ttu-id="81d18-141">De diagnostische instellingen configureren op toepassingsniveau gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="81d18-141">The Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="81d18-142">Deze gebeurtenissen opnemen [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) gebeurtenissen, [Reliable Services](service-fabric-reliable-services-diagnostics.md) en sommige gebeurtenissen op systeemniveau Service Fabric worden opgeslagen in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="81d18-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events to be stored in Azure Storage.</span></span>

<span data-ttu-id="81d18-143">Producten zoals [Elasticsearch](https://www.elastic.co/guide/index.html) of uw eigen proces, krijgen de gebeurtenissen van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="81d18-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get the events from the storage account.</span></span> <span data-ttu-id="81d18-144">Er is momenteel geen manier om te filteren of Let op de gebeurtenissen die worden verzonden naar de tabel.</span><span class="sxs-lookup"><span data-stu-id="81d18-144">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="81d18-145">Als u een proces voor het verwijderen van gebeurtenissen uit de tabel niet implementeert, wordt de tabel blijven groeien.</span><span class="sxs-lookup"><span data-stu-id="81d18-145">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span>

<span data-ttu-id="81d18-146">Wanneer u een cluster met behulp van de portal maakt, wordt ten zeerste aanbevolen dat u de sjabloon downloaden **voordat u op OK** om het cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="81d18-146">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="81d18-147">Raadpleeg voor meer informatie, [een Service Fabric-cluster instellen met behulp van een Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="81d18-147">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="81d18-148">U moet de sjabloon wijzigingen later aanbrengen omdat u geen enkele wijzigingen aanbrengen met behulp van de portal.</span><span class="sxs-lookup"><span data-stu-id="81d18-148">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

<span data-ttu-id="81d18-149">U kunt sjablonen exporteren vanuit de portal met behulp van de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="81d18-149">You can export templates from the portal by using the following steps.</span></span> <span data-ttu-id="81d18-150">Deze sjablonen mag moeilijker te gebruiken, omdat ze wellicht hebben null-waarden die vereiste informatie ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="81d18-150">However, these templates can be more difficult to use because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="81d18-151">Open uw resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="81d18-151">Open your resource group.</span></span>
2. <span data-ttu-id="81d18-152">Selecteer **instellingen** om het deelvenster instellingen openen.</span><span class="sxs-lookup"><span data-stu-id="81d18-152">Select **Settings** to display the settings panel.</span></span>
3. <span data-ttu-id="81d18-153">Selecteer **implementaties** om het deelvenster implementatie historie weer te geven.</span><span class="sxs-lookup"><span data-stu-id="81d18-153">Select **Deployments** to display the deployment history panel.</span></span>
4. <span data-ttu-id="81d18-154">Selecteer een implementatie om de details van de implementatie weer te geven.</span><span class="sxs-lookup"><span data-stu-id="81d18-154">Select a deployment to display the details of the deployment.</span></span>
5. <span data-ttu-id="81d18-155">Selecteer **exportsjabloon** om het deelvenster sjabloon weer te geven.</span><span class="sxs-lookup"><span data-stu-id="81d18-155">Select **Export Template** to display the template panel.</span></span>
6. <span data-ttu-id="81d18-156">Selecteer **opslaan naar bestand** exporteren van een ZIP-bestand dat de sjabloon, een parameter en een PowerShell-bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="81d18-156">Select **Save to file** to export a .zip file that contains the template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="81d18-157">Nadat u de bestanden hebt geëxporteerd, moet u een wijziging aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="81d18-157">After you export the files, you need to make a modification.</span></span> <span data-ttu-id="81d18-158">Bewerk het bestand parameters.json en verwijder de **adminPassword** element.</span><span class="sxs-lookup"><span data-stu-id="81d18-158">Edit the parameters.json file and remove the **adminPassword** element.</span></span> <span data-ttu-id="81d18-159">Hierdoor wordt een wachtwoord wordt gevraagd wanneer het script voor implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="81d18-159">This will cause a prompt for the password when the deployment script is run.</span></span> <span data-ttu-id="81d18-160">Wanneer u het script voor implementatie uitvoert, moet u wellicht los van null-parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="81d18-160">When you're running the deployment script, you might have to fix null parameter values.</span></span>

<span data-ttu-id="81d18-161">De gedownloade sjabloon gebruiken een configuratie bij te werken:</span><span class="sxs-lookup"><span data-stu-id="81d18-161">To use the downloaded template to update a configuration:</span></span>

1. <span data-ttu-id="81d18-162">Pak de inhoud naar een map op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="81d18-162">Extract the contents to a folder on your local computer.</span></span>
2. <span data-ttu-id="81d18-163">De inhoud naar aanleiding van de nieuwe configuratie niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="81d18-163">Modify the contents to reflect the new configuration.</span></span>
3. <span data-ttu-id="81d18-164">Start PowerShell en Ga naar de map waar u de inhoud hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="81d18-164">Start PowerShell and change to the folder where you extracted the content.</span></span>
4. <span data-ttu-id="81d18-165">Voer **deploy.ps1** en vul de abonnements-ID, de Resourcegroepnaam (Gebruik dezelfde naam van de configuratie bijwerken) en de naam van een unieke implementatie.</span><span class="sxs-lookup"><span data-stu-id="81d18-165">Run **deploy.ps1** and fill in the subscription ID, the resource group name (use the same name to update the configuration), and a unique deployment name.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="81d18-166">De extensie voor diagnostische gegevens als onderdeel van het maken van het cluster implementeren met behulp van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="81d18-166">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="81d18-167">Voor het maken van een cluster met Resource Manager, moet u de configuratie van diagnostische JSON toevoegen aan het volledige cluster Resource Manager-sjabloon voordat u het cluster maakt.</span><span class="sxs-lookup"><span data-stu-id="81d18-167">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="81d18-168">We bieden een voorbeeldsjabloon vijf VM-cluster Resource Manager met de configuratie van diagnostische toegevoegd als onderdeel van onze voorbeelden Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="81d18-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="81d18-169">U kunt het zien op deze locatie in de galerie van Azure Samples: [cluster met vijf knooppunten met diagnostische gegevens van Resource Manager-sjabloon voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="81d18-169">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="81d18-170">Als u de instelling van de diagnostische gegevens in de Resource Manager-sjabloon, open het bestand azuredeploy.json en zoeken naar **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="81d18-170">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="81d18-171">Als u een cluster met behulp van deze sjabloon, selecteert de **implementeren in Azure** knop beschikbaar op de vorige koppeling.</span><span class="sxs-lookup"><span data-stu-id="81d18-171">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="81d18-172">U kunt ook u kunt het Resource Manager-voorbeeld downloaden, wijzigingen aanbrengen en een cluster maken met de gewijzigde sjabloon met behulp van de `New-AzureRmResourceGroupDeployment` opdracht in een Azure PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="81d18-172">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="81d18-173">Zie de volgende code voor de parameters die u aan de opdracht doorgeeft.</span><span class="sxs-lookup"><span data-stu-id="81d18-173">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="81d18-174">Zie het artikel voor gedetailleerde informatie over het implementeren van een resourcegroep met behulp van PowerShell [een resourcegroep implementeren met de Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="81d18-174">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="81d18-175">De extensie voor diagnostische gegevens aan een bestaand cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="81d18-175">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="81d18-176">Als u een bestaand cluster dat geen diagnostische gegevens die zijn geïmplementeerd, of als u wilt wijzigen van een bestaande configuratie, kunt u deze kunt toevoegen of bijwerken.</span><span class="sxs-lookup"><span data-stu-id="81d18-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="81d18-177">Wijzig de Resource Manager-sjabloon die wordt gebruikt voor het maken van het bestaande cluster of de sjabloon downloaden van de portal, zoals eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="81d18-177">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="81d18-178">Het bestand template.json wijzigen door de volgende taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="81d18-178">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="81d18-179">Een nieuwe opslagresource toevoegen aan de sjabloon door toe te voegen aan de bronnensectie.</span><span class="sxs-lookup"><span data-stu-id="81d18-179">Add a new storage resource to the template by adding to the resources section.</span></span>

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

 <span data-ttu-id="81d18-180">Vervolgens voegt u het gedeelte parameters direct na de definities van de account opslag tussen `supportLogStorageAccountName` en `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="81d18-180">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="81d18-181">Vervang de tijdelijke aanduiding voor tekst *opslagaccountnaam hier* met de naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="81d18-181">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="81d18-182">Werk vervolgens de `VirtualMachineProfile` gedeelte van het bestand template.json door de volgende code binnen de matrix extensies toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="81d18-182">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="81d18-183">Zorg ervoor dat een komma toe te voegen aan het begin of einde, afhankelijk van waar het ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="81d18-183">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="81d18-184">Nadat u het bestand template.json aanpassen zoals is beschreven, publiceert u de Resource Manager-sjabloon opnieuw.</span><span class="sxs-lookup"><span data-stu-id="81d18-184">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="81d18-185">Als de sjabloon is geëxporteerd, het bestand deploy.ps1 uitvoert rapport opnieuw publiceert de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="81d18-185">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="81d18-186">Nadat u hebt geïmplementeerd, zorg ervoor dat **ProvisioningState** is **geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="81d18-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-to-collect-health-and-load-events"></a><span data-ttu-id="81d18-187">Bijwerken van diagnostische gegevens te verzamelen health gebeurtenissen laden</span><span class="sxs-lookup"><span data-stu-id="81d18-187">Update diagnostics to collect health and load events</span></span>

<span data-ttu-id="81d18-188">Beginnen met de 5,4 release van Service Fabric, zijn status en load metrische gebeurtenissen beschikbaar voor de verzameling.</span><span class="sxs-lookup"><span data-stu-id="81d18-188">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="81d18-189">Deze gebeurtenissen gebeurtenissen die door het systeem of uw code worden gegenereerd met behulp van de status aangeven of rapportage-API's, zoals laden [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) of [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="81d18-189">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="81d18-190">Hierdoor kan voor het aggregeren en weergeven van systeemstatus na verloop van tijd en voor waarschuwingen op basis van status- of load-gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="81d18-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="81d18-191">Om weer te geven deze gebeurtenissen in Visual Studio diagnostische logboeken toevoegen ' Microsoft-ServiceFabric:4:0x4000000000000008 ' aan de lijst met ETW-providers.</span><span class="sxs-lookup"><span data-stu-id="81d18-191">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="81d18-192">Voor het verzamelen van gebeurtenissen, wijzigt u de resource manager-sjabloon wilt opnemen</span><span class="sxs-lookup"><span data-stu-id="81d18-192">To collect the events, modify the resource manager template to include</span></span>

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

## <a name="update-diagnostics-to-collect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="81d18-193">Bijwerken van diagnostische gegevens om te verzamelen en logboeken van de nieuwe EventSource kanalen uploaden</span><span class="sxs-lookup"><span data-stu-id="81d18-193">Update Diagnostics to collect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="81d18-194">Voor het bijwerken van diagnostische gegevens voor het verzamelen van Logboeken van de nieuwe EventSource kanalen die vertegenwoordigen een nieuwe toepassing die u wilt implementeren, voeren dezelfde stappen als in de [vorige sectie](#deploywadarm) voor het instellen van diagnostische gegevens voor een bestaand cluster.</span><span class="sxs-lookup"><span data-stu-id="81d18-194">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as in the [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="81d18-195">Werk de `EtwEventSourceProviderConfiguration` sectie in het bestand template.json vermeldingen toevoegen voor de nieuwe EventSource kanalen voordat u de configuratie toepassen met behulp van bijwerken de `New-AzureRmResourceGroupDeployment` PowerShell-opdracht.</span><span class="sxs-lookup"><span data-stu-id="81d18-195">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="81d18-196">De naam van de bron van de gebeurtenis wordt gedefinieerd als onderdeel van uw code in het bestand ServiceEventSource.cs Visual Studio gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="81d18-196">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="81d18-197">Als uw gebeurtenisbron mijn Eventsource heet, bijvoorbeeld de volgende code om de gebeurtenissen uit mijn Eventsource plaatsen in een tabel met de naam MyDestinationTableName toevoegen.</span><span class="sxs-lookup"><span data-stu-id="81d18-197">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="81d18-198">Wijzigen voor het verzamelen van prestatiemeteritems of de gebeurtenislogboeken van de Resource Manager-sjabloon met behulp van de voorbeelden die is opgegeven in [virtuele Windows-machine maken met controle en diagnostische gegevens met behulp van een Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="81d18-198">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="81d18-199">Vervolgens publiceert u de Resource Manager-sjabloon opnieuw.</span><span class="sxs-lookup"><span data-stu-id="81d18-199">Then, republish the Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81d18-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81d18-200">Next steps</span></span>
<span data-ttu-id="81d18-201">Zie de diagnostische gebeurtenissen verzonden voor inzicht in meer detail welke gebeurtenissen u letten moet tijdens het oplossen van problemen [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) en [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="81d18-201">To understand in more detail what events you should look for while troubleshooting issues, see the diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="81d18-202">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="81d18-202">Related articles</span></span>
* [<span data-ttu-id="81d18-203">Meer informatie over het verzamelen van prestatiemeteritems of logboeken met behulp van de extensie voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="81d18-203">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="81d18-204">Service Fabric-oplossing in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="81d18-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

