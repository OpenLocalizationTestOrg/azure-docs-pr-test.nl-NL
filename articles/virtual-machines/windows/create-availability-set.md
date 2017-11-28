---
title: Maak een VM-beschikbaarheid instellen in Azure | Microsoft Docs
description: Informatie over het maken van een beschikbaarheidsset beheerde of onbeheerde beschikbaarheidsset voor uw virtuele machines met behulp van Azure PowerShell of de portal in het Resource Manager-implementatiemodel.
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
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="d532a-104">Toename VM beschikbaarheid door het maken van een Azure beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="d532a-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="d532a-105">Beschikbaarheidssets redundantie voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d532a-105">Availability sets provide redundancy to your application.</span></span> <span data-ttu-id="d532a-106">Het is raadzaam dat u twee of meer virtuele machines in een beschikbaarheidsset te groeperen.</span><span class="sxs-lookup"><span data-stu-id="d532a-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="d532a-107">Deze configuratie zorgt ervoor dat tijdens de gepland of ongepland onderhoud ten minste één virtuele machine beschikbaar is en voldoet aan de 99,95% Azure SLA.</span><span class="sxs-lookup"><span data-stu-id="d532a-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet the 99.95% Azure SLA.</span></span> <span data-ttu-id="d532a-108">Zie de [SLA voor virtuele machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d532a-108">For more information, see the [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d532a-109">Virtuele machines moeten worden gemaakt in dezelfde resourcegroep bevinden als de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="d532a-109">VMs must be created in the same resource group as the availability set.</span></span>
> 

<span data-ttu-id="d532a-110">Als u wilt dat uw virtuele machine deel uitmaken van een beschikbaarheidsset, moet u eerst de beschikbaarheidsset maken of bij het maken van uw eerste virtuele machine in de set.</span><span class="sxs-lookup"><span data-stu-id="d532a-110">If you want your VM to be part of an availability set, you need to create the availability set first or while you are creating your first VM in the set.</span></span> <span data-ttu-id="d532a-111">Als uw VM beheerd schijven gebruikt, kan de beschikbaarheidsset moet worden gemaakt als een beschikbaarheidsset beheerde.</span><span class="sxs-lookup"><span data-stu-id="d532a-111">If your VM will be using Managed Disks, the availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="d532a-112">Zie voor meer informatie over het maken en de hand van beschikbaarheidssets [de beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d532a-112">For more information about creating and using availability sets, see [Manage the availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="d532a-113">De portal gebruiken voor het maken van een beschikbaarheidsset voordat u uw virtuele machines</span><span class="sxs-lookup"><span data-stu-id="d532a-113">Use the portal to create an availability set before creating your VMs</span></span>
1. <span data-ttu-id="d532a-114">Klik in het hub-menu op **Bladeren** en selecteer **beschikbaarheidssets**.</span><span class="sxs-lookup"><span data-stu-id="d532a-114">In the hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="d532a-115">Op de **beschikbaarheidssets blade**, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d532a-115">On the **Availability sets blade**, click **Add**.</span></span>
   
    ![Schermafbeelding van de knop toevoegen voor het maken van een nieuwe beschikbaarheid instellen.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="d532a-117">Op de **beschikbaarheidsset maken** blade Vul de gegevens voor de set.</span><span class="sxs-lookup"><span data-stu-id="d532a-117">On the **Create availability set** blade, complete the information for your set.</span></span>
   
    ![Schermafbeelding van de informatie die u wilt opgeven voor het maken van de beschikbaarheidsset.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="d532a-119">**Naam** -de naam moet 1-80 tekens bestaan uit getallen, letters, punten, onderstrepingstekens en streepjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="d532a-119">**Name** - the name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="d532a-120">Het eerste teken moet een letter of cijfer.</span><span class="sxs-lookup"><span data-stu-id="d532a-120">The first character must be a letter or number.</span></span> <span data-ttu-id="d532a-121">Het laatste teken moet een letter, cijfer of onderstrepingsteken zijn.</span><span class="sxs-lookup"><span data-stu-id="d532a-121">The last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="d532a-122">**Fault-domeinen** -domeinen met fouten definiëren in de groep van virtuele machines die een gemeenschappelijk power-bron- en switch delen.</span><span class="sxs-lookup"><span data-stu-id="d532a-122">**Fault domains** - fault domains define the group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="d532a-123">Standaard worden de virtuele machines worden gescheiden over maximaal drie domeinen met fouten en kunnen worden gewijzigd in tussen 1 en 3.</span><span class="sxs-lookup"><span data-stu-id="d532a-123">By default, the VMs  are separated across up to three fault domains and can be changed to between 1 and 3.</span></span>
   * <span data-ttu-id="d532a-124">**Bijwerken van domeinen** - vijf update domeinen worden standaard toegewezen en dit kan worden ingesteld op tussen 1 en 20.</span><span class="sxs-lookup"><span data-stu-id="d532a-124">**Update domains** -  five update domains are assigned by default and this can be set to between 1 and 20.</span></span> <span data-ttu-id="d532a-125">Update domeinen duiden op groepen van virtuele machines en de onderliggende fysieke hardware die op hetzelfde moment kan worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="d532a-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="d532a-126">Bijvoorbeeld, als er vijf-domeinen bijwerken wanneer meer dan vijf virtuele machines worden geconfigureerd in een enkel Beschikbaarheidsset opgeeft, de zesde virtuele machine worden opgenomen in hetzelfde updatedomein als de eerste virtuele machine, de zevende in de dezelfde UD als de tweede virtuele machine, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="d532a-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same update domain as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on.</span></span> <span data-ttu-id="d532a-127">De volgorde van de opnieuw wordt opgestart niet mogelijk sequentiële, maar slechts één updatedomein tegelijk zal worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="d532a-127">The order of the reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="d532a-128">**Abonnement** -de te gebruiken als u meer dan één abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="d532a-128">**Subscription** - select the subscription to use if you have more than one.</span></span>
   * <span data-ttu-id="d532a-129">**Resourcegroep** -Selecteer een bestaande resourcegroep door te klikken op de pijl en te selecteren van een resourcegroep in de vervolgkeuzelijst omlaag.</span><span class="sxs-lookup"><span data-stu-id="d532a-129">**Resource group** - select an existing resource group by clicking the arrow and selecting a resource group from the drop down.</span></span> <span data-ttu-id="d532a-130">U kunt ook een nieuwe resourcegroep maken door een naam te typen.</span><span class="sxs-lookup"><span data-stu-id="d532a-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="d532a-131">De naam mag geen van de volgende tekens bevatten: letters, cijfers, punten, streepjes, onderstrepingstekens en openen of sluithaakje.</span><span class="sxs-lookup"><span data-stu-id="d532a-131">The name can contain any of the following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="d532a-132">De naam mag niet eindigen op een punt.</span><span class="sxs-lookup"><span data-stu-id="d532a-132">The name cannot end in a period.</span></span> <span data-ttu-id="d532a-133">Alle van de virtuele machines in de beschikbaarheidsgroep moet worden gemaakt in dezelfde resourcegroep bevinden als de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="d532a-133">All of the VMs in the availability group need to be created in the same resource group as the availability set.</span></span>
   * <span data-ttu-id="d532a-134">**Locatie** -Selecteer een locatie in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="d532a-134">**Location** - select a location from the drop-down.</span></span>
   * <span data-ttu-id="d532a-135">**Beheerde** : Selecteer *Ja* voor het maken van een beheerde beschikbaarheid instellen voor gebruik met virtuele machines die gebruikmaken van beheerde schijven voor opslag.</span><span class="sxs-lookup"><span data-stu-id="d532a-135">**Managed** - select *Yes* to create a managed availability set to use with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="d532a-136">Selecteer **Nee** als de virtuele machines die weergegeven in de set worden met niet-beheerde schijven in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d532a-136">Select **No** if the VMs that will be in the set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="d532a-137">Wanneer u klaar bent u de gegevens invoert, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="d532a-137">When you are done entering the information, click **Create**.</span></span> 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a><span data-ttu-id="d532a-138">De portal gebruiken om een virtuele machine en op hetzelfde moment beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="d532a-138">Use the portal to create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="d532a-139">Als u een nieuwe virtuele machine via de portal maakt, kunt u ook een nieuwe beschikbaarheidsset voor de virtuele machine bij het maken van de eerste virtuele machine in de set.</span><span class="sxs-lookup"><span data-stu-id="d532a-139">If you are creating a new VM using the portal, you can also create a new availability set for the VM while you create the first VM in the set.</span></span> <span data-ttu-id="d532a-140">Als u kiest moet worden beheerd schijven gebruikt voor uw virtuele machine, kunt u een beheerde beschikbaarheidsset wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d532a-140">If you choose to use Managed Disks for your VM, a managed availability set will be created.</span></span>

![Schermafbeelding van het proces voor het maken van een nieuwe beschikbaarheidsset bij het maken van de virtuele machine.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a><span data-ttu-id="d532a-142">Een nieuwe virtuele machine toevoegen aan een bestaande beschikbaarheidsset in de portal</span><span class="sxs-lookup"><span data-stu-id="d532a-142">Add a new VM to an existing availability set in the portal</span></span>
<span data-ttu-id="d532a-143">Voor elke extra VM die u maakt die in de set moet behoren, zorg ervoor dat u dit hebt gemaakt in dezelfde **resourcegroep** en selecteer vervolgens de bestaande beschikbaarheidsset in stap 3.</span><span class="sxs-lookup"><span data-stu-id="d532a-143">For each additional VM that you create that should belong in the set, make sure that you create it in the same **resource group** and then select the existing availability set in Step 3.</span></span> 

![Schermopname die laat zien hoe u een bestaande beschikbaarheidsset gebruiken voor uw virtuele machine selecteert.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a><span data-ttu-id="d532a-145">Gebruik PowerShell voor het maken van een beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="d532a-145">Use PowerShell to create an availability set</span></span>
<span data-ttu-id="d532a-146">In dit voorbeeld maakt u een beschikbaarheidsset benoemde **myAvailabilitySet** in de **myResourceGroup** resourcegroep in de **VS-West** locatie.</span><span class="sxs-lookup"><span data-stu-id="d532a-146">This example creates an availability set named **myAvailabilitySet** in the **myResourceGroup** resource group in the **West US** location.</span></span> <span data-ttu-id="d532a-147">Dit moet doen voordat u de eerste virtuele machine die zich in de set maakt.</span><span class="sxs-lookup"><span data-stu-id="d532a-147">This needs to be done before you create the first VM that will be in the set.</span></span>

<span data-ttu-id="d532a-148">Voordat u begint, zorg ervoor dat u de nieuwste versie van de AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="d532a-148">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="d532a-149">Voer de volgende opdracht om deze te installeren.</span><span class="sxs-lookup"><span data-stu-id="d532a-149">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="d532a-150">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d532a-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="d532a-151">Als u beheerde schijven voor uw virtuele machines gebruikt, typt u:</span><span class="sxs-lookup"><span data-stu-id="d532a-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="d532a-152">Als u uw eigen storage-accounts voor uw virtuele machines gebruikt, typt u:</span><span class="sxs-lookup"><span data-stu-id="d532a-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="d532a-153">Zie voor meer informatie [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="d532a-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d532a-154">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="d532a-154">Troubleshooting</span></span>
* <span data-ttu-id="d532a-155">Bij het maken van een virtuele machine, als de gewenste beschikbaarheidsset niet in de vervolgkeuzelijst in de portal kunt u deze gemaakt in een andere resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d532a-155">When you create a VM, if the availability set you want isn't in the drop-down list in the portal you may have created it in a different resource group.</span></span> <span data-ttu-id="d532a-156">Als u niet weet de resourcegroep voor uw beschikbaarheid instellen, gaat u naar het hub-menu en klik op Bladeren > beschikbaarheidssets voor een overzicht van uw beschikbaarheidssets en welke resourcegroepen waartoe ze behoren.</span><span class="sxs-lookup"><span data-stu-id="d532a-156">If you don't know the resource group for your availability set, go to the hub menu and click Browse > Availability sets to see a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d532a-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d532a-157">Next steps</span></span>
<span data-ttu-id="d532a-158">Extra opslagruimte toevoegen aan uw virtuele machine met het toevoegen van een extra [gegevensschijf](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d532a-158">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

