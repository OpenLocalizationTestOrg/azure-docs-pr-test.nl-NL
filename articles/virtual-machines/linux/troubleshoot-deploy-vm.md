---
title: Problemen met implementatie Linux virtuele machine in Azure | Microsoft Docs
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
ms.openlocfilehash: 8bc9de90a49caf9155073caaa160585c6cc3728b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="40cbc-103">Problemen met implementatie Linux virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="40cbc-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="40cbc-104">Voor het oplossen van problemen bij de implementatie in Azure virtuele machine (VM), Controleer de [top problemen](#top-issues) voor algemene fouten en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="40cbc-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="40cbc-105">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts raadplegen op [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="40cbc-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="40cbc-106">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="40cbc-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="40cbc-107">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.</span><span class="sxs-lookup"><span data-stu-id="40cbc-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="40cbc-108">Meest voorkomende problemen</span><span class="sxs-lookup"><span data-stu-id="40cbc-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="40cbc-109">Het cluster kan het aangevraagde VM-grootte niet ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="40cbc-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="40cbc-110">Probeer de aanvraag met een kleinere VM.</span><span class="sxs-lookup"><span data-stu-id="40cbc-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="40cbc-111">Als de grootte van de aangevraagde virtuele machine kan niet worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="40cbc-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="40cbc-112">Stop de virtuele machines in de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="40cbc-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="40cbc-113">Klik op **resourcegroepen** > uw resourcegroep > **Resources** > uw beschikbaarheidsset > **virtuele Machines** > uw virtuele machine >  **Stop**.</span><span class="sxs-lookup"><span data-stu-id="40cbc-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="40cbc-114">Nadat de virtuele machines stoppen, moet u de virtuele machine maken in de gewenste grootte.</span><span class="sxs-lookup"><span data-stu-id="40cbc-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="40cbc-115">De nieuwe virtuele machine eerst te starten en selecteert u elk van de gestopte virtuele machines en klik op Start.</span><span class="sxs-lookup"><span data-stu-id="40cbc-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="40cbc-116">Het cluster heeft geen gratis resources</span><span class="sxs-lookup"><span data-stu-id="40cbc-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="40cbc-117">De aanvraag later opnieuw.</span><span class="sxs-lookup"><span data-stu-id="40cbc-117">Retry the request later.</span></span>
- <span data-ttu-id="40cbc-118">Als de nieuwe virtuele machine deel van een andere beschikbaarheidsset uitmaken kan</span><span class="sxs-lookup"><span data-stu-id="40cbc-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="40cbc-119">Een virtuele machine maken in een andere beschikbaarheidsset (in dezelfde regio).</span><span class="sxs-lookup"><span data-stu-id="40cbc-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="40cbc-120">De nieuwe virtuele machine toevoegen aan hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="40cbc-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="40cbc-121">Hoe kan ik mijn maandelijkse tegoed voor Visual studio Enterprise (BizSpark) activeren</span><span class="sxs-lookup"><span data-stu-id="40cbc-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="40cbc-122">Als u wilt uw maandelijkse tegoed hebt geactiveerd, ziet u dit [artikel](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="40cbc-122">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-the-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="40cbc-123">Waarom kan ik het GPU-stuurprogramma niet voor een virtuele Ubuntu-machine NV installeren?</span><span class="sxs-lookup"><span data-stu-id="40cbc-123">Why can I not install the GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="40cbc-124">Linux GPU-ondersteuning is momenteel alleen beschikbaar op Azure NC Virtual machines Ubuntu Server 16.04 TNS uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="40cbc-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="40cbc-125">Zie voor meer informatie [GPU-stuurprogramma's instellen voor N-reeks virtuele machines met Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="40cbc-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="40cbc-126">De stuurprogramma's ontbreken voor mijn Linux-VM met N-serie</span><span class="sxs-lookup"><span data-stu-id="40cbc-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="40cbc-127">Stuurprogramma's voor op basis van Linux virtuele machines zich bevinden [hier](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="40cbc-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="40cbc-128">Ik kan een GPU-exemplaar niet vinden in mijn VM N-serie</span><span class="sxs-lookup"><span data-stu-id="40cbc-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="40cbc-129">Als u wilt profiteren van de GPU-mogelijkheden van N-reeks virtuele machines in Azure waarop Windows Server 2016 of Windows Server 2012 R2 wordt uitgevoerd, moet u NVIDIA grafische stuurprogramma's installeren op elke virtuele machine na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="40cbc-129">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="40cbc-130">Stuurprogramma-installatie-informatie is beschikbaar voor [VM's van Windows](../windows/n-series-driver-setup.md) en [virtuele Linux-machines](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="40cbc-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="40cbc-131">Virtuele machines N-reeks is beschikbaar in mijn regio?</span><span class="sxs-lookup"><span data-stu-id="40cbc-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="40cbc-132">U kunt controleren dat de beschikbaarheid van de [producten die per regio tabel](https://azure.microsoft.com/regions/services), en prijzen [hier](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="40cbc-132">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="40cbc-133">Ik wil niet kunnen zien van VM-grootte-familie die ik wil wanneer het formaat van mijn VM.</span><span class="sxs-lookup"><span data-stu-id="40cbc-133">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="40cbc-134">Wanneer een virtuele machine wordt uitgevoerd, wordt geïmplementeerd met een fysieke server.</span><span class="sxs-lookup"><span data-stu-id="40cbc-134">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="40cbc-135">De fysieke servers in de Azure-regio's worden gegroepeerd in clusters van algemene fysieke hardware.</span><span class="sxs-lookup"><span data-stu-id="40cbc-135">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="40cbc-136">Formaat van een virtuele machine die u moet de virtuele machine worden verplaatst naar andere hardware clusters verschilt, afhankelijk van welke implementatiemodel is gebruikt voor het implementeren van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="40cbc-136">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="40cbc-137">Virtuele machines die worden geïmplementeerd in het klassieke implementatiemodel, de cloud service-implementatie moeten worden verwijderd en opnieuw als u wilt wijzigen in een grootte in een ander gezin van de grootte van de virtuele machines zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="40cbc-137">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="40cbc-138">Virtuele machines in de Resource Manager-implementatiemodel zijn geïmplementeerd, moet u alle virtuele machines stoppen in beschikbaarheidsset voordat u wijzigt de grootte van een virtuele machine in de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="40cbc-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="40cbc-139">De vermelde VM-grootte wordt niet ondersteund tijdens de implementatie in Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="40cbc-139">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="40cbc-140">Kies een grootte die wordt ondersteund op de beschikbaarheidsset cluster.</span><span class="sxs-lookup"><span data-stu-id="40cbc-140">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="40cbc-141">Het wordt aanbevolen wanneer de grootste VM-grootte u denkt dat u nodig hebt en hebt die uw eerste implementatie voor de beschikbaarheidsset kiezen voor het maken van een beschikbaarheidsset ingesteld.</span><span class="sxs-lookup"><span data-stu-id="40cbc-141">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="40cbc-142">Welke Linux-distributies/versies worden ondersteund in Azure?</span><span class="sxs-lookup"><span data-stu-id="40cbc-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="40cbc-143">U kunt de lijst met op Linux vinden op [Azure-Endorsed distributies](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="40cbc-143">You can find the list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="40cbc-144">Kan ik een bestaande klassieke virtuele machine toevoegen aan een beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="40cbc-144">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="40cbc-145">Ja.</span><span class="sxs-lookup"><span data-stu-id="40cbc-145">Yes.</span></span> <span data-ttu-id="40cbc-146">U kunt een bestaande klassieke virtuele machine toevoegen aan een nieuwe of bestaande Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="40cbc-146">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="40cbc-147">Zie voor meer informatie [een bestaande virtuele machine toevoegen aan een beschikbaarheidsset](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="40cbc-147">For more information see [Add an existing virtual machine to an availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="40cbc-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="40cbc-148">Next steps</span></span>
<span data-ttu-id="40cbc-149">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts raadplegen op [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="40cbc-149">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="40cbc-150">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="40cbc-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="40cbc-151">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.</span><span class="sxs-lookup"><span data-stu-id="40cbc-151">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
