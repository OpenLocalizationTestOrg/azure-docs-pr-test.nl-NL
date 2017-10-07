---
title: aaaUpgrade een virtuele machine van Azure-schaalset | Microsoft Docs
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
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="eafbf-103">Een virtuele-machineschaalset bijwerken</span><span class="sxs-lookup"><span data-stu-id="eafbf-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="eafbf-104">Dit artikel wordt beschreven hoe u een besturingssysteem update tooan Azure virtuele-machineschaalset instellen zonder uitvaltijd kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="eafbf-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="eafbf-105">In deze context omvat een update OS Hallo versie of SKU Hallo OS wijzigen en het wijzigen van Hallo-URI van een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="eafbf-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="eafbf-106">Zonder uitvaltijd bijwerken van virtuele machines één op een tijdstip of in groepen (zoals een foutdomein op een tijdstip) in plaats van in één keer wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="eafbf-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="eafbf-107">Op deze manier kunnen alle virtuele machines die niet wordt bijgewerkt blijven uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="eafbf-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="eafbf-108">tooavoid dubbelzinnigheid, gaan we onderscheid OS-update kunt u vier typen tooperform:</span><span class="sxs-lookup"><span data-stu-id="eafbf-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="eafbf-109">Het wijzigen van Hallo versie of SKU van een platforminstallatiekopie.</span><span class="sxs-lookup"><span data-stu-id="eafbf-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="eafbf-110">Bijvoorbeeld, het wijzigen van Ubuntu 14.04.2-LTS-versie uit 14.04.201506100 too14.04.201507060 of Hallo Ubuntu 15.10/laatste SKU too16.04.0-LTS/latest wijzigen.</span><span class="sxs-lookup"><span data-stu-id="eafbf-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="eafbf-111">Dit scenario wordt beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="eafbf-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="eafbf-112">Het wijzigen van URI die nieuwe versie van een aangepaste installatiekopie die u hebt ontwikkeld tooa verwijst Hallo (**eigenschappen** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **installatiekopie** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="eafbf-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="eafbf-113">Dit scenario wordt beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="eafbf-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="eafbf-114">Verwijzing naar afbeelding van een scale-set die is gemaakt met Azure beheerd schijven Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="eafbf-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="eafbf-115">Besturingssysteem van patchen Hallo binnen een virtuele machine (voorbeelden hiervan zijn een beveiligingspatch installeren en uitvoeren van Windows Update).</span><span class="sxs-lookup"><span data-stu-id="eafbf-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="eafbf-116">Dit scenario wordt ondersteund, maar niet behandeld in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="eafbf-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="eafbf-117">Virtuele-machineschaalsets die zijn geïmplementeerd als onderdeel van een [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster niet hier worden besproken.</span><span class="sxs-lookup"><span data-stu-id="eafbf-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="eafbf-118">Zie [Patch Windows-besturingssysteem in uw Service Fabric-cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) voor meer informatie over Service Fabric-patching.</span><span class="sxs-lookup"><span data-stu-id="eafbf-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="eafbf-119">Hallo basic volgorde voor het wijzigen van Hallo OS-versie/SKU van een platforminstallatiekopie of Hallo-URI van een aangepaste installatiekopie ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="eafbf-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="eafbf-120">Hallo virtuele machine scale set model worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="eafbf-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="eafbf-121">Hallo-versie, SKU, verwijzing naar afbeelding of de URI-waarde in Hallo model wijzigen.</span><span class="sxs-lookup"><span data-stu-id="eafbf-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="eafbf-122">Hallo model bijwerken.</span><span class="sxs-lookup"><span data-stu-id="eafbf-122">Update hello model.</span></span>
4. <span data-ttu-id="eafbf-123">Voer een *manualUpgrade* op Hallo virtuele machines in de schaalset Hallo aanroepen.</span><span class="sxs-lookup"><span data-stu-id="eafbf-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="eafbf-124">Deze stap is alleen relevant als *upgradePolicy* te is ingesteld,**handmatige** in uw scale ingesteld.</span><span class="sxs-lookup"><span data-stu-id="eafbf-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="eafbf-125">Als er te**automatische**, alle Hallo virtuele machines kunnen worden bijgewerkt in één keer dus uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="eafbf-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="eafbf-126">Met deze informatie in gedachten, gaan we kijken hoe u Hallo-versie van een schaal instellen in PowerShell en via Hallo REST-API kan bijwerken.</span><span class="sxs-lookup"><span data-stu-id="eafbf-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="eafbf-127">Deze voorbeelden verrekend Hallo geval van een besturingssysteemkopie, maar in dit artikel biedt voldoende informatie voor u tooadapt dit proces tooa aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="eafbf-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="eafbf-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eafbf-128">PowerShell</span></span>
<span data-ttu-id="eafbf-129">In dit voorbeeld bijgewerkt in een Windows virtuele-machineschaalset (maken toohello nieuwe versie 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="eafbf-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="eafbf-130">Na het bijwerken van Hallo model, wordt een update-exemplaar voor een virtuele machine op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="eafbf-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="eafbf-131">Als u Hallo URI voor een aangepaste installatiekopie in plaats van een platform-versie van de afbeelding wijzigen bijwerkt, vervangt u 'set Hallo nieuwe versie' hello regel met een opdracht die wordt bijgewerkt Hallo broninstallatiekopie URI.</span><span class="sxs-lookup"><span data-stu-id="eafbf-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="eafbf-132">Bijvoorbeeld, als Hallo scale set is gemaakt zonder gebruik van beheerde Azure-schijven, eruit Hallo update als volgt:</span><span class="sxs-lookup"><span data-stu-id="eafbf-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="eafbf-133">Als een aangepaste installatiekopie gebaseerd schaalset is gemaakt met Azure beheerd schijven, en vervolgens de verwijzing naar afbeelding van Hallo zou worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="eafbf-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="eafbf-134">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="eafbf-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="eafbf-135">Hallo REST-API</span><span class="sxs-lookup"><span data-stu-id="eafbf-135">hello REST API</span></span>
<span data-ttu-id="eafbf-136">Hier volgen enkele voorbeelden van Python die hello Azure REST-API tooroll uit een update OS-versie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eafbf-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="eafbf-137">Hallo lightweight maken beide gebruik [azurerm](https://pypi.python.org/pypi/azurerm) bibliotheek met REST API van Azure wrapper functies toodo GET op Hallo schaal model, gevolgd door een PUT met een bijgewerkte model instelt.</span><span class="sxs-lookup"><span data-stu-id="eafbf-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="eafbf-138">Ze ook zoeken op de virtuele machine-exemplaren weergaven tooidentify Hallo virtuele machines per updatedomein.</span><span class="sxs-lookup"><span data-stu-id="eafbf-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="eafbf-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="eafbf-139">Vmssupgrade</span></span>
 <span data-ttu-id="eafbf-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is een pythonscript dat is gebruikt tooroll uit een OS upgrade tooa met virtuele-machineschaalset één updatedomein tegelijk worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="eafbf-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![Vmssupgrade script voor het kiezen van virtuele machines of een updatedomein](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="eafbf-142">Dit script kunt u specifieke virtuele machines tooupdate kiezen of geef een updatedomein.</span><span class="sxs-lookup"><span data-stu-id="eafbf-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="eafbf-143">Het ondersteunt wijzigen van een platform-versie van de installatiekopie en het Hallo-URI van een aangepaste installatiekopie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="eafbf-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="eafbf-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="eafbf-144">Vmsseditor</span></span>
<span data-ttu-id="eafbf-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is een algemene editor voor de virtuele-machineschaalsets waarin de virtuele machine de status als een heatmap waarbij één rij één updatedomein vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="eafbf-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="eafbf-146">U kunt onder andere Hallo-model voor een schaalset bijwerken met een nieuwe versie, SKU of aangepaste installatiekopie URI en selecteer vervolgens een fout met betrekking tot domeinen tooupgrade.</span><span class="sxs-lookup"><span data-stu-id="eafbf-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="eafbf-147">Wanneer u doet dit, worden alle Hallo virtuele machines in dat updatedomein bijgewerkte toohello nieuw model.</span><span class="sxs-lookup"><span data-stu-id="eafbf-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="eafbf-148">U kunt ook een uitrollende upgrade op basis van de batchgrootte Hallo van uw keuze doen.</span><span class="sxs-lookup"><span data-stu-id="eafbf-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="eafbf-149">Hallo volgende schermafbeelding ziet u een model van een schaal voor Ubuntu 14.04-2LTS versie 14.04.201507060 instelt.</span><span class="sxs-lookup"><span data-stu-id="eafbf-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="eafbf-150">Veel meer opties zijn toegevoegd toothis hulpprogramma sinds deze schermafbeelding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eafbf-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Model van een schaal ingesteld voor Ubuntu 14.04-2LTS Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="eafbf-152">Nadat u op **Upgrade** en vervolgens **Details ophalen**, virtuele machines in UD 0 tooupdate gestart.</span><span class="sxs-lookup"><span data-stu-id="eafbf-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![Vmsseditor tonen worden bijgewerkt](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

