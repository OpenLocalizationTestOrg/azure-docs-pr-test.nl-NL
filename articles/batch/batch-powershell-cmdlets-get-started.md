---
title: Aan de slag met PowerShell voor Azure Batch | Microsoft Docs
description: Een korte inleiding in de Azure PowerShell-cmdlets die u kunt gebruiken voor het beheren van Batch-resources.
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e33be6ed658e00250ea1e80cd7da4d348fb18296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="a10e3-103">Batch-resources beheren met PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="a10e3-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="a10e3-104">Met de PowerShell-cmdlets voor Azure Batch kunt u veel dezelfde taken die u uitvoert met de Batch-API's, Azure Portal en de Azure-opdrachtregelinterface (CLI), uitvoeren en er scripts voor uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a10e3-104">With the Azure Batch PowerShell cmdlets, you can perform and script many of the same tasks you carry out with the Batch APIs, the Azure portal, and the Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="a10e3-105">Dit is een korte inleiding in de cmdlets die u kunt gebruiken om uw Batch-accounts te beheren en te werken met uw Batch-resources, zoals pools en taken.</span><span class="sxs-lookup"><span data-stu-id="a10e3-105">This is a quick introduction to the cmdlets you can use to manage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="a10e3-106">Zie [Naslaginformatie over Azure Batch-cmdlets](/powershell/module/azurerm.batch/#batch) voor een volledige lijst met Batch-cmdlets en gedetailleerde cmdlet-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="a10e3-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see the [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="a10e3-107">Dit artikel is gebaseerd op cmdlets in Azure PowerShell versie 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="a10e3-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="a10e3-108">Het wordt aangeraden Azure PowerShell regelmatig bij te werken om te profiteren van service-updates en verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="a10e3-108">We recommend that you update your Azure PowerShell frequently to take advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a10e3-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a10e3-109">Prerequisites</span></span>
<span data-ttu-id="a10e3-110">Voer de volgende bewerkingen uit als u Azure PowerShell wilt gebruiken voor het beheer van de Batch-resources.</span><span class="sxs-lookup"><span data-stu-id="a10e3-110">Perform the following operations to use Azure PowerShell to manage your Batch resources.</span></span>

* [<span data-ttu-id="a10e3-111">Azure PowerShell installeren en configureren </span><span class="sxs-lookup"><span data-stu-id="a10e3-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="a10e3-112">Voer de cmdlet **Login-AzureRmAccount** uit om verbinding te maken met uw abonnement (de Azure Batch-cmdlets zijn meegeleverd in de Azure Resource Manager-module):</span><span class="sxs-lookup"><span data-stu-id="a10e3-112">Run the **Login-AzureRmAccount** cmdlet to connect to your subscription (the Azure Batch cmdlets ship in the Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="a10e3-113">**Registreer bij de naamruimte van de Batch-provider**.</span><span class="sxs-lookup"><span data-stu-id="a10e3-113">**Register with the Batch provider namespace**.</span></span> <span data-ttu-id="a10e3-114">Deze bewerking hoeft slechts **één keer per abonnement** te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a10e3-114">This operation only needs to be performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="a10e3-115">Batch-accounts en -sleutels beheren</span><span class="sxs-lookup"><span data-stu-id="a10e3-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="a10e3-116">Batch-account maken</span><span class="sxs-lookup"><span data-stu-id="a10e3-116">Create a Batch account</span></span>
<span data-ttu-id="a10e3-117">Met **New-AzureRmBatchAccount** wordt een Batch-account in een opgegeven resourcegroep gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a10e3-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="a10e3-118">Als u nog geen resourcegroep hebt, maakt u er een door de cmdlet [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="a10e3-118">If you don't already have a resource group, create one by running the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="a10e3-119">Geef een van de Azure-gebieden op in de parameter **locatie**, bijvoorbeeld 'VS - midden'.</span><span class="sxs-lookup"><span data-stu-id="a10e3-119">Specify one of the Azure regions in the **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="a10e3-120">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a10e3-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="a10e3-121">Maak vervolgens een Batch-account in de resourcegroep, waarbij u in <*accountnaam*> een naam voor het account opgeeft, en de locatie en naam van uw resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a10e3-121">Then, create a Batch account in the resource group, specifying a name for the account in <*account_name*> and the location and name of your resource group.</span></span> <span data-ttu-id="a10e3-122">Het kan even duren voordat het Batch-account is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a10e3-122">Creating the Batch account can take some time to complete.</span></span> <span data-ttu-id="a10e3-123">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a10e3-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="a10e3-124">De Batch-accountnaam moet uniek zijn voor de Azure-regio voor de resourcegroep, minimaal 3 en maximaal 24 tekens bevatten en alleen bestaan uit kleine letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="a10e3-124">The Batch account name must be unique to the Azure region for the resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="a10e3-125">Toegangssleutels van account ophalen</span><span class="sxs-lookup"><span data-stu-id="a10e3-125">Get account access keys</span></span>
<span data-ttu-id="a10e3-126">Met **Get-AzureRmBatchAccountKeys** worden de toegangssleutels weergegeven die aan een Azure Batch-account zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a10e3-126">**Get-AzureRmBatchAccountKeys** shows the access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="a10e3-127">Voer bijvoorbeeld de volgende opdracht uit om de primaire en secundaire sleutels op te halen van het account dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a10e3-127">For example, run the following to get the primary and secondary keys of the account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="a10e3-128">Een nieuwe toegangssleutel genereren</span><span class="sxs-lookup"><span data-stu-id="a10e3-128">Generate a new access key</span></span>
<span data-ttu-id="a10e3-129">Met **New-AzureRmBatchAccountKey** wordt een nieuwe primaire of secundaire accountsleutel voor een Azure Batch-account gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="a10e3-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="a10e3-130">Typ bijvoorbeeld de volgende opdracht voor het genereren van een nieuwe primaire sleutel voor het Batch-account:</span><span class="sxs-lookup"><span data-stu-id="a10e3-130">For example, to generate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="a10e3-131">Als u een nieuwe secundaire sleutel wilt genereren, geeft u 'Secundair' op voor de parameter **KeyType**.</span><span class="sxs-lookup"><span data-stu-id="a10e3-131">To generate a new secondary key, specify "Secondary" for the **KeyType** parameter.</span></span> <span data-ttu-id="a10e3-132">U moet de primaire en secundaire sleutels afzonderlijk opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="a10e3-132">You have to regenerate the primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="a10e3-133">Batch-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="a10e3-133">Delete a Batch account</span></span>
<span data-ttu-id="a10e3-134">Met **Remove-AzureRmBatchAccount** wordt een Batch-account verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a10e3-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="a10e3-135">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a10e3-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="a10e3-136">Als hierom wordt gevraagd, bevestigt u dat u het account wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a10e3-136">When prompted, confirm you want to remove the account.</span></span> <span data-ttu-id="a10e3-137">Het kan even duren voordat het account is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a10e3-137">Account removal can take some time to complete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="a10e3-138">Een BatchAccountContext-object maken</span><span class="sxs-lookup"><span data-stu-id="a10e3-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="a10e3-139">Als u wilt verifiëren met de Batch PowerShell-cmdlets wanneer u Batch-pools, -jobs, -taken en andere -resources maakt en beheert, maakt u eerst een BatchAccountContext-object om uw accountnaam en sleutels op te slaan.</span><span class="sxs-lookup"><span data-stu-id="a10e3-139">To authenticate using the Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object to store your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="a10e3-140">U geeft het BatchAccountContext-object door aan cmdlets waarvoor de parameter **BatchContext** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a10e3-140">You pass the BatchAccountContext object into cmdlets that use the **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="a10e3-141">Standaard wordt de primaire sleutel van het account gebruikt voor verificatie, maar u kunt expliciet de te gebruiken sleutel selecteren door de eigenschap **KeyInUse** van het object BatchAccountContext te wijzigen: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="a10e3-141">By default, the account's primary key is used for authentication, but you can explicitly select the key to use by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="a10e3-142">Batch-resources maken en wijzigen</span><span class="sxs-lookup"><span data-stu-id="a10e3-142">Create and modify Batch resources</span></span>
<span data-ttu-id="a10e3-143">Gebruik cmdlets zoals **New-AzureBatchPool**, **New-AzureBatchJob** en **New-AzureBatchTask** om resources onder een Batch-account te maken.</span><span class="sxs-lookup"><span data-stu-id="a10e3-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** to create resources under a Batch account.</span></span> <span data-ttu-id="a10e3-144">Er zijn overeenkomende **Get-**- en **Set-**-cmdlets voor het bijwerken van de eigenschappen van bestaande resources en **Remove-**-cmdlets om resources onder een Batch-account te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a10e3-144">There are corresponding **Get-** and **Set-** cmdlets to update the properties of existing resources, and  **Remove-** cmdlets to remove resources under a Batch account.</span></span>

<span data-ttu-id="a10e3-145">Wanneer u veel van deze cmdlets gebruikt, moet u niet alleen een BatchContext-object doorgeven, maar ook objecten maken of doorgeven die gedetailleerde resource-instellingen bevatten, zoals weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a10e3-145">When using many of these cmdlets, in addition to passing a BatchContext object, you need to create or pass objects that contain detailed resource settings, as shown in the following example.</span></span> <span data-ttu-id="a10e3-146">Raadpleeg de gedetailleerde Help-informatie voor elke cmdlet voor meer voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="a10e3-146">See the detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="a10e3-147">Batch-pool maken</span><span class="sxs-lookup"><span data-stu-id="a10e3-147">Create a Batch pool</span></span>
<span data-ttu-id="a10e3-148">Wanneer u een Batch-pool maakt of bijwerkt, selecteert u de cloudserviceconfiguratie of de virtuele-machineconfiguratie voor het besturingssysteem op de rekenknooppunten (zie [Overzicht van Batch-functies](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="a10e3-148">When creating or updating a Batch pool, you select either the cloud service configuration or the virtual machine configuration for the operating system on the compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="a10e3-149">Als u de cloudserviceconfiguratie opgeeft, worden uw rekenknooppunten gerepliceerd met één van de [Azure-gastbesturingssysteemversies](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="a10e3-149">If you specify the cloud service configuration, your compute nodes are imaged with one of the [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="a10e3-150">Als u de VM-configuratie opgeeft, kunt u één van de ondersteunde Linux- of Windows-VM-installatiekopieën opgeven die worden vermeld in de [Azure Virtual Machines Marketplace][vm_marketplace], of u geeft een aangepaste installatiekopie op die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a10e3-150">If you specify the virtual machine configuration, you can either specify one of the supported Linux or Windows VM images listed in the [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="a10e3-151">Bij het uitvoeren van **New-AzureBatchPool** geeft u de instellingen van het besturingssysteem door in een PSCloudServiceConfiguration- of PSVirtualMachineConfiguration-object.</span><span class="sxs-lookup"><span data-stu-id="a10e3-151">When you run **New-AzureBatchPool**, pass the operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="a10e3-152">Met de volgende cmdlet wordt bijvoorbeeld een nieuwe Batch-pool gemaakt met rekenknooppunten met de grootte Klein in de cloudserviceconfiguratie, met een installatiekopie van de meest recente versie van het besturingssysteem van type 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="a10e3-152">For example, the following cmdlet creates a new Batch pool with size Small compute nodes in the cloud service configuration, imaged with the latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="a10e3-153">Hier geeft de parameter **CloudServiceConfiguration** de variabele *$configuration* op als het PSCloudServiceConfiguration-object.</span><span class="sxs-lookup"><span data-stu-id="a10e3-153">Here, the **CloudServiceConfiguration** parameter specifies the *$configuration* variable as the PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="a10e3-154">Met de parameter **BatchContext** wordt een eerder gedefinieerde variabele *$context* opgegeven als het BatchAccountContext-object.</span><span class="sxs-lookup"><span data-stu-id="a10e3-154">The **BatchContext** parameter specifies a previously defined variable *$context* as the BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="a10e3-155">Het doelaantal rekenknooppunten in de nieuwe pool wordt bepaald met een formule voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="a10e3-155">The target number of compute nodes in the new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="a10e3-156">In dit geval is de formule gewoon **$TargetDedicated=4**, waarmee wordt aangegeven dat het aantal rekenknooppunten in de pool maximaal 4 is.</span><span class="sxs-lookup"><span data-stu-id="a10e3-156">In this case, the formula is simply **$TargetDedicated=4**, indicating the number of compute nodes in the pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="a10e3-157">Query voor pools, jobs, taken en andere details</span><span class="sxs-lookup"><span data-stu-id="a10e3-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="a10e3-158">Gebruik cmdlets zoals **Get-AzureBatchPool**, **Get-AzureBatchJob** en **Get-AzureBatchTask** om een query uit te voeren voor entiteiten die zijn gemaakt onder een Batch-account.</span><span class="sxs-lookup"><span data-stu-id="a10e3-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** to query for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="a10e3-159">Query voor gegevens</span><span class="sxs-lookup"><span data-stu-id="a10e3-159">Query for data</span></span>
<span data-ttu-id="a10e3-160">Gebruik bijvoorbeeld **Get-AzureBatchPools** om uw pools te vinden.</span><span class="sxs-lookup"><span data-stu-id="a10e3-160">As an example, use **Get-AzureBatchPools** to find your pools.</span></span> <span data-ttu-id="a10e3-161">Standaard wordt deze query voor alle pools onder uw account uitgevoerd, in de veronderstelling dat u het object BatchAccountContext al hebt opgeslagen in *$context*:</span><span class="sxs-lookup"><span data-stu-id="a10e3-161">By default this queries for all pools under your account, assuming you already stored the BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="a10e3-162">Een OData-filter gebruiken</span><span class="sxs-lookup"><span data-stu-id="a10e3-162">Use an OData filter</span></span>
<span data-ttu-id="a10e3-163">U kunt een OData-filter opgeven met behulp van de parameter **Filter** om alleen de objecten te zoeken waarin u bent geïnteresseerd.</span><span class="sxs-lookup"><span data-stu-id="a10e3-163">You can supply an OData filter using the **Filter** parameter to find only the objects you’re interested in.</span></span> <span data-ttu-id="a10e3-164">U kunt bijvoorbeeld alle pools zoeken met id's die beginnen met 'myPool':</span><span class="sxs-lookup"><span data-stu-id="a10e3-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="a10e3-165">Deze methode is niet zo flexibel als het gebruik van een 'Where-Object' in een lokale pijplijn.</span><span class="sxs-lookup"><span data-stu-id="a10e3-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="a10e3-166">De query wordt rechtstreeks naar de Batch-service verzonden zodat al het filteren aan de serverzijde plaatsvindt, waardoor er internetbandbreedte wordt bespaard.</span><span class="sxs-lookup"><span data-stu-id="a10e3-166">However, the query gets sent to the Batch service directly so that all filtering happens on the server side, saving Internet bandwidth.</span></span>

### <a name="use-the-id-parameter"></a><span data-ttu-id="a10e3-167">De parameter Id gebruiken</span><span class="sxs-lookup"><span data-stu-id="a10e3-167">Use the Id parameter</span></span>
<span data-ttu-id="a10e3-168">Een alternatief voor een OData-filter is het gebruik van de parameter **Id**.</span><span class="sxs-lookup"><span data-stu-id="a10e3-168">An alternative to an OData filter is to use the **Id** parameter.</span></span> <span data-ttu-id="a10e3-169">Als u een query uit wilt voeren voor een specifieke pool met id 'myPool':</span><span class="sxs-lookup"><span data-stu-id="a10e3-169">To query for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="a10e3-170">Met de parameter **Id** wordt alleen een zoekopdracht voor een volledige id ondersteund, geen jokertekens of filters van het OData-type.</span><span class="sxs-lookup"><span data-stu-id="a10e3-170">The **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-the-maxcount-parameter"></a><span data-ttu-id="a10e3-171">De parameter MaxCount gebruiken</span><span class="sxs-lookup"><span data-stu-id="a10e3-171">Use the MaxCount parameter</span></span>
<span data-ttu-id="a10e3-172">Standaard worden met elke cmdlet maximaal 1000 objecten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="a10e3-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="a10e3-173">Als deze limiet is bereikt, moet u uw filter verfijnen zodat er minder objecten worden opgehaald, of moet u expliciet een maximum instellen met de parameter **MaxCount**.</span><span class="sxs-lookup"><span data-stu-id="a10e3-173">If you reach this limit, either refine your filter to bring back fewer objects, or explicitly set a maximum using the **MaxCount** parameter.</span></span> <span data-ttu-id="a10e3-174">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a10e3-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="a10e3-175">Als u de bovengrens wilt verwijderen, stelt u **MaxCount** in op 0 of minder.</span><span class="sxs-lookup"><span data-stu-id="a10e3-175">To remove the upper bound, set **MaxCount** to 0 or less.</span></span>

### <a name="use-the-powershell-pipeline"></a><span data-ttu-id="a10e3-176">De PowerShell-pijplijn gebruiken</span><span class="sxs-lookup"><span data-stu-id="a10e3-176">Use the PowerShell pipeline</span></span>
<span data-ttu-id="a10e3-177">Met Batch-cmdlets kunt u gebruikmaken van de PowerShell-pijplijn om gegevens tussen cmdlets te verzenden.</span><span class="sxs-lookup"><span data-stu-id="a10e3-177">Batch cmdlets can leverage the PowerShell pipeline to send data between cmdlets.</span></span> <span data-ttu-id="a10e3-178">Dit heeft hetzelfde effect als het opgeven van een parameter, maar het vergemakkelijkt het werken met meerdere entiteiten.</span><span class="sxs-lookup"><span data-stu-id="a10e3-178">This has the same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="a10e3-179">Zo kunt u bijvoorbeeld alle taken onder uw account zoeken en weergeven:</span><span class="sxs-lookup"><span data-stu-id="a10e3-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="a10e3-180">Start elk computerknooppunt in een groep opnieuw op:</span><span class="sxs-lookup"><span data-stu-id="a10e3-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="a10e3-181">Beheer van toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="a10e3-181">Application package management</span></span>
<span data-ttu-id="a10e3-182">Toepassingspakketten bieden een vereenvoudigde manier om toepassingen te implementeren op de rekenknooppunten in groepen.</span><span class="sxs-lookup"><span data-stu-id="a10e3-182">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span></span> <span data-ttu-id="a10e3-183">Met de Batch PowerShell-cmdlets kunt u toepassingspakketten in uw Batch-account uploaden en beheren, en pakketversies implementeren op rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="a10e3-183">With the Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions to compute nodes.</span></span>

<span data-ttu-id="a10e3-184">Een toepassing **maken**:</span><span class="sxs-lookup"><span data-stu-id="a10e3-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="a10e3-185">Een toepassingspakket **toevoegen**:</span><span class="sxs-lookup"><span data-stu-id="a10e3-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="a10e3-186">Stel de **standaardversie** voor de toepassing in:</span><span class="sxs-lookup"><span data-stu-id="a10e3-186">Set the **default version** for the application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="a10e3-187">**Geeft een overzicht van** de pakketten van een toepassing</span><span class="sxs-lookup"><span data-stu-id="a10e3-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="a10e3-188">Een toepassingspakket **verwijderen**</span><span class="sxs-lookup"><span data-stu-id="a10e3-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="a10e3-189">Een toepassing **verwijderen**</span><span class="sxs-lookup"><span data-stu-id="a10e3-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="a10e3-190">Voordat u de toepassing verwijdert, moet u alle versies van de toepassingspakketten van een toepassing verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a10e3-190">You must delete all of an application's application package versions before you delete the application.</span></span> <span data-ttu-id="a10e3-191">U ontvangt een 'conflictfout' als u een toepassing probeert te verwijderen die nog toepassingspakketten heeft.</span><span class="sxs-lookup"><span data-stu-id="a10e3-191">You will receive a 'Conflict' error if you try to delete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="a10e3-192">Een toepassingspakket implementeren</span><span class="sxs-lookup"><span data-stu-id="a10e3-192">Deploy an application package</span></span>
<span data-ttu-id="a10e3-193">U kunt een of meer toepassingspakketten voor implementatie opgeven wanneer u een groep maakt.</span><span class="sxs-lookup"><span data-stu-id="a10e3-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="a10e3-194">Wanneer u een pakket opgeeft tijdens het maken van een groep, wordt dit pakket geïmplementeerd op elk knooppunt dat wordt gekoppeld aan de groep.</span><span class="sxs-lookup"><span data-stu-id="a10e3-194">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span></span> <span data-ttu-id="a10e3-195">Pakketten worden ook geïmplementeerd als een knooppunt opnieuw wordt gestart of teruggezet.</span><span class="sxs-lookup"><span data-stu-id="a10e3-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="a10e3-196">Geef de optie voor `-ApplicationPackageReference` op als u een groep maakt, zodat een toepassingspakket wordt geïmplementeerd naar de knooppunten van de groep wanneer deze lid worden van de groep.</span><span class="sxs-lookup"><span data-stu-id="a10e3-196">Specify the `-ApplicationPackageReference` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span></span> <span data-ttu-id="a10e3-197">Maak eerst een **PSApplicationPackageReference**-object en configureer dit met de toepassings-id en pakketversie die u wilt implementeren op de rekenknooppunten van de groep:</span><span class="sxs-lookup"><span data-stu-id="a10e3-197">First, create a **PSApplicationPackageReference** object, and configure it with the application Id and package version you want to deploy to the pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="a10e3-198">Nu maakt u de adresgroep en geeft u het pakketverwijzingsobject op als het argument voor de optie `ApplicationPackageReferences`:</span><span class="sxs-lookup"><span data-stu-id="a10e3-198">Now create the pool, and specify the package reference object as the argument to the `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="a10e3-199">Zie [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) (Toepassingen implementeren naar rekenknooppunten met Batch-toepassingspakketten) voor meer informatie over toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="a10e3-199">You can find more information on application packages in [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a10e3-200">U moet [een Azure Storage-account koppelen](#linked-storage-account-autostorage) aan het Batch-account om toepassingspakketten te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a10e3-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="a10e3-201">De toepassingspakketten van een groep bijwerken</span><span class="sxs-lookup"><span data-stu-id="a10e3-201">Update a pool's application packages</span></span>
<span data-ttu-id="a10e3-202">Als u de toepassingen wilt bijwerken die zijn toegewezen aan een bestaande groep, maakt u eerst een PSApplicationPackageReference-object met de gewenste eigenschappen (toepassings-id en pakketversie):</span><span class="sxs-lookup"><span data-stu-id="a10e3-202">To update the applications assigned to an existing pool, first create a PSApplicationPackageReference object with the desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="a10e3-203">Vervolgens haalt u de adresgroep op uit Batch, wist u eventuele bestaande pakketten, voegt u de nieuwe pakketverwijzing toe en werkt u de Batch-service bij met de nieuwe adresgroepinstellingen:</span><span class="sxs-lookup"><span data-stu-id="a10e3-203">Next, get the pool from Batch, clear out any existing packages, add our new package reference, and update the Batch service with the new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="a10e3-204">Nu hebt u de eigenschappen van de adresgroep bijgewerkt in de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="a10e3-204">You've now updated the pool's properties in the Batch service.</span></span> <span data-ttu-id="a10e3-205">Voor de werkelijke implementatie van het nieuwe toepassingspakket op rekenknooppunten in de adresgroep moet u deze knooppunten echter opnieuw starten of de installatiekopie ervan terugzetten.</span><span class="sxs-lookup"><span data-stu-id="a10e3-205">To actually deploy the new application package to compute nodes in the pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="a10e3-206">U kunt elk knooppunt in een adresgroep met de volgende opdracht opnieuw starten:</span><span class="sxs-lookup"><span data-stu-id="a10e3-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="a10e3-207">U kunt meerdere toepassingspakketten op de rekenknooppunten in de adresgroep implementeren.</span><span class="sxs-lookup"><span data-stu-id="a10e3-207">You can deploy multiple application packages to the compute nodes in a pool.</span></span> <span data-ttu-id="a10e3-208">Als u een toepassingspakket wilt *toevoegen* in plaats van de huidige geïmplementeerde pakketten te vervangen, laat dan de `$pool.ApplicationPackageReferences.Clear()`-regel hierboven weg.</span><span class="sxs-lookup"><span data-stu-id="a10e3-208">If you'd like to *add* an application package instead of replacing the currently deployed packages, omit the `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a10e3-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a10e3-209">Next steps</span></span>
* <span data-ttu-id="a10e3-210">Zie [Naslaginformatie over Azure Batch-cmdlets](/powershell/module/azurerm.batch/#batch) voor gedetailleerde cmdlet-syntaxis en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="a10e3-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="a10e3-211">Zie [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) (Toepassingen implementeren naar rekenknooppunten met Batch-toepassingspakketten) voor meer informatie over toepassingen en toepassingspakketten in Batch.</span><span class="sxs-lookup"><span data-stu-id="a10e3-211">For more information about applications and application packages in Batch, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/