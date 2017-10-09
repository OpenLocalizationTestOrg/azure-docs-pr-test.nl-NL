---
title: een VHD generalize toocreate aaaUpload meerdere virtuele machines in Azure | Microsoft Docs
description: Upload een gegeneraliseerde VHD tooan Azure storage-account toocreate een virtuele machine van Windows-toouse met Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a>Uploaden van een gegeneraliseerde VHD tooAzure toocreate een nieuwe virtuele machine

In dit onderwerp bevat informatie over het uploaden van een gegeneraliseerde onbeheerde schijf tooa storage-account en maak vervolgens een nieuwe virtuele machine met Hallo geüpload schijf. Een algemene VHD-installatiekopie heeft al uw persoonlijke accountgegevens verwijderd met behulp van Sysprep. 

Als u een virtuele machine vanaf een speciale VHD in een opslagaccount toocreate wilt, Zie [een virtuele machine maken vanaf een speciale VHD](sa-create-vm-specialized.md).

In dit onderwerp worden met behulp van storage-accounts, maar we raden klanten toousing beheerd schijven in plaats daarvan verplaatsen. Zie voor een volledig overzicht van hoe tooprepare, uploaden en maak een nieuwe virtuele machine met schijven die worden beheerd, [Maak een nieuwe virtuele machine uit een gegeneraliseerde VHD geüpload tooAzure schijven beheerd](upload-generalized-managed.md).



## <a name="prepare-hello-vm"></a>Hallo VM voorbereiden

