---
title: een Azure-netwerk (klassiek) met meerdere subnetten aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk (klassiek) met meerdere subnetten in Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="8bb3b-103">Een virtueel netwerk (klassiek) maken met meerdere subnetten</span><span class="sxs-lookup"><span data-stu-id="8bb3b-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8bb3b-104">Azure heeft twee [verschillende implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) voor het maken en werken met resources: Resource Manager en classic.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="8bb3b-105">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="8bb3b-106">Microsoft raadt u aan het maken van de meeste nieuwe virtuele netwerken via Hallo [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="8bb3b-107">Informatie over hoe toocreate een eenvoudige Azure-netwerk (klassiek) dat is gescheiden openbare en particuliere subnetten in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="8bb3b-108">U kunt Azure-resources, zoals virtuele machines en cloudservices in een subnet maken.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="8bb3b-109">Resources die zijn gemaakt in virtuele netwerken (klassiek) kunnen communiceren met elkaar en met resources in andere netwerken verbonden tooa virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="8bb3b-110">Meer informatie over alle [virtueel netwerk](virtual-network-manage-network.md) en [subnet](virtual-network-manage-subnet.md) instellingen.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="8bb3b-111">Virtuele netwerken (klassiek), worden onmiddellijk verwijderd door Azure wanneer een [abonnement is uitgeschakeld](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="8bb3b-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="8bb3b-112">Virtuele netwerken (klassiek) verwijderd, ongeacht of de bronnen in het virtuele netwerk Hallo bestaan.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="8bb3b-113">Als u later Hallo abonnement opnieuw inschakelt, resources die beschikbaar in het virtuele netwerk Hallo waren moeten opnieuw worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="8bb3b-114">U kunt een virtueel netwerk (klassiek) maken met behulp van Hallo [Azure-portal](#portal), Hallo [Azure-opdrachtregelinterface (CLI) 1.0](#azure-cli), of [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="8bb3b-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="8bb3b-115">Portal</span><span class="sxs-lookup"><span data-stu-id="8bb3b-115">Portal</span></span>

1. <span data-ttu-id="8bb3b-116">Ga in een internetbrowser toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8bb3b-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8bb3b-117">Meld u aan met uw [Azure-account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="8bb3b-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="8bb3b-118">Als u geen Azure-account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="8bb3b-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="8bb3b-119">Klik op **+ nieuw** in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="8bb3b-120">Voer *virtueel netwerk* in Hallo **zoeken Hallo Marketplace** vak bovenaan Hallo Hallo **nieuw** blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="8bb3b-121">Klik op **virtueel netwerk** wanneer deze wordt weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="8bb3b-122">Selecteer **klassieke** in Hallo **een implementatiemodel selecteren** vak Hallo **virtueel netwerk** blade die wordt weergegeven, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="8bb3b-123">Voer de volgende waarden op Hallo Hallo **virtueel netwerk maken (klassiek)** blade en klik vervolgens op **maken**:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="8bb3b-124">Instelling</span><span class="sxs-lookup"><span data-stu-id="8bb3b-124">Setting</span></span>|<span data-ttu-id="8bb3b-125">Waarde</span><span class="sxs-lookup"><span data-stu-id="8bb3b-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="8bb3b-126">Naam</span><span class="sxs-lookup"><span data-stu-id="8bb3b-126">Name</span></span>|<span data-ttu-id="8bb3b-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="8bb3b-127">myVnet</span></span>|
    |<span data-ttu-id="8bb3b-128">Adresruimte</span><span class="sxs-lookup"><span data-stu-id="8bb3b-128">Address space</span></span>|<span data-ttu-id="8bb3b-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="8bb3b-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="8bb3b-130">Subnetnaam</span><span class="sxs-lookup"><span data-stu-id="8bb3b-130">Subnet name</span></span>|<span data-ttu-id="8bb3b-131">Openbaar</span><span class="sxs-lookup"><span data-stu-id="8bb3b-131">Public</span></span>|
    |<span data-ttu-id="8bb3b-132">Subnetadresbereik</span><span class="sxs-lookup"><span data-stu-id="8bb3b-132">Subnet address range</span></span>|<span data-ttu-id="8bb3b-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="8bb3b-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="8bb3b-134">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="8bb3b-134">Resource group</span></span>|<span data-ttu-id="8bb3b-135">Laat **nieuw** geselecteerd en voer vervolgens **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="8bb3b-136">Abonnement en de locatie</span><span class="sxs-lookup"><span data-stu-id="8bb3b-136">Subscription and location</span></span>|<span data-ttu-id="8bb3b-137">Selecteer uw abonnement en locatie.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-137">Select your subscription and location.</span></span>

    <span data-ttu-id="8bb3b-138">Als u nieuwe tooAzure, meer informatie over [resourcegroepen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnementen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), en [locaties](https://azure.microsoft.com/regions) (ook wel aangeduid tooas *regio's*).</span><span class="sxs-lookup"><span data-stu-id="8bb3b-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="8bb3b-139">U kunt in Hallo-portal slechts één subnet maken wanneer u een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="8bb3b-140">In deze zelfstudie maakt u een tweede subnet nadat u Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="8bb3b-141">U kunt later Internet toegankelijke resources maken in Hallo **openbare** subnet.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="8bb3b-142">U bronnen die niet toegankelijk is vanaf Internet Hallo in Hallo ook mogelijk maken **persoonlijke** subnet.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="8bb3b-143">toocreate Hallo tweede subnet, voer **myVnet** in Hallo **zoeken bronnen** vak bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="8bb3b-144">Klik op **myVnet** wanneer deze wordt weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="8bb3b-145">Klik op **subnetten** (in Hallo **instellingen** sectie) op Hallo **virtueel netwerk maken (klassiek)** blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="8bb3b-146">Klik op **+ toevoegen** op Hallo **myVnet - subnetten** blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="8bb3b-147">Voer **persoonlijke** voor **naam** op Hallo **subnet toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="8bb3b-148">Voer **10.0.1.0/24** voor **-adresbereik**.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="8bb3b-149">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-149">Click **OK**.</span></span>
8. <span data-ttu-id="8bb3b-150">Op Hallo **myVnet - subnetten** blade ziet u Hallo **openbare** en **persoonlijke** subnetten die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="8bb3b-151">**Optionele**: als u deze zelfstudie hebt voltooid, kunt u toodelete Hallo resources die u hebt gemaakt, zodat u geen gebruik kosten:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="8bb3b-152">Klik op **overzicht** op Hallo **myVnet** blade.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="8bb3b-153">Klik op Hallo **verwijderen** pictogram op Hallo **myVnet** blade.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="8bb3b-154">tooconfirm hello verwijdering, klikt u op **Ja** in Hallo **virtuele netwerk verwijderen** vak.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="8bb3b-155">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8bb3b-155">Azure CLI</span></span>

1. <span data-ttu-id="8bb3b-156">U kunt ofwel [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), of gebruik Hallo CLI binnen hello Azure Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="8bb3b-157">Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="8bb3b-158">Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="8bb3b-159">tooget help voor CLI-opdrachten, typ `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="8bb3b-160">Aanmelden tooAzure met Hallo-opdracht die volgt op in een sessie CLI.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="8bb3b-161">Als u op **Try it** in Hallo vak hieronder een Cloud-Shell wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="8bb3b-162">U kunt tooyour Azure-abonnement, aanmelden zonder in te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="8bb3b-163">tooensure hello CLI is in Service Management-modus, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="8bb3b-164">Een virtueel netwerk maken met een particulier subnet:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="8bb3b-165">Maak een openbare subnet binnen het virtuele netwerk Hallo:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="8bb3b-166">Hallo virtueel netwerk en subnetten bekijken:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="8bb3b-167">**Optionele**: U kunt toodelete Hallo resources die u hebt gemaakt wanneer u klaar bent met deze zelfstudie, zodat u geen gebruik kosten:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="8bb3b-168">Hoewel u niet een resource groep toocreate een virtueel netwerk (klassiek) opgeven in met behulp van Hallo CLI, Azure Hallo virtueel netwerk maakt in een resourcegroep met de naam *standaard netwerken*.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="8bb3b-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bb3b-169">PowerShell</span></span>

1. <span data-ttu-id="8bb3b-170">Installeer de meest recente versie Hallo Hallo PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="8bb3b-171">Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8bb3b-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="8bb3b-172">Een PowerShell-sessie starten.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="8bb3b-173">In PowerShell aanmelden tooAzure hiertoe Hallo `Add-AzureAccount` opdracht.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="8bb3b-174">Wijzig de volgende Hallo pad en bestandsnaam naar gelang van toepassing, vervolgens uw bestaande netwerk-configuratiebestand exporteren:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="8bb3b-175">toocreate een virtueel netwerk met openbare en particuliere subnetten, gebruiken alle tekst editor tooadd hello **VirtualNetworkSite** element zijn dat toohello netwerk configuratiebestand volgt.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="8bb3b-176">Bekijk Hallo volledige [network-configuratieschema bestand](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="8bb3b-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="8bb3b-177">Hallo netwerk-configuratiebestand importeren:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="8bb3b-178">Een configuratiebestand gewijzigde netwerk importeren kan leiden tot wijzigingen tooexisting virtuele netwerken (klassiek) in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="8bb3b-179">Zorg ervoor dat u alleen Hallo vorige virtueel netwerk toevoegen en u niet wijzigen of verwijderen van een bestaande virtuele netwerken uit uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="8bb3b-180">Hallo virtueel netwerk en subnetten bekijken:</span><span class="sxs-lookup"><span data-stu-id="8bb3b-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="8bb3b-181">**Optionele**: U kunt toodelete Hallo resources die u hebt gemaakt wanneer u klaar bent met deze zelfstudie, zodat u geen gebruik kosten.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="8bb3b-182">toodelete hello virtueel netwerk, volledige stap 4-6 opnieuw, deze tijd verwijderen Hallo **VirtualNetworkSite** element dat u in stap 5 hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="8bb3b-183">Hoewel u niet een resource groep toocreate een virtueel netwerk (klassiek) opgeven in met behulp van PowerShell, Azure Hallo virtueel netwerk maakt in een resourcegroep met de naam *standaard netwerken*.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="8bb3b-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8bb3b-184">Next steps</span></span>

- <span data-ttu-id="8bb3b-185">toolearn over alle virtueel netwerk en subnetinstellingen, Zie [virtuele netwerken beheren](virtual-network-manage-network.md) en [beheren van virtueel netwerksubnetten](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="8bb3b-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="8bb3b-186">U beschikt over verschillende opties voor het gebruik van virtuele netwerken en subnetten in een productie-omgeving toomeet verschillende vereisten.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="8bb3b-187">toofilter binnenkomend en uitgaand verkeer van de subnetten, maken en toepassen van [netwerkbeveiligingsgroepen](virtual-networks-nsg.md) toosubnets.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="8bb3b-188">Maak een [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of een [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtuele machine en sluit vervolgens tooan bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="8bb3b-189">tooconnect twee virtuele netwerken in dezelfde Azure-locatie hello, maakt u een [virtueel netwerk peering](create-peering-different-deployment-models.md) tussen Hallo virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="8bb3b-190">U kunt een virtueel netwerk (Resource Manager) tooa virtueel netwerk (klassiek) peer, maar u een peering tussen twee virtuele netwerken (klassiek) niet maken.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="8bb3b-191">Hallo virtueel netwerk tooan on-premises netwerk verbinding via een [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span><span class="sxs-lookup"><span data-stu-id="8bb3b-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
