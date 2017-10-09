---
title: een virtuele-Machineschaalset met aaaCreate hello Azure-portal | Microsoft Docs
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
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a><span data-ttu-id="9641d-104">Hoe toocreate een virtuele-Machineschaalset met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9641d-104">How toocreate a Virtual Machine Scale Set with hello Azure portal</span></span>
<span data-ttu-id="9641d-105">Deze zelfstudie laat zien hoe eenvoudig het is een virtuele-Machineschaalset toocreate in een paar minuten met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9641d-105">This tutorial shows you how easy it is toocreate a Virtual Machine Scale Set in just a few minutes, by using hello Azure portal.</span></span> <span data-ttu-id="9641d-106">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="9641d-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="choose-hello-vm-image-from-hello-marketplace"></a><span data-ttu-id="9641d-107">Kies Hallo VM-installatiekopie in marketplace Hallo</span><span class="sxs-lookup"><span data-stu-id="9641d-107">Choose hello VM image from hello marketplace</span></span>
<span data-ttu-id="9641d-108">U kunt eenvoudig een schaal CentOS, virtuele CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server of installatiekopieën van Windows Server in te stellen vanuit de portal Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="9641d-108">From hello portal, you can easily deploy a scale set with CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server, or Windows Server images.</span></span>

<span data-ttu-id="9641d-109">Ga eerst toohello [Azure-portal](https://portal.azure.com) in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="9641d-109">First, navigate toohello [Azure portal](https://portal.azure.com) in a web browser.</span></span> <span data-ttu-id="9641d-110">Klik op `New`, zoeken naar `scale set`, en selecteer vervolgens Hallo `Virtual machine scale set` post:</span><span class="sxs-lookup"><span data-stu-id="9641d-110">Click `New`, search for `scale set`, and then select hello `Virtual machine scale set` entry:</span></span>

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a><span data-ttu-id="9641d-112">Hallo scale set maken</span><span class="sxs-lookup"><span data-stu-id="9641d-112">Create hello scale set</span></span>
<span data-ttu-id="9641d-113">U kunt nu Hallo standaardinstellingen gebruiken en snel maken Hallo schaalset.</span><span class="sxs-lookup"><span data-stu-id="9641d-113">Now you can use hello default settings and quickly create hello scale set.</span></span>

* <span data-ttu-id="9641d-114">Op Hallo `Basics` blade een naam voor het Hallo-schaalset.</span><span class="sxs-lookup"><span data-stu-id="9641d-114">On hello `Basics` blade, enter a name for hello scale set.</span></span> <span data-ttu-id="9641d-115">Deze naam wordt Hallo base Hallo FQDN Hallo load balancer voor schaalset hello, zorg er dus Hallo naam uniek is in alle Azure.</span><span class="sxs-lookup"><span data-stu-id="9641d-115">This name becomes hello base of hello FQDN of hello load balancer in front of hello scale set, so make sure hello name is unique across all Azure.</span></span>
* <span data-ttu-id="9641d-116">Selecteer het gewenste besturingssysteem typt u de gewenste gebruikersnaam invoeren en selecteren welke verificatiemethode typt u liever.</span><span class="sxs-lookup"><span data-stu-id="9641d-116">Select your desired OS type, enter your desired username, and select which authentication type you prefer.</span></span> <span data-ttu-id="9641d-117">Als u een wachtwoord kiest, moet deze zijn minstens 12 tekens lang en drie buiten Hallo de volgende vier complexiteitsvereisten voldoen aan: één kleine letter, één hoofdletter, één cijfer en één speciaal teken.</span><span class="sxs-lookup"><span data-stu-id="9641d-117">If you choose a password, it must be at least 12 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="9641d-118">Zie meer informatie over [vereisten voor gebruikersnaam en wachtwoord](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="9641d-118">See more about [username and password requirements](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span> <span data-ttu-id="9641d-119">Als u ervoor kiest `SSH public key`, ervoor tooonly plakken in uw openbare sleutel niet uw persoonlijke sleutel:</span><span class="sxs-lookup"><span data-stu-id="9641d-119">If you choose `SSH public key`, be sure tooonly paste in your public key, NOT your private key:</span></span>

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* <span data-ttu-id="9641d-121">Kies of u zou doen zoals toolimit hello tooa plaatsing van één groep schaalset of dat dit meerdere plaatsing groepen moet omvatten.</span><span class="sxs-lookup"><span data-stu-id="9641d-121">Choose whether you would like toolimit hello scale set tooa single placement group or whether it should span multiple placement groups.</span></span> <span data-ttu-id="9641d-122">Bij het toestaan van Hallo schaalset toospan plaatsing groepen kan voor de schaal wordt meer dan 100 virtuele machines in capaciteit (omhoog too1, 000) met bepaalde beperkingen.</span><span class="sxs-lookup"><span data-stu-id="9641d-122">Allowing hello scale set toospan placement groups allows for scale sets over 100 VMs in capacity (up too1,000) with certain limitations.</span></span> <span data-ttu-id="9641d-123">Zie voor meer informatie [deze documentatie](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="9641d-123">For more information, see [this documentation](./virtual-machine-scale-sets-placement-groups.md).</span></span>
* <span data-ttu-id="9641d-124">Voer uw gewenste Resourcegroepnaam en de locatie en klik vervolgens op `OK`.</span><span class="sxs-lookup"><span data-stu-id="9641d-124">Enter your desired resource group name and location, and then click `OK`.</span></span>
* <span data-ttu-id="9641d-125">Op Hallo `Virtual machine scale set service settings` blade: Geef de gewenste domeinnaamlabel (basis Hallo Hallo FQDN-naam voor de load balancer Hallo voor Hallo schaalset).</span><span class="sxs-lookup"><span data-stu-id="9641d-125">On hello `Virtual machine scale set service settings` blade: enter your desired domain name label (hello base of hello FQDN for hello load balancer in front of hello scale set).</span></span> <span data-ttu-id="9641d-126">Dit label moet uniek zijn binnen alle Azure.</span><span class="sxs-lookup"><span data-stu-id="9641d-126">This label must be unique across all Azure.</span></span>
* <span data-ttu-id="9641d-127">Kies uw schijfimage gewenste besturingssysteem, het aantal exemplaren en de grootte van de machine.</span><span class="sxs-lookup"><span data-stu-id="9641d-127">Choose your desired operating system disk image, instance count, and machine size.</span></span>
* <span data-ttu-id="9641d-128">De gewenste schijf kiezen: beheerd of onbeheerd.</span><span class="sxs-lookup"><span data-stu-id="9641d-128">Choose your desired disk type: managed or unmanaged.</span></span> <span data-ttu-id="9641d-129">Zie voor meer informatie [deze documentatie](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="9641d-129">For more information, see [this documentation](./virtual-machine-scale-sets-managed-disks.md).</span></span> <span data-ttu-id="9641d-130">Als u hebt gekozen toohave hello schaalset span meerdere plaatsing groepen, deze optie niet meer beschikbaar omdat de beheerde schijf is vereist voor schaal sets toospan plaatsing groepen.</span><span class="sxs-lookup"><span data-stu-id="9641d-130">If you chose toohave hello scale set span multiple placement groups, this option will not be available because managed disk is required for scale sets toospan placement groups.</span></span>
* <span data-ttu-id="9641d-131">In- of uitschakelen voor automatisch schalen en configureren als ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="9641d-131">Enable or disable autoscale and configure if enabled:</span></span>

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* <span data-ttu-id="9641d-133">Op Hallo `Summary` blade als validatie is voltooid, klikt u op `OK` toostart hello schaalset implementatie.</span><span class="sxs-lookup"><span data-stu-id="9641d-133">On hello `Summary` blade, when validation is done, click `OK` toostart hello scale set deployment.</span></span>


## <a name="connect-tooa-vm-in-hello-scale-set"></a><span data-ttu-id="9641d-134">Verbinding maken met tooa VM in de schaalset Hallo</span><span class="sxs-lookup"><span data-stu-id="9641d-134">Connect tooa VM in hello scale set</span></span>
<span data-ttu-id="9641d-135">Als u hebt gekozen toolimit schaal ingesteld tooa plaatsing van één groep, wordt de Hallo scale set wordt geïmplementeerd met NAT-regels geconfigureerd toolet u toohello scale ingesteld eenvoudig verbinding maken (als u niet het geval is, tooconnect toohello virtuele machines in Hallo scale is ingesteld, moet u waarschijnlijk toocreate een jumpbox in Hallo hetzelfde virtuele netwerk als Hallo schaalset).</span><span class="sxs-lookup"><span data-stu-id="9641d-135">If you chose toolimit your scale set tooa single placement group, then hello scale set is deployed with NAT rules configured toolet you connect toohello scale set easily (if not, tooconnect toohello virtual machines in hello scale set, you likely need toocreate a jumpbox in hello same virtual network as hello scale set).</span></span> <span data-ttu-id="9641d-136">toosee, gaat u toohello `Inbound NAT Rules` tabblad Hallo load balancer voor Hallo scale set:</span><span class="sxs-lookup"><span data-stu-id="9641d-136">toosee them, navigate toohello `Inbound NAT Rules` tab of hello load balancer for hello scale set:</span></span>

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

<span data-ttu-id="9641d-138">U kunt deze NAT-regels met een VM in het Hallo-scale set tooeach verbinden.</span><span class="sxs-lookup"><span data-stu-id="9641d-138">You can connect tooeach VM in hello scale set using these NAT rules.</span></span> <span data-ttu-id="9641d-139">Bijvoorbeeld: voor een Windows-scale set, als er een NAT-regel op de binnenkomende poort 50000 u kan verbinding maken toothat machine via RDP op `<load-balancer-ip-address>:50000`.</span><span class="sxs-lookup"><span data-stu-id="9641d-139">For instance, for a Windows scale set, if there is a NAT rule on incoming port 50000, you could connect toothat machine via RDP on `<load-balancer-ip-address>:50000`.</span></span> <span data-ttu-id="9641d-140">Voor een Linux-schaalset zou u verbinding met de opdracht Hallo `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span><span class="sxs-lookup"><span data-stu-id="9641d-140">For a Linux scale set, you would connect using hello command `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9641d-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9641d-141">Next steps</span></span>
<span data-ttu-id="9641d-142">Zie voor documentatie op hoe toodeploy scale ingesteld van Hallo CLI [deze documentatie](virtual-machine-scale-sets-cli-quick-create.md).</span><span class="sxs-lookup"><span data-stu-id="9641d-142">For documentation on how toodeploy scale sets from hello CLI, see [this documentation](virtual-machine-scale-sets-cli-quick-create.md).</span></span>

<span data-ttu-id="9641d-143">Zie voor documentatie over hoe toodeploy scale ingesteld van PowerShell, [deze documentatie](virtual-machine-scale-sets-windows-create.md).</span><span class="sxs-lookup"><span data-stu-id="9641d-143">For documentation on how toodeploy scale sets from PowerShell, see [this documentation](virtual-machine-scale-sets-windows-create.md).</span></span>

<span data-ttu-id="9641d-144">Zie voor documentatie over hoe toodeploy schaal wordt ingesteld vanuit Visual Studio, [deze documentatie](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="9641d-144">For documentation on how toodeploy scale sets from Visual Studio, see [this documentation](virtual-machine-scale-sets-vs-create.md).</span></span>

<span data-ttu-id="9641d-145">Bekijk voor algemene documentatie Hallo [documentatie overzichtspagina voor schaalsets](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9641d-145">For general documentation, check out hello [documentation overview page for scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="9641d-146">Raadpleeg voor algemene informatie Hallo [belangrijkste startpagina voor schaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="9641d-146">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

