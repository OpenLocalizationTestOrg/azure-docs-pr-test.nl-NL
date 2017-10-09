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
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a>Configureer persoonlijke IP-adressen voor een virtuele machine met behulp van PowerShell

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek. Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel. Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel. In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel. U kunt ook [statisch privé IP-adres in het klassieke implementatiemodel Hallo beheren](virtual-networks-static-private-ip-classic-ps.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Hallo voorbeeld PowerShell onderstaande opdrachten verwacht een eenvoudige omgeving al gemaakt dat is gebaseerd op Hallo bovenstaande scenario. Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-arm-ps.md).

## <a name="create-a-vm-with-a-static-private-ip-address"></a>Een virtuele machine met een statisch privé-IP-adres maken
een virtuele machine met de naam toocreate *DNS01* in Hallo *FrontEnd* subnet van een VNet met de naam *TestVNet* met een statisch privé IP-adres van *192.168.1.101*, Volg onderstaande stappen voor Hallo:

1. Variabelen voor Hallo storage-account, locatie, resourcegroep en referenties toobe gebruikt instellen. U moet voor Hallo VM tooenter een gebruikersnaam en wachtwoord. Hallo-account en resource opslaggroep moet al bestaan.

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. Ophalen Hallo virtueel netwerk en subnet gewenste toocreate Hallo virtuele machine in.

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. Maak een openbare IP-adres tooaccess-Hallo VM van Hallo Internet indien nodig.

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. Maak een NIC Hallo statisch privé IP-adres gewenste tooassign toohello VM. Zorg ervoor Hallo IP is uit Hallo-subnetbereik die u toevoegt Hallo virtuele machine. Dit is de belangrijkste stap Hallo voor dit artikel, waarin u Hallo persoonlijke IP-toobe statisch instellen.

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. Maak Hallo VM die gebruikmaakt van Hallo NIC die eerder is gemaakt.

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

    Verwachte uitvoer:
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a>Statische privé IP-adresgegevens voor een netwerkinterface ophalen
tooview hello statische privé-IP adresgegevens voor Hallo virtuele machine gemaakt met Hallo script bovenstaande Hallo volgende PowerShell-opdracht uitvoeren en houd rekening met waarden voor Hallo *PrivateIpAddress* en  *PrivateIpAllocationMethod*:

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

Verwachte uitvoer:

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

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a>Een statisch privé IP-adres verwijderen uit een netwerkinterface
tooremove hello statisch privé IP-adres toegevoegd toohello VM in Hallo script hierboven uitvoeren Hallo volgende PowerShell-opdrachten:

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Verwachte uitvoer:

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

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a>Toevoegen van een statisch privé IP-adres tooa netwerkinterface
tooadd een statisch privé IP-adres toohello VM gemaakt met behulp van de bovenstaande Hallo-script uitvoeren Hallo volgende opdrachten:

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a>Hallo toewijzingsmethode voor een particuliere IP-adres toegewezen tooa netwerkinterface wijzigen

Een persoonlijke IP-adres is toegewezen tooa NIC met een statische of dynamische toewijzingsmethode Hallo. Dynamische IP-adressen kunnen wijzigen nadat het starten van een virtuele machine die in Hallo voorheen gestopt (toewijzing ongedaan gemaakt) staat. Dit kan mogelijk problemen veroorzaken als Hallo VM is een service die is vereist Hallo host hetzelfde IP-adres, zelfs na het opnieuw opstarten van gestopt (toewijzing ongedaan gemaakt). Statische IP-adressen worden bewaard totdat Hallo VM wordt verwijderd. Hallo toewijzingsmethode toochange van een IP-adres, Hallo na script, dat de toewijzingsmethode hello wordt gewijzigd van dynamische toostatic uitvoeren. Als de toewijzingsmethode Hallo voor Hallo huidige privé IP-adres statisch is, wijzigt *statische* te*dynamische* voordat Hallo script wordt uitgevoerd.

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

Als naam Hallo Hallo NIC kunt u niet weet, kunt u een lijst met NIC's binnen een resourcegroep weergeven door te voeren Hallo volgende opdracht:

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.
* Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.
* Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).

