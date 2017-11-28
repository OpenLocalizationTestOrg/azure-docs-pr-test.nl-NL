---
title: "Configureren van privé IP-adressen voor virtuele machines - Azure PowerShell | Microsoft Docs"
description: "Informatie over het configureren van privé IP-adressen voor virtuele machines met behulp van PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2810190897c44c944912ef3325b1f40479aa3078
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="2ce82-103">Configureer persoonlijke IP-adressen voor een virtuele machine met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ce82-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="2ce82-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="2ce82-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="2ce82-105">Microsoft raadt aan resources te maken via het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2ce82-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="2ce82-106">Lees het artikel [Azure-implementatiemodellen begrijpen](../azure-resource-manager/resource-manager-deployment-model.md) voor meer informatie over de verschillen tussen de twee modellen.</span><span class="sxs-lookup"><span data-stu-id="2ce82-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="2ce82-107">Dit artikel is van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2ce82-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="2ce82-108">U kunt ook [statisch privé IP-adres in het klassieke implementatiemodel beheren](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2ce82-108">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="2ce82-109">Het voorbeeld PowerShell onderstaande opdrachten een eenvoudige omgeving al gemaakt verwacht op basis van de bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="2ce82-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="2ce82-110">Als u wilt de opdrachten uitvoeren zoals ze worden weergegeven in dit document, eerst de testomgeving wordt beschreven in bouwen [een vnet maken](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2ce82-110">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="2ce82-111">Een virtuele machine met een statisch privé-IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="2ce82-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="2ce82-112">Maken van een virtuele machine met de naam *DNS01* in de *FrontEnd* subnet van een VNet met de naam *TestVNet* met een statisch privé IP-adres van *192.168.1.101*, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2ce82-112">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="2ce82-113">Stel de variabelen voor de storage-account, locatie, resourcegroep en referenties moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2ce82-113">Set variables for the storage account, location, resource group, and credentials to be used.</span></span> <span data-ttu-id="2ce82-114">U moet een gebruikersnaam en wachtwoord invoeren voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2ce82-114">You will need to enter a user name and password for the VM.</span></span> <span data-ttu-id="2ce82-115">De storage-account en resource group moet al bestaan.</span><span class="sxs-lookup"><span data-stu-id="2ce82-115">The storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type the name and password of the local administrator account."
    ```

2. <span data-ttu-id="2ce82-116">Ophalen van het virtuele netwerk en subnet dat u wilt maken van de virtuele machine in.</span><span class="sxs-lookup"><span data-stu-id="2ce82-116">Retrieve the virtual network and subnet you want to create the VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="2ce82-117">Maak indien nodig een openbaar IP-adres voor toegang tot de virtuele machine via het Internet.</span><span class="sxs-lookup"><span data-stu-id="2ce82-117">If necessary, create a public IP address to access the VM from the Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="2ce82-118">Maak een NIC met behulp van het statische privé IP-adres dat u wilt toewijzen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2ce82-118">Create a NIC using the static private IP address you want to assign to the VM.</span></span> <span data-ttu-id="2ce82-119">Zorg ervoor dat het IP-adres uit het subnetbereik dat u de virtuele machine wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2ce82-119">Make sure the IP is from the subnet range you are adding the VM to.</span></span> <span data-ttu-id="2ce82-120">Dit is de belangrijkste stap voor dit artikel, waarin het instellen van het particuliere IP-adres naar statisch.</span><span class="sxs-lookup"><span data-stu-id="2ce82-120">This is the main step for this article, where you set the private IP to be static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="2ce82-121">De virtuele machine maken met de NIC die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2ce82-121">Create the VM using the NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="2ce82-122">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2ce82-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="2ce82-123">Statische privé IP-adresgegevens voor een netwerkinterface ophalen</span><span class="sxs-lookup"><span data-stu-id="2ce82-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="2ce82-124">Voer de volgende PowerShell-opdracht om weer te geven het statische privé IP-adresgegevens voor de virtuele machine met het bovenstaande script gemaakt, en houd rekening met de waarden voor *PrivateIpAddress* en *PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="2ce82-124">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="2ce82-125">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2ce82-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="2ce82-126">Een statisch privé IP-adres verwijderen uit een netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="2ce82-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="2ce82-127">Verwijderen van het statische privé IP-adres toegevoegd aan de virtuele machine in het bovenstaande script Voer de volgende PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2ce82-127">To remove the static private IP address added to the VM in the script above, run the following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="2ce82-128">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2ce82-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-to-a-network-interface"></a><span data-ttu-id="2ce82-129">Een statisch privé IP-adres toevoegen aan een netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="2ce82-129">Add a static private IP address to a network interface</span></span>
<span data-ttu-id="2ce82-130">Als u wilt een statisch privé IP-adres toevoegen aan de virtuele machine gemaakt met behulp van het bovenstaande script, voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2ce82-130">To add a static private IP address to the VM created using the script above, run the following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-the-allocation-method-for-a-private-ip-address-assigned-to-a-network-interface"></a><span data-ttu-id="2ce82-131">De toewijzingsmethode voor een particuliere IP-adres is toegewezen aan een netwerkinterface wijzigen</span><span class="sxs-lookup"><span data-stu-id="2ce82-131">Change the allocation method for a private IP address assigned to a network interface</span></span>

<span data-ttu-id="2ce82-132">Een persoonlijke IP-adres is toegewezen aan een NIC met de statische of dynamische toewijzingsmethode.</span><span class="sxs-lookup"><span data-stu-id="2ce82-132">A private IP address is assigned to a NIC with the static or dynamic allocation method.</span></span> <span data-ttu-id="2ce82-133">Dynamische IP-adressen kunnen wijzigen na het starten van een virtuele machine die eerder gestopt (toewijzing ongedaan gemaakt is).</span><span class="sxs-lookup"><span data-stu-id="2ce82-133">Dynamic IP addresses can change after starting a VM that was previously in the stopped (deallocated) state.</span></span> <span data-ttu-id="2ce82-134">Dit kan problemen veroorzaken als de virtuele machine host fungeert voor een service die hetzelfde IP-adres zelfs na opnieuw opstarten van gestopt (toewijzing ongedaan gemaakt vereist).</span><span class="sxs-lookup"><span data-stu-id="2ce82-134">This can potentially cause issues if the VM is hosting a service that requires the same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="2ce82-135">Statische IP-adressen worden bewaard totdat de virtuele machine wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2ce82-135">Static IP addresses are retained until the VM is deleted.</span></span> <span data-ttu-id="2ce82-136">Als u wilt wijzigen van de toewijzingsmethode van een IP-adres, voer het volgende script, waardoor de toewijzingsmethode van dynamisch in statisch is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="2ce82-136">To change the allocation method of an IP address, run the following script, which changes the allocation method from dynamic to static.</span></span> <span data-ttu-id="2ce82-137">Als de toewijzingsmethode voor de huidige privé IP-adres statisch is, wijzigt u *statische* naar *dynamische* voordat het script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2ce82-137">If the allocation method for the current private IP address is static, change *Static* to *Dynamic* before executing the script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "The allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for the IP address" $IP"." -NoNewline
```

<span data-ttu-id="2ce82-138">Als u de naam van de NIC niet weet, kunt u een lijst met NIC's binnen een resourcegroep weergeven met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2ce82-138">If you don't know the name of the NIC, you can view a list of NICs within a resource group by entering the following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="2ce82-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2ce82-139">Next steps</span></span>
* <span data-ttu-id="2ce82-140">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="2ce82-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="2ce82-141">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="2ce82-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="2ce82-142">Raadpleeg de [gereserveerd IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ce82-142">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

