---
title: Meerdere IP-adressen voor virtuele machines in Azure - PowerShell | Microsoft Docs
description: Meer informatie over meerdere IP-adressen toewijzen aan een virtuele machine met behulp van PowerShell | Resource Manager.
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
ms.openlocfilehash: 29f64aeefc2a7deb1f84d759c2323347536b9c27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-powershell"></a><span data-ttu-id="adb46-103">Meerdere IP-adressen toewijzen aan virtuele machines met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="adb46-103">Assign multiple IP addresses to virtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="adb46-104">Dit artikel wordt uitgelegd hoe u een virtuele machine (VM) maken via het Azure Resource Manager-implementatiemodel met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adb46-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="adb46-105">Meerdere IP-adressen kunnen niet worden toegewezen aan resources die zijn gemaakt met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="adb46-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="adb46-106">Lees voor meer informatie over Azure-implementatiemodellen de [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="adb46-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="adb46-107"><a name = "create"></a>Een virtuele machine maken met meerdere IP-adressen</span><span class="sxs-lookup"><span data-stu-id="adb46-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="adb46-108">Welke stappen volgen wordt uitgelegd hoe een voorbeeld van de virtuele machine maken met meerdere IP-adressen, zoals beschreven in het scenario.</span><span class="sxs-lookup"><span data-stu-id="adb46-108">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="adb46-109">Variabele waarden zoals vereist voor uw implementatie te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="adb46-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="adb46-110">Open een PowerShell-opdrachtprompt en voer de overige stappen in deze sectie binnen één PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="adb46-110">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="adb46-111">Als u nog niet PowerShell geïnstalleerd en geconfigureerd, voer de stappen in de [installeren en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="adb46-111">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="adb46-112">Meld u aan bij uw account met de `login-azurermaccount` opdracht.</span><span class="sxs-lookup"><span data-stu-id="adb46-112">Login to your account with the `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="adb46-113">Vervang *myResourceGroup* en *westus* met een naam en locatie van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="adb46-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="adb46-114">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="adb46-114">Create a resource group.</span></span> <span data-ttu-id="adb46-115">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="adb46-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="adb46-116">Maak een virtueel netwerk (VNet) en het subnet in dezelfde locatie als de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="adb46-116">Create a virtual network (VNet) and subnet in the same location as the resource group:</span></span>

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

    # Get the subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="adb46-117">Een netwerkbeveiligingsgroep (NSG) en een regel maken.</span><span class="sxs-lookup"><span data-stu-id="adb46-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="adb46-118">Het NSG beveiligt de virtuele machine met regels voor binnenkomend en uitgaand.</span><span class="sxs-lookup"><span data-stu-id="adb46-118">The NSG secures the VM using inbound and outbound rules.</span></span> <span data-ttu-id="adb46-119">In dit geval is er een binnenkomende regel gemaakt voor poort 3389, waarmee binnenkomende verbindingen met een extern bureaublad worden toegestaan.</span><span class="sxs-lookup"><span data-stu-id="adb46-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

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

6. <span data-ttu-id="adb46-120">Definieer de primaire IP-configuratie voor de NIC.</span><span class="sxs-lookup"><span data-stu-id="adb46-120">Define the primary IP configuration for the NIC.</span></span> <span data-ttu-id="adb46-121">10.0.0.4 wijzigen naar een geldig adres in het subnet dat u hebt gemaakt, als u de eerder gedefinieerde waarde hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="adb46-121">Change 10.0.0.4 to a valid address in the subnet you created, if you didn't use the value defined previously.</span></span> <span data-ttu-id="adb46-122">Voordat u een statisch IP-adres toewijst, wordt het aanbevolen dat u eerst bevestigen dat dit nog niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="adb46-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="adb46-123">Voer de opdracht `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="adb46-123">Enter the command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="adb46-124">De uitvoer geretourneerd als het adres beschikbaar is, *True*.</span><span class="sxs-lookup"><span data-stu-id="adb46-124">If the address is available, the output returns *True*.</span></span> <span data-ttu-id="adb46-125">De uitvoer geretourneerd als deze niet beschikbaar is, *False* en een lijst met adressen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="adb46-125">If it's not available, the output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="adb46-126">In de volgende opdrachten **< vervangen-met-uw unieke-naam > vervangt door de unieke DNS-naam te gebruiken.**</span><span class="sxs-lookup"><span data-stu-id="adb46-126">In the following commands, **Replace <replace-with-your-unique-name> with the unique DNS name to use.**</span></span> <span data-ttu-id="adb46-127">De naam moet uniek zijn in alle openbare IP-adressen binnen een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="adb46-127">The name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="adb46-128">Dit is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="adb46-128">This is an optional parameter.</span></span> <span data-ttu-id="adb46-129">Het kan worden verwijderd als u alleen verbinding wilt maken met de virtuele machine met behulp van het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="adb46-129">It can be removed if you only want to connect to the VM using the public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="adb46-130">Wanneer u meerdere IP-configuraties aan een NIC toewijst, één configuratie moet worden toegewezen als de *-primaire*.</span><span class="sxs-lookup"><span data-stu-id="adb46-130">When you assign multiple IP configurations to a NIC, one configuration must be assigned as the *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="adb46-131">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="adb46-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="adb46-132">Lees meer informatie over prijzen voor IP-adres, de [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="adb46-132">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="adb46-133">Er is een limiet aan het aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="adb46-133">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="adb46-134">Lees voor meer informatie over de limieten het artikel [Azure-limieten](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="adb46-134">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="adb46-135">Definieer de secundaire IP-configuraties voor de NIC.</span><span class="sxs-lookup"><span data-stu-id="adb46-135">Define the secondary IP configurations for the NIC.</span></span> <span data-ttu-id="adb46-136">U kunt toevoegen of verwijderen van configuraties indien nodig.</span><span class="sxs-lookup"><span data-stu-id="adb46-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="adb46-137">Elk IP-adresconfiguratie moet een particulier IP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="adb46-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="adb46-138">Elke configuratie kan desgewenst een openbaar IP-adres toegewezen hebben.</span><span class="sxs-lookup"><span data-stu-id="adb46-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
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

8. <span data-ttu-id="adb46-139">De NIC maken en koppelen van de drie IP-configuraties:</span><span class="sxs-lookup"><span data-stu-id="adb46-139">Create the NIC and associate the three IP configurations to it:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="adb46-140">Hoewel alle configuraties zijn toegewezen aan één NIC in dit artikel, kunt u meerdere IP-configuraties kunt toewijzen aan elke NIC die is gekoppeld aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="adb46-140">Though all configurations are assigned to one NIC in this article, you can assign multiple IP configurations to every NIC attached to the VM.</span></span> <span data-ttu-id="adb46-141">Lees voor meer informatie over het maken van een virtuele machine met meerdere NIC's, de [een virtuele machine maken met meerdere NIC's](virtual-network-deploy-multinic-arm-ps.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="adb46-141">To learn how to create a VM with multiple NICs, read the [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="adb46-142">De virtuele machine maken door te voeren van de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="adb46-142">Create the VM by entering the following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted to enter a sername and password for the VM you're reating.
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
    
    # Create the VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="adb46-143">De particuliere IP-adressen toevoegen aan het besturingssysteem van de virtuele machine via de stappen voor het besturingssysteem in de [toevoegen IP-adressen naar een VM-besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="adb46-143">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="adb46-144">Het openbare IP-adressen niet aan het besturingssysteem toevoegen.</span><span class="sxs-lookup"><span data-stu-id="adb46-144">Do not add the public IP addresses to the operating system.</span></span>

## <span data-ttu-id="adb46-145"><a name="add"></a>IP-adressen toevoegen aan een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="adb46-145"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="adb46-146">U kunt persoonlijke en openbare IP-adressen toevoegen aan een NIC via de stappen volgen.</span><span class="sxs-lookup"><span data-stu-id="adb46-146">You can add private and public IP addresses to a NIC by completing the steps that follow.</span></span> <span data-ttu-id="adb46-147">De voorbeelden in de volgende secties wordt ervan uitgegaan dat er al een virtuele machine met de drie IP-configuraties beschreven in de [scenario](#Scenario) in dit artikel, maar het is niet vereist dat u doen.</span><span class="sxs-lookup"><span data-stu-id="adb46-147">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="adb46-148">Open een PowerShell-opdrachtprompt en voer de overige stappen in deze sectie binnen één PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="adb46-148">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="adb46-149">Als u nog niet PowerShell geïnstalleerd en geconfigureerd, voer de stappen in de [installeren en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="adb46-149">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="adb46-150">"Waarden" van de volgende $Variables wijzigen in de naam van de NIC die u wilt toevoegen, IP-adres en de resourcegroep en locatie van die de NIC bestaat in:</span><span class="sxs-lookup"><span data-stu-id="adb46-150">Change the "values" of the following $Variables to the name of the NIC you want to add IP address to and the resource group and location the NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="adb46-151">Als u de naam van de NIC die u wilt wijzigen, voert de volgende opdrachten niet weet, klikt u vervolgens de waarden van de vorige variabelen te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="adb46-151">If you don't know the name of the NIC you want to change, enter the following commands, then change the values of the previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="adb46-152">Maken van een variabele en stel deze in op de bestaande NIC door de volgende opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="adb46-152">Create a variable and set it to the existing NIC by typing the following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="adb46-153">Wijzig in de volgende opdrachten *MyVNet* en *MySubnet* tot de namen van de VNet en de NIC is verbonden met subnet.</span><span class="sxs-lookup"><span data-stu-id="adb46-153">In the following commands, change *MyVNet* and *MySubnet* to the names of the VNet and subnet the NIC is connected to.</span></span> <span data-ttu-id="adb46-154">Voer de opdrachten voor het ophalen van de VNet en subnet objecten die de NIC is verbonden met:</span><span class="sxs-lookup"><span data-stu-id="adb46-154">Enter the commands to retrieve the VNet and subnet objects the NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="adb46-155">Als u de naam van het VNet of subnet die de NIC is verbonden met niet weet, voert u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="adb46-155">If you don't know the VNet or subnet name the NIC is connected to, enter the following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="adb46-156">In de uitvoer is vergelijkbaar met de volgende voorbeelduitvoer tekst zoeken:</span><span class="sxs-lookup"><span data-stu-id="adb46-156">In the output, look for text similar to the following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="adb46-157">In deze uitvoer *MyVnet* is het VNet en *MySubnet* is het de NIC is verbonden met subnet.</span><span class="sxs-lookup"><span data-stu-id="adb46-157">In this output, *MyVnet* is the VNet and *MySubnet* is the subnet the NIC is connected to.</span></span>

5. <span data-ttu-id="adb46-158">Volg de stappen in een van de volgende secties, op basis van uw vereisten:</span><span class="sxs-lookup"><span data-stu-id="adb46-158">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="adb46-159">**Een persoonlijke IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="adb46-159">**Add a private IP address**</span></span>

    <span data-ttu-id="adb46-160">Als u wilt een particulier IP-adres toevoegen aan een NIC, moet u een IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="adb46-160">To add a private IP address to a NIC, you must create an IP configuration.</span></span> <span data-ttu-id="adb46-161">De volgende opdracht maakt een configuratie met een statisch IP-adres 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="adb46-161">The following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="adb46-162">Wanneer u een statisch IP-adres opgeeft, moet dit een ongebruikt adres voor het subnet.</span><span class="sxs-lookup"><span data-stu-id="adb46-162">When specifying a static IP address, it must be an unused address for the subnet.</span></span> <span data-ttu-id="adb46-163">Het raadzaam dat u eerst het adres om te controleren of deze beschikbaar is door te voeren test de `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` opdracht.</span><span class="sxs-lookup"><span data-stu-id="adb46-163">It's recommended that you first test the address to ensure it's available by entering the `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="adb46-164">De uitvoer geretourneerd als het IP-adres beschikbaar is, *True*.</span><span class="sxs-lookup"><span data-stu-id="adb46-164">If the IP address is available, the output returns *True*.</span></span> <span data-ttu-id="adb46-165">De uitvoer geretourneerd als deze niet beschikbaar is, *False*, en een lijst met adressen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="adb46-165">If it's not available, the output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="adb46-166">Configuraties die u nodig hebt, gebruik van unieke namen en privé IP-adressen (voor configuraties met statische IP-adressen) maken.</span><span class="sxs-lookup"><span data-stu-id="adb46-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="adb46-167">De privé IP-adres toevoegen aan het besturingssysteem van de virtuele machine via de stappen voor het besturingssysteem in de [toevoegen IP-adressen naar een VM-besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="adb46-167">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="adb46-168">**Een openbaar IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="adb46-168">**Add a public IP address**</span></span>

    <span data-ttu-id="adb46-169">Een openbaar IP-adres wordt toegevoegd door het koppelen van een resource met openbare IP-adres aan een nieuwe IP-configuratie of een bestaande IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="adb46-169">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="adb46-170">Voer de stappen in een van de secties die volgen, die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="adb46-170">Complete the steps in one of the sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="adb46-171">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="adb46-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="adb46-172">Lees meer informatie over prijzen voor IP-adres, de [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="adb46-172">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="adb46-173">Er is een limiet aan het aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="adb46-173">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="adb46-174">Lees voor meer informatie over de limieten het artikel [Azure-limieten](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="adb46-174">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="adb46-175">**Koppel het openbare IP-adres resource naar een nieuwe IP-configuratie**</span><span class="sxs-lookup"><span data-stu-id="adb46-175">**Associate the public IP address resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="adb46-176">Als u een openbaar IP-adres in een nieuw IP-configuratie toevoegt, moet u ook een privé IP-adres toevoegen, omdat alle IP-configuraties moeten een particulier IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="adb46-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="adb46-177">U kunt een bestaande resource voor openbare IP-adres toevoegen of u een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="adb46-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="adb46-178">Voer de volgende opdracht om een nieuwe maken:</span><span class="sxs-lookup"><span data-stu-id="adb46-178">To create a new one, enter the following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="adb46-179">Een nieuwe IP-configuratie maken met een statisch privé IP-adres en de bijbehorende *myPublicIp3* openbaar IP adres resource, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="adb46-179">To create a new IP configuration with a static private IP address and the associated *myPublicIp3* public IP address resource, enter the following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="adb46-180">**Koppel het openbare IP-adres resource aan een bestaande IP-configuratie**</span><span class="sxs-lookup"><span data-stu-id="adb46-180">**Associate the public IP address resource to an existing IP configuration**</span></span>

        <span data-ttu-id="adb46-181">Een openbare IP-adres resource kan alleen worden gekoppeld aan een IP-configuratie die nog geen die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="adb46-181">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="adb46-182">U kunt bepalen of een IP-configuratie een gekoppeld openbare IP-adres heeft met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="adb46-182">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="adb46-183">U ziet de uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="adb46-183">You see output similar to the following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="adb46-184">Aangezien de **PublicIpAddress** kolom voor *IpConfig 3* is leeg, geen openbare IP-adres-resource is momenteel gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="adb46-184">Since the **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="adb46-185">U kunt een bestaande resource voor openbare IP-adres toevoegen aan IpConfig 3 of Voer de volgende opdracht een te maken:</span><span class="sxs-lookup"><span data-stu-id="adb46-185">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="adb46-186">Voer de volgende opdracht om te koppelen van het openbare IP-adres resource aan de bestaande IP-configuratie met de naam *IpConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="adb46-186">Enter the following command to associate the public IP address resource to the existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="adb46-187">Stel de NIC met de nieuwe IP-configuratie met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="adb46-187">Set the NIC with the new IP configuration by entering the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="adb46-188">Bekijk de privé IP-adressen en openbare IP-adres resources toegewezen aan de NIC met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="adb46-188">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="adb46-189">De privé IP-adres toevoegen aan het besturingssysteem van de virtuele machine via de stappen voor het besturingssysteem in de [toevoegen IP-adressen naar een VM-besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="adb46-189">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="adb46-190">Het openbare IP-adres niet aan het besturingssysteem toevoegen.</span><span class="sxs-lookup"><span data-stu-id="adb46-190">Do not add the public IP address to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
