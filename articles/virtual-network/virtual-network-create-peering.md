---
title: Maak een virtueel netwerk van Azure-peering - Resource Manager - hetzelfde abonnement | Microsoft Docs
description: Informatie over het maken van een virtueel netwerk peering tussen virtuele netwerken via Resource Manager gemaakt en die aanwezig zijn in dezelfde Azure-abonnement.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: a32a6b33e04c603325ab3612f61e5852682eac7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="307c9-103">Maak een virtueel netwerk peering - Resource Manager, hetzelfde abonnement</span><span class="sxs-lookup"><span data-stu-id="307c9-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="307c9-104">In deze zelfstudie leert u een virtueel netwerk tussen virtuele netwerken die zijn gemaakt via Resource Manager-peering maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="307c9-105">Beide virtuele netwerken zich in hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="307c9-105">Both virtual networks exist in the same subscription.</span></span> <span data-ttu-id="307c9-106">Peering twee virtuele netwerken kunnen resources in verschillende virtuele netwerken met elkaar communiceren met de bandbreedte en de latentie, alsof de resources in hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="307c9-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="307c9-107">Meer informatie over [virtuele netwerk peering](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="307c9-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="307c9-108">De stappen voor het maken van een virtueel netwerk peering verschillen, afhankelijk van of de virtuele netwerken zijn in dezelfde of verschillende abonnementen en die zijn [Azure implementatiemodel](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) via de virtuele netwerken worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="307c9-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="307c9-109">Meer informatie over het maken van een virtueel netwerk peering in andere scenario's door te klikken op het scenario uit de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="307c9-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="307c9-110">Azure-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="307c9-110">Azure deployment model</span></span>  | <span data-ttu-id="307c9-111">Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="307c9-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="307c9-112">Beide Resource Manager</span><span class="sxs-lookup"><span data-stu-id="307c9-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="307c9-113">Andere</span><span class="sxs-lookup"><span data-stu-id="307c9-113">Different</span></span>|
|[<span data-ttu-id="307c9-114">Een Resource Manager, een klassiek</span><span class="sxs-lookup"><span data-stu-id="307c9-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="307c9-115">Dezelfde</span><span class="sxs-lookup"><span data-stu-id="307c9-115">Same</span></span>|
|[<span data-ttu-id="307c9-116">Een Resource Manager, een klassiek</span><span class="sxs-lookup"><span data-stu-id="307c9-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="307c9-117">Andere</span><span class="sxs-lookup"><span data-stu-id="307c9-117">Different</span></span>|

<span data-ttu-id="307c9-118">Een virtueel netwerk peering kan niet worden gemaakt tussen twee virtuele netwerken die zijn geïmplementeerd via het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="307c9-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="307c9-119">Een virtueel netwerk peering kan alleen worden gemaakt tussen twee virtuele netwerken die zijn opgenomen in dezelfde Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="307c9-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="307c9-120">Als u virtuele netwerken die zijn beide gemaakt via het klassieke implementatiemodel wilt, of die zijn opgenomen in verschillende Azure-regio's verbinden, kunt u een Azure [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) verbinding van de virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="307c9-120">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

<span data-ttu-id="307c9-121">U kunt de [Azure-portal](#portal), de Azure [opdrachtregelinterface](#cli) (CLI) Azure [PowerShell](#powershell), of een [Azure Resource Manager-sjabloon](#template)peering van een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-121">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) to create a virtual network peering.</span></span> <span data-ttu-id="307c9-122">Klik op een van de vorige hulpprogramma koppelingen om rechtstreeks naar de stappen voor het maken van een virtueel netwerk peering met behulp van het hulpprogramma naar keuze te gaan.</span><span class="sxs-lookup"><span data-stu-id="307c9-122">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="307c9-123"><a name="portal"></a>Maken van de peering - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="307c9-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="307c9-124">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="307c9-124">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="307c9-125">Het account dat u zich met aanmeldt moet hebben de vereiste machtigingen om de peering van een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-125">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="307c9-126">Zie de [machtigingen](#permissions) sectie van dit artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="307c9-126">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="307c9-127">Klik op **+ nieuw**, klikt u op **Networking**, klikt u vervolgens op **virtueel netwerk**.</span><span class="sxs-lookup"><span data-stu-id="307c9-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="307c9-128">In de **virtueel netwerk maken** blade invoert, of Selecteer waarden voor de volgende instellingen en klik vervolgens op **maken**:</span><span class="sxs-lookup"><span data-stu-id="307c9-128">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="307c9-129">**Naam**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="307c9-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="307c9-130">**Adresruimte**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="307c9-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="307c9-131">**Subnetnaam**: *standaard*</span><span class="sxs-lookup"><span data-stu-id="307c9-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="307c9-132">**Subnet-adresbereik**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="307c9-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="307c9-133">**Abonnement**: uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="307c9-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="307c9-134">**Resourcegroep**: Selecteer **nieuw** en voer *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="307c9-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="307c9-135">**Locatie**: *VS-Oost*</span><span class="sxs-lookup"><span data-stu-id="307c9-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="307c9-136">Volg de stappen 2-3 opnieuw opgeven van de volgende waarden in stap 3:</span><span class="sxs-lookup"><span data-stu-id="307c9-136">Complete steps 2-3 again specifying the following values in step 3:</span></span>
    - <span data-ttu-id="307c9-137">**Naam**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="307c9-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="307c9-138">**Adresruimte**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="307c9-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="307c9-139">**Subnetnaam**: *standaard*</span><span class="sxs-lookup"><span data-stu-id="307c9-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="307c9-140">**Subnet-adresbereik**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="307c9-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="307c9-141">**Abonnement**: uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="307c9-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="307c9-142">**Resourcegroep**: Selecteer **gebruik bestaande** en selecteer *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="307c9-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="307c9-143">**Locatie**: *VS-Oost*</span><span class="sxs-lookup"><span data-stu-id="307c9-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="307c9-144">In de **zoeken bronnen** vak aan de bovenkant van de portal type *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="307c9-144">In the **Search resources** box at the top of the portal, type *myResourceGroup*.</span></span> <span data-ttu-id="307c9-145">Klik op **myResourceGroup** wanneer deze wordt weergegeven in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="307c9-145">Click **myResourceGroup** when it appears in the search results.</span></span> <span data-ttu-id="307c9-146">Een blade wordt weergegeven voor de **myresourcegroup** resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="307c9-146">A blade appears for the **myresourcegroup** resource group.</span></span> <span data-ttu-id="307c9-147">De resourcegroep bevat de twee virtuele netwerken in de vorige stappen hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="307c9-147">The resource group contains the two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="307c9-148">Klik op **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="307c9-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="307c9-149">In de **myVnet1** blade die wordt weergegeven, klikt u op **Peerings** uit de verticale lijst met opties aan de linkerkant van de blade.</span><span class="sxs-lookup"><span data-stu-id="307c9-149">In the **myVnet1** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
8. <span data-ttu-id="307c9-150">In de **myVnet1 - Peerings** blade die werden weergegeven, klikt u op **+ toevoegen**</span><span class="sxs-lookup"><span data-stu-id="307c9-150">In the **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="307c9-151">In de **toevoegen peering** blade die wordt weergegeven, invoeren, of de volgende opties selecteren en klik vervolgens op **OK**:</span><span class="sxs-lookup"><span data-stu-id="307c9-151">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="307c9-152">**Naam**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="307c9-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="307c9-153">**Virtueel netwerk implementatiemodel**: Selecteer **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="307c9-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="307c9-154">**Abonnement**: uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="307c9-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="307c9-155">**Virtueel netwerk**: klik op **Kies een virtueel netwerk**, klikt u vervolgens op **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="307c9-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="307c9-156">**Toestaan van toegang tot het virtuele netwerk:** ervoor te zorgen dat **ingeschakeld** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="307c9-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="307c9-157">Er zijn geen andere instellingen worden gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="307c9-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="307c9-158">Lees voor meer informatie over instellingen voor alle peering [beheren van virtueel netwerk peerings](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="307c9-158">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="307c9-159">Wanneer u op **OK** in de vorige stap, de **toevoegen peering** blade wordt gesloten en u ziet de **myVnet1 - Peerings** blade opnieuw.</span><span class="sxs-lookup"><span data-stu-id="307c9-159">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="307c9-160">Na een paar seconden weergegeven de peering die u hebt gemaakt in de blade.</span><span class="sxs-lookup"><span data-stu-id="307c9-160">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="307c9-161">**Geïnitieerd** wordt vermeld in de **PEERING STATUS** kolom voor de **myVnet1ToMyVnet2** peering u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="307c9-161">**Initiated** is listed in the **PEERING STATUS** column for the **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="307c9-162">U hebt ingesteld als peer Vnet1 naar Vnet2, maar u moet nu myVnet2 naar myVnet1 peer.</span><span class="sxs-lookup"><span data-stu-id="307c9-162">You've peered Vnet1 to Vnet2, but now you must peer myVnet2 to myVnet1.</span></span> <span data-ttu-id="307c9-163">De peering moet worden gemaakt in beide richtingen waarmee bronnen in de virtuele netwerken met elkaar communiceren.</span><span class="sxs-lookup"><span data-stu-id="307c9-163">The peering must be created in both directions to enable resources in the virtual networks to communicate with each other.</span></span>
11. <span data-ttu-id="307c9-164">Herhaal stap 5-10 nogmaals voor myVnet2.</span><span class="sxs-lookup"><span data-stu-id="307c9-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="307c9-165">Naam van de peering *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="307c9-165">Name the peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="307c9-166">Een paar seconden na het klikken op **OK** peering voor MyVnet2, maken de **myVnet2ToMyVnet1** peering u zojuist hebt gemaakt wordt vermeld met **verbonden** in de  **STATUS van de PEERING** kolom.</span><span class="sxs-lookup"><span data-stu-id="307c9-166">A few seconds after clicking **OK** to create the peering for MyVnet2, the **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in the **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="307c9-167">Stap 5-7 opnieuw uitvoeren voor MyVnet1.</span><span class="sxs-lookup"><span data-stu-id="307c9-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="307c9-168">De **PEERING STATUS** voor de **myVnet1ToVNet2** peering is nu er ook **verbonden**.</span><span class="sxs-lookup"><span data-stu-id="307c9-168">The **PEERING STATUS** for the **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="307c9-169">De peering is tot stand gebracht nadat er **verbonden** in de **PEERING STATUS** kolom voor beide virtuele netwerken in de peering.</span><span class="sxs-lookup"><span data-stu-id="307c9-169">The peering is successfully established after you see **Connected** in the **PEERING STATUS** column for both virtual networks in the peering.</span></span>
14. <span data-ttu-id="307c9-170">**Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine op een andere, te valideren.</span><span class="sxs-lookup"><span data-stu-id="307c9-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
15. <span data-ttu-id="307c9-171">**Optionele**: voor het verwijderen van de resources die u in deze zelfstudie maakt, voert u de stappen in de [resources verwijderen](#delete-portal) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="307c9-171">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="307c9-172">Alle Azure-resources die in een virtueel netwerk hebt u zich nu met elkaar communiceren via hun IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="307c9-172">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="307c9-173">Als u van standaard Azure-naamomzetting voor de virtuele netwerken gebruikmaakt, zich de resources in de virtuele netwerken niet voor de naamomzetting tussen de virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="307c9-173">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="307c9-174">Als u wilt voor het omzetten van namen over virtuele netwerken in een peering, moet u uw eigen DNS-server maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-174">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="307c9-175">Meer informatie over het instellen van [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="307c9-175">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="307c9-176"><a name="cli"></a>Peering - maken Azure CLI</span><span class="sxs-lookup"><span data-stu-id="307c9-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="307c9-177">Het volgende script:</span><span class="sxs-lookup"><span data-stu-id="307c9-177">The following script:</span></span>

- <span data-ttu-id="307c9-178">De Azure CLI versie 2.0.4 vereist of hoger.</span><span class="sxs-lookup"><span data-stu-id="307c9-178">Requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="307c9-179">Uitvoeren als u wilt zoeken naar de versie, de `az --version` opdracht.</span><span class="sxs-lookup"><span data-stu-id="307c9-179">To find the version, run the `az --version` command.</span></span> <span data-ttu-id="307c9-180">Als u Azure CLI 2.0 wilt upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="307c9-180">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="307c9-181">Werkt in een Bash-shell.</span><span class="sxs-lookup"><span data-stu-id="307c9-181">Works in a Bash shell.</span></span> <span data-ttu-id="307c9-182">Zie voor opties op Azure CLI-scripts die worden uitgevoerd op Windows-client [uitvoeren van de Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="307c9-182">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="307c9-183">In plaats van installatie van de CLI en de bijbehorende afhankelijkheden, kunt u de Azure-Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="307c9-183">Instead of installing the CLI and its dependencies, you can use the Azure Cloud Shell.</span></span> <span data-ttu-id="307c9-184">De Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks in Azure Portal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="307c9-184">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="307c9-185">In deze shell is de Azure CLI vooraf geïnstalleerd en geconfigureerd voor gebruik met uw account.</span><span class="sxs-lookup"><span data-stu-id="307c9-185">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="307c9-186">Klik op de **Try it** knop in het script dat volgt, waardoor een Cloud-Shell waarmee u zich aanmeldt bij uw Azure-account met aanmelden kunnen.</span><span class="sxs-lookup"><span data-stu-id="307c9-186">Click the **Try it** button in the script that follows, which invokes a Cloud Shell that logs you can log in to your Azure account with.</span></span> <span data-ttu-id="307c9-187">Voor het uitvoeren van het script, klikt u op de **kopie** knop en plak de inhoud in uw Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="307c9-187">To execute the script, click the **Copy** button and paste the contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="307c9-188">Een resourcegroep en twee virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="307c9-189">Een virtueel netwerk peering tussen de twee virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-189">Create a virtual network peering between the two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get the id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 to VNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="307c9-190">Nadat het script wordt uitgevoerd, Controleer de peerings voor elke virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="307c9-190">After the script executes, review the peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="307c9-191">Voer de vorige opdracht opnieuw, vervangen *myVnet1* met *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="307c9-191">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="307c9-192">De uitvoer van beide opdrachten toont **verbonden** in de **PeeringState** kolom.</span><span class="sxs-lookup"><span data-stu-id="307c9-192">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>

     <span data-ttu-id="307c9-193">Alle Azure-resources die in een virtueel netwerk hebt u zich nu met elkaar communiceren via hun IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="307c9-193">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="307c9-194">Als u van standaard Azure-naamomzetting voor de virtuele netwerken gebruikmaakt, zich de resources in de virtuele netwerken niet voor de naamomzetting tussen de virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="307c9-194">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="307c9-195">Als u wilt voor het omzetten van namen over virtuele netwerken in een peering, moet u uw eigen DNS-server maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-195">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="307c9-196">Meer informatie over het instellen van [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="307c9-196">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="307c9-197">**Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine op een andere, te valideren.</span><span class="sxs-lookup"><span data-stu-id="307c9-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
5. <span data-ttu-id="307c9-198">**Optionele**: voor het verwijderen van de resources die u in deze zelfstudie maakt, voert u de stappen in [resources verwijderen](#delete-cli) in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="307c9-198">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="307c9-199"><a name="powershell"></a>Maken van de peering - PowerShell</span><span class="sxs-lookup"><span data-stu-id="307c9-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="307c9-200">Installeer de meest recente versie van de PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/)-module.</span><span class="sxs-lookup"><span data-stu-id="307c9-200">Install the latest version of the PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="307c9-201">Zie [Overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) als u nog geen ervaring hebt met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="307c9-201">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="307c9-202">Als u een PowerShell-sessie wilt starten, gaat u naar **Start**, voert u **powershell** in en klikt u vervolgens op **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="307c9-202">To start a PowerShell session, go to **Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="307c9-203">Meld u in PowerShell aan bij Azure door het commando `login-azurermaccount` in te voeren.</span><span class="sxs-lookup"><span data-stu-id="307c9-203">In PowerShell, log in to Azure by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="307c9-204">Het account dat u zich met aanmeldt moet hebben de vereiste machtigingen om de peering van een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-204">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="307c9-205">Zie de [machtigingen](#permissions) sectie van dit artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="307c9-205">See the [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="307c9-206">Een resourcegroep en twee virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="307c9-207">Kopieer het volgende script voor het uitvoeren van het script, plak deze in PowerShell en druk vervolgens op `Enter` nadat de laatste regel wordt weergegeven op het scherm:</span><span class="sxs-lookup"><span data-stu-id="307c9-207">To execute the script, copy the following script, paste it into PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>

    ```powershell
    # Variables for common values used throughout the script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="307c9-208">Een virtueel netwerk peering tussen de twee virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-208">Create a virtual network peering between the two virtual networks.</span></span> <span data-ttu-id="307c9-209">Het volgende script kopiëren, plakken PowerShell en druk vervolgens op `Enter` nadat de laatste regel wordt weergegeven op het scherm:</span><span class="sxs-lookup"><span data-stu-id="307c9-209">Copy the following script, paste in to PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>
    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 to VNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="307c9-210">Als u wilt controleren van de subnetten voor het virtuele netwerk, Kopieer de volgende opdracht, plakken PowerShell en druk vervolgens op `Enter`:</span><span class="sxs-lookup"><span data-stu-id="307c9-210">To review the subnets for the virtual network, copy the following command, paste in to PowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="307c9-211">Voer de vorige opdracht opnieuw, vervangen *myVnet1* met *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="307c9-211">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="307c9-212">De uitvoer van beide opdrachten toont **verbonden** in de **PeeringState** kolom.</span><span class="sxs-lookup"><span data-stu-id="307c9-212">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>
7. <span data-ttu-id="307c9-213">**Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine op een andere, te valideren.</span><span class="sxs-lookup"><span data-stu-id="307c9-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
8. <span data-ttu-id="307c9-214">**Optionele**: voor het verwijderen van de resources die u in deze zelfstudie maakt, voert u de stappen in [resources verwijderen](#delete-powershell) in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="307c9-214">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="307c9-215">Alle Azure-resources die in een virtueel netwerk hebt u zich nu met elkaar communiceren via hun IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="307c9-215">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="307c9-216">Als u van standaard Azure-naamomzetting voor de virtuele netwerken gebruikmaakt, zich de resources in de virtuele netwerken niet voor de naamomzetting tussen de virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="307c9-216">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="307c9-217">Als u wilt voor het omzetten van namen over virtuele netwerken in een peering, moet u uw eigen DNS-server maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-217">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="307c9-218">Meer informatie over het instellen van [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="307c9-218">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="307c9-219"><a name="template"></a>Maken van de peering - Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="307c9-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="307c9-220">Verwijzing [peering van een virtueel netwerk maken](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="307c9-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="307c9-221">Bij de sjabloon worden instructies geleverd voor de implementatie van de sjabloon via Azure Portal, PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="307c9-221">Instructions are provided with the template for deploying the template using the Azure portal, PowerShell, or the Azure CLI.</span></span> <span data-ttu-id="307c9-222">Meld u aan op afhankelijk van wat u hulpprogramma kiezen voor het implementeren van de sjabloon met met een account dat de vereiste machtigingen heeft voor de peering van een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="307c9-222">Log in to whichever tool you choose to deploy the template with using an account that has the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="307c9-223">Zie de [machtigingen](#permissions) sectie van dit artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="307c9-223">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="307c9-224">**Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine op een andere, te valideren.</span><span class="sxs-lookup"><span data-stu-id="307c9-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
3. <span data-ttu-id="307c9-225">**Optionele**: voor het verwijderen van de resources die u in deze zelfstudie maakt, voert u de stappen in de [resources verwijderen](#delete) sectie van dit artikel, met behulp van de Azure-portal, PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="307c9-225">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete) section of this article, using either the Azure portal, PowerShell, or the Azure CLI.</span></span>

## <span data-ttu-id="307c9-226"><a name="permissions"></a>Machtigingen</span><span class="sxs-lookup"><span data-stu-id="307c9-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="307c9-227">De accounts die u gebruikt voor het maken van een virtueel netwerk peering moeten de benodigde rol of machtiging hebben.</span><span class="sxs-lookup"><span data-stu-id="307c9-227">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="307c9-228">Bijvoorbeeld, als u twee virtuele netwerken met de naam VNet1 en VNet2 zijn peering, uw account moet worden toegewezen aan de volgende minimale rol of machtiging voor elke virtuele netwerk:</span><span class="sxs-lookup"><span data-stu-id="307c9-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="307c9-229">Virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="307c9-229">Virtual network</span></span>|<span data-ttu-id="307c9-230">Rol</span><span class="sxs-lookup"><span data-stu-id="307c9-230">Role</span></span>|<span data-ttu-id="307c9-231">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="307c9-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="307c9-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="307c9-232">VNet1</span></span>|[<span data-ttu-id="307c9-233">Inzender voor netwerken</span><span class="sxs-lookup"><span data-stu-id="307c9-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="307c9-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="307c9-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="307c9-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="307c9-235">VNet2</span></span>|[<span data-ttu-id="307c9-236">Inzender voor netwerken</span><span class="sxs-lookup"><span data-stu-id="307c9-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="307c9-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="307c9-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="307c9-238">Meer informatie over [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) en het toewijzen van specifieke machtigingen voor [aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (alleen voor Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="307c9-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="307c9-239"><a name="delete"></a>Resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="307c9-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="307c9-240">Wanneer u deze zelfstudie hebt voltooid, kunt u mogelijk wilt verwijderen van de resources die u hebt gemaakt in de zelfstudie, zodat u geen gebruik kosten.</span><span class="sxs-lookup"><span data-stu-id="307c9-240">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="307c9-241">Verwijderen van een resourcegroep, verwijdert tevens alle bronnen die zich in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="307c9-241">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="307c9-242"><a name="delete-portal"></a>Azure-portal</span><span class="sxs-lookup"><span data-stu-id="307c9-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="307c9-243">Voer in het zoekvak portal **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="307c9-243">In the portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="307c9-244">Klik in de zoekresultaten op **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="307c9-244">In the search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="307c9-245">Op de **myResourceGroup** blade, klikt u op de **verwijderen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="307c9-245">On the **myResourceGroup** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="307c9-246">Het verwijderen te bevestigen, in de **TYPE de naam van een RESOURCEGROEP** Voer **myResourceGroup**, en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="307c9-246">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="307c9-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="307c9-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="307c9-248">Voer de volgende opdracht in:</span><span class="sxs-lookup"><span data-stu-id="307c9-248">Enter the following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="307c9-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="307c9-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="307c9-250">Voer de volgende opdracht in:</span><span class="sxs-lookup"><span data-stu-id="307c9-250">Enter the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="307c9-251">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="307c9-251">Next steps</span></span>

- <span data-ttu-id="307c9-252">Grondig raken met belangrijke [peering beperkingen virtueel netwerk en het gedrag](virtual-network-manage-peering.md#requirements-and-constraints) voordat het maken van een virtueel netwerk voor productie-peering gebruikt.</span><span class="sxs-lookup"><span data-stu-id="307c9-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="307c9-253">Meer informatie over alle [peering virtuele netwerkinstellingen](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="307c9-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="307c9-254">Meer informatie over hoe [maken van een hub en spaak netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) met het virtuele netwerk peering.</span><span class="sxs-lookup"><span data-stu-id="307c9-254">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
