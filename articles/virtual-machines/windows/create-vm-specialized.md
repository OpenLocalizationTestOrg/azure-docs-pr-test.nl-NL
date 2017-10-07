---
title: een Windows-VM vanaf een speciale VHD in Azure aaaCreate | Microsoft Docs
description: Een nieuwe Windows VM maken door het koppelen van een gespecialiseerde beheerde schijf als besturingssysteemschijf Hallo met Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>Een virtuele Windows-machine maken van een gespecialiseerde schijf

Maak een nieuwe virtuele machine door het koppelen van een gespecialiseerde beheerde schijf als Hallo besturingssysteemschijf met behulp van Powershell. Een speciale schijf is een kopie van de virtuele harde schijf (VHD) van een bestaande virtuele machine die wordt onderhouden door Hallo gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM. 

Wanneer u een speciale VHD toocreate een nieuwe virtuele machine, Hallo Hallo nieuwe virtuele machine behoudt Hallo computernaam van de oorspronkelijke VM. Andere computer-specifieke informatie wordt ook opgeslagen en in sommige gevallen kan deze dubbele gegevens problemen kan veroorzaken. Zich bewust zijn van welke typen computerspecifieke informatie uw toepassingen afhankelijk zijn van bij het kopiëren van een virtuele machine.

U hebt hiervoor twee opties:
* [Een VHD uploaden](#option-1-upload-a-specialized-vhd)
* [Kopiëren van een bestaande virtuele machine in Azure](#option-2-copy-an-existing-azure-vm)

Dit onderwerp leest u hoe toouse schijven die worden beheerd. Als u een verouderde implementatie hebt waarvoor een opslagaccount gebruikt, Zie [een virtuele machine vanaf een speciale VHD in een opslagaccount maken](sa-create-vm-specialized.md)

## <a name="before-you-begin"></a>Voordat u begint
Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Optie 1: Een gespecialiseerde VHD uploaden

U kunt VHD van een speciale virtuele machine met een lokale virtualisatie hulpprogramma gemaakt, zoals Hyper-V of een virtuele machine die zijn geëxporteerd uit een andere cloud Hallo uploaden.

### <a name="prepare-hello-vm"></a>Hallo VM voorbereiden
Als u van plan toouse bent Hallo VHD-toocreate is een nieuwe virtuele machine, Controleer Hallo stappen zijn voltooid. 
  
  * [Voorbereiden van een Windows-VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Geen** generalize Hallo van virtuele machine met behulp van Sysprep.
  * Verwijder eventuele Gast virtualisatie-hulpprogramma's en de agents die zijn geïnstalleerd op Hallo VM (zoals VMware tools).
  * Zorg ervoor dat Hallo VM geconfigureerde toopull is het IP-adres en DNS-instellingen via DHCP. Dit zorgt ervoor dat Hallo-server verkrijgt IP-adres binnen Hallo VNet wanneer deze opgestart wordt. 


### <a name="get-hello-storage-account"></a>Hallo storage-account ophalen
U moet een opslag-account in Azure toostore Hallo VHD geüpload. U kunt een bestaand opslagaccount gebruiken of een nieuwe maken. 

tooshow hello beschikbaar storage-accounts, typt u:

```powershell
Get-AzureRmStorageAccount
```

Als u een bestaand opslagaccount toouse wilt, gaat u verder toohello [uploaden Hallo VHD](#upload-the-vhd-to-your-storage-account) sectie.

Als u een opslagaccount toocreate moet, volg deze stappen:

1. U moet Hallo-naam van resourcegroep Hallo waar Hallo storage-account moet worden gemaakt. toofind uit alle Hallo resourcegroepen in uw abonnement, type:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    een resourcegroep met de naam toocreate *myResourceGroup* in Hallo *VS-West* regio, type:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Maken van een opslagaccount met de naam *mystorageaccount* in deze resourcegroep via Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Hallo VHD tooyour storage-account uploaden 
Gebruik Hallo [toevoegen AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload Hallo VHD tooa container in uw opslagaccount. In dit voorbeeld uploads Hallo bestand *myVHD.vhd* van `"C:\Users\Public\Documents\Virtual hard disks\"` tooa opslagaccount met de naam *mystorageaccount* in Hallo *myResourceGroup* resourcegroep. Hallo-bestand wordt opgeslagen in het Hallo-container met de naam *mycontainer* en worden nieuwe bestandsnaam Hallo *myUploadedVHD.vhd*.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


Als dit lukt, kunt u een antwoord dat vergelijkbare toothis lijkt krijgen:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

Afhankelijk van uw netwerkverbinding en het Hallo-grootte van het VHD-bestand met deze opdracht kan een tijdje duren toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>Een beheerde schijf van Hallo VHD maken

Maken van een beheerde schijf vanuit Hallo VHD in uw storage-account met gespecialiseerde [nieuw AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). In dit voorbeeld wordt **myOSDisk1** voor schijfnaam hello, Hallo puts schijf in *StandardLRS* opslag en maakt gebruik van *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* zoals hello URI voor Hallo bron VHD.

Maak een nieuwe resourcegroep voor Hallo nieuwe virtuele machine.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Maken van nieuwe OS-schijf Hallo van Hallo VHD geüpload. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>Optie 2: Een bestaande virtuele machine van Azure kopiëren

U kunt een kopie van een virtuele machine dat maakt gebruik van schijven die worden beheerd door het maken van een momentopname van Hallo VM vervolgens met die toocreate momentopname van een nieuwe schijf- en een nieuwe virtuele machine beheerde maken.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Een momentopname van de besturingssysteemschijf Hallo

U kunt nemen een momentopname van en volledige virtuele machine (inclusief alle schijven) of van één schijf. Hallo volgende stappen ziet u hoe een momentopname van NET Hallo OS schijf van het gebruik van uw VM tootake Hallo [nieuw AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet. 

Sommige parameters instellen. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Hallo VM-object ophalen.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
De naam van de schijf Hallo OS ophalen.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Hallo momentopname configuratie maken. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Hallo momentopname.

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Als u van plan toouse Hallo momentopname toocreate een virtuele machine die behoeften toobe hoge prestaties bent, gebruikt u Hallo parameter `-AccountType Premium_LRS` met Hallo nieuw AzureRmSnapshot-opdracht. Hallo-parameter wordt Hallo momentopname gemaakt, zodat deze wordt opgeslagen als een schijf Premium beheerd. Premium-schijven beheerd zijn duurder dan de standaard. Dus wees zeker dat u echt Premium voordat u de parameter Hallo nodig hebt.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Een nieuwe schijf maken vanuit een momentopname Hallo

Maak een beheerde schijf van Hallo momentopname over met [nieuw AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). In dit voorbeeld wordt *myOSDisk* voor de naam van de schijf Hallo.

Maak een nieuwe resourcegroep voor Hallo nieuwe virtuele machine.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

De naam van de schijf Hallo OS ingesteld. 

```powershell
$osDiskName = 'myOsDisk'
```

Hallo-beheerde schijven maken.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>Maken van nieuwe virtuele machine Hallo 

Maken van netwerken en andere VM-resources toobe die wordt gebruikt door Hallo nieuwe virtuele machine.

### <a name="create-hello-subnet-and-vnet"></a>Hallo-subNet en een vNet maken

Hallo vNet en subNet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).

Hallo subNet maken. In dit voorbeeld wordt een subnet met de naam **mySubNet**, in de resourcegroep Hallo **myDestinationResourceGroup**, en stelt Hallo adresvoorvoegsel subnet te**10.0.0.0/24**.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Hallo vNet maken. In dit voorbeeld sets Hallo virtueel netwerk naam toobe **myVnetName**, locatie te Hallo**VS-West**, en het adresvoorvoegsel voor het virtuele netwerk hello te Hallo**10.0.0.0/16**. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Netwerkbeveiligingsgroep hello en een RDP-regel maken
toobe kunnen toolog in tooyour VM met RDP, moet u een regel waarmee RDP-toegang op poort 3389 toohave. Omdat hello VHD voor nieuwe virtuele machine is gemaakt vanuit een bestaande gespecialiseerde VM hello, kunt u een account van de virtuele bronmachine Hallo voor RDP.

In dit voorbeeld wordt de naam van het NSG te Hallo**myNsg** en Hallo RDP regelnaam te**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Zie voor meer informatie over eindpunten en NSG-regels [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="create-a-public-ip-address-and-nic"></a>Een openbaar IP-adres en NIC maken
tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.

Hallo openbare IP-adres maken. In dit voorbeeld Hallo naam openbare IP-adres te ingesteld**myIP**.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Hallo NIC. maken In dit voorbeeld Hallo NIC naam te is ingesteld**myNicName**.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Hallo VM-naam en de grootte instellen

In dit voorbeeld sets Hallo VM-naam te*myVM* en Hallo VM-grootte te*Standard_A2*.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Hallo NIC toevoegen
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Hallo OS-schijf toevoegen 

Toevoegen Hallo OS schijf toohello configuratie met behulp van [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk). Dit voorbeeld wordt ingesteld Hallo grootte van Hallo schijf te*128 GB* en wordt Hallo-beheerde schijven als een *Windows* besturingssysteemschijf.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>Hallo VM voltooien 

Maak Hallo-VM met [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)Hallo configuraties die we zojuist hebben gemaakt.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

Als deze opdracht voltooid is, ziet u uitvoer als volgt:

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Controleer of deze Hallo die VM is gemaakt
U ziet Hallo nieuw gemaakte VM in Hallo [Azure-portal](https://portal.azure.com)onder **Bladeren** > **virtuele machines**, of met behulp van de volgende PowerShell Hallo opdrachten:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>Volgende stappen
toosign in tooyour nieuwe virtuele machine, bladeren toohello VM in Hallo [portal](https://portal.azure.com), klikt u op **Connect**, en open Hallo Remote Desktop RDP-bestand. Gebruik de accountreferenties op Hallo van uw oorspronkelijke toosign van de virtuele machine in tooyour nieuwe virtuele machine. Zie voor meer informatie [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md).

