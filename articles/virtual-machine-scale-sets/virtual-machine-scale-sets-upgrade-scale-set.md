---
title: Upgrade van een Azure virtuele-machineschaalset | Microsoft Docs
description: Een Azure virtuele-machineschaalset bijwerken
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: c7093e221ff8fe69ded1cfbce4f3ddeb1a195666
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="44d16-103">Een virtuele-machineschaalset bijwerken</span><span class="sxs-lookup"><span data-stu-id="44d16-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="44d16-104">Dit artikel wordt beschreven hoe kunt u een update OS uitrolt naar een virtuele machine van Azure schaal instellen zonder uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="44d16-104">This article describes how you can roll out an OS update to an Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="44d16-105">In deze context is omvat een update OS het wijzigen van de versie of SKU van het besturingssysteem en het wijzigen van de URI van een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="44d16-105">In this context, an OS update involves changing the version or SKU of the OS or changing the URI of a custom image.</span></span> <span data-ttu-id="44d16-106">Zonder uitvaltijd bijwerken van virtuele machines één op een tijdstip of in groepen (zoals een foutdomein op een tijdstip) in plaats van in één keer wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="44d16-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="44d16-107">Op deze manier kunnen alle virtuele machines die niet wordt bijgewerkt blijven uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="44d16-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="44d16-108">Om te voorkomen dubbelzinnigheid, gaan we onderscheiden vier typen OS-update die u wilt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="44d16-108">To avoid ambiguity, let’s distinguish four types of OS update you might want to perform:</span></span>

