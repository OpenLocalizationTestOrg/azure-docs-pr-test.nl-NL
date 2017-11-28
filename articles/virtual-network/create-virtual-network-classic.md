---
title: Een Azure-netwerk (klassiek) maken met meerdere subnetten | Microsoft Docs
description: Ontdek hoe u een virtueel netwerk (klassiek) maken met meerdere subnetten in Azure.
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
ms.openlocfilehash: 95c2f4fe40590a8d809f634fb5b2c92d07421bb0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="4c9f8-103">Een virtueel netwerk (klassiek) maken met meerdere subnetten</span><span class="sxs-lookup"><span data-stu-id="4c9f8-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c9f8-104">Azure heeft twee [verschillende implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) voor het maken en werken met resources: Resource Manager en classic.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="4c9f8-105">Dit artikel gaat over het gebruik van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="4c9f8-106">Microsoft raadt u aan het maken van de meeste nieuwe virtuele netwerken via de [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-106">Microsoft recommends creating most new virtual networks through the [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="4c9f8-107">Informatie over het maken van een eenvoudige Azure-netwerk (klassiek) met afzonderlijke openbare en particuliere subnetten in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-107">In this tutorial, learn how to create a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="4c9f8-108">U kunt Azure-resources, zoals virtuele machines en cloudservices in een subnet maken.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="4c9f8-109">Resources die zijn gemaakt in virtuele netwerken (klassiek) kunnen communiceren met elkaar en met resources in andere netwerken die zijn verbonden met een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected to a virtual network.</span></span>

<span data-ttu-id="4c9f8-110">Meer informatie over alle [virtueel netwerk](virtual-network-manage-network.md) en [subnet](virtual-network-manage-subnet.md) instellingen.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="4c9f8-111">Virtuele netwerken (klassiek), worden onmiddellijk verwijderd door Azure wanneer een [abonnement is uitgeschakeld](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="4c9f8-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="4c9f8-112">Virtuele netwerken (klassiek) verwijderd, ongeacht of de bronnen in het virtuele netwerk bestaan.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-112">Virtual networks (classic) are deleted regardless of whether resources exist in the virtual network.</span></span> <span data-ttu-id="4c9f8-113">Als u later het abonnement opnieuw inschakelt, resources die beschikbaar in het virtuele netwerk waren moeten opnieuw worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-113">If you later re-enable the subscription, resources that existed in the virtual network must be recreated.</span></span>

<span data-ttu-id="4c9f8-114">U een virtueel netwerk (klassiek) kunt maken met behulp van de [Azure-portal](#portal), wordt de [Azure-opdrachtregelinterface (CLI) 1.0](#azure-cli), of [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="4c9f8-114">You can create a virtual network (classic) by using the [Azure portal](#portal), the [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="4c9f8-115">Portal</span><span class="sxs-lookup"><span data-stu-id="4c9f8-115">Portal</span></span>

1. <span data-ttu-id="4c9f8-116">In een internetbrowser, gaat u naar de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c9f8-116">In an Internet browser, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4c9f8-117">Meld u aan met uw [Azure-account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="4c9f8-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="4c9f8-118">Als u geen Azure-account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="4c9f8-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="4c9f8-119">Klik op **+ nieuw** in de portal.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-119">Click **+New** in the portal.</span></span>
3. <span data-ttu-id="4c9f8-120">Voer *virtueel netwerk* in de **zoeken van de Marketplace** vak aan de bovenkant van de **nieuw** blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-120">Enter *Virtual network* in the **Search the Marketplace** box at the top of the **New** blade that appears.</span></span>  <span data-ttu-id="4c9f8-121">Klik op **virtueel netwerk** wanneer deze wordt weergegeven in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-121">Click **Virtual network** when it appears in the search results.</span></span>
4. <span data-ttu-id="4c9f8-122">Selecteer **klassieke** in de **een implementatiemodel selecteren** vak de **virtueel netwerk** blade die wordt weergegeven, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-122">Select **Classic** in the **Select a deployment model** box in the **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="4c9f8-123">Voer de volgende waarden op de **virtueel netwerk maken (klassiek)** blade en klik vervolgens op **maken**:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-123">Enter the following values on the **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="4c9f8-124">Instelling</span><span class="sxs-lookup"><span data-stu-id="4c9f8-124">Setting</span></span>|<span data-ttu-id="4c9f8-125">Waarde</span><span class="sxs-lookup"><span data-stu-id="4c9f8-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="4c9f8-126">Naam</span><span class="sxs-lookup"><span data-stu-id="4c9f8-126">Name</span></span>|<span data-ttu-id="4c9f8-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="4c9f8-127">myVnet</span></span>|
    |<span data-ttu-id="4c9f8-128">Adresruimte</span><span class="sxs-lookup"><span data-stu-id="4c9f8-128">Address space</span></span>|<span data-ttu-id="4c9f8-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4c9f8-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="4c9f8-130">Subnetnaam</span><span class="sxs-lookup"><span data-stu-id="4c9f8-130">Subnet name</span></span>|<span data-ttu-id="4c9f8-131">Openbaar</span><span class="sxs-lookup"><span data-stu-id="4c9f8-131">Public</span></span>|
    |<span data-ttu-id="4c9f8-132">Subnetadresbereik</span><span class="sxs-lookup"><span data-stu-id="4c9f8-132">Subnet address range</span></span>|<span data-ttu-id="4c9f8-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4c9f8-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="4c9f8-134">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="4c9f8-134">Resource group</span></span>|<span data-ttu-id="4c9f8-135">Laat **nieuw** geselecteerd en voer vervolgens **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="4c9f8-136">Abonnement en de locatie</span><span class="sxs-lookup"><span data-stu-id="4c9f8-136">Subscription and location</span></span>|<span data-ttu-id="4c9f8-137">Selecteer uw abonnement en locatie.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-137">Select your subscription and location.</span></span>

    <span data-ttu-id="4c9f8-138">Als u geen ervaring met Azure, meer informatie over [resourcegroepen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnementen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), en [locaties](https://azure.microsoft.com/regions) (ook wel *regio's*).</span><span class="sxs-lookup"><span data-stu-id="4c9f8-138">If you're new to Azure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred to as *regions*).</span></span>
4. <span data-ttu-id="4c9f8-139">U kunt slechts één subnet in de portal maken wanneer u een virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-139">In the portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="4c9f8-140">In deze zelfstudie maakt u een tweede subnet nadat u het virtuele netwerk hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-140">In this tutorial, you create a second subnet after you create the virtual network.</span></span> <span data-ttu-id="4c9f8-141">U kunt later maken met Internet toegankelijke bronnen in de **openbare** subnet.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-141">You might later create Internet-accessible resources in the **Public** subnet.</span></span> <span data-ttu-id="4c9f8-142">U bronnen die niet toegankelijk is vanaf het Internet in ook mogelijk maakt de **persoonlijke** subnet.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-142">You also might create resources that aren't accessible from the Internet in the **Private** subnet.</span></span> <span data-ttu-id="4c9f8-143">Voer voor het maken van het tweede subnet **myVnet** in de **zoeken bronnen** vak aan de bovenkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-143">To create the second subnet, enter **myVnet** in the **Search resources** box at the top of the page.</span></span> <span data-ttu-id="4c9f8-144">Klik op **myVnet** wanneer deze wordt weergegeven in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-144">Click **myVnet** when it appears in the search results.</span></span>
5. <span data-ttu-id="4c9f8-145">Klik op **subnetten** (in de **instellingen** sectie) op de **virtueel netwerk maken (klassiek)** blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-145">Click **Subnets** (in the **SETTINGS** section) on the **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="4c9f8-146">Klik op **+ toevoegen** op de **myVnet - subnetten** blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-146">Click **+Add** on the **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="4c9f8-147">Voer **persoonlijke** voor **naam** op de **subnet toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-147">Enter **Private** for **Name** on the **Add subnet** blade.</span></span> <span data-ttu-id="4c9f8-148">Voer **10.0.1.0/24** voor **-adresbereik**.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="4c9f8-149">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-149">Click **OK**.</span></span>
8. <span data-ttu-id="4c9f8-150">Op de **myVnet - subnetten** , ziet u de **openbare** en **persoonlijke** subnetten die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-150">On the **myVnet - Subnets** blade, you can see the **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="4c9f8-151">**Optionele**: wanneer u deze zelfstudie hebt voltooid, wilt u mogelijk de resources verwijderen die u hebt gemaakt, zodat u geen gebruik kosten:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-151">**Optional**: When you finish this tutorial, you might want to delete the resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="4c9f8-152">Klik op **overzicht** op de **myVnet** blade.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-152">Click **Overview** on the **myVnet** blade.</span></span>
    - <span data-ttu-id="4c9f8-153">Klik op de **verwijderen** pictogram op de **myVnet** blade.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-153">Click the **Delete** icon on the **myVnet** blade.</span></span>
    - <span data-ttu-id="4c9f8-154">Het verwijderen te bevestigen, klikt u op **Ja** in de **virtuele netwerk verwijderen** vak.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-154">To confirm the deletion, click **Yes** in the **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="4c9f8-155">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4c9f8-155">Azure CLI</span></span>

1. <span data-ttu-id="4c9f8-156">U kunt ofwel [installeren en configureren van de Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), of gebruik de CLI vanuit de Azure-Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-156">You can either [install and configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use the CLI within the Azure Cloud Shell.</span></span> <span data-ttu-id="4c9f8-157">De Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks in Azure Portal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-157">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="4c9f8-158">In deze shell is de Azure CLI vooraf geïnstalleerd en geconfigureerd voor gebruik met uw account.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-158">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="4c9f8-159">Typ voor hulp bij CLI-opdrachten, `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-159">To get help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="4c9f8-160">In een sessie CLI aanmelden bij Azure met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-160">In a CLI session, log in to Azure with the command that follows.</span></span> <span data-ttu-id="4c9f8-161">Als u op **Try it** in het onderstaande vak een Cloud-Shell wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-161">If you click **Try it** in the box below, a Cloud Shell opens.</span></span> <span data-ttu-id="4c9f8-162">U kunt aanmelden bij uw Azure-abonnement zonder invoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-162">You can log in to your Azure subscription, without entering the following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="4c9f8-163">Om ervoor te zorgen de CLI in Service Management-modus, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-163">To ensure the CLI is in Service Management mode, enter the following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="4c9f8-164">Een virtueel netwerk maken met een particulier subnet:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="4c9f8-165">Maak een openbare subnet binnen het virtuele netwerk:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-165">Create a public subnet within the virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="4c9f8-166">Controleer het virtuele netwerk en subnetten:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-166">Review the virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="4c9f8-167">**Optionele**: U kunt de resources die u hebt gemaakt wanneer u klaar bent met deze zelfstudie, zodat u geen gebruik kosten verwijderen:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-167">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="4c9f8-168">Hoewel u een resourcegroep voor het maken van een virtueel netwerk (klassiek) in de CLI niet opgeven, Azure maakt van het virtuele netwerk in een resourcegroep met de naam *standaard netwerken*.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-168">Though you can't specify a resource group to create a virtual network (classic) in using the CLI, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="4c9f8-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c9f8-169">PowerShell</span></span>

1. <span data-ttu-id="4c9f8-170">Installeer de nieuwste versie van de PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-170">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="4c9f8-171">Zie [Overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) als u nog geen ervaring hebt met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-171">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="4c9f8-172">Een PowerShell-sessie starten.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="4c9f8-173">Meld u in PowerShell aan bij Azure door het commando `Add-AzureAccount` in te voeren.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-173">In PowerShell, log in to Azure by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="4c9f8-174">Wijzig het volgende pad en bestandsnaam naar gelang van toepassing, en uw bestaande netwerk-configuratiebestand exporteren:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-174">Change the following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="4c9f8-175">Gebruik een virtueel netwerk maakt met openbare en particuliere subnetten, een teksteditor om toe te voegen de **VirtualNetworkSite** element zijn dat naar het configuratiebestand van het netwerk volgt.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-175">To create a virtual network with public and private subnets, use any text editor to add the **VirtualNetworkSite** element that follows to the network configuration file.</span></span>

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

    <span data-ttu-id="4c9f8-176">Bekijk de volledige [network-configuratieschema bestand](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c9f8-176">Review the full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="4c9f8-177">Importeer het configuratiebestand van het netwerk:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-177">Import the network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="4c9f8-178">Een configuratiebestand gewijzigde netwerk importeren kan leiden tot wijzigingen in bestaande virtuele netwerken (klassiek) in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-178">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="4c9f8-179">Zorg ervoor dat u alleen de vorige virtueel netwerk toevoegen en u niet wijzigen of verwijderen van een bestaande virtuele netwerken uit uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-179">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="4c9f8-180">Controleer het virtuele netwerk en subnetten:</span><span class="sxs-lookup"><span data-stu-id="4c9f8-180">Review the virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="4c9f8-181">**Optionele**: U kunt de resources die u hebt gemaakt wanneer u klaar bent met deze zelfstudie, zodat u geen gebruik kosten verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-181">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="4c9f8-182">Voor het verwijderen van het virtuele netwerk volledige stap 4-6 opnieuw verwijderen van deze tijd de **VirtualNetworkSite** element dat u in stap 5 hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-182">To delete the virtual network, complete steps 4-6 again, this time removing the **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="4c9f8-183">Hoewel u een resourcegroep voor het maken van een virtueel netwerk (klassiek) in met behulp van PowerShell kan niet opgeeft, Azure maakt van het virtuele netwerk in een resourcegroep met de naam *standaard netwerken*.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-183">Though you can't specify a resource group to create a virtual network (classic) in using PowerShell, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="4c9f8-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4c9f8-184">Next steps</span></span>

- <span data-ttu-id="4c9f8-185">Zie voor meer informatie over alle virtueel netwerk en subnetinstellingen, [virtuele netwerken beheren](virtual-network-manage-network.md) en [beheren van virtueel netwerksubnetten](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="4c9f8-185">To learn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="4c9f8-186">U beschikt over verschillende opties voor het gebruik van virtuele netwerken en subnetten in een productieomgeving om te voldoen aan verschillende vereisten.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-186">You have various options for using virtual networks and subnets in a production environment to meet different requirements.</span></span>
- <span data-ttu-id="4c9f8-187">Van binnenkomende en uitgaande subnetverkeer filteren, maken en toepassen [netwerkbeveiligingsgroepen](virtual-networks-nsg.md) aan subnetten.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-187">To filter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) to subnets.</span></span>
- <span data-ttu-id="4c9f8-188">Maak een [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of een [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtuele machine en maak verbinding met een bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it to an existing virtual network.</span></span>
- <span data-ttu-id="4c9f8-189">Voor verbinding twee virtuele netwerken in dezelfde Azure-locatie, maak een [virtueel netwerk peering](create-peering-different-deployment-models.md) tussen de virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-189">To connect two virtual networks in the same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between the virtual networks.</span></span> <span data-ttu-id="4c9f8-190">U kunt een virtueel netwerk (Resource Manager) peer met een virtueel netwerk (klassiek), maar u kunt geen maken een peering tussen twee virtuele netwerken (klassiek).</span><span class="sxs-lookup"><span data-stu-id="4c9f8-190">You can peer a virtual network (Resource Manager) to a virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="4c9f8-191">Het virtuele netwerk verbinding met een on-premises netwerk via een [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span><span class="sxs-lookup"><span data-stu-id="4c9f8-191">Connect the virtual network to an on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
