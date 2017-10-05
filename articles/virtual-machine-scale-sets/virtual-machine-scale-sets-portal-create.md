---
title: Maak een virtuele-Machineschaalset met de Azure portal | Microsoft Docs
description: Met Azure portal-schaalsets implementeren.
keywords: Virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7157a429829974b45dad29ac53fb5fb46c71f821
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-the-azure-portal"></a><span data-ttu-id="069bc-104">Het maken van een virtuele-Machineschaalset met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="069bc-104">How to create a Virtual Machine Scale Set with the Azure portal</span></span>
<span data-ttu-id="069bc-105">Deze zelfstudie laat zien hoe eenvoudig het is een virtuele-Machineschaalset maken in een paar minuten met behulp van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="069bc-105">This tutorial shows you how easy it is to create a Virtual Machine Scale Set in just a few minutes, by using the Azure portal.</span></span> <span data-ttu-id="069bc-106">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="069bc-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="choose-the-vm-image-from-the-marketplace"></a><span data-ttu-id="069bc-107">Een installatiekopie voor de virtuele machine kiezen in de marketplace</span><span class="sxs-lookup"><span data-stu-id="069bc-107">Choose the VM image from the marketplace</span></span>
<span data-ttu-id="069bc-108">U kunt een schaal CentOS, virtuele CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server of installatiekopieën van Windows Server in te stellen eenvoudig implementeren vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="069bc-108">From the portal, you can easily deploy a scale set with CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server, or Windows Server images.</span></span>

