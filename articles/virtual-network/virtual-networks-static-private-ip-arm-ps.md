---
title: "aaaConfigure privé IP-adressen voor virtuele machines - Azure PowerShell | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé-IP-adressen voor virtuele machines met behulp van PowerShell."
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
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="28bb7-103">Configureer persoonlijke IP-adressen voor een virtuele machine met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="28bb7-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="28bb7-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="28bb7-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="28bb7-105">Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="28bb7-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="28bb7-106">Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="28bb7-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="28bb7-107">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="28bb7-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="28bb7-108">U kunt ook [statisch privé IP-adres in het klassieke implementatiemodel Hallo beheren](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="28bb7-108">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="28bb7-109">Hallo voorbeeld PowerShell onderstaande opdrachten verwacht een eenvoudige omgeving al gemaakt dat is gebaseerd op Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="28bb7-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="28bb7-110">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="28bb7-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="28bb7-111">Een virtuele machine met een statisch privé-IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="28bb7-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="28bb7-112">een virtuele machine met de naam toocreate *DNS01* in Hallo *FrontEnd* subnet van een VNet met de naam *TestVNet* met een statisch privé IP-adres van *192.168.1.101*, Volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="28bb7-112">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="28bb7-113">Variabelen voor Hallo storage-account, locatie, resourcegroep en referenties toobe gebruikt instellen.</span><span class="sxs-lookup"><span data-stu-id="28bb7-113">Set variables for hello storage account, location, resource group, and credentials toobe used.</span></span> <span data-ttu-id="28bb7-114">U moet voor Hallo VM tooenter een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="28bb7-114">You will need tooenter a user name and password for hello VM.</span></span> <span data-ttu-id="28bb7-115">Hallo-account en resource opslaggroep moet al bestaan.</span><span class="sxs-lookup"><span data-stu-id="28bb7-115">hello storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. <span data-ttu-id="28bb7-116">Ophalen Hallo virtueel netwerk en subnet gewenste toocreate Hallo virtuele machine in.</span><span class="sxs-lookup"><span data-stu-id="28bb7-116">Retrieve hello virtual network and subnet you want toocreate hello VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="28bb7-117">Maak een openbare IP-adres tooaccess-Hallo VM van Hallo Internet indien nodig.</span><span class="sxs-lookup"><span data-stu-id="28bb7-117">If necessary, create a public IP address tooaccess hello VM from hello Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="28bb7-118">Maak een NIC Hallo statisch privé IP-adres gewenste tooassign toohello VM.</span><span class="sxs-lookup"><span data-stu-id="28bb7-118">Create a NIC using hello static private IP address you want tooassign toohello VM.</span></span> <span data-ttu-id="28bb7-119">Zorg ervoor Hallo IP is uit Hallo-subnetbereik die u toevoegt Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="28bb7-119">Make sure hello IP is from hello subnet range you are adding hello VM to.</span></span> <span data-ttu-id="28bb7-120">Dit is de belangrijkste stap Hallo voor dit artikel, waarin u Hallo persoonlijke IP-toobe statisch instellen.</span><span class="sxs-lookup"><span data-stu-id="28bb7-120">This is hello main step for this article, where you set hello private IP toobe static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="28bb7-121">Maak Hallo VM die gebruikmaakt van Hallo NIC die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="28bb7-121">Create hello VM using hello NIC created above.</span></span>

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

    <span data-ttu-id="28bb7-122">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="28bb7-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="28bb7-123">Statische privé IP-adresgegevens voor een netwerkinterface ophalen</span><span class="sxs-lookup"><span data-stu-id="28bb7-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="28bb7-124">tooview hello statische privé-IP adresgegevens voor Hallo virtuele machine gemaakt met Hallo script bovenstaande Hallo volgende PowerShell-opdracht uitvoeren en houd rekening met waarden voor Hallo *PrivateIpAddress* en  *PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="28bb7-124">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="28bb7-125">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="28bb7-125">Expected output:</span></span>

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

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="28bb7-126">Een statisch privé IP-adres verwijderen uit een netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="28bb7-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="28bb7-127">tooremove hello statisch privé IP-adres toegevoegd toohello VM in Hallo script hierboven uitvoeren Hallo volgende PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="28bb7-127">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="28bb7-128">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="28bb7-128">Expected output:</span></span>

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

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a><span data-ttu-id="28bb7-129">Toevoegen van een statisch privé IP-adres tooa netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="28bb7-129">Add a static private IP address tooa network interface</span></span>
<span data-ttu-id="28bb7-130">tooadd een statisch privé IP-adres toohello VM gemaakt met behulp van de bovenstaande Hallo-script uitvoeren Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="28bb7-130">tooadd a static private IP address toohello VM created using hello script above, run hello following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a><span data-ttu-id="28bb7-131">Hallo toewijzingsmethode voor een particuliere IP-adres toegewezen tooa netwerkinterface wijzigen</span><span class="sxs-lookup"><span data-stu-id="28bb7-131">Change hello allocation method for a private IP address assigned tooa network interface</span></span>

<span data-ttu-id="28bb7-132">Een persoonlijke IP-adres is toegewezen tooa NIC met een statische of dynamische toewijzingsmethode Hallo.</span><span class="sxs-lookup"><span data-stu-id="28bb7-132">A private IP address is assigned tooa NIC with hello static or dynamic allocation method.</span></span> <span data-ttu-id="28bb7-133">Dynamische IP-adressen kunnen wijzigen nadat het starten van een virtuele machine die in Hallo voorheen gestopt (toewijzing ongedaan gemaakt) staat.</span><span class="sxs-lookup"><span data-stu-id="28bb7-133">Dynamic IP addresses can change after starting a VM that was previously in hello stopped (deallocated) state.</span></span> <span data-ttu-id="28bb7-134">Dit kan mogelijk problemen veroorzaken als Hallo VM is een service die is vereist Hallo host hetzelfde IP-adres, zelfs na het opnieuw opstarten van gestopt (toewijzing ongedaan gemaakt).</span><span class="sxs-lookup"><span data-stu-id="28bb7-134">This can potentially cause issues if hello VM is hosting a service that requires hello same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="28bb7-135">Statische IP-adressen worden bewaard totdat Hallo VM wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="28bb7-135">Static IP addresses are retained until hello VM is deleted.</span></span> <span data-ttu-id="28bb7-136">Hallo toewijzingsmethode toochange van een IP-adres, Hallo na script, dat de toewijzingsmethode hello wordt gewijzigd van dynamische toostatic uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="28bb7-136">toochange hello allocation method of an IP address, run hello following script, which changes hello allocation method from dynamic toostatic.</span></span> <span data-ttu-id="28bb7-137">Als de toewijzingsmethode Hallo voor Hallo huidige privé IP-adres statisch is, wijzigt *statische* te*dynamische* voordat Hallo script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="28bb7-137">If hello allocation method for hello current private IP address is static, change *Static* too*Dynamic* before executing hello script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

<span data-ttu-id="28bb7-138">Als naam Hallo Hallo NIC kunt u niet weet, kunt u een lijst met NIC's binnen een resourcegroep weergeven door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="28bb7-138">If you don't know hello name of hello NIC, you can view a list of NICs within a resource group by entering hello following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="28bb7-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="28bb7-139">Next steps</span></span>
* <span data-ttu-id="28bb7-140">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="28bb7-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="28bb7-141">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="28bb7-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="28bb7-142">Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="28bb7-142">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

