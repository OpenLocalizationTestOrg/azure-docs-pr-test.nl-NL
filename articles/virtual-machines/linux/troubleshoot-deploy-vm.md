---
title: problemen met Linux virtuele machine in Azure implementeren aaaTroubleshoot | Microsoft Docs
description: Problemen met implementatie Linux virtuele machine in Azurethe Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="afc52-103">Problemen met implementatie Linux virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="afc52-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="afc52-104">tootroubleshoot implementatieproblemen van virtuele machine (VM) in Azure, bekijk Hallo [top problemen](#top-issues) voor algemene fouten en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="afc52-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="afc52-105">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="afc52-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="afc52-106">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="afc52-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="afc52-107">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.</span><span class="sxs-lookup"><span data-stu-id="afc52-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="afc52-108">Meest voorkomende problemen</span><span class="sxs-lookup"><span data-stu-id="afc52-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="afc52-109">Hallo-cluster kan niet ondersteunen Hallo aangevraagde VM-grootte</span><span class="sxs-lookup"><span data-stu-id="afc52-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="afc52-110">Probeer Hallo-aanvraag met een kleinere VM.</span><span class="sxs-lookup"><span data-stu-id="afc52-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="afc52-111">Als hello aangevraagde grootte van Hallo dat VM kan niet worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="afc52-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="afc52-112">Stop alle Hallo-VM's in de beschikbaarheidsset Hallo.</span><span class="sxs-lookup"><span data-stu-id="afc52-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="afc52-113">Klik op **resourcegroepen** > uw resourcegroep > **Resources** > uw beschikbaarheidsset > **virtuele Machines** > uw virtuele machine >  **Stop**.</span><span class="sxs-lookup"><span data-stu-id="afc52-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="afc52-114">Nadat alle virtuele machines stoppen Hallo, Hallo VM maken in Hallo gewenst grootte.</span><span class="sxs-lookup"><span data-stu-id="afc52-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="afc52-115">Start eerst Hallo van nieuwe virtuele machine en vervolgens Selecteer Hallo gestopt VM's en klik op Start.</span><span class="sxs-lookup"><span data-stu-id="afc52-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="afc52-116">Hallo-cluster heeft geen gratis resources</span><span class="sxs-lookup"><span data-stu-id="afc52-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="afc52-117">Hallo aanvraag later opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="afc52-117">Retry hello request later.</span></span>
- <span data-ttu-id="afc52-118">Als hello nieuwe virtuele machine kan deel uitmaken van een andere beschikbaarheidsset instellen</span><span class="sxs-lookup"><span data-stu-id="afc52-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="afc52-119">Een virtuele machine maken in een andere beschikbaarheidsset (in Hallo dezelfde regio).</span><span class="sxs-lookup"><span data-stu-id="afc52-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="afc52-120">Toevoegen van nieuwe VM-toohello Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="afc52-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="afc52-121">Hoe kan ik mijn maandelijkse tegoed voor Visual studio Enterprise (BizSpark) activeren</span><span class="sxs-lookup"><span data-stu-id="afc52-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="afc52-122">tooactivate uw maandelijkse tegoed, ziet u dit [artikel](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="afc52-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="afc52-123">Waarom kan ik Hallo GPU-stuurprogramma niet voor een virtuele Ubuntu-machine NV installeren?</span><span class="sxs-lookup"><span data-stu-id="afc52-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="afc52-124">Linux GPU-ondersteuning is momenteel alleen beschikbaar op Azure NC Virtual machines Ubuntu Server 16.04 TNS uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="afc52-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="afc52-125">Zie voor meer informatie [GPU-stuurprogramma's instellen voor N-reeks virtuele machines met Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="afc52-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="afc52-126">De stuurprogramma's ontbreken voor mijn Linux-VM met N-serie</span><span class="sxs-lookup"><span data-stu-id="afc52-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="afc52-127">Stuurprogramma's voor op basis van Linux virtuele machines zich bevinden [hier](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="afc52-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="afc52-128">Ik kan een GPU-exemplaar niet vinden in mijn VM N-serie</span><span class="sxs-lookup"><span data-stu-id="afc52-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="afc52-129">tootake profiteren van Hallo GPU-mogelijkheden van Azure N-serie VM's met WindowsServer 2016 of Windows Server 2012 R2, moet u NVIDIA grafische stuurprogramma's installeren op elke virtuele machine na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="afc52-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="afc52-130">Stuurprogramma-installatie-informatie is beschikbaar voor [VM's van Windows](../windows/n-series-driver-setup.md) en [virtuele Linux-machines](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="afc52-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="afc52-131">Virtuele machines N-reeks is beschikbaar in mijn regio?</span><span class="sxs-lookup"><span data-stu-id="afc52-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="afc52-132">U kunt controleren Hallo beschikbaarheid van Hallo [producten die per regio tabel](https://azure.microsoft.com/regions/services), en prijzen [hier](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="afc52-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="afc52-133">Ik wil niet kunnen toosee VM-grootte familie die ik wil wanneer het formaat van mijn VM.</span><span class="sxs-lookup"><span data-stu-id="afc52-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="afc52-134">Wanneer een virtuele machine wordt uitgevoerd, is het geïmplementeerde tooa fysieke server.</span><span class="sxs-lookup"><span data-stu-id="afc52-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="afc52-135">Hallo fysieke servers in de Azure-regio's worden gegroepeerd in clusters van algemene fysieke hardware.</span><span class="sxs-lookup"><span data-stu-id="afc52-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="afc52-136">Formaat van een virtuele machine waarvoor Hallo VM toobe verplaatst toodifferent hardware clusters verschilt, afhankelijk van welke implementatiemodel gebruikte toodeploy Hallo VM is.</span><span class="sxs-lookup"><span data-stu-id="afc52-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="afc52-137">Virtuele machines die worden geïmplementeerd in het klassieke implementatiemodel, Hallo cloud service-implementatie moeten worden verwijderd en opnieuw geïmplementeerd toochange Hallo VMs tooa grootte in een ander grootte gezin.</span><span class="sxs-lookup"><span data-stu-id="afc52-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="afc52-138">Virtuele machines in de Resource Manager-implementatiemodel zijn geïmplementeerd, moet u alle virtuele machines stoppen in Hallo beschikbaarheidsset voordat u de grootte van een virtuele machine in de beschikbaarheidsset Hallo Hallo wijzigt.</span><span class="sxs-lookup"><span data-stu-id="afc52-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="afc52-139">Hallo wordt vermelde VM-grootte niet ondersteund tijdens de implementatie in Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="afc52-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="afc52-140">Kies een grootte die wordt ondersteund op Hallo beschikbaarheidsset-cluster.</span><span class="sxs-lookup"><span data-stu-id="afc52-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="afc52-141">Het wordt aanbevolen bij het maken van dat een beschikbaarheidsset toochoose Hallo VM maximumgrootte u denkt dat u nodig hebt en u hebt uw eerste implementatie toohello beschikbaarheidsset worden.</span><span class="sxs-lookup"><span data-stu-id="afc52-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="afc52-142">Welke Linux-distributies/versies worden ondersteund in Azure?</span><span class="sxs-lookup"><span data-stu-id="afc52-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="afc52-143">U kunt de lijst Hallo op Linux vinden op [Azure-Endorsed distributies](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="afc52-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="afc52-144">Kan ik een bestaande beschikbaarheidsset voor klassieke VM tooan toevoegen?</span><span class="sxs-lookup"><span data-stu-id="afc52-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="afc52-145">Ja.</span><span class="sxs-lookup"><span data-stu-id="afc52-145">Yes.</span></span> <span data-ttu-id="afc52-146">U kunt een bestaande klassieke VM tooa nieuwe toevoegen of bestaande Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="afc52-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="afc52-147">Zie voor meer informatie [toevoegen van een bestaande beschikbaarheidsset voor de virtuele machine tooan](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="afc52-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="afc52-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="afc52-148">Next steps</span></span>
<span data-ttu-id="afc52-149">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="afc52-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="afc52-150">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="afc52-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="afc52-151">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.</span><span class="sxs-lookup"><span data-stu-id="afc52-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