<span data-ttu-id="069bc-109">Eerst, navigeer naar de [Azure-portal](https://portal.azure.com) in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="069bc-109">First, navigate to the [Azure portal](https://portal.azure.com) in a web browser.</span></span> <span data-ttu-id="069bc-110">Klik op `New`, zoeken naar `scale set`, en selecteer vervolgens de `Virtual machine scale set` post:</span><span class="sxs-lookup"><span data-stu-id="069bc-110">Click `New`, search for `scale set`, and then select the `Virtual machine scale set` entry:</span></span>

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-the-scale-set"></a><span data-ttu-id="069bc-112">De schaalset maken</span><span class="sxs-lookup"><span data-stu-id="069bc-112">Create the scale set</span></span>
<span data-ttu-id="069bc-113">U kunt nu de standaardinstellingen gebruiken en de schaalaanpassingsset snel maken.</span><span class="sxs-lookup"><span data-stu-id="069bc-113">Now you can use the default settings and quickly create the scale set.</span></span>

* <span data-ttu-id="069bc-114">Op de `Basics` blade een naam voor de scale-set.</span><span class="sxs-lookup"><span data-stu-id="069bc-114">On the `Basics` blade, enter a name for the scale set.</span></span> <span data-ttu-id="069bc-115">Deze naam wordt het grondtal van de FQDN-naam van de load balancer voor de schaalaanpassingsset, dus zorg ervoor dat de naam uniek is in alle Azure.</span><span class="sxs-lookup"><span data-stu-id="069bc-115">This name becomes the base of the FQDN of the load balancer in front of the scale set, so make sure the name is unique across all Azure.</span></span>
* <span data-ttu-id="069bc-116">Selecteer het gewenste besturingssysteem typt u de gewenste gebruikersnaam invoeren en selecteren welke verificatiemethode typt u liever.</span><span class="sxs-lookup"><span data-stu-id="069bc-116">Select your desired OS type, enter your desired username, and select which authentication type you prefer.</span></span> <span data-ttu-id="069bc-117">Als u een wachtwoord kiest, moet deze zijn minstens 12 tekens lang en drie van de volgende vier complexiteitsvereisten voldoen aan: één kleine letter, één hoofdletter, één cijfer en één speciaal teken.</span><span class="sxs-lookup"><span data-stu-id="069bc-117">If you choose a password, it must be at least 12 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="069bc-118">Zie meer informatie over [vereisten voor gebruikersnaam en wachtwoord](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="069bc-118">See more about [username and password requirements](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span> <span data-ttu-id="069bc-119">Als u ervoor kiest `SSH public key`, zorg ervoor dat alleen plakken in uw openbare sleutel niet uw persoonlijke sleutel:</span><span class="sxs-lookup"><span data-stu-id="069bc-119">If you choose `SSH public key`, be sure to only paste in your public key, NOT your private key:</span></span>

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* <span data-ttu-id="069bc-121">Kies of u wilt beperken van de schaal is ingesteld op een groep één plaatsing of of dit meerdere plaatsing groepen moet omvatten.</span><span class="sxs-lookup"><span data-stu-id="069bc-121">Choose whether you would like to limit the scale set to a single placement group or whether it should span multiple placement groups.</span></span> <span data-ttu-id="069bc-122">Schaal kunt u de schaal is ingesteld op span plaatsing groepen toe, stelt u meer dan 100 virtuele machines in capaciteit (maximaal 1000) met bepaalde beperkingen.</span><span class="sxs-lookup"><span data-stu-id="069bc-122">Allowing the scale set to span placement groups allows for scale sets over 100 VMs in capacity (up to 1,000) with certain limitations.</span></span> <span data-ttu-id="069bc-123">Zie voor meer informatie [deze documentatie](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="069bc-123">For more information, see [this documentation](./virtual-machine-scale-sets-placement-groups.md).</span></span>
* <span data-ttu-id="069bc-124">Voer uw gewenste Resourcegroepnaam en de locatie en klik vervolgens op `OK`.</span><span class="sxs-lookup"><span data-stu-id="069bc-124">Enter your desired resource group name and location, and then click `OK`.</span></span>
* <span data-ttu-id="069bc-125">Op de `Virtual machine scale set service settings` blade: Geef de gewenste domeinnaamlabel (de basis van de FQDN-naam voor de load balancer voor de schaalaanpassingsset).</span><span class="sxs-lookup"><span data-stu-id="069bc-125">On the `Virtual machine scale set service settings` blade: enter your desired domain name label (the base of the FQDN for the load balancer in front of the scale set).</span></span> <span data-ttu-id="069bc-126">Dit label moet uniek zijn binnen alle Azure.</span><span class="sxs-lookup"><span data-stu-id="069bc-126">This label must be unique across all Azure.</span></span>
* <span data-ttu-id="069bc-127">Kies uw schijfimage gewenste besturingssysteem, het aantal exemplaren en de grootte van de machine.</span><span class="sxs-lookup"><span data-stu-id="069bc-127">Choose your desired operating system disk image, instance count, and machine size.</span></span>
* <span data-ttu-id="069bc-128">De gewenste schijf kiezen: beheerd of onbeheerd.</span><span class="sxs-lookup"><span data-stu-id="069bc-128">Choose your desired disk type: managed or unmanaged.</span></span> <span data-ttu-id="069bc-129">Zie voor meer informatie [deze documentatie](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="069bc-129">For more information, see [this documentation](./virtual-machine-scale-sets-managed-disks.md).</span></span> <span data-ttu-id="069bc-130">Als u hebt gekozen om de schaal instelt span meerdere plaatsing groepen, deze optie niet meer beschikbaar omdat de beheerde schijf is vereist voor schaalsets meerdere groepen voor plaatsing.</span><span class="sxs-lookup"><span data-stu-id="069bc-130">If you chose to have the scale set span multiple placement groups, this option will not be available because managed disk is required for scale sets to span placement groups.</span></span>
* <span data-ttu-id="069bc-131">In- of uitschakelen voor automatisch schalen en configureren als ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="069bc-131">Enable or disable autoscale and configure if enabled:</span></span>

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* <span data-ttu-id="069bc-133">Op de `Summary` blade als validatie is voltooid, klikt u op `OK` ingesteld voor het starten van de schaal implementatie.</span><span class="sxs-lookup"><span data-stu-id="069bc-133">On the `Summary` blade, when validation is done, click `OK` to start the scale set deployment.</span></span>


## <a name="connect-to-a-vm-in-the-scale-set"></a><span data-ttu-id="069bc-134">Verbinding maken met een virtuele machine in de schaalset</span><span class="sxs-lookup"><span data-stu-id="069bc-134">Connect to a VM in the scale set</span></span>
<span data-ttu-id="069bc-135">Als u wilt beperken schaal ingesteld op een enkele plaatsing-groep, wordt klikt u vervolgens de schaalaanpassingsset geïmplementeerd met NAT-regels geconfigureerd waarmee u verbinding maken met de schaal eenvoudig ingesteld (zo niet, verbinding maken met de virtuele machines in de schaalset, u waarschijnlijk hoeft te maken van een jumpbox in dezelfde  virtueel netwerk als de schaal instellen).</span><span class="sxs-lookup"><span data-stu-id="069bc-135">If you chose to limit your scale set to a single placement group, then the scale set is deployed with NAT rules configured to let you connect to the scale set easily (if not, to connect to the virtual machines in the scale set, you likely need to create a jumpbox in the same virtual network as the scale set).</span></span> <span data-ttu-id="069bc-136">Om ze te bekijken, gaat u naar de `Inbound NAT Rules` tabblad van de load balancer voor de schaalaanpassingsset:</span><span class="sxs-lookup"><span data-stu-id="069bc-136">To see them, navigate to the `Inbound NAT Rules` tab of the load balancer for the scale set:</span></span>

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

<span data-ttu-id="069bc-138">U kunt verbinding maken met elke virtuele machine in de schaal instelt met behulp van deze NAT-regels.</span><span class="sxs-lookup"><span data-stu-id="069bc-138">You can connect to each VM in the scale set using these NAT rules.</span></span> <span data-ttu-id="069bc-139">Bijvoorbeeld: voor een Windows-scale set, als er een NAT-regel op de binnenkomende poort 50000 u kan verbinding maken met die machine via RDP op `<load-balancer-ip-address>:50000`.</span><span class="sxs-lookup"><span data-stu-id="069bc-139">For instance, for a Windows scale set, if there is a NAT rule on incoming port 50000, you could connect to that machine via RDP on `<load-balancer-ip-address>:50000`.</span></span> <span data-ttu-id="069bc-140">Voor een Linux-scale set, zou u verbinding met de opdracht `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span><span class="sxs-lookup"><span data-stu-id="069bc-140">For a Linux scale set, you would connect using the command `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="069bc-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="069bc-141">Next steps</span></span>
<span data-ttu-id="069bc-142">Zie voor documentatie over het implementeren van de schaal wordt ingesteld vanuit de CLI, [deze documentatie](virtual-machine-scale-sets-cli-quick-create.md).</span><span class="sxs-lookup"><span data-stu-id="069bc-142">For documentation on how to deploy scale sets from the CLI, see [this documentation](virtual-machine-scale-sets-cli-quick-create.md).</span></span>

<span data-ttu-id="069bc-143">Zie voor documentatie over het implementeren van de schaal wordt ingesteld vanuit PowerShell, [deze documentatie](virtual-machine-scale-sets-windows-create.md).</span><span class="sxs-lookup"><span data-stu-id="069bc-143">For documentation on how to deploy scale sets from PowerShell, see [this documentation](virtual-machine-scale-sets-windows-create.md).</span></span>

<span data-ttu-id="069bc-144">Zie voor documentatie over het implementeren van de schaal wordt ingesteld vanuit Visual Studio, [deze documentatie](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="069bc-144">For documentation on how to deploy scale sets from Visual Studio, see [this documentation](virtual-machine-scale-sets-vs-create.md).</span></span>

<span data-ttu-id="069bc-145">Bekijk voor algemene documentatie, de [documentatie overzichtspagina voor schaalsets](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="069bc-145">For general documentation, check out the [documentation overview page for scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="069bc-146">Bekijk voor algemene informatie, de [belangrijkste startpagina voor schaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="069bc-146">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

