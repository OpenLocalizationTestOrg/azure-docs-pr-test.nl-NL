---
title: Virtuele Machine Scale Sets gekoppeld gegevensschijven aaaAzure | Microsoft Docs
description: Meer informatie over hoe toouse gekoppeld gegevensschijven met virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="f6d4e-103">Virtuele-machineschaalsets in Azure en gekoppelde gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="f6d4e-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="f6d4e-104">[Virtuele-machineschaalsets](/azure/virtual-machine-scale-sets/) in Azure ondersteunen nu virtuele machines met gekoppelde gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="f6d4e-105">Gegevensschijven kunnen worden gedefinieerd in het opslagprofiel Hallo voor schaalsets die zijn gemaakt met beheerde Azure-schijven.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="f6d4e-106">Eerder waren hello alleen direct gekoppelde opslag beschikbare opties met virtuele machines in schaalsets Hallo OS station en tijdelijke stations.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="f6d4e-107">Wanneer u een schaal bijgesloten gegevensschijven die zijn gedefinieerd in te stellen maakt, moet u nog steeds toomount en indeling Hallo schijven uit binnen een VM-toouse ze (alleen like voor zelfstandige virtuele Azure-machines).</span><span class="sxs-lookup"><span data-stu-id="f6d4e-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="f6d4e-108">Een handige manier toodo die dit toouse een extensie voor aangepaste scripts die een Standaardscript toopartition aanroept en formatteren van alle Hallo gegevensschijven op een virtuele machine is.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="f6d4e-109">Een schaalset maken met gekoppelde gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="f6d4e-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="f6d4e-110">Een eenvoudige manier toocreate een met gekoppelde schijven schaalset is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss maken_ opdracht.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="f6d4e-111">Hallo volgende voorbeeld maakt een Azure-resourcegroep en een VM-schaalset van 10 Ubuntu VM's, elk met 2 bijgesloten gegevensschijven, 50 GB en 100 GB respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="f6d4e-112">Houd er rekening mee dat Hallo _vmss maken_ wordt standaard een bepaalde configuratiewaarden als u ze niet opgeven.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="f6d4e-113">toosee hello beschikbare opties dat kunt u proberen overschrijven:</span><span class="sxs-lookup"><span data-stu-id="f6d4e-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="f6d4e-114">Een andere manier toocreate een schaal gekoppelde gegevensschijven in te stellen is een schaal in een Azure Resource Manager-sjabloon instellen toodefine bevatten een _dataDisks_ sectie in Hallo _storageProfile_, en Hallo implementeren de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="f6d4e-115">Hallo 50 en 100 GB schijf bovenstaande voorbeeld zou als volgt in Hallo sjabloon worden gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="f6d4e-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="f6d4e-116">Ziet u een voorbeeld van een voltooid, gereed toodeploy van een scale set-sjabloon met een gekoppelde schijf hier gedefinieerd: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="f6d4e-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="f6d4e-117">Toevoegen van een bestaande schaal voor gegevens schijf tooan instellen</span><span class="sxs-lookup"><span data-stu-id="f6d4e-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="f6d4e-118">U kunt alleen koppelen schijven tooa scale gegevensset die is gemaakt met [Azure beheerd schijven](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="f6d4e-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="f6d4e-119">U kunt geen gegevens schijf tooa VM schaal ingesteld met Azure CLI toevoegen _az vmss schijf koppelen_ opdracht.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="f6d4e-120">Geef een LUN op die nog niet in gebruik is.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="f6d4e-121">Hallo na CLI voorbeeld wordt een 50 GB station toolun 3 toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="f6d4e-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="f6d4e-122">Hallo volgende PowerShell-voorbeeld wordt een 50 GB station toolun 3 toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="f6d4e-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="f6d4e-123">Andere VM-grootten hebben andere beperkingen op Hallo aantal gekoppelde schijven die ze ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="f6d4e-124">Controleer Hallo [kenmerken van virtuele machine grootte](../virtual-machines/windows/sizes.md) voordat een nieuwe schijf toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="f6d4e-125">U kunt ook een schijf toevoegen door het toevoegen van een nieuwe vermelding toohello _dataDisks_ eigenschap in Hallo _storageProfile_ instellen van een scale-definitie en het toepassen van Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="f6d4e-126">tootest deze, zoeken naar een bestaande scale setdefinitie in Hallo [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f6d4e-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="f6d4e-127">Selecteer _bewerken_ en een nieuwe schijf toohello lijst met gegevensschijven toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="f6d4e-128">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="f6d4e-128">E.g.</span></span> <span data-ttu-id="f6d4e-129">bovenstaande Hallo-voorbeeld gebruikt:</span><span class="sxs-lookup"><span data-stu-id="f6d4e-129">using hello example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="f6d4e-130">Selecteer vervolgens _plaatsen_ tooapply hello tooyour scale set wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="f6d4e-131">Dit voorbeeld zou moeten werken als u gebruikmaakt van een VM-formaat dat meer dan twee gekoppelde gegevensschijven ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="f6d4e-132">Wanneer u een wijziging tooa schaal definitie zoals het toevoegen of verwijderen van een gegevensschijf ingesteld, is van toepassing tooall nieuw gemaakte virtuele machines, maar is alleen van toepassing tooexisting VMs hello _upgradePolicy_ eigenschap te 'automatisch' is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="f6d4e-133">Als deze optie is ingesteld te 'handmatig', moet u toomanually Hallo nieuwe model tooexisting VM's van toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="f6d4e-134">U kunt dit doen in Hallo-portal met Hallo _Update AzureRmVmssInstance_ PowerShell-opdracht of met behulp van Hallo _az vmss update-exemplaren_ CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="f6d4e-135">Toe te voegen vooraf ingestelde schijven tooan scale-bestaande gegevensset</span><span class="sxs-lookup"><span data-stu-id="f6d4e-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="f6d4e-136">Wanneer u schijven tooan bestaande toevoegt schaalset model ontwikkeld, Hallo schijf wordt altijd gemaakt leeg.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="f6d4e-137">Dit scenario omvat ook nieuwe exemplaren gemaakt door Hallo schaalset.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="f6d4e-138">Dit gedrag is omdat Hallo scaleset definitie een lege gegevensschijf heeft.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="f6d4e-139">In de volgorde toocreate vooraf ingestelde gegevensstations voor een bestaand scale set-model, kunt u een van de volgende twee opties kiezen:</span><span class="sxs-lookup"><span data-stu-id="f6d4e-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="f6d4e-140">Gegevens kopiëren van Hallo exemplaar 0 VM toohello gegevens een of meer schijven in Hallo andere virtuele machines door het uitvoeren van een aangepast script.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="f6d4e-141">Maken van een begeleide afbeelding met schijf Hallo OS plus gegevensschijf (met gegevens Hallo vereist) en maak een nieuwe scaleset met Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="f6d4e-142">Op deze manier om nieuwe virtuele machine gemaakt heeft een schijf die die is opgegeven in de definitie Hallo van Hallo scaleset.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="f6d4e-143">Aangezien deze definitie tooan afbeelding met een gegevensschijf die gegevens aangepast verwijzen wordt, terug elke virtuele machine op Hallo scaleset automatisch met deze wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="f6d4e-144">Hallo manier toocreate een aangepaste installatiekopie u hier vindt: [een begeleide afbeelding van een gegeneraliseerde virtuele machine in Azure maken](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="f6d4e-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="f6d4e-145">Hallo gebruiker moet toocapture Hallo 0 virtuele die vereiste gegevens heeft Hallo-instantie en gebruik vervolgens deze vhd voor Hallo installatiekopie definitie.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="f6d4e-146">Een gegevensschijf verwijderen uit een schaalset</span><span class="sxs-lookup"><span data-stu-id="f6d4e-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="f6d4e-147">U kunt een gegevensschijf verwijderen uit een VM-schaalset met behulp van de Azure CLI-opdracht _az vmss disk detach_.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="f6d4e-148">Bijvoorbeeld hello volgende opdracht wordt gedefinieerd op lun 2 Hallo-schijf:</span><span class="sxs-lookup"><span data-stu-id="f6d4e-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="f6d4e-149">Op dezelfde manier kunt u ook een schijf verwijderen uit een schaal ingesteld door het verwijderen van een item uit Hallo _dataDisks_ eigenschap in Hallo _storageProfile_ en Hallo wijziging toe te passen.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="f6d4e-150">Aanvullende opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f6d4e-150">Additional notes</span></span>
<span data-ttu-id="f6d4e-151">Ondersteuning voor Azure Managed schijven en schaal ingesteld gekoppelde gegevensschijven is beschikbaar in de API-versie [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) of hoger van Hallo Microsoft.Compute-API.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="f6d4e-152">In de aanvankelijke implementatie van de gekoppelde schijfondersteuning voor schaalsets Hallo kan niet u koppelen of ontkoppelen van gegevensschijven van afzonderlijke virtuele machines in een schaalset.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="f6d4e-153">De ondersteuning in Azure Portal voor gekoppelde gegevensschijven in schaalsets is oorspronkelijk beperkt.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="f6d4e-154">Afhankelijk van uw vereisten dat kunt u Azure-sjablonen, CLI, PowerShell SDK's en REST-API toomanage gekoppelde schijven.</span><span class="sxs-lookup"><span data-stu-id="f6d4e-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


