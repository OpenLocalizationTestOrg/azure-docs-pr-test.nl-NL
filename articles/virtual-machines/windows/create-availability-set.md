---
title: aaaCreate de beschikbaarheid van een virtuele machine in Azure instellen | Microsoft Docs
description: Informatie over hoe ingesteld toocreate een beschikbare beheerde of onbeheerde beschikbaarheid instellen voor uw virtuele machines met Azure PowerShell of Hallo portal Hallo Resource Manager-implementatiemodel.
keywords: Beschikbaarheidsset
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="7d382-104">Toename VM beschikbaarheid door het maken van een Azure beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="7d382-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="7d382-105">Beschikbaarheidssets bieden redundantie tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="7d382-105">Availability sets provide redundancy tooyour application.</span></span> <span data-ttu-id="7d382-106">Het is raadzaam dat u twee of meer virtuele machines in een beschikbaarheidsset te groeperen.</span><span class="sxs-lookup"><span data-stu-id="7d382-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="7d382-107">Deze configuratie zorgt ervoor dat tijdens de gepland of ongepland onderhoud ten minste één virtuele machine zal beschikbaar zijn en voldoen aan Hallo 99,95% Azure SLA.</span><span class="sxs-lookup"><span data-stu-id="7d382-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet hello 99.95% Azure SLA.</span></span> <span data-ttu-id="7d382-108">Zie voor meer informatie, Hallo [SLA voor virtuele Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="7d382-108">For more information, see hello [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d382-109">Virtuele machines moeten worden gemaakt in Hallo dezelfde resourcegroep als Hallo beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="7d382-109">VMs must be created in hello same resource group as hello availability set.</span></span>
> 

