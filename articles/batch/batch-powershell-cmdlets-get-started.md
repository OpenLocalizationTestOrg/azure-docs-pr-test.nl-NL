---
title: aaaGet gestart met PowerShell voor Azure Batch | Microsoft Docs
description: Een korte inleiding toohello Azure PowerShell-cmdlets kunt u toomanage Batch-resources.
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
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="3bb1c-103">Batch-resources beheren met PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="3bb1c-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="3bb1c-104">Hello Azure Batch PowerShell-cmdlets, kunt u uitvoeren en veel van Hallo script dezelfde taken die u uitvoert met de Batch-API's Hallo hello Azure-portal en hello Azure-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="3bb1c-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="3bb1c-105">Dit is een korte inleiding toohello-cmdlets kunt u gebruiken toomanage uw Batch-accounts en werken met uw Batch-resources zoals pools, jobs en taken.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="3bb1c-106">Zie voor een volledige lijst van Batch-cmdlets en gedetailleerde cmdlet-syntaxis Hallo [naslaginformatie over Azure Batch-cmdlets](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="3bb1c-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="3bb1c-107">Dit artikel is gebaseerd op cmdlets in Azure PowerShell versie 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="3bb1c-108">We bevelen aan dat u uw Azure PowerShell regelmatig tootake profiteren van de service-updates en verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bb1c-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3bb1c-109">Prerequisites</span></span>
<span data-ttu-id="3bb1c-110">Hallo operations toouse Azure PowerShell toomanage na uw Batch-resources uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="3bb1c-111">Azure PowerShell installeren en configureren </span><span class="sxs-lookup"><span data-stu-id="3bb1c-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="3bb1c-112">Voer Hallo **Login-AzureRmAccount** cmdlet tooconnect tooyour abonnement (hello Azure Batch-cmdlets verzenden in hello Azure Resource Manager-module):</span><span class="sxs-lookup"><span data-stu-id="3bb1c-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="3bb1c-113">**Registreren bij de naamruimte van de provider Batch Hallo**.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="3bb1c-114">Deze bewerking hoeft slechts toobe uitgevoerd **eenmaal per abonnement**.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="3bb1c-115">Batch-accounts en -sleutels beheren</span><span class="sxs-lookup"><span data-stu-id="3bb1c-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="3bb1c-116">Batch-account maken</span><span class="sxs-lookup"><span data-stu-id="3bb1c-116">Create a Batch account</span></span>
<span data-ttu-id="3bb1c-117">Met **New-AzureRmBatchAccount** wordt een Batch-account in een opgegeven resourcegroep gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="3bb1c-118">Als u nog een resourcegroep hebt, maakt een door Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="3bb1c-119">Geef een hello Azure gebieden in Hallo **locatie** parameter, zoals 'VS-midden'.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="3bb1c-120">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="3bb1c-121">Maak een Batch-account in de resourcegroep hello, Hallo-account in een naam geven <*account_name*> en Hallo locatie en naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="3bb1c-122">Hallo Batch-account maken kan sommige toocomplete tijd in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="3bb1c-123">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="3bb1c-124">Hallo Batch-account is de naam moet uniek toohello Azure-regio voor de resourcegroep Hallo tussen 3 en 24 tekens bevatten en gebruik alleen kleine letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="3bb1c-125">Toegangssleutels van account ophalen</span><span class="sxs-lookup"><span data-stu-id="3bb1c-125">Get account access keys</span></span>
<span data-ttu-id="3bb1c-126">**Get-AzureRmBatchAccountKeys** toont Hallo toegangstoetsen die zijn gekoppeld aan een Azure Batch-account.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="3bb1c-127">Bijvoorbeeld uitvoeren Hallo na tooget Hallo primaire en secundaire sleutels van Hallo-account voor die u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="3bb1c-128">Een nieuwe toegangssleutel genereren</span><span class="sxs-lookup"><span data-stu-id="3bb1c-128">Generate a new access key</span></span>
<span data-ttu-id="3bb1c-129">Met **New-AzureRmBatchAccountKey** wordt een nieuwe primaire of secundaire accountsleutel voor een Azure Batch-account gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="3bb1c-130">Typ bijvoorbeeld toogenerate een nieuwe primaire sleutel voor uw Batch-account:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="3bb1c-131">een nieuwe secundaire sleutel toogenerate 'Secundair' opgeeft voor Hallo **KeyType** parameter.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="3bb1c-132">U hebben tooregenerate Hallo primaire en secundaire sleutels afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="3bb1c-133">Batch-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="3bb1c-133">Delete a Batch account</span></span>
<span data-ttu-id="3bb1c-134">Met **Remove-AzureRmBatchAccount** wordt een Batch-account verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="3bb1c-135">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="3bb1c-136">Wanneer u wordt gevraagd, bevestig gewenste tooremove Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="3bb1c-137">Account is verwijderd, kan sommige toocomplete tijd duren.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="3bb1c-138">Een BatchAccountContext-object maken</span><span class="sxs-lookup"><span data-stu-id="3bb1c-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="3bb1c-139">met behulp van tooauthenticate Batch PowerShell-cmdlets hello, wanneer u maken en beheren van Batch-pools, jobs, taken en andere resources, maak eerst een BatchAccountContext-object toostore uw accountnaam en sleutels:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="3bb1c-140">U die gebruik Hallo Hallo BatchAccountContext-object in cmdlets doorgeven **BatchContext** parameter.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="3bb1c-141">Standaard de primaire sleutel van het Hallo-account wordt gebruikt voor verificatie, maar u kunt Hallo sleutel toouse expliciet selecteren door te wijzigen van het object BatchAccountContext **KeyInUse** eigenschap: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="3bb1c-142">Batch-resources maken en wijzigen</span><span class="sxs-lookup"><span data-stu-id="3bb1c-142">Create and modify Batch resources</span></span>
<span data-ttu-id="3bb1c-143">Gebruik cmdlets zoals **New-AzureBatchPool**, **New-AzureBatchJob**, en **New-AzureBatchTask** toocreate resources onder een Batch-account.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="3bb1c-144">Er zijn overeenkomende **Get -** en **Set -** cmdlets tooupdate Hallo eigenschappen van bestaande bronnen, en **Remove -** cmdlets tooremove resources onder een Batch-account.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="3bb1c-145">Wanneer u veel van deze cmdlets in toevoeging toopassing een BatchContext-object, of u kunt toocreate objecten die gedetailleerde broninstellingen bevatten, zoals wordt weergegeven in het volgende voorbeeld Hallo doorgeeft.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="3bb1c-146">Zie Hallo gedetailleerde Help-informatie voor elke cmdlet voor meer voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="3bb1c-147">Batch-pool maken</span><span class="sxs-lookup"><span data-stu-id="3bb1c-147">Create a Batch pool</span></span>
<span data-ttu-id="3bb1c-148">Bij het maken of bijwerken van een Batch-pool, u Hallo cloud serviceconfiguratie of virtuele-machineconfiguratie Hallo selecteren voor hello besturingssysteem op Hallo rekenknooppunten (Zie [overzicht Batch-functies](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="3bb1c-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="3bb1c-149">Als u de configuratie voor cloud service Hallo opgeeft, uw rekenknooppunten installatiekopie gemaakt wordt met een Hallo [Azure Gast OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="3bb1c-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="3bb1c-150">Als u de configuratie van de virtuele machine Hallo opgeeft, kunt u opgeven of installatiekopieën van virtuele machine van Windows hello opgenomen in een van de Hallo Linux ondersteund [Azure Virtual Machines Marketplace][vm_marketplace], of geef een aangepaste afbeelding die u hebt voorbereid.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="3bb1c-151">Bij het uitvoeren van **New-AzureBatchPool**, besturingssysteeminstellingen Hallo doorgeven in een PSCloudServiceConfiguration of PSVirtualMachineConfiguration object.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="3bb1c-152">Bijvoorbeeld: hello volgende cmdlet maakt een nieuwe Batch-pool met grootte klein rekenknooppunten in Hallo cloud service-configuratie, wordt een installatiekopie gemaakt met de Hallo nieuwste besturingssysteemversie van type 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="3bb1c-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="3bb1c-153">Hier Hallo **CloudServiceConfiguration** parameter geeft u op Hallo *$configuration* variabele als Hallo PSCloudServiceConfiguration object.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="3bb1c-154">Hallo **BatchContext** parameter geeft u een eerder gedefinieerde variabele *$context* als Hallo BatchAccountContext-object.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="3bb1c-155">Hallo doelaantal rekenknooppunten in de nieuwe groep hello wordt bepaald door een formule voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="3bb1c-156">In dit geval Hallo formule is gewoon **$TargetDedicated = 4**, maximaal die het aantal rekenknooppunten in de pool Hallo Hallo aangeeft is 4.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="3bb1c-157">Query voor pools, jobs, taken en andere details</span><span class="sxs-lookup"><span data-stu-id="3bb1c-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="3bb1c-158">Gebruik cmdlets zoals **Get-AzureBatchPool**, **Get-AzureBatchJob**, en **Get-AzureBatchTask** tooquery voor entiteiten die zijn gemaakt onder een Batch-account.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="3bb1c-159">Query voor gegevens</span><span class="sxs-lookup"><span data-stu-id="3bb1c-159">Query for data</span></span>
<span data-ttu-id="3bb1c-160">Gebruik bijvoorbeeld **Get-AzureBatchPools** toofind uw pools.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="3bb1c-161">Deze query voor alle pools onder uw account standaard, ervan uitgaande dat u al opgeslagen Hallo BatchAccountContext-object in *$context*:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="3bb1c-162">Een OData-filter gebruiken</span><span class="sxs-lookup"><span data-stu-id="3bb1c-162">Use an OData filter</span></span>
<span data-ttu-id="3bb1c-163">U kunt opgeven dat een OData-filter met de Hallo **Filter** parameter toofind Hallo alleen objecten die u geïnteresseerd bent in.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="3bb1c-164">U kunt bijvoorbeeld alle pools zoeken met id's die beginnen met 'myPool':</span><span class="sxs-lookup"><span data-stu-id="3bb1c-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="3bb1c-165">Deze methode is niet zo flexibel als het gebruik van een 'Where-Object' in een lokale pijplijn.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="3bb1c-166">Hallo query opgehaald toohello Batch-service rechtstreeks verzonden zodat al het filteren aan de serverzijde hello, waardoor er internetbandbreedte gebeurt.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="3bb1c-167">Hallo-Id-parameter gebruiken</span><span class="sxs-lookup"><span data-stu-id="3bb1c-167">Use hello Id parameter</span></span>
<span data-ttu-id="3bb1c-168">Een alternatieve tooan OData-filter is toouse hello **Id** parameter.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="3bb1c-169">tooquery voor een specifieke pool met id 'myPool':</span><span class="sxs-lookup"><span data-stu-id="3bb1c-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="3bb1c-170">Hallo **Id** parameter ondersteunt alleen volledige id zoeken, geen jokertekens of filters voor OData-type.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="3bb1c-171">Gebruik de parameter MaxCount Hallo</span><span class="sxs-lookup"><span data-stu-id="3bb1c-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="3bb1c-172">Standaard worden met elke cmdlet maximaal 1000 objecten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="3bb1c-173">Als u deze limiet is bereikt, is uw toobring filter verfijnen er minder objecten of expliciet ingesteld met behulp van Hallo maximaal **MaxCount** parameter.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="3bb1c-174">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="3bb1c-175">bovengrens tooremove hello, stel **MaxCount** too0 of minder.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="3bb1c-176">Gebruik Hallo PowerShell-pipeline</span><span class="sxs-lookup"><span data-stu-id="3bb1c-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="3bb1c-177">Hallo PowerShell pijplijn toosend gegevens tussen cmdlets kunt gebruikmaken van batch-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="3bb1c-178">Dit heeft hetzelfde effect als het opgeven van een parameter, maar zorgt ervoor dat werken met meerdere entiteiten eenvoudiger Hallo.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="3bb1c-179">Zo kunt u bijvoorbeeld alle taken onder uw account zoeken en weergeven:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="3bb1c-180">Start elk computerknooppunt in een groep opnieuw op:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="3bb1c-181">Beheer van toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="3bb1c-181">Application package management</span></span>
<span data-ttu-id="3bb1c-182">Toepassingspakketten bieden een eenvoudige manier toodeploy toepassingen toohello rekenknooppunten in uw pools.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="3bb1c-183">Met Hallo Batch PowerShell-cmdlets, kunt u uploaden en toepassingspakketten in uw Batch-account beheren en implementeren van pakket versies toocompute knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="3bb1c-184">Een toepassing **maken**:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="3bb1c-185">Een toepassingspakket **toevoegen**:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="3bb1c-186">Set Hallo **standaardversie** voor Hallo toepassing:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="3bb1c-187">**Geeft een overzicht van** de pakketten van een toepassing</span><span class="sxs-lookup"><span data-stu-id="3bb1c-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="3bb1c-188">Een toepassingspakket **verwijderen**</span><span class="sxs-lookup"><span data-stu-id="3bb1c-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="3bb1c-189">Een toepassing **verwijderen**</span><span class="sxs-lookup"><span data-stu-id="3bb1c-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="3bb1c-190">U moet alle toepassingspakketversies van een toepassing verwijderen voordat u de toepassing hello verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="3bb1c-191">U ontvangt een foutbericht als u probeert een toepassing die momenteel toepassingspakketten is toodelete.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="3bb1c-192">Een toepassingspakket implementeren</span><span class="sxs-lookup"><span data-stu-id="3bb1c-192">Deploy an application package</span></span>
<span data-ttu-id="3bb1c-193">U kunt een of meer toepassingspakketten voor implementatie opgeven wanneer u een groep maakt.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="3bb1c-194">Wanneer u een pakket tijdens het maken van toepassingen opgeeft, is het geïmplementeerde tooeach knooppunt als Hallo knooppunt joins groep.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="3bb1c-195">Pakketten worden ook geïmplementeerd als een knooppunt opnieuw wordt gestart of teruggezet.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="3bb1c-196">Geef Hallo `-ApplicationPackageReference` optie bij het maken van een groep toodeploy knooppunten van een pakket toohello van groep van toepassingen als ze Hallo adresgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="3bb1c-197">Maak eerst een **PSApplicationPackageReference** object en deze configureren met Hallo Id en pakketnaam toepassingsversie gewenste toodeploy toohello pool van rekenknooppunten:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="3bb1c-198">Nu Hallo-pool maken en Hallo pakket reference-object opgeven als argument toohello Hallo `ApplicationPackageReferences` optie:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="3bb1c-199">U vindt meer informatie over toepassingspakketten in [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="3bb1c-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3bb1c-200">U moet [een Azure Storage-account koppelen](#linked-storage-account-autostorage) tooyour Batch-account toouse toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="3bb1c-201">De toepassingspakketten van een groep bijwerken</span><span class="sxs-lookup"><span data-stu-id="3bb1c-201">Update a pool's application packages</span></span>
<span data-ttu-id="3bb1c-202">tooupdate hello toepassingen die zijn toegewezen tooan bestaande groep, worden eerst een PSApplicationPackageReference-object maken met Hallo gewenst eigenschappen (Id en pakketnaam toepassingsversie):</span><span class="sxs-lookup"><span data-stu-id="3bb1c-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="3bb1c-203">Vervolgens Hallo van toepassingen niet ophalen uit de Batch, eventuele bestaande pakketten wissen onze nieuwe pakket verwijzing toevoegen en Hallo Batch-service bijwerken met nieuwe groepsinstellingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="3bb1c-204">U hebt nu Hallo van groepseigenschappen in Hallo Batch-service bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="3bb1c-205">tooactually implementeren Hallo nieuwe toepassing pakket toocompute knooppunten in de groep hello, u moet echter opnieuw opstart of installatiekopie die knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="3bb1c-206">U kunt elk knooppunt in een adresgroep met de volgende opdracht opnieuw starten:</span><span class="sxs-lookup"><span data-stu-id="3bb1c-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="3bb1c-207">U kunt meerdere toepassing pakketten toohello-rekenknooppunten in een pool implementeren.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="3bb1c-208">Als u te wilt*toevoegen* toepassingspakketten in plaats van het vervangen van momenteel geïmplementeerd hello-pakketten weglaten Hallo `$pool.ApplicationPackageReferences.Clear()` bovenstaande regel.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3bb1c-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3bb1c-209">Next steps</span></span>
* <span data-ttu-id="3bb1c-210">Zie [Naslaginformatie over Azure Batch-cmdlets](/powershell/module/azurerm.batch/#batch) voor gedetailleerde cmdlet-syntaxis en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3bb1c-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="3bb1c-211">Zie voor meer informatie over de toepassingen en in een Batch-toepassingspakketten [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="3bb1c-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/