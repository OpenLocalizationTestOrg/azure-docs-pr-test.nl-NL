---
title: problemen met Windows virtuele machine in Azure implementeren aaaTroubleshoot | Microsoft Docs
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="ef30e-103">Problemen met implementatie Windows virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="ef30e-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="ef30e-104">tootroubleshoot implementatieproblemen van virtuele machine (VM) in Azure, bekijk Hallo [top problemen](#top-issues) voor algemene fouten en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="ef30e-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="ef30e-105">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ef30e-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="ef30e-106">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="ef30e-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="ef30e-107">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.</span><span class="sxs-lookup"><span data-stu-id="ef30e-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="ef30e-108">Meest voorkomende problemen</span><span class="sxs-lookup"><span data-stu-id="ef30e-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="ef30e-109">Hallo-cluster kan niet ondersteunen Hallo aangevraagde VM-grootte</span><span class="sxs-lookup"><span data-stu-id="ef30e-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="ef30e-110">Probeer Hallo-aanvraag met een kleinere VM.</span><span class="sxs-lookup"><span data-stu-id="ef30e-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="ef30e-111">Als hello aangevraagde grootte van Hallo dat VM kan niet worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="ef30e-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="ef30e-112">Stop alle Hallo-VM's in de beschikbaarheidsset Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef30e-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="ef30e-113">Klik op **resourcegroepen** > uw resourcegroep > **Resources** > uw beschikbaarheidsset > **virtuele Machines** > uw virtuele machine >  **Stop**.</span><span class="sxs-lookup"><span data-stu-id="ef30e-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="ef30e-114">Nadat alle virtuele machines stoppen Hallo, Hallo VM maken in Hallo gewenst grootte.</span><span class="sxs-lookup"><span data-stu-id="ef30e-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="ef30e-115">Start eerst Hallo van nieuwe virtuele machine en vervolgens Selecteer Hallo gestopt VM's en klik op Start.</span><span class="sxs-lookup"><span data-stu-id="ef30e-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="ef30e-116">Hallo-cluster heeft geen gratis resources</span><span class="sxs-lookup"><span data-stu-id="ef30e-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="ef30e-117">Hallo aanvraag later opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="ef30e-117">Retry hello request later.</span></span>
- <span data-ttu-id="ef30e-118">Als hello nieuwe virtuele machine kan deel uitmaken van een andere beschikbaarheidsset instellen</span><span class="sxs-lookup"><span data-stu-id="ef30e-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="ef30e-119">Een virtuele machine maken in een andere beschikbaarheidsset (in Hallo dezelfde regio).</span><span class="sxs-lookup"><span data-stu-id="ef30e-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="ef30e-120">Toevoegen van nieuwe VM-toohello Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef30e-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="ef30e-121">Hoe kan ik gebruiken en de installatiekopie van een windows-client implementeren in Azure?</span><span class="sxs-lookup"><span data-stu-id="ef30e-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="ef30e-122">U kunt Windows 7, Windows 8 of Windows 10 in Azure gebruiken voor ontwikkel-/ Testscenario's als u een juiste Visual Studio (voorheen MSDN)-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="ef30e-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="ef30e-123">Dit [artikel](client-images.md) overzichten Hallo in aanmerking komt vereisten voor het uitvoeren van Windows-client in Azure en het gebruik van Hallo galerie van Azure-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="ef30e-123">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and uses of hello Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a><span data-ttu-id="ef30e-124">Hoe kan ik een virtuele machine met Hallo hybride gebruik voordeel (HUB) implementeren?</span><span class="sxs-lookup"><span data-stu-id="ef30e-124">How can I deploy a virtual machine using hello Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="ef30e-125">Er zijn een aantal virtuele machines van verschillende manieren toodeploy Windows Hello Azure hybride gebruik Benefit.</span><span class="sxs-lookup"><span data-stu-id="ef30e-125">There are a couple of different ways toodeploy Windows virtual machines with hello Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="ef30e-126">Voor een Enterprise Agreement-abonnement:</span><span class="sxs-lookup"><span data-stu-id="ef30e-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="ef30e-127">• VM's van specifieke Marketplace-installatiekopieën die vooraf geconfigureerd met Azure hybride gebruik voordeel zijn implementeren.</span><span class="sxs-lookup"><span data-stu-id="ef30e-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="ef30e-128">Voor Enterprise-overeenkomst:</span><span class="sxs-lookup"><span data-stu-id="ef30e-128">For Enterprise agreement:</span></span>

<span data-ttu-id="ef30e-129">• Een aangepaste VM uploaden en implementeren met behulp van een Resource Manager-sjabloon of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef30e-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="ef30e-130">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef30e-130">For more information, see hello following resources:</span></span>

 - [<span data-ttu-id="ef30e-131">Overzicht van Azure hybride gebruik Benefit</span><span class="sxs-lookup"><span data-stu-id="ef30e-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="ef30e-132">Downloadbare Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="ef30e-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="ef30e-133">[Azure hybride gebruik voordeel voor WindowsServer en Windows-Client](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="ef30e-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="ef30e-134">Hoe kan ik Hallo hybride gebruiken voordeel gebruiken in Azure</span><span class="sxs-lookup"><span data-stu-id="ef30e-134">How can I use hello Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="ef30e-135">Hoe kan ik mijn maandelijkse tegoed voor Visual studio Enterprise (BizSpark) activeren</span><span class="sxs-lookup"><span data-stu-id="ef30e-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="ef30e-136">tooactivate uw maandelijkse tegoed, ziet u dit [artikel](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="ef30e-136">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a><span data-ttu-id="ef30e-137">Hoe tooadd Enterprise ontwikkelen en testen toomy Enterprise Agreement (EA) tooget tooWindow clientimages toegang?</span><span class="sxs-lookup"><span data-stu-id="ef30e-137">How tooadd Enterprise Dev/Test toomy Enterprise Agreement (EA) tooget access tooWindow client images?</span></span>

<span data-ttu-id="ef30e-138">Hallo mogelijkheid toocreate abonnementen op basis van Hallo Enterprise ontwikkelen en testen bieden is beperkt tooAccount eigenaars die toodo machtiging hebben gekregen in dat geval door een ondernemingsadministrator bent.</span><span class="sxs-lookup"><span data-stu-id="ef30e-138">hello ability toocreate subscriptions based on hello Enterprise Dev/Test offer is restricted tooAccount Owners who have been given permission toodo so by an Enterprise Administrator.</span></span> <span data-ttu-id="ef30e-139">Hallo accounteigenaar abonnementen via Hallo Portal voor Azure-Account maakt en vervolgens actieve Visual Studio-abonnees moet toevoegen als medebeheerders.</span><span class="sxs-lookup"><span data-stu-id="ef30e-139">hello Account Owner creates subscriptions via hello Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="ef30e-140">Zodat ze kunnen beheren en gebruiken van Hallo-resources die nodig zijn voor het ontwikkelen en testen.</span><span class="sxs-lookup"><span data-stu-id="ef30e-140">So that they can manage and use hello resources needed for development and testing.</span></span> <span data-ttu-id="ef30e-141">Zie voor meer informatie [Enterprise ontwikkelen en testen](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="ef30e-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="ef30e-142">De stuurprogramma's ontbreken voor mijn Windows-VM met N-serie</span><span class="sxs-lookup"><span data-stu-id="ef30e-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="ef30e-143">Stuurprogramma's voor Windows-VM's zich bevinden [hier](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="ef30e-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="ef30e-144">Ik kan een GPU-exemplaar niet vinden in mijn VM N-serie</span><span class="sxs-lookup"><span data-stu-id="ef30e-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="ef30e-145">tootake profiteren van Hallo GPU-mogelijkheden van Azure N-serie VM's met WindowsServer 2016 of Windows Server 2012 R2, moet u NVIDIA grafische stuurprogramma's installeren op elke virtuele machine na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="ef30e-145">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="ef30e-146">Stuurprogramma-installatie-informatie is beschikbaar voor [VM's van Windows](n-series-driver-setup.md) en [virtuele Linux-machines](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="ef30e-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="ef30e-147">Worden de clientinstallatiekopieën van de voor N-serie ondersteund?</span><span class="sxs-lookup"><span data-stu-id="ef30e-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="ef30e-148">Azure ondersteunt momenteel alleen N-reeks op virtuele machines met Windows Server- en Linux-besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="ef30e-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="ef30e-149">Virtuele machines N-reeks is beschikbaar in mijn regio?</span><span class="sxs-lookup"><span data-stu-id="ef30e-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="ef30e-150">U kunt controleren Hallo beschikbaarheid van Hallo [producten die per regio tabel](https://azure.microsoft.com/regions/services), en prijzen [hier](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="ef30e-150">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a><span data-ttu-id="ef30e-151">Welke clientimages kan ik gebruiken en te implementeren in Azure, en hoe tooI ze?</span><span class="sxs-lookup"><span data-stu-id="ef30e-151">What client images can I use and deploy in Azure, and how tooI get them?</span></span>

<span data-ttu-id="ef30e-152">U kunt Windows 7, Windows 8 of Windows 10 in Azure voor ontwikkel-/ Testscenario's geleverde dat een juiste Visual Studio (voorheen MSDN)-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="ef30e-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="ef30e-153">Installatiekopieën van Windows 10 zijn beschikbaar in de galerie van Azure Hallo binnen [in aanmerking komende ontwikkelen en testen biedt](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="ef30e-153">Windows 10 images are available from hello Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="ef30e-154">Visual Studio-abonnees binnen elk type aanbieding kunnen ook [voldoende voorbereiden en maken](prepare-for-upload-vhd-image.md) een 64-bits installatiekopie voor Windows 7, Windows 8 of Windows 10 en vervolgens [tooAzure uploaden](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="ef30e-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="ef30e-155">Hallo gebruik blijft beperkt toodev en testen door actieve Visual Studio-abonnees.</span><span class="sxs-lookup"><span data-stu-id="ef30e-155">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="ef30e-156">Dit [artikel](client-images.md) overzichten Hallo in aanmerking komt vereisten voor het uitvoeren van Windows-client in Azure en het gebruik van Hallo galerie van Azure-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="ef30e-156">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="ef30e-157">Ik wil niet kunnen toosee VM-grootte familie die ik wil wanneer het formaat van mijn VM.</span><span class="sxs-lookup"><span data-stu-id="ef30e-157">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="ef30e-158">Wanneer een virtuele machine wordt uitgevoerd, is het geïmplementeerde tooa fysieke server.</span><span class="sxs-lookup"><span data-stu-id="ef30e-158">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="ef30e-159">Hallo fysieke servers in de Azure-regio's worden gegroepeerd in clusters van algemene fysieke hardware.</span><span class="sxs-lookup"><span data-stu-id="ef30e-159">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="ef30e-160">Formaat van een virtuele machine waarvoor Hallo VM toobe verplaatst toodifferent hardware clusters verschilt, afhankelijk van welke implementatiemodel gebruikte toodeploy Hallo VM is.</span><span class="sxs-lookup"><span data-stu-id="ef30e-160">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="ef30e-161">Virtuele machines die worden geïmplementeerd in het klassieke implementatiemodel, Hallo cloud service-implementatie moeten worden verwijderd en opnieuw geïmplementeerd toochange Hallo VMs tooa grootte in een ander grootte gezin.</span><span class="sxs-lookup"><span data-stu-id="ef30e-161">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="ef30e-162">Virtuele machines in de Resource Manager-implementatiemodel zijn geïmplementeerd, moet u alle virtuele machines stoppen in Hallo beschikbaarheidsset voordat u de grootte van een virtuele machine in de beschikbaarheidsset Hallo Hallo wijzigt.</span><span class="sxs-lookup"><span data-stu-id="ef30e-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="ef30e-163">Hallo wordt vermelde VM-grootte niet ondersteund tijdens de implementatie in Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="ef30e-163">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="ef30e-164">Kies een grootte die wordt ondersteund op Hallo beschikbaarheidsset-cluster.</span><span class="sxs-lookup"><span data-stu-id="ef30e-164">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="ef30e-165">Het wordt aanbevolen bij het maken van dat een beschikbaarheidsset toochoose Hallo VM maximumgrootte u denkt dat u nodig hebt en u hebt uw eerste implementatie toohello beschikbaarheidsset worden.</span><span class="sxs-lookup"><span data-stu-id="ef30e-165">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="ef30e-166">Kan ik een bestaande beschikbaarheidsset voor klassieke VM tooan toevoegen?</span><span class="sxs-lookup"><span data-stu-id="ef30e-166">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="ef30e-167">Ja.</span><span class="sxs-lookup"><span data-stu-id="ef30e-167">Yes.</span></span> <span data-ttu-id="ef30e-168">U kunt een bestaande klassieke VM tooa nieuwe toevoegen of bestaande Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="ef30e-168">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="ef30e-169">Zie voor meer informatie [toevoegen van een bestaande beschikbaarheidsset voor de virtuele machine tooan](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="ef30e-169">For more information see [Add an existing virtual machine tooan availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="ef30e-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef30e-170">Next steps</span></span>
<span data-ttu-id="ef30e-171">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ef30e-171">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="ef30e-172">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="ef30e-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="ef30e-173">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.</span><span class="sxs-lookup"><span data-stu-id="ef30e-173">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