<span data-ttu-id="7d382-110">Als u wilt dat uw VM toobe een deel van een beschikbaarheidsset, moet u toocreate Hallo beschikbaarheid instellen eerste of terwijl u uw eerste virtuele machine in maakt Hallo set.</span><span class="sxs-lookup"><span data-stu-id="7d382-110">If you want your VM toobe part of an availability set, you need toocreate hello availability set first or while you are creating your first VM in hello set.</span></span> <span data-ttu-id="7d382-111">Als uw VM beheerd schijven gebruikt, moet de beschikbaarheidsset Hallo worden gemaakt als een beschikbaarheidsset beheerde.</span><span class="sxs-lookup"><span data-stu-id="7d382-111">If your VM will be using Managed Disks, hello availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="7d382-112">Zie voor meer informatie over het maken en de hand van beschikbaarheidssets [Hallo beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d382-112">For more information about creating and using availability sets, see [Manage hello availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="7d382-113">Hallo portal toocreate beschikbaarheidsset voordat u uw virtuele machines gebruiken</span><span class="sxs-lookup"><span data-stu-id="7d382-113">Use hello portal toocreate an availability set before creating your VMs</span></span>
1. <span data-ttu-id="7d382-114">Klik in het menu hub Hallo op **Bladeren** en selecteer **beschikbaarheidssets**.</span><span class="sxs-lookup"><span data-stu-id="7d382-114">In hello hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="7d382-115">Op Hallo **beschikbaarheidssets blade**, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7d382-115">On hello **Availability sets blade**, click **Add**.</span></span>
   
    ![Schermafbeelding van Hallo knop voor het maken van een nieuwe beschikbaarheidsset toevoegen.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="7d382-117">Op Hallo **beschikbaarheidsset maken** blade, volledige Hallo-informatie voor uw set.</span><span class="sxs-lookup"><span data-stu-id="7d382-117">On hello **Create availability set** blade, complete hello information for your set.</span></span>
   
    ![Schermopname die toont informatie die u nodig tooenter toocreate Hallo beschikbaarheid Hallo ingesteld.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="7d382-119">**Naam** -Hallo-naam moet 1-80 tekens bestaan uit getallen, letters, punten, onderstrepingstekens en streepjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="7d382-119">**Name** - hello name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="7d382-120">Hallo eerste teken moet een letter of cijfer zijn.</span><span class="sxs-lookup"><span data-stu-id="7d382-120">hello first character must be a letter or number.</span></span> <span data-ttu-id="7d382-121">Hallo laatste teken moet een letter, cijfer of onderstrepingsteken zijn.</span><span class="sxs-lookup"><span data-stu-id="7d382-121">hello last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="7d382-122">**Fault-domeinen** -domeinen met fouten definiëren Hallo groep virtuele machines die een gemeenschappelijk power-bron- en switch delen.</span><span class="sxs-lookup"><span data-stu-id="7d382-122">**Fault domains** - fault domains define hello group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="7d382-123">Standaard kunnen Hallo VMs gescheiden zijn in up toothree domeinen met fouten en gewijzigde toobetween 1 en 3.</span><span class="sxs-lookup"><span data-stu-id="7d382-123">By default, hello VMs  are separated across up toothree fault domains and can be changed toobetween 1 and 3.</span></span>
   * <span data-ttu-id="7d382-124">**Bijwerken van domeinen** - vijf update domeinen worden standaard toegewezen en deze toobetween 1 en 20 kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7d382-124">**Update domains** -  five update domains are assigned by default and this can be set toobetween 1 and 20.</span></span> <span data-ttu-id="7d382-125">Update domeinen groepen van virtuele machines en de onderliggende fysieke hardware die kan worden opgestart op Hallo duiden op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="7d382-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="7d382-126">Bijvoorbeeld, als er vijf update domeinen, wanneer meer dan vijf virtuele machines worden geconfigureerd in een enkel Beschikbaarheidsset, Hallo zesde virtuele machine worden opgenomen in Hallo hetzelfde updatedomein als eerste virtuele machine Hallo Hallo zevende opgeeft Hallo dezelfde UD als Hallo tweede virtuele machine, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="7d382-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, hello sixth virtual machine will be placed into hello same update domain as hello first virtual machine, hello seventh in hello same UD as hello second virtual machine, and so on.</span></span> <span data-ttu-id="7d382-127">mogelijk sequentiële volgorde Hallo Hallo opnieuw te worden opgestart niet, maar slechts één updatedomein tegelijk zal worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="7d382-127">hello order of hello reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="7d382-128">**Abonnement** -Selecteer Hallo abonnement toouse als er meer dan één.</span><span class="sxs-lookup"><span data-stu-id="7d382-128">**Subscription** - select hello subscription toouse if you have more than one.</span></span>
   * <span data-ttu-id="7d382-129">**Resourcegroep** -Selecteer een bestaande resourcegroep door te klikken op de pijl Hallo en een resourcegroep te selecteren Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="7d382-129">**Resource group** - select an existing resource group by clicking hello arrow and selecting a resource group from hello drop down.</span></span> <span data-ttu-id="7d382-130">U kunt ook een nieuwe resourcegroep maken door een naam te typen.</span><span class="sxs-lookup"><span data-stu-id="7d382-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="7d382-131">Hallo naam mag geen van de volgende tekens Hallo: letters, cijfers, punten, streepjes, onderstrepingstekens en openen of sluithaakje.</span><span class="sxs-lookup"><span data-stu-id="7d382-131">hello name can contain any of hello following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="7d382-132">Hallo-naam mag niet eindigen op een punt.</span><span class="sxs-lookup"><span data-stu-id="7d382-132">hello name cannot end in a period.</span></span> <span data-ttu-id="7d382-133">Alle Hallo virtuele machines in de beschikbaarheidsgroep Hallo toobe in Hallo hebt gemaakt, moeten dezelfde resourcegroep als Hallo beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="7d382-133">All of hello VMs in hello availability group need toobe created in hello same resource group as hello availability set.</span></span>
   * <span data-ttu-id="7d382-134">**Locatie** -Selecteer een locatie in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="7d382-134">**Location** - select a location from hello drop-down.</span></span>
   * <span data-ttu-id="7d382-135">**Beheerde** : Selecteer *Ja* toocreate een beschikbare beheerde ingesteld toouse met virtuele machines die gebruikmaken van beheerde schijven voor opslag.</span><span class="sxs-lookup"><span data-stu-id="7d382-135">**Managed** - select *Yes* toocreate a managed availability set toouse with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="7d382-136">Selecteer **Nee** als Hallo virtuele machines die weergegeven in het Hallo-set worden niet-beheerde schijven in een opslagaccount gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7d382-136">Select **No** if hello VMs that will be in hello set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="7d382-137">Wanneer u klaar bent met het invoeren van Hallo gegevens, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="7d382-137">When you are done entering hello information, click **Create**.</span></span> 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a><span data-ttu-id="7d382-138">Gebruik Hallo portal toocreate een virtuele machine en een beschikbaarheid op Hallo dezelfde instellen tijd</span><span class="sxs-lookup"><span data-stu-id="7d382-138">Use hello portal toocreate a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="7d382-139">Als u een nieuwe virtuele machine met behulp van Hallo portal maakt, kunt u ook een nieuwe beschikbaarheidsset voor Hallo VM bij het maken van Hallo maken eerste VM in het Hallo-set.</span><span class="sxs-lookup"><span data-stu-id="7d382-139">If you are creating a new VM using hello portal, you can also create a new availability set for hello VM while you create hello first VM in hello set.</span></span> <span data-ttu-id="7d382-140">Als u toouse beheerd schijven voor uw virtuele machine kiest, kunt u een beheerde beschikbaarheidsset wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7d382-140">If you choose toouse Managed Disks for your VM, a managed availability set will be created.</span></span>

![Schermafbeelding van Hallo-proces voor het maken van een nieuwe beschikbaarheidsset bij het maken van Hallo VM.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a><span data-ttu-id="7d382-142">Voeg een nieuwe VM tooan bestaande beschikbaarheidsset Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="7d382-142">Add a new VM tooan existing availability set in hello portal</span></span>
<span data-ttu-id="7d382-143">Hallo voor elke extra VM die u maakt moet deel uitmaken van Hallo set, zorg ervoor dat u maakt in dezelfde **resourcegroep** en vervolgens selecteert Hallo bestaande beschikbaarheidsset in stap 3.</span><span class="sxs-lookup"><span data-stu-id="7d382-143">For each additional VM that you create that should belong in hello set, make sure that you create it in hello same **resource group** and then select hello existing availability set in Step 3.</span></span> 

![Schermopname die laat zien hoe de bestaande beschikbaarheidsset tooselect toouse ingesteld voor uw virtuele machine.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a><span data-ttu-id="7d382-145">Gebruik PowerShell toocreate een beschikbaarheidsset instellen</span><span class="sxs-lookup"><span data-stu-id="7d382-145">Use PowerShell toocreate an availability set</span></span>
<span data-ttu-id="7d382-146">In dit voorbeeld maakt u een beschikbaarheidsset benoemde **myAvailabilitySet** in Hallo **myResourceGroup** resourcegroep in Hallo **VS-West** locatie.</span><span class="sxs-lookup"><span data-stu-id="7d382-146">This example creates an availability set named **myAvailabilitySet** in hello **myResourceGroup** resource group in hello **West US** location.</span></span> <span data-ttu-id="7d382-147">Dit moet doen voordat u Hallo maakt toobe eerste virtuele machine die zich in Hallo set.</span><span class="sxs-lookup"><span data-stu-id="7d382-147">This needs toobe done before you create hello first VM that will be in hello set.</span></span>

<span data-ttu-id="7d382-148">Voordat u begint, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="7d382-148">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="7d382-149">Voer Hallo na de opdracht tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="7d382-149">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="7d382-150">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7d382-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="7d382-151">Als u beheerde schijven voor uw virtuele machines gebruikt, typt u:</span><span class="sxs-lookup"><span data-stu-id="7d382-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="7d382-152">Als u uw eigen storage-accounts voor uw virtuele machines gebruikt, typt u:</span><span class="sxs-lookup"><span data-stu-id="7d382-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="7d382-153">Zie voor meer informatie [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="7d382-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7d382-154">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7d382-154">Troubleshooting</span></span>
* <span data-ttu-id="7d382-155">Bij het maken van een virtuele machine als Hallo beschikbaarheid sets die u wilt zich niet in Hallo vervolgkeuzelijst in de portal Hallo u mogelijk hebt gemaakt in een andere resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="7d382-155">When you create a VM, if hello availability set you want isn't in hello drop-down list in hello portal you may have created it in a different resource group.</span></span> <span data-ttu-id="7d382-156">Als u niet weet Hallo resourcegroep voor uw beschikbaarheid instellen, gaat u toohello hub-menu en klik op Bladeren > beschikbaarheidssets toosee Hiermee stelt u een lijst van de beschikbaarheid en welke resourcegroepen waartoe ze behoren.</span><span class="sxs-lookup"><span data-stu-id="7d382-156">If you don't know hello resource group for your availability set, go toohello hub menu and click Browse > Availability sets toosee a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d382-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7d382-157">Next steps</span></span>
<span data-ttu-id="7d382-158">Toevoegen van extra opslagruimte tooyour VM door toe te voegen een extra [gegevensschijf](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d382-158">Add additional storage tooyour VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