* <span data-ttu-id="44d16-109">Het wijzigen van de versie of SKU van een platforminstallatiekopie.</span><span class="sxs-lookup"><span data-stu-id="44d16-109">Changing the version or SKU of a platform image.</span></span> <span data-ttu-id="44d16-110">Bijvoorbeeld, het wijzigen van Ubuntu 14.04.2-LTS versie van 14.04.201506100 14.04.201507060, of de Ubuntu 15.10/laatste SKU wijzigen naar 16.04.0-LTS/latest.</span><span class="sxs-lookup"><span data-stu-id="44d16-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 to 14.04.201507060, or changing the Ubuntu 15.10/latest SKU to 16.04.0-LTS/latest.</span></span> <span data-ttu-id="44d16-111">Dit scenario wordt beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="44d16-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="44d16-112">Het wijzigen van de URI die naar een nieuwe versie van een aangepaste installatiekopie verwijst gemaakt (**eigenschappen** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **installatiekopie** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="44d16-112">Changing the URI that points to a new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="44d16-113">Dit scenario wordt beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="44d16-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="44d16-114">Het wijzigen van de verwijzing naar afbeelding van een scale-set die is gemaakt met beheerde Azure-schijven.</span><span class="sxs-lookup"><span data-stu-id="44d16-114">Changing the image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="44d16-115">Het besturingssysteem van een virtuele machine patchen (voorbeelden hiervan zijn een beveiligingspatch installeren en uitvoeren van Windows Update).</span><span class="sxs-lookup"><span data-stu-id="44d16-115">Patching the OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="44d16-116">Dit scenario wordt ondersteund, maar niet behandeld in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="44d16-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="44d16-117">Virtuele-machineschaalsets die zijn geïmplementeerd als onderdeel van een [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster niet hier worden besproken.</span><span class="sxs-lookup"><span data-stu-id="44d16-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="44d16-118">Zie [Patch Windows-besturingssysteem in uw Service Fabric-cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) voor meer informatie over Service Fabric-patching.</span><span class="sxs-lookup"><span data-stu-id="44d16-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="44d16-119">De volgorde van de basis voor het wijzigen van de OS-versie/SKU van een platforminstallatiekopie van het of de URI van een aangepaste installatiekopie ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="44d16-119">The basic sequence for changing the OS version/SKU of a platform image or the URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="44d16-120">Haal de virtuele machine scale set-model.</span><span class="sxs-lookup"><span data-stu-id="44d16-120">Get the virtual machine scale set model.</span></span>
2. <span data-ttu-id="44d16-121">De versie, de SKU, de verwijzing naar afbeelding of de URI-waarde in het model wijzigen.</span><span class="sxs-lookup"><span data-stu-id="44d16-121">Change the version, SKU, image reference, or URI value in the model.</span></span>
3. <span data-ttu-id="44d16-122">Het model bijwerken.</span><span class="sxs-lookup"><span data-stu-id="44d16-122">Update the model.</span></span>
4. <span data-ttu-id="44d16-123">Voer een *manualUpgrade* aanroepen op de virtuele machines in de schaalset.</span><span class="sxs-lookup"><span data-stu-id="44d16-123">Do a *manualUpgrade* call on the virtual machines in the scale set.</span></span> <span data-ttu-id="44d16-124">Deze stap is alleen relevant als *upgradePolicy* is ingesteld op **handmatige** in uw scale ingesteld.</span><span class="sxs-lookup"><span data-stu-id="44d16-124">This step is only relevant if *upgradePolicy* is set to **Manual** in your scale set.</span></span> <span data-ttu-id="44d16-125">Als deze is ingesteld op **automatische**, alle virtuele machines kunnen worden bijgewerkt in één keer dus uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="44d16-125">If it is set to **Automatic**, all the virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="44d16-126">Met deze informatie in gedachten, gaan we kijken hoe u de versie van een schaal instellen in PowerShell en via de REST-API kan bijwerken.</span><span class="sxs-lookup"><span data-stu-id="44d16-126">With this information in mind, let’s see how you could update the version of a scale set in PowerShell, and by using the REST API.</span></span> <span data-ttu-id="44d16-127">Deze voorbeelden hebben betrekking op het geval van een besturingssysteemkopie, maar dit artikel bevat onvoldoende informatie voor u aan te passen aan een aangepaste installatiekopie van dit proces.</span><span class="sxs-lookup"><span data-stu-id="44d16-127">These examples cover the case of a platform image, but this article provides enough information for you to adapt this process to a custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="44d16-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="44d16-128">PowerShell</span></span>
<span data-ttu-id="44d16-129">In dit voorbeeld bijgewerkt in een Windows virtuele-machineschaalset ingesteld (maken naar de nieuwe versie 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="44d16-129">This example updates a Windows virtual machine scale set (creating to the new version 4.0.20160229.</span></span> <span data-ttu-id="44d16-130">Na het bijwerken van het model wordt een update-exemplaar voor een virtuele machine op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="44d16-130">After updating the model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get the VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update the virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="44d16-131">Als u de URI voor een aangepaste installatiekopie in plaats van het wijzigen van een installatiekopie platform versie bijwerken wilt, moet u de regel 'instellen voor de nieuwe versie' vervangen door een opdracht die de broninstallatiekopie URI wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="44d16-131">If you are updating the URI for a custom image instead of changing a platform image version, replace the “set the new version” line with a command that will update the source image URI.</span></span> <span data-ttu-id="44d16-132">Bijvoorbeeld, als de scale-set is gemaakt zonder gebruik van beheerde Azure-schijven, eruit de update als volgt:</span><span class="sxs-lookup"><span data-stu-id="44d16-132">For example, if the scale set was created without using Azure Managed Disks, the update would look like this:</span></span>

```powershell
# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="44d16-133">Als een aangepaste installatiekopie gebaseerd schaalset is gemaakt met Azure beheerd schijven, en vervolgens de verwijzing naar afbeelding zou worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="44d16-133">If a custom image based scale set was created using Azure Managed Disks, then the image reference would be updated.</span></span> <span data-ttu-id="44d16-134">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="44d16-134">For example:</span></span>

```powershell
# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="the-rest-api"></a><span data-ttu-id="44d16-135">De REST-API</span><span class="sxs-lookup"><span data-stu-id="44d16-135">The REST API</span></span>
<span data-ttu-id="44d16-136">Hier volgen enkele voorbeelden van Python die gebruikmaken van de REST-API van Azure implementeert een update OS-versie.</span><span class="sxs-lookup"><span data-stu-id="44d16-136">Here are a couple of Python examples that use the Azure REST API to roll out an OS version update.</span></span> <span data-ttu-id="44d16-137">Beide gebruik van de lightweight [azurerm](https://pypi.python.org/pypi/azurerm) bibliotheek met REST API van Azure wrapper functies GET op schaal model, gevolgd door een PUT met een bijgewerkte model instelt.</span><span class="sxs-lookup"><span data-stu-id="44d16-137">Both use the lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions to do a GET on the scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="44d16-138">Ze ook bekijken weergaven van de virtuele machine-exemplaren voor het identificeren van de virtuele machines door updatedomein.</span><span class="sxs-lookup"><span data-stu-id="44d16-138">They also look at virtual machine instances views to identify the virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="44d16-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="44d16-139">Vmssupgrade</span></span>
 <span data-ttu-id="44d16-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is een pythonscript dat wordt gebruikt voor het bijwerken van het besturingssysteem implementeert op een actieve virtuele machine schaal één updatedomein tegelijk worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="44d16-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used to roll out an OS upgrade to a running virtual machine scale set one update domain at a time.</span></span>

![Vmssupgrade script voor het kiezen van virtuele machines of een updatedomein](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="44d16-142">Dit script kunt u specifieke virtuele machines bijwerken of geef het updatedomein van een te kiezen.</span><span class="sxs-lookup"><span data-stu-id="44d16-142">This script lets you choose specific virtual machines to update or specify an update domain.</span></span> <span data-ttu-id="44d16-143">Het ondersteunt wijzigen van een platform-versie van de installatiekopie en het wijzigen van de URI van een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="44d16-143">It supports changing a platform image version or changing the URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="44d16-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="44d16-144">Vmsseditor</span></span>
<span data-ttu-id="44d16-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is een algemene editor voor de virtuele-machineschaalsets waarin de virtuele machine de status als een heatmap waarbij één rij één updatedomein vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="44d16-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="44d16-146">U kunt onder andere het model voor een schaalset bijwerken met een nieuwe versie, SKU of aangepaste installatiekopie URI en selecteer vervolgens de domeinen met fouten om bij te werken.</span><span class="sxs-lookup"><span data-stu-id="44d16-146">Among other things, you can update the model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains to upgrade.</span></span> <span data-ttu-id="44d16-147">Wanneer u doet dit, worden alle virtuele machines in dat updatedomein bijgewerkt naar het nieuwe model.</span><span class="sxs-lookup"><span data-stu-id="44d16-147">When you do so, all the virtual machines in that update domain are upgraded to the new model.</span></span> <span data-ttu-id="44d16-148">U kunt ook een uitrollende upgrade op basis van de batchgrootte van uw keuze doen.</span><span class="sxs-lookup"><span data-stu-id="44d16-148">Alternatively, you can do a rolling upgrade based on the batch size of your choice.</span></span>  

<span data-ttu-id="44d16-149">De volgende schermafbeelding ziet een model van een schaal voor Ubuntu 14.04-2LTS versie 14.04.201507060 instelt.</span><span class="sxs-lookup"><span data-stu-id="44d16-149">The following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="44d16-150">Veel meer opties zijn toegevoegd aan dit hulpprogramma sinds deze schermafbeelding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44d16-150">Many more options have been added to this tool since this screenshot was taken.</span></span>

![Model van een schaal ingesteld voor Ubuntu 14.04-2LTS Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="44d16-152">Nadat u op **Upgrade** en vervolgens **Details ophalen**, virtuele machines in UD 0 starten om bij te werken.</span><span class="sxs-lookup"><span data-stu-id="44d16-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start to update.</span></span>

![Vmsseditor tonen worden bijgewerkt](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

