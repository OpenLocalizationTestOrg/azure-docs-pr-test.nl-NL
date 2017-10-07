---
title: aaaMultiple IP-adressen voor virtuele machines in Azure - PowerShell | Microsoft Docs
description: Meer informatie over hoe tooassign meerdere IP-adressen tooa virtuele machine met behulp van PowerShell | Resource Manager.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a><span data-ttu-id="be304-103">Meerdere IP-adressen toewijzen toovirtual machines met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="be304-103">Assign multiple IP addresses toovirtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="be304-104">Dit artikel wordt uitgelegd hoe toocreate een virtuele machine (VM) via hello Azure Resource Manager deployment model met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be304-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="be304-105">Meerdere IP-adressen kunnen niet worden toegewezen als tooresources via de klassieke implementatiemodel Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="be304-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="be304-106">meer informatie over Azure-implementatiemodellen, Hallo lezen toolearn [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="be304-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="be304-107"><a name = "create"></a>Een virtuele machine maken met meerdere IP-adressen</span><span class="sxs-lookup"><span data-stu-id="be304-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="be304-108">Hallo in de volgende procedure wordt uitgelegd hoe toocreate een voorbeeld van de virtuele machine met meerdere IP-adressen, zoals beschreven in Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="be304-108">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="be304-109">Variabele waarden zoals vereist voor uw implementatie te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="be304-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="be304-110">Open een PowerShell-opdrachtprompt en volledige Hallo resterende stappen in deze sectie binnen één PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="be304-110">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="be304-111">Als u nog niet PowerShell geïnstalleerd en geconfigureerd, voltooid Hallo stappen voor het Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="be304-111">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="be304-112">Tooyour aanmeldingsaccount Hello `login-azurermaccount` opdracht.</span><span class="sxs-lookup"><span data-stu-id="be304-112">Login tooyour account with hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="be304-113">Vervang *myResourceGroup* en *westus* met een naam en locatie van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="be304-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="be304-114">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="be304-114">Create a resource group.</span></span> <span data-ttu-id="be304-115">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="be304-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="be304-116">Maken van een virtueel netwerk (VNet) en het subnet in Hallo dezelfde locatie als Hallo resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="be304-116">Create a virtual network (VNet) and subnet in hello same location as hello resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="be304-117">Een netwerkbeveiligingsgroep (NSG) en een regel maken.</span><span class="sxs-lookup"><span data-stu-id="be304-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="be304-118">Hallo NSG Hallo VM beveiligt met regels voor binnenkomend en uitgaand.</span><span class="sxs-lookup"><span data-stu-id="be304-118">hello NSG secures hello VM using inbound and outbound rules.</span></span> <span data-ttu-id="be304-119">In dit geval is er een binnenkomende regel gemaakt voor poort 3389, waarmee binnenkomende verbindingen met een extern bureaublad worden toegestaan.</span><span class="sxs-lookup"><span data-stu-id="be304-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="be304-120">Definieer Hallo primaire IP-configuratie voor Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="be304-120">Define hello primary IP configuration for hello NIC.</span></span> <span data-ttu-id="be304-121">Wijziging 10.0.0.4 tooa geldig adres in Hallo subnet die u hebt gemaakt, als u hebt eerder gedefinieerde Hallo-waarde gebruikt.</span><span class="sxs-lookup"><span data-stu-id="be304-121">Change 10.0.0.4 tooa valid address in hello subnet you created, if you didn't use hello value defined previously.</span></span> <span data-ttu-id="be304-122">Voordat u een statisch IP-adres toewijst, wordt het aanbevolen dat u eerst bevestigen dat dit nog niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="be304-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="be304-123">Voer de opdracht Hallo `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="be304-123">Enter hello command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="be304-124">Als het Hallo-adres beschikbaar is, Hallo retourneert uitvoer *True*.</span><span class="sxs-lookup"><span data-stu-id="be304-124">If hello address is available, hello output returns *True*.</span></span> <span data-ttu-id="be304-125">Als niet beschikbaar is, retourneert-uitvoervenster het Hallo *False* en een lijst met adressen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="be304-125">If it's not available, hello output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="be304-126">In het Hallo-opdrachten, na **< vervangen-met-uw unieke-naam > vervangt door Hallo unieke DNS-naam toouse.**</span><span class="sxs-lookup"><span data-stu-id="be304-126">In hello following commands, **Replace <replace-with-your-unique-name> with hello unique DNS name toouse.**</span></span> <span data-ttu-id="be304-127">Hallo-naam moet uniek zijn in alle openbare IP-adressen binnen een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="be304-127">hello name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="be304-128">Dit is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="be304-128">This is an optional parameter.</span></span> <span data-ttu-id="be304-129">Het kan worden verwijderd als u wilt dat alleen tooconnect toohello VM via Hallo openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="be304-129">It can be removed if you only want tooconnect toohello VM using hello public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="be304-130">Wanneer u meerdere IP-configuraties tooa NIC toewijst, één configuratie moet worden toegewezen als Hallo *-primaire*.</span><span class="sxs-lookup"><span data-stu-id="be304-130">When you assign multiple IP configurations tooa NIC, one configuration must be assigned as hello *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="be304-131">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="be304-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="be304-132">meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="be304-132">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="be304-133">Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="be304-133">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="be304-134">meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.</span><span class="sxs-lookup"><span data-stu-id="be304-134">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="be304-135">Hallo secundaire IP-configuraties definiëren voor Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="be304-135">Define hello secondary IP configurations for hello NIC.</span></span> <span data-ttu-id="be304-136">U kunt toevoegen of verwijderen van configuraties indien nodig.</span><span class="sxs-lookup"><span data-stu-id="be304-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="be304-137">Elk IP-adresconfiguratie moet een particulier IP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="be304-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="be304-138">Elke configuratie kan desgewenst een openbaar IP-adres toegewezen hebben.</span><span class="sxs-lookup"><span data-stu-id="be304-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="be304-139">Hallo NIC maken en koppelen van Hallo drie IP-configuraties tooit:</span><span class="sxs-lookup"><span data-stu-id="be304-139">Create hello NIC and associate hello three IP configurations tooit:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="be304-140">Hoewel alle configuraties zijn tooone NIC in dit artikel worden toegewezen, kunt u meerdere IP-configuraties tooevery NIC die is gekoppeld toohello VM kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="be304-140">Though all configurations are assigned tooone NIC in this article, you can assign multiple IP configurations tooevery NIC attached toohello VM.</span></span> <span data-ttu-id="be304-141">hoe een virtuele machine met meerdere NIC's, toocreate Lees toolearn hello [een virtuele machine maken met meerdere NIC's](virtual-network-deploy-multinic-arm-ps.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="be304-141">toolearn how toocreate a VM with multiple NICs, read hello [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="be304-142">Hallo VM maken door te voeren van Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="be304-142">Create hello VM by entering hello following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="be304-143">Toevoegen Hallo privé-IP-adressen toohello VM besturingssysteem via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="be304-143">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="be304-144">Voeg geen Hallo openbare IP-adressen toohello besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="be304-144">Do not add hello public IP addresses toohello operating system.</span></span>

## <span data-ttu-id="be304-145"><a name="add"></a>IP-adressen tooa VM toevoegen</span><span class="sxs-lookup"><span data-stu-id="be304-145"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="be304-146">U kunt persoonlijke en openbare IP-adressen tooa NIC toevoegen via Hallo stappen volgen.</span><span class="sxs-lookup"><span data-stu-id="be304-146">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="be304-147">Hallo voorbeelden in de volgende secties Hallo wordt ervan uitgegaan dat er al een virtuele machine met Hallo drie IP-configuraties beschreven in Hallo [scenario](#Scenario) in dit artikel, maar het is niet vereist dat u doen.</span><span class="sxs-lookup"><span data-stu-id="be304-147">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="be304-148">Open een PowerShell-opdrachtprompt en volledige Hallo resterende stappen in deze sectie binnen één PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="be304-148">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="be304-149">Als u nog niet PowerShell geïnstalleerd en geconfigureerd, voltooid Hallo stappen voor het Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="be304-149">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="be304-150">Hallo "waarden" Hallo achter $Variables toohello naam Hallo NIC u tooadd IP-adres tooand Hallo resource groep en locatie Hallo die NIC bestaat in wilt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="be304-150">Change hello "values" of hello following $Variables toohello name of hello NIC you want tooadd IP address tooand hello resource group and location hello NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="be304-151">Als u niet Hallo-naam van de NIC die u wilt dat toochange hello weet, Voer Hallo opdrachten te volgen en Hallo waarden van de vorige variabelen Hallo wijzigen:</span><span class="sxs-lookup"><span data-stu-id="be304-151">If you don't know hello name of hello NIC you want toochange, enter hello following commands, then change hello values of hello previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="be304-152">Maak een variabele en stel deze toohello NIC bestaande door Hallo volgende opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="be304-152">Create a variable and set it toohello existing NIC by typing hello following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="be304-153">Wijzig in Hallo opdrachten te volgen, *MyVNet* en *MySubnet* toohello namen van Hallo VNet en subnet Hallo NIC is verbonden met.</span><span class="sxs-lookup"><span data-stu-id="be304-153">In hello following commands, change *MyVNet* and *MySubnet* toohello names of hello VNet and subnet hello NIC is connected to.</span></span> <span data-ttu-id="be304-154">Voer Hallo opdrachten tooretrieve hello VNet en subnet objecten Hallo die NIC is verbonden met:</span><span class="sxs-lookup"><span data-stu-id="be304-154">Enter hello commands tooretrieve hello VNet and subnet objects hello NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="be304-155">Als u Hallo VNet of subnet naam Hallo die NIC is verbonden met niet weet, voert u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="be304-155">If you don't know hello VNet or subnet name hello NIC is connected to, enter hello following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="be304-156">Zoeken in de uitvoer van Hallo tekst vergelijkbare toohello voorbeelduitvoer te volgen:</span><span class="sxs-lookup"><span data-stu-id="be304-156">In hello output, look for text similar toohello following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="be304-157">In deze uitvoer *MyVnet* hello VNet is en *MySubnet* Hallo subnet Hallo NIC is verbonden met is.</span><span class="sxs-lookup"><span data-stu-id="be304-157">In this output, *MyVnet* is hello VNet and *MySubnet* is hello subnet hello NIC is connected to.</span></span>

5. <span data-ttu-id="be304-158">Voer Hallo stappen in een Hallo uit te voeren, op basis van uw vereisten:</span><span class="sxs-lookup"><span data-stu-id="be304-158">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="be304-159">**Een persoonlijke IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="be304-159">**Add a private IP address**</span></span>

    <span data-ttu-id="be304-160">een persoonlijke IP-adres tooa NIC tooadd, moet u een IP-configuratie maken.</span><span class="sxs-lookup"><span data-stu-id="be304-160">tooadd a private IP address tooa NIC, you must create an IP configuration.</span></span> <span data-ttu-id="be304-161">Hallo volgende opdracht maakt u een configuratie met een statisch IP-adres 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="be304-161">hello following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="be304-162">Wanneer u een statisch IP-adres opgeeft, moet dit een ongebruikt adres voor het Hallo-subnet.</span><span class="sxs-lookup"><span data-stu-id="be304-162">When specifying a static IP address, it must be an unused address for hello subnet.</span></span> <span data-ttu-id="be304-163">Het raadzaam dat u eerst testen Hallo adres tooensure deze beschikbaar is door te voeren Hallo `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` opdracht.</span><span class="sxs-lookup"><span data-stu-id="be304-163">It's recommended that you first test hello address tooensure it's available by entering hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="be304-164">Als Hallo IP-adres beschikbaar is, Hallo retourneert uitvoer *True*.</span><span class="sxs-lookup"><span data-stu-id="be304-164">If hello IP address is available, hello output returns *True*.</span></span> <span data-ttu-id="be304-165">Als niet beschikbaar is, retourneert-uitvoervenster het Hallo *False*, en een lijst met adressen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="be304-165">If it's not available, hello output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="be304-166">Configuraties die u nodig hebt, gebruik van unieke namen en privé IP-adressen (voor configuraties met statische IP-adressen) maken.</span><span class="sxs-lookup"><span data-stu-id="be304-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="be304-167">Hallo persoonlijke IP-adres toohello VM besturingssysteem toevoegen via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="be304-167">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="be304-168">**Een openbaar IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="be304-168">**Add a public IP address**</span></span>

    <span data-ttu-id="be304-169">Een openbaar IP-adres wordt toegevoegd door een openbare IP-adres resource tooeither koppelen van een nieuwe IP-configuratie of een bestaande IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="be304-169">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="be304-170">Stappen Hallo in een van Hallo secties die volgen, die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="be304-170">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="be304-171">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="be304-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="be304-172">meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="be304-172">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="be304-173">Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="be304-173">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="be304-174">meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.</span><span class="sxs-lookup"><span data-stu-id="be304-174">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="be304-175">**Hallo openbare IP-resource tooa nieuwe IP-adresconfiguratie koppelen**</span><span class="sxs-lookup"><span data-stu-id="be304-175">**Associate hello public IP address resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="be304-176">Als u een openbaar IP-adres in een nieuw IP-configuratie toevoegt, moet u ook een privé IP-adres toevoegen, omdat alle IP-configuraties moeten een particulier IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="be304-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="be304-177">U kunt een bestaande resource voor openbare IP-adres toevoegen of u een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="be304-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="be304-178">toocreate een nieuw wachtwoord invoeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="be304-178">toocreate a new one, enter hello following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="be304-179">toocreate een nieuwe IP-configuratie met een statisch privé IP-adres en het Hallo gekoppeld *myPublicIp3* openbare IP-adres adres resource, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="be304-179">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIp3* public IP address resource, enter hello following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="be304-180">**Hallo openbare IP-resource tooan bestaande IP-adresconfiguratie koppelen**</span><span class="sxs-lookup"><span data-stu-id="be304-180">**Associate hello public IP address resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="be304-181">Een openbare IP-adres resource kan alleen worden gekoppeld tooan IP-configuratie die nog geen die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="be304-181">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="be304-182">U kunt bepalen of een IP-configuratie een gekoppeld openbare IP-adres heeft door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="be304-182">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="be304-183">U ziet het vergelijkbare toohello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="be304-183">You see output similar toohello following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="be304-184">Sinds Hallo **PublicIpAddress** kolom voor *IpConfig 3* is leeg, geen openbare IP-adres-resource is momenteel gekoppeld tooit.</span><span class="sxs-lookup"><span data-stu-id="be304-184">Since hello **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="be304-185">U kunt een bestaand openbaar IP-adres resource tooIpConfig-3 toevoegen, of Voer Hallo opdracht toocreate een volgende:</span><span class="sxs-lookup"><span data-stu-id="be304-185">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="be304-186">Voer Hallo opdracht resource toohello bestaande IP-configuratie met de naam van tooassociate Hallo openbare IP-adressen te volgen *IpConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="be304-186">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="be304-187">Hallo NIC met het nieuwe IP-configuratie Hallo instellen door te voeren van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="be304-187">Set hello NIC with hello new IP configuration by entering hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="be304-188">Hallo privé IP-adressen weergeven en Hallo openbare IP-adres resources toegewezen toohello NIC door te voeren Hallo de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="be304-188">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="be304-189">Hallo persoonlijke IP-adres toohello VM besturingssysteem toevoegen via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="be304-189">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="be304-190">Voeg geen Hallo openbare IP-adres toohello besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="be304-190">Do not add hello public IP address toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
