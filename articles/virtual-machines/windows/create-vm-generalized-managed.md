---
title: aaaCreate VM vanaf een beheerde VM-installatiekopie in Azure | Microsoft Docs
description: Een virtuele Windows-machine maken van een algemene beheerde VM installatiekopie met behulp van Azure PowerShell Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Een virtuele machine maken van een begeleide afbeelding

U kunt meerdere virtuele machines maken in een beheerde VM-installatiekopie in Azure. Een beheerde VM-installatiekopie bevat Hallo informatie een virtuele machine, met inbegrip van het besturingssysteem en gegevensschijven Hallo toocreate nodig. Hallo virtuele harde schijven die gezamenlijk Hallo afbeelding, inclusief zowel Hallo OS-schijven en eventuele gegevensschijven, als beheerde schijven zijn opgeslagen. 


## <a name="prerequisites"></a>Vereisten

Moet u toohave al [gemaakt van een beheerde VM-installatiekopie](capture-image-resource.md) toouse voor het maken van nieuwe virtuele machine Hallo. 

Zorg ervoor dat u beschikt over de nieuwste versies Hallo Hallo AzureRM.Compute en AzureRM.Network PowerShell-modules. Open een PowerShell een opdrachtprompt als beheerder en Voer Hallo opdracht tooinstall na deze.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).



## <a name="collect-information-about-hello-image"></a>Informatie over de installatiekopie Hallo verzamelen

Eerst we moet toogather basisinformatie over de installatiekopie van het Hallo en een variabele voor de installatiekopie van het Hallo maken. In dit voorbeeld wordt een beheerde VM-installatiekopie met de naam **myImage** die in Hallo **myResourceGroup** resourcegroep in Hallo **West-Centraal VS** locatie. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Een virtueel netwerk maken
Hallo vNet en subnet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).

1. Hallo subnet maken. In dit voorbeeld wordt een subnet met de naam **mySubnet** met het Hallo-adresvoorvoegsel van **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Hallo virtueel netwerk maken. In dit voorbeeld wordt een virtueel netwerk met de naam **myVnet** met het Hallo-adresvoorvoegsel van **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Een openbaar IP-adres en een netwerkinterface maken

tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.

1. Een openbaar IP-adres maken. In dit voorbeeld wordt een openbaar IP-adres met de naam **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Hallo NIC. maken In dit voorbeeld wordt een NIC met de naam **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Netwerkbeveiligingsgroep hello en een RDP-regel maken

toobe kunnen toolog in tooyour VM met RDP, moet u toohave een netwerkbeveiligingsregel (NSG) waarmee op poort 3389 van RDP-toegang. 

In dit voorbeeld maakt u een NSG met de naam **myNsg** die een regel aangeroepen bevat **myRdpRule** waarmee RDP-verkeer via poort 3389. Zie voor meer informatie over Nsg [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Een variabele voor Hallo virtueel netwerk maken

Maak een variabele voor het virtuele netwerk Hallo voltooid. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Hallo-referenties voor Hallo VM ophalen

Hallo wordt volgende cmdlet een venster geopend waarin u een nieuwe gebruiker-naam en het wachtwoord toouse Hallo lokale administrator-account wordt invoeren voor toegang op afstand tot Hallo VM. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Set variabelen voor Hallo VM naam, computernaam en grootte van Hallo VM Hallo

1. Variabelen voor Hallo VM-naam en de naam van computer maken. Dit voorbeeld wordt Hallo VM-naam als **myVM** en Hallo-computernaam als **computer**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Hallo-grootte van Hallo virtuele machine instellen. In dit voorbeeld maakt **Standard_DS1_v2** grootte van de virtuele machine. Zie Hallo [VM-grootten](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentatie voor meer informatie.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Hallo VM-naam en de grootte van toohello VM-configuratie toevoegen.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Set Hallo VM-installatiekopie als bronafbeelding voor Hallo nieuwe virtuele machine

Stel broninstallatiekopie Hallo Hallo-id van VM-installatiekopie Hallo beheerd.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Configuratie van het besturingssysteem Hallo en toevoegen van Hallo NIC.

Hallo opslagtype (PremiumLRS of StandardLRS) en het Hallo-grootte van de besturingssysteemschijf Hallo invoeren. In dit voorbeeld wordt het accounttype hello te**PremiumLRS**, schijfgrootte te Hallo**128 GB** en schijfcache te**ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Hallo VM maken

Maken van nieuwe virtuele machine met behulp van Hallo-configuratie die we hebben gemaakt en opgeslagen in Hallo Hallo **$vm** variabele.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Controleer of deze Hallo die VM is gemaakt
Wanneer voltooid, ziet u VM nieuw wordt gemaakt in Hallo Hallo [Azure-portal](https://portal.azure.com) onder **Bladeren** > **virtuele machines**, of met behulp van de volgende Hallo PowerShell-opdrachten:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Volgende stappen
toomanage uw nieuwe virtuele machine met Azure PowerShell, Zie [maken en beheren van Windows-VM's met Azure PowerShell-module Hallo](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