Een gegeneraliseerde VHD heeft al uw persoonlijke accountgegevens verwijderd met behulp van Sysprep. Als u van plan toouse Hallo VHD als een installatiekopie toocreate bent nieuwe virtuele machines van moet:
  
  * [Voorbereiden van een Windows-VHD tooupload tooAzure](prepare-for-upload-vhd-image.md). 
  * Hallo virtuele machine met behulp van Sysprep generalize

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>Een virtuele Windows-machine met behulp van Sysprep generalize
Deze sectie leest u hoe toogeneralize uw Windows-machine voor gebruik als een afbeelding. Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en bereidt Hallo machine toobe gebruikt als een installatiekopie. Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Zorg ervoor dat het Hallo-serverfuncties op Hallo machine worden ondersteund door Sysprep. Zie voor meer informatie [Sysprep-ondersteuning voor serverfuncties](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Als u Sysprep voordat u uploadt uw VHD tooAzure voor Hallo eerst uitvoert, controleert u of u hebt [uw virtuele machine voorbereid](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat Sysprep wordt uitgevoerd. 
> 
> 

1. Meld u aan toohello virtuele Windows-computer.
2. Hallo-opdrachtpromptvenster open als beheerder. Hallo directory ook wijzigen**%windir%\system32\sysprep**, en voer vervolgens `sysprep.exe`.
3. In Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster, **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat Hallo **Generalize** selectievakje is ingeschakeld.
4. In **afsluitopties**, selecteer **afsluiten**.
5. Klik op **OK**.
   
    ![Sysprep starten](./media/upload-generalized-managed/sysprepgeneral.png)
6. Wanneer Sysprep is voltooid, afgesloten Hallo virtuele machine. 

> [!IMPORTANT]
> Hallo VM niet opnieuw opstarten nadat u bent gereed uploaden Hallo VHD tooAzure of maken van een afbeelding van Hallo VM. Als Hallo VM per ongeluk opnieuw opgestart wordt, voert u Sysprep toogeneralize deze opnieuw.
> 
> 


## <a name="upload-hello-vhd"></a>Hallo VHD uploaden

Hallo VHD tooan Azure storage-account uploaden.

### <a name="log-in-tooazure"></a>Meld u bij tooAzure
Als er geen PowerShell-versie 1.4 al of hoger is geïnstalleerd, lezen [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

1. Open Azure PowerShell en meld tooyour Azure-account. Een pop-upvenster wordt geopend voor tooenter u de referenties van uw Azure-account.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Hallo abonnement-id's voor uw beschikbare abonnementen ophalen.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Set Hallo juiste abonnement Hallo abonnement-id. Vervang `<subscriptionID>` corrigeren abonnement met de Hallo Hallo-ID.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a>Hallo storage-account ophalen
U moet een opslagaccount in Azure toostore Hallo geüpload VM-installatiekopie. U kunt een bestaand opslagaccount gebruiken of een nieuwe maken. 

tooshow hello beschikbaar storage-accounts, typt u:

```powershell
Get-AzureRmStorageAccount
```

Als u een bestaand opslagaccount toouse wilt, gaat u verder toohello [Hallo VM-installatiekopie uploaden](#upload-the-vm-vhd-to-your-storage-account) sectie.

Als u een opslagaccount toocreate moet, volg deze stappen:

1. U moet Hallo-naam van resourcegroep Hallo waar Hallo storage-account moet worden gemaakt. toofind uit alle Hallo resourcegroepen in uw abonnement, type:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    een resourcegroep met de naam toocreate **myResourceGroup** in Hallo **VS-West** regio, type:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Maken van een opslagaccount met de naam **mystorageaccount** in deze resourcegroep via Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a>Hallo uploaden starten 

Gebruik Hallo [toevoegen AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload Hallo installatiekopie tooa container in uw opslagaccount. In dit voorbeeld uploads Hallo bestand **myVHD.vhd** van `"C:\Users\Public\Documents\Virtual hard disks\"` tooa opslagaccount met de naam **mystorageaccount** in Hallo **myResourceGroup** resourcegroep. Hallo-bestand worden opgenomen in het Hallo-container met de naam **mycontainer** en worden nieuwe bestandsnaam Hallo **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
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

Afhankelijk van uw netwerkverbinding en het Hallo-grootte van het VHD-bestand met deze opdracht kan een tijdje duren toocomplete.


## <a name="create-a-new-vm"></a>Een nieuwe virtuele machine maken 

U kunt nu gebruik Hallo geüpload VHD toocreate een nieuwe virtuele machine. 

### <a name="set-hello-uri-of-hello-vhd"></a>Hallo-URI van Hallo VHD instellen

Hallo URI voor Hallo VHD toouse heeft Hallo indeling: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**VHD. In dit voorbeeld Hallo VHD met de naam **myVHD** is in het opslagaccount hello **mystorageaccount** in Hallo container **mycontainer**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Een virtueel netwerk maken
Hallo vNet en subnet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).

1. Hallo subnet maken. Hallo volgende voorbeeld maakt u een subnet met de naam **mySubnet** in de resourcegroep Hallo **myResourceGroup** met het Hallo-adresvoorvoegsel van **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Hallo virtueel netwerk maken. Hallo volgende voorbeeld maakt u een virtueel netwerk met de naam **myVnet** in Hallo **VS-West** locatie met het Hallo-adresvoorvoegsel van **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Een openbaar IP-adres en een netwerkinterface maken
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

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Netwerkbeveiligingsgroep hello en een RDP-regel maken
toobe kunnen toolog in tooyour VM met RDP, moet u een regel waarmee RDP-toegang op poort 3389 toohave. 

In dit voorbeeld maakt u een NSG met de naam **myNsg** die een regel aangeroepen bevat **myRdpRule** waarmee RDP-verkeer via poort 3389. Zie voor meer informatie over Nsg [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Een variabele voor Hallo virtueel netwerk maken
Maak een variabele voor het virtuele netwerk Hallo voltooid. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Hallo VM maken
Hallo toont volgende PowerShell-script hoe tooset Hallo virtuele-machineconfiguraties en gebruik Hallo VM-installatiekopie als bron voor de nieuwe installatie Hallo Hallo geüpload.



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a>Controleer of deze Hallo die VM is gemaakt
Wanneer voltooid, ziet u VM nieuw wordt gemaakt in Hallo Hallo [Azure-portal](https://portal.azure.com) onder **Bladeren** > **virtuele machines**, of met behulp van de volgende Hallo PowerShell-opdrachten:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Volgende stappen
toomanage uw nieuwe virtuele machine met Azure PowerShell, Zie [virtuele machines beheren met Azure Resource Manager en PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


