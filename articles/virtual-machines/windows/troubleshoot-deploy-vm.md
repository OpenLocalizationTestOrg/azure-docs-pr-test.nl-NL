---
title: Problemen met implementatie Windows virtuele machine in Azure | Microsoft Docs
description: Problemen met implementatie Windows virtuele machine in Azurethe Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 6800c137097c2803f28dec7365f6d3f2a173b411
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="357bf-103">Problemen met implementatie Windows virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="357bf-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="357bf-104">Voor het oplossen van problemen bij de implementatie in Azure virtuele machine (VM), Controleer de [top problemen](#top-issues) voor algemene fouten en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="357bf-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="357bf-105">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts raadplegen op [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="357bf-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="357bf-106">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="357bf-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="357bf-107">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.</span><span class="sxs-lookup"><span data-stu-id="357bf-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="357bf-108">Meest voorkomende problemen</span><span class="sxs-lookup"><span data-stu-id="357bf-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="357bf-109">Het cluster kan het aangevraagde VM-grootte niet ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="357bf-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="357bf-110">Probeer de aanvraag met een kleinere VM.</span><span class="sxs-lookup"><span data-stu-id="357bf-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="357bf-111">Als de grootte van de aangevraagde virtuele machine kan niet worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="357bf-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="357bf-112">Stop de virtuele machines in de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="357bf-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="357bf-113">Klik op **resourcegroepen** > uw resourcegroep > **Resources** > uw beschikbaarheidsset > **virtuele Machines** > uw virtuele machine >  **Stop**.</span><span class="sxs-lookup"><span data-stu-id="357bf-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="357bf-114">Nadat de virtuele machines stoppen, moet u de virtuele machine maken in de gewenste grootte.</span><span class="sxs-lookup"><span data-stu-id="357bf-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="357bf-115">De nieuwe virtuele machine eerst te starten en selecteert u elk van de gestopte virtuele machines en klik op Start.</span><span class="sxs-lookup"><span data-stu-id="357bf-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="357bf-116">Het cluster heeft geen gratis resources</span><span class="sxs-lookup"><span data-stu-id="357bf-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="357bf-117">De aanvraag later opnieuw.</span><span class="sxs-lookup"><span data-stu-id="357bf-117">Retry the request later.</span></span>
- <span data-ttu-id="357bf-118">Als de nieuwe virtuele machine deel van een andere beschikbaarheidsset uitmaken kan</span><span class="sxs-lookup"><span data-stu-id="357bf-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="357bf-119">Een virtuele machine maken in een andere beschikbaarheidsset (in dezelfde regio).</span><span class="sxs-lookup"><span data-stu-id="357bf-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="357bf-120">De nieuwe virtuele machine toevoegen aan hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="357bf-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="357bf-121">Hoe kan ik gebruiken en de installatiekopie van een windows-client implementeren in Azure?</span><span class="sxs-lookup"><span data-stu-id="357bf-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="357bf-122">U kunt Windows 7, Windows 8 of Windows 10 in Azure gebruiken voor ontwikkel-/ Testscenario's als u een juiste Visual Studio (voorheen MSDN)-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="357bf-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="357bf-123">Dit [artikel](client-images.md) geeft een overzicht van de vereisten in aanmerking komt voor actieve Windows-client in Azure en maakt gebruik van de installatiekopieën van het Azure-galerie.</span><span class="sxs-lookup"><span data-stu-id="357bf-123">This [article](client-images.md) outlines the eligibility requirements for running Windows client in Azure and uses of the Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-the-hybrid-use-benefit-hub"></a><span data-ttu-id="357bf-124">Hoe kan ik een virtuele machine met de hybride gebruik voordeel (HUB) implementeren?</span><span class="sxs-lookup"><span data-stu-id="357bf-124">How can I deploy a virtual machine using the Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="357bf-125">Er zijn een aantal verschillende manieren voor het implementeren van virtuele machines en de schaalvoordelen van Azure hybride gebruik van Windows.</span><span class="sxs-lookup"><span data-stu-id="357bf-125">There are a couple of different ways to deploy Windows virtual machines with the Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="357bf-126">Voor een Enterprise Agreement-abonnement:</span><span class="sxs-lookup"><span data-stu-id="357bf-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="357bf-127">• VM's van specifieke Marketplace-installatiekopieën die vooraf geconfigureerd met Azure hybride gebruik voordeel zijn implementeren.</span><span class="sxs-lookup"><span data-stu-id="357bf-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="357bf-128">Voor Enterprise-overeenkomst:</span><span class="sxs-lookup"><span data-stu-id="357bf-128">For Enterprise agreement:</span></span>

<span data-ttu-id="357bf-129">• Een aangepaste VM uploaden en implementeren met behulp van een Resource Manager-sjabloon of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="357bf-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="357bf-130">Zie de volgende bronnen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="357bf-130">For more information, see the following resources:</span></span>

 - [<span data-ttu-id="357bf-131">Overzicht van Azure hybride gebruik Benefit</span><span class="sxs-lookup"><span data-stu-id="357bf-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="357bf-132">Downloadbare Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="357bf-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="357bf-133">[Azure hybride gebruik voordeel voor WindowsServer en Windows-Client](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="357bf-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="357bf-134">Hoe kan ik het voordeel van hybride gebruiken in Azure gebruiken</span><span class="sxs-lookup"><span data-stu-id="357bf-134">How can I use the Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="357bf-135">Hoe kan ik mijn maandelijkse tegoed voor Visual studio Enterprise (BizSpark) activeren</span><span class="sxs-lookup"><span data-stu-id="357bf-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="357bf-136">Als u wilt uw maandelijkse tegoed hebt geactiveerd, ziet u dit [artikel](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="357bf-136">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-to-add-enterprise-devtest-to-my-enterprise-agreement-ea-to-get-access-to-window-client-images"></a><span data-ttu-id="357bf-137">Het Enterprise ontwikkelen en testen voor mijn Enterprise Agreement (EA) voor toegang tot venster clientinstallatiekopieën toevoegen?</span><span class="sxs-lookup"><span data-stu-id="357bf-137">How to add Enterprise Dev/Test to my Enterprise Agreement (EA) to get access to Window client images?</span></span>

<span data-ttu-id="357bf-138">De mogelijkheid te maken op basis van de aanbieding Enterprise ontwikkelen en testen abonnementen is beperkt tot de eigenaren van de Account die gemachtigd is om dit te doen door een ondernemingsadministrator.</span><span class="sxs-lookup"><span data-stu-id="357bf-138">The ability to create subscriptions based on the Enterprise Dev/Test offer is restricted to Account Owners who have been given permission to do so by an Enterprise Administrator.</span></span> <span data-ttu-id="357bf-139">De accounteigenaar abonnementen via de Portal van het Azure-Account maakt en vervolgens actieve Visual Studio-abonnees moet toevoegen als medebeheerders.</span><span class="sxs-lookup"><span data-stu-id="357bf-139">The Account Owner creates subscriptions via the Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="357bf-140">Zodat ze kunnen beheren en gebruiken van de benodigde resources voor het ontwikkelen en testen.</span><span class="sxs-lookup"><span data-stu-id="357bf-140">So that they can manage and use the resources needed for development and testing.</span></span> <span data-ttu-id="357bf-141">Zie voor meer informatie [Enterprise ontwikkelen en testen](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="357bf-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="357bf-142">De stuurprogramma's ontbreken voor mijn Windows-VM met N-serie</span><span class="sxs-lookup"><span data-stu-id="357bf-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="357bf-143">Stuurprogramma's voor Windows-VM's zich bevinden [hier](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="357bf-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="357bf-144">Ik kan een GPU-exemplaar niet vinden in mijn VM N-serie</span><span class="sxs-lookup"><span data-stu-id="357bf-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="357bf-145">Als u wilt profiteren van de GPU-mogelijkheden van N-reeks virtuele machines in Azure waarop Windows Server 2016 of Windows Server 2012 R2 wordt uitgevoerd, moet u NVIDIA grafische stuurprogramma's installeren op elke virtuele machine na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="357bf-145">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="357bf-146">Stuurprogramma-installatie-informatie is beschikbaar voor [VM's van Windows](n-series-driver-setup.md) en [virtuele Linux-machines](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="357bf-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="357bf-147">Worden de clientinstallatiekopieën van de voor N-serie ondersteund?</span><span class="sxs-lookup"><span data-stu-id="357bf-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="357bf-148">Azure ondersteunt momenteel alleen N-reeks op virtuele machines met Windows Server- en Linux-besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="357bf-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="357bf-149">Virtuele machines N-reeks is beschikbaar in mijn regio?</span><span class="sxs-lookup"><span data-stu-id="357bf-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="357bf-150">U kunt controleren dat de beschikbaarheid van de [producten die per regio tabel](https://azure.microsoft.com/regions/services), en prijzen [hier](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="357bf-150">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-to-i-get-them"></a><span data-ttu-id="357bf-151">Welke clientimages kan ik gebruiken en te implementeren in Azure, en hoe naar ik ze?</span><span class="sxs-lookup"><span data-stu-id="357bf-151">What client images can I use and deploy in Azure, and how to I get them?</span></span>

<span data-ttu-id="357bf-152">U kunt Windows 7, Windows 8 of Windows 10 in Azure voor ontwikkel-/ Testscenario's geleverde dat een juiste Visual Studio (voorheen MSDN)-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="357bf-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="357bf-153">Installatiekopieën van Windows 10 zijn beschikbaar in de galerie van Azure binnen [in aanmerking komende ontwikkelen en testen biedt](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="357bf-153">Windows 10 images are available from the Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="357bf-154">Visual Studio-abonnees binnen elk type aanbieding kunnen ook [voldoende voorbereiden en maken](prepare-for-upload-vhd-image.md) een 64-bits installatiekopie voor Windows 7, Windows 8 of Windows 10 en vervolgens [uploaden naar Azure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="357bf-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload to Azure](upload-generalized-managed.md).</span></span> <span data-ttu-id="357bf-155">Het gebruik blijft beperkt tot ontwikkelen en testen door actieve Visual Studio-abonnees.</span><span class="sxs-lookup"><span data-stu-id="357bf-155">The use remains limited to dev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="357bf-156">Dit [artikel](client-images.md) geeft een overzicht van de vereisten in aanmerking komt voor actieve Windows-client in Azure en het gebruik van de installatiekopieën van het Azure-galerie.</span><span class="sxs-lookup"><span data-stu-id="357bf-156">This [article](client-images.md) outlines the eligibility requirements for running Windows client in Azure and use of the Azure Gallery images.</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="357bf-157">Ik wil niet kunnen zien van VM-grootte-familie die ik wil wanneer het formaat van mijn VM.</span><span class="sxs-lookup"><span data-stu-id="357bf-157">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="357bf-158">Wanneer een virtuele machine wordt uitgevoerd, wordt geïmplementeerd met een fysieke server.</span><span class="sxs-lookup"><span data-stu-id="357bf-158">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="357bf-159">De fysieke servers in de Azure-regio's worden gegroepeerd in clusters van algemene fysieke hardware.</span><span class="sxs-lookup"><span data-stu-id="357bf-159">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="357bf-160">Formaat van een virtuele machine die u moet de virtuele machine worden verplaatst naar andere hardware clusters verschilt, afhankelijk van welke implementatiemodel is gebruikt voor het implementeren van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="357bf-160">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="357bf-161">Virtuele machines die worden geïmplementeerd in het klassieke implementatiemodel, de cloud service-implementatie moeten worden verwijderd en opnieuw als u wilt wijzigen in een grootte in een ander gezin van de grootte van de virtuele machines zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="357bf-161">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="357bf-162">Virtuele machines in de Resource Manager-implementatiemodel zijn geïmplementeerd, moet u alle virtuele machines stoppen in beschikbaarheidsset voordat u wijzigt de grootte van een virtuele machine in de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="357bf-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="357bf-163">De vermelde VM-grootte wordt niet ondersteund tijdens de implementatie in Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="357bf-163">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="357bf-164">Kies een grootte die wordt ondersteund op de beschikbaarheidsset cluster.</span><span class="sxs-lookup"><span data-stu-id="357bf-164">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="357bf-165">Het wordt aanbevolen wanneer de grootste VM-grootte u denkt dat u nodig hebt en hebt die uw eerste implementatie voor de beschikbaarheidsset kiezen voor het maken van een beschikbaarheidsset ingesteld.</span><span class="sxs-lookup"><span data-stu-id="357bf-165">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="357bf-166">Kan ik een bestaande klassieke virtuele machine toevoegen aan een beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="357bf-166">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="357bf-167">Ja.</span><span class="sxs-lookup"><span data-stu-id="357bf-167">Yes.</span></span> <span data-ttu-id="357bf-168">U kunt een bestaande klassieke virtuele machine toevoegen aan een nieuwe of bestaande Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="357bf-168">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="357bf-169">Zie voor meer informatie [een bestaande virtuele machine toevoegen aan een beschikbaarheidsset](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="357bf-169">For more information see [Add an existing virtual machine to an availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="357bf-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="357bf-170">Next steps</span></span>
<span data-ttu-id="357bf-171">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts raadplegen op [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="357bf-171">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="357bf-172">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="357bf-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="357bf-173">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.</span><span class="sxs-lookup"><span data-stu-id="357bf-173">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
