---
title: een virtuele Azure-netwerk peering - aaaCreate Resource Manager - hetzelfde abonnement | Microsoft Docs
description: Meer informatie over hoe toocreate via de Resource-Manager die aanwezig zijn in Hallo dezelfde een virtueel netwerk peering tussen virtuele netwerken gemaakt Azure-abonnement.
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
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="57676-103">Maak een virtueel netwerk peering - Resource Manager, hetzelfde abonnement</span><span class="sxs-lookup"><span data-stu-id="57676-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="57676-104">In deze zelfstudie leert u toocreate een virtueel netwerk tussen virtuele netwerken die zijn gemaakt via Resource Manager-peering.</span><span class="sxs-lookup"><span data-stu-id="57676-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="57676-105">Beide virtuele netwerken bestaan in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="57676-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="57676-106">Peering twee virtuele netwerken kunnen resources in verschillende virtuele netwerken toocommunicate met elkaar met dezelfde bandbreedte en latentie Hallo alsof Hallo resources in Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="57676-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="57676-107">Meer informatie over [virtuele netwerk peering](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57676-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="57676-108">Hallo stappen toocreate een virtueel netwerk peering zijn verschillend, afhankelijk van of Hallo virtuele netwerken in Hallo dezelfde of verschillende, abonnementen en die zijn [Azure implementatiemodel](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Hallo virtuele netwerken worden gemaakt via.</span><span class="sxs-lookup"><span data-stu-id="57676-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="57676-109">Meer informatie over hoe toocreate een virtueel netwerk door te klikken op Hallo scenario uit de volgende tabel Hallo-peering in andere scenario's:</span><span class="sxs-lookup"><span data-stu-id="57676-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="57676-110">Azure-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="57676-110">Azure deployment model</span></span>  | <span data-ttu-id="57676-111">Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="57676-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="57676-112">Beide Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57676-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="57676-113">Andere</span><span class="sxs-lookup"><span data-stu-id="57676-113">Different</span></span>|
|[<span data-ttu-id="57676-114">Een Resource Manager, een klassiek</span><span class="sxs-lookup"><span data-stu-id="57676-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="57676-115">Dezelfde</span><span class="sxs-lookup"><span data-stu-id="57676-115">Same</span></span>|
|[<span data-ttu-id="57676-116">Een Resource Manager, een klassiek</span><span class="sxs-lookup"><span data-stu-id="57676-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="57676-117">Andere</span><span class="sxs-lookup"><span data-stu-id="57676-117">Different</span></span>|

<span data-ttu-id="57676-118">Een virtueel netwerk peering kan niet worden gemaakt tussen twee virtuele netwerken die zijn geïmplementeerd via Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="57676-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="57676-119">Een virtueel netwerk peering kan alleen worden gemaakt tussen twee virtuele netwerken die bestaan in Hallo dezelfde Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="57676-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="57676-120">Als u tooconnect virtuele netwerken die zijn beide gemaakt via de klassieke implementatiemodel hello, of die zijn opgenomen in verschillende Azure-regio's nodig hebt, kunt u een Azure [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hallo virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="57676-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="57676-121">U kunt Hallo [Azure-portal](#portal), hello Azure [opdrachtregelinterface](#cli) (CLI) Azure [PowerShell](#powershell), of een [Azure Resource Manager-sjabloon](#template) toocreate peering van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="57676-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="57676-122">Klik op Hallo vorige hulpprogramma koppelingen toogo direct toohello stappen voor het maken van een virtueel netwerk peering met behulp van het hulpprogramma naar keuze.</span><span class="sxs-lookup"><span data-stu-id="57676-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="57676-123"><a name="portal"></a>Maken van de peering - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="57676-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="57676-124">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="57676-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="57676-125">Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering.</span><span class="sxs-lookup"><span data-stu-id="57676-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="57676-126">Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="57676-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="57676-127">Klik op **+ nieuw**, klikt u op **Networking**, klikt u vervolgens op **virtueel netwerk**.</span><span class="sxs-lookup"><span data-stu-id="57676-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="57676-128">In Hallo **virtueel netwerk maken** blade invoert, of Selecteer waarden voor Hallo na instellingen en klik vervolgens op **maken**:</span><span class="sxs-lookup"><span data-stu-id="57676-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="57676-129">**Naam**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="57676-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="57676-130">**Adresruimte**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="57676-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="57676-131">**Subnetnaam**: *standaard*</span><span class="sxs-lookup"><span data-stu-id="57676-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="57676-132">**Subnet-adresbereik**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="57676-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="57676-133">**Abonnement**: uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="57676-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="57676-134">**Resourcegroep**: Selecteer **nieuw** en voer *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="57676-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="57676-135">**Locatie**: *VS-Oost*</span><span class="sxs-lookup"><span data-stu-id="57676-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="57676-136">Voer de stappen 2-3 opnieuw geven Hallo volgende waarden in stap 3:</span><span class="sxs-lookup"><span data-stu-id="57676-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="57676-137">**Naam**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="57676-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="57676-138">**Adresruimte**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="57676-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="57676-139">**Subnetnaam**: *standaard*</span><span class="sxs-lookup"><span data-stu-id="57676-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="57676-140">**Subnet-adresbereik**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="57676-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="57676-141">**Abonnement**: uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="57676-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="57676-142">**Resourcegroep**: Selecteer **gebruik bestaande** en selecteer *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="57676-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="57676-143">**Locatie**: *VS-Oost*</span><span class="sxs-lookup"><span data-stu-id="57676-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="57676-144">In Hallo **zoeken bronnen** vak Hallo boven aan het Hallo-portal, type *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="57676-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="57676-145">Klik op **myResourceGroup** wanneer deze wordt weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="57676-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="57676-146">Een blade wordt weergegeven voor Hallo **myresourcegroup** resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="57676-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="57676-147">Hallo resourcegroep bevat Hallo twee virtuele netwerken in de vorige stappen hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="57676-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="57676-148">Klik op **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="57676-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="57676-149">In Hallo **myVnet1** blade die wordt weergegeven, klikt u op **Peerings** uit Hallo verticale lijst met opties op de linkerkant van de blade Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="57676-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="57676-150">In Hallo **myVnet1 - Peerings** blade die werden weergegeven, klikt u op **+ toevoegen**</span><span class="sxs-lookup"><span data-stu-id="57676-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="57676-151">In Hallo **toevoegen peering** blade die wordt weergegeven, invoeren, of selecteer Hallo volgend opties en klik vervolgens op **OK**:</span><span class="sxs-lookup"><span data-stu-id="57676-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="57676-152">**Naam**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="57676-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="57676-153">**Virtueel netwerk implementatiemodel**: Selecteer **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="57676-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="57676-154">**Abonnement**: uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="57676-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="57676-155">**Virtueel netwerk**: klik op **Kies een virtueel netwerk**, klikt u vervolgens op **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="57676-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="57676-156">**Toestaan van toegang tot het virtuele netwerk:** ervoor te zorgen dat **ingeschakeld** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="57676-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="57676-157">Er zijn geen andere instellingen worden gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="57676-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="57676-158">toolearn over alle peering instellingen lezen [beheren van virtueel netwerk peerings](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="57676-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="57676-159">Wanneer u op **OK** in de vorige stap Hallo Hallo **toevoegen peering** blade wordt gesloten en u ziet Hallo **myVnet1 - Peerings** blade opnieuw.</span><span class="sxs-lookup"><span data-stu-id="57676-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="57676-160">Na enkele seconden verschijnt Hallo peering u hebt gemaakt in Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="57676-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="57676-161">**Geïnitieerd** wordt vermeld in Hallo **PEERING STATUS** kolom voor Hallo **myVnet1ToMyVnet2** peering u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="57676-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="57676-162">U hebt ingesteld als peer Vnet1 tooVnet2, maar u moet nu myVnet2 toomyVnet1 peer.</span><span class="sxs-lookup"><span data-stu-id="57676-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="57676-163">Hallo peering moet worden gemaakt in beide richtingen tooenable bronnen in Hallo virtuele netwerken toocommunicate met elkaar.</span><span class="sxs-lookup"><span data-stu-id="57676-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="57676-164">Herhaal stap 5-10 nogmaals voor myVnet2.</span><span class="sxs-lookup"><span data-stu-id="57676-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="57676-165">Naam Hallo peering *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="57676-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="57676-166">Een paar seconden na het klikken op **OK** toocreate Hallo-peering voor MyVnet2, hello **myVnet2ToMyVnet1** peering u zojuist hebt gemaakt wordt vermeld met **verbonden** in Hallo  **STATUS van de PEERING** kolom.</span><span class="sxs-lookup"><span data-stu-id="57676-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="57676-167">Stap 5-7 opnieuw uitvoeren voor MyVnet1.</span><span class="sxs-lookup"><span data-stu-id="57676-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="57676-168">Hallo **PEERING STATUS** voor Hallo **myVnet1ToVNet2** peering is nu er ook **verbonden**.</span><span class="sxs-lookup"><span data-stu-id="57676-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="57676-169">Hallo-peering is tot stand gebracht nadat er **verbonden** in Hallo **PEERING STATUS** kolom voor beide virtuele netwerken in het Hallo-peering.</span><span class="sxs-lookup"><span data-stu-id="57676-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="57676-170">**Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="57676-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="57676-171">**Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, stappen voor voltooid Hallo Hallo [resources verwijderen](#delete-portal) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="57676-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="57676-172">Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="57676-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="57676-173">Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="57676-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="57676-174">Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken.</span><span class="sxs-lookup"><span data-stu-id="57676-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="57676-175">Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="57676-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="57676-176"><a name="cli"></a>Peering - maken Azure CLI</span><span class="sxs-lookup"><span data-stu-id="57676-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="57676-177">Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="57676-177">hello following script:</span></span>

- <span data-ttu-id="57676-178">Hello Azure CLI versie 2.0.4 vereist of hoger.</span><span class="sxs-lookup"><span data-stu-id="57676-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="57676-179">toofind hello versie, Voer Hallo `az --version` opdracht.</span><span class="sxs-lookup"><span data-stu-id="57676-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="57676-180">Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="57676-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="57676-181">Werkt in een Bash-shell.</span><span class="sxs-lookup"><span data-stu-id="57676-181">Works in a Bash shell.</span></span> <span data-ttu-id="57676-182">Zie voor opties op Azure CLI-scripts die worden uitgevoerd op Windows-client [hello Azure CLI uitvoeren in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="57676-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="57676-183">U kunt in plaats van installatie Hallo CLI en de bijbehorende afhankelijkheden, hello Azure Cloud Shell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="57676-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="57676-184">Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="57676-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="57676-185">Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft.</span><span class="sxs-lookup"><span data-stu-id="57676-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="57676-186">Klik op Hallo **Try it** knop in Hallo-script dat volgt, waardoor een Cloud-Shell waarmee u zich aanmeldt tooyour kunnen aanmelden met Azure-account.</span><span class="sxs-lookup"><span data-stu-id="57676-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="57676-187">tooexecute Hallo script, klikt u op Hallo **kopie** knop en plak Hallo inhoud in uw Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="57676-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="57676-188">Een resourcegroep en twee virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="57676-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
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

2. <span data-ttu-id="57676-189">Maak een virtueel netwerk tussen de twee virtuele netwerken Hallo-peering.</span><span class="sxs-lookup"><span data-stu-id="57676-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="57676-190">Na het Hallo-script wordt uitgevoerd, controleert u Hallo peerings voor elke virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="57676-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="57676-191">Voer de vorige opdracht Hallo opnieuw, vervangen *myVnet1* met *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="57676-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="57676-192">Hallo-uitvoer van beide opdrachten toont **verbonden** in Hallo **PeeringState** kolom.</span><span class="sxs-lookup"><span data-stu-id="57676-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="57676-193">Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="57676-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="57676-194">Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="57676-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="57676-195">Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken.</span><span class="sxs-lookup"><span data-stu-id="57676-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="57676-196">Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="57676-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="57676-197">**Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="57676-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="57676-198">**Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-cli) in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="57676-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="57676-199"><a name="powershell"></a>Maken van de peering - PowerShell</span><span class="sxs-lookup"><span data-stu-id="57676-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="57676-200">Installeer de meest recente versie Hallo Hallo PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span><span class="sxs-lookup"><span data-stu-id="57676-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="57676-201">Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="57676-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="57676-202">toostart een PowerShell-sessie te gaan**Start**, voer **powershell**, en klik vervolgens op **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="57676-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="57676-203">In PowerShell aanmelden tooAzure hiertoe Hallo `login-azurermaccount` opdracht.</span><span class="sxs-lookup"><span data-stu-id="57676-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="57676-204">Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering.</span><span class="sxs-lookup"><span data-stu-id="57676-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="57676-205">Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="57676-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="57676-206">Een resourcegroep en twee virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="57676-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="57676-207">tooexecute hello script kopiëren Hallo volgende script, plakt u deze in PowerShell en druk vervolgens op `Enter` nadat de laatste regel hello wordt weergegeven op het welkomstscherm:</span><span class="sxs-lookup"><span data-stu-id="57676-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
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

5. <span data-ttu-id="57676-208">Maak een virtueel netwerk tussen de twee virtuele netwerken Hallo-peering.</span><span class="sxs-lookup"><span data-stu-id="57676-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="57676-209">Kopiëren Hallo volgende script, plak in tooPowerShell en druk vervolgens op `Enter` nadat de laatste regel hello wordt weergegeven op het welkomstscherm:</span><span class="sxs-lookup"><span data-stu-id="57676-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="57676-210">tooreview hello subnetten voor het virtuele netwerk hello, kopie Hallo volgende opdracht, plak in tooPowerShell en druk vervolgens op `Enter`:</span><span class="sxs-lookup"><span data-stu-id="57676-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="57676-211">Voer de vorige opdracht Hallo opnieuw, vervangen *myVnet1* met *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="57676-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="57676-212">Hallo-uitvoer van beide opdrachten toont **verbonden** in Hallo **PeeringState** kolom.</span><span class="sxs-lookup"><span data-stu-id="57676-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="57676-213">**Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="57676-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="57676-214">**Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-powershell) in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="57676-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="57676-215">Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="57676-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="57676-216">Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="57676-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="57676-217">Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken.</span><span class="sxs-lookup"><span data-stu-id="57676-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="57676-218">Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="57676-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="57676-219"><a name="template"></a>Maken van de peering - Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="57676-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="57676-220">Verwijzing [peering van een virtueel netwerk maken](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="57676-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="57676-221">Instructies zijn opgegeven door Hallo-sjabloon voor het Hallo-sjabloon implementeren met behulp van hello Azure-portal, PowerShell of hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="57676-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="57676-222">Aanmelden toowhichever hulpprogramma u toodeploy Hallo sjabloon met het gebruik van een account met kiest Hallo noodzakelijke machtigingen toocreate peering van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="57676-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="57676-223">Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="57676-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="57676-224">**Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="57676-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="57676-225">**Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, stappen voor voltooid Hallo Hallo [resources verwijderen](#delete) sectie van dit artikel, met een Azure-portal, PowerShell of Azure CLI Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="57676-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="57676-226"><a name="permissions"></a>Machtigingen</span><span class="sxs-lookup"><span data-stu-id="57676-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="57676-227">Hallo-accounts gebruiken van een virtueel netwerk peering toocreate beschikken Hallo benodigde rol of machtigingen.</span><span class="sxs-lookup"><span data-stu-id="57676-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="57676-228">Bijvoorbeeld, als u twee virtuele netwerken met de naam VNet1 en VNet2 zijn peering, moet uw account worden toegewezen Hallo minimale rol of machtiging voor elke virtuele netwerk te volgen:</span><span class="sxs-lookup"><span data-stu-id="57676-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="57676-229">Virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="57676-229">Virtual network</span></span>|<span data-ttu-id="57676-230">Rol</span><span class="sxs-lookup"><span data-stu-id="57676-230">Role</span></span>|<span data-ttu-id="57676-231">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="57676-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="57676-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="57676-232">VNet1</span></span>|[<span data-ttu-id="57676-233">Inzender voor netwerken</span><span class="sxs-lookup"><span data-stu-id="57676-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="57676-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="57676-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="57676-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="57676-235">VNet2</span></span>|[<span data-ttu-id="57676-236">Inzender voor netwerken</span><span class="sxs-lookup"><span data-stu-id="57676-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="57676-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="57676-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="57676-238">Meer informatie over [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) en het toewijzen van specifieke machtigingen te[aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (alleen voor Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="57676-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="57676-239"><a name="delete"></a>Resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="57676-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="57676-240">Wanneer u deze zelfstudie hebt voltooid, kunt u toodelete Hallo resources die u hebt gemaakt in de zelfstudie hello, zodat u geen gebruik kosten.</span><span class="sxs-lookup"><span data-stu-id="57676-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="57676-241">Verwijderen van een resourcegroep, worden ook alle resources die in de resourcegroep Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="57676-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="57676-242"><a name="delete-portal"></a>Azure-portal</span><span class="sxs-lookup"><span data-stu-id="57676-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="57676-243">Voer in de portal zoekvak Hallo **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="57676-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="57676-244">Klik in de zoekresultaten Hallo **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="57676-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="57676-245">Op Hallo **myResourceGroup** blade, klikt u op Hallo **verwijderen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="57676-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="57676-246">tooconfirm hello wordt verwijderd, Hallo **TYPE Hallo RESOURCEGROEPNAAM** Voer **myResourceGroup**, en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="57676-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="57676-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="57676-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="57676-248">Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="57676-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="57676-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="57676-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="57676-250">Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="57676-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="57676-251">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="57676-251">Next steps</span></span>

- <span data-ttu-id="57676-252">Grondig raken met belangrijke [peering beperkingen virtueel netwerk en het gedrag](virtual-network-manage-peering.md#requirements-and-constraints) voordat het maken van een virtueel netwerk voor productie-peering gebruikt.</span><span class="sxs-lookup"><span data-stu-id="57676-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="57676-253">Meer informatie over alle [peering virtuele netwerkinstellingen](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="57676-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="57676-254">Meer informatie over hoe te[maken van een hub en spaak netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) met het virtuele netwerk peering.</span><span class="sxs-lookup"><span data-stu-id="57676-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
