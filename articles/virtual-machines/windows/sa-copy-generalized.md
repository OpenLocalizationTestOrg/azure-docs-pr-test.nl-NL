---
title: een installatiekopie van een niet-beheerde van een gegeneraliseerde virtuele machine in Azure aaaCreate | Microsoft Docs
description: Een unmanged installatiekopie maken van een gegeneraliseerde virtuele Windows-machine toouse toocreate meerdere exemplaren van een virtuele machine in Azure.
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Hoe toocreate een niet-beheerde virtuele machine een installatiekopie van een Azure VM

In dit artikel bevat informatie over met behulp van storage-accounts. Het is raadzaam dat u beheerde schijven en beheerde installatiekopieën in plaats van een opslagaccount gebruiken. Zie voor meer informatie [beheerde-installatiekopie van een gegeneraliseerde virtuele machine in Azure](capture-image-resource.md).

Dit artikel ziet u hoe toouse Azure PowerShell toocreate een installatiekopie van een gegeneraliseerde virtuele machine van Azure met behulp van een opslagaccount. U kunt een andere virtuele machine vervolgens Hallo installatiekopie toocreate. Hallo installatiekopie bevat Hallo besturingssysteemschijf en gegevensschijven Hallo die aangesloten toohello virtuele machine zijn. Hallo installatiekopie bevat geen virtuele Hallo-netwerkbronnen, dus moet u tooset van deze bronnen bij het maken van nieuwe virtuele machine Hallo. 

## <a name="prerequisites"></a>Vereisten
U moet Azure PowerShell-versie toohave 1.0.x of hoger zijn geïnstalleerd. Als u nog niet PowerShell hebt geïnstalleerd, leest u [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor de installatiestappen.

## <a name="generalize-hello-vm"></a>Hallo VM generalize 
Deze sectie leest u hoe toogeneralize uw Windows-machine voor gebruik als een afbeelding. Het generaliseren van een virtuele machine verwijdert alle persoonlijke gegevens over uw account, onder andere en bereidt Hallo machine toobe gebruikt als een installatiekopie. Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Zorg ervoor dat het Hallo-serverfuncties op Hallo machine worden ondersteund door Sysprep. Zie voor meer informatie [Sysprep-ondersteuning voor serverfuncties](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Als u uw VHD tooAzure voor Hallo eerst uploadt, controleert u of u hebt [uw virtuele machine voorbereid](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat Sysprep wordt uitgevoerd. 
> 
> 

U kunt ook een Linux-VM met generalize `sudo waagent -deprovision+user` en gebruik vervolgens PowerShell toocapture Hallo VM. Zie voor meer informatie over het gebruik van Hallo CLI toocapture een virtuele machine [hoe toogeneralize en vastleggen een Linux-virtuele machine met Azure CLI Hallo ](../linux/capture-image.md).


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

## <a name="log-in-tooazure-powershell"></a>Meld u bij tooAzure PowerShell
1. Open Azure PowerShell en meld tooyour Azure-account.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Een pop-upvenster wordt geopend voor tooenter u de referenties van uw Azure-account.
2. Hallo abonnement-id's voor uw beschikbare abonnementen ophalen.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Set Hallo juiste abonnement Hallo abonnement-id.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Hallo VM ongedaan en Hallo status toogeneralized instellen
1. Hallo VM netwerkbronnen ongedaan.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    Hallo *Status* voor Hallo VM in hello Azure portal wordt gewijzigd van **gestopt** te**gestopt (toewijzing opgeheven)**.
2. Hallo-status van Hallo virtuele machine te instellen**gegeneraliseerd**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Controleer de status van de Hallo Hallo VM. Hallo **OSState/gegeneraliseerd** sectie voor Hallo VM Hallo hebt **DisplayStatus** instellen te**VM is gegeneraliseerd**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Hallo installatiekopie maken

Maak een installatiekopie van een niet-beheerde virtuele machine in Hallo bestemming storage-container die u met deze opdracht. Hallo installatiekopie wordt gemaakt in Hallo hetzelfde opslagaccount als Hallo oorspronkelijke virtuele machine. Hallo `-Path` parameter slaat een kopie van Hallo JSON-sjabloon voor Hallo bron VM tooyour lokale computer. Hallo `-DestinationContainerName` parameter heet Hallo Hallo-container die u toohold uw afbeeldingen wilt. Als het Hallo-container bestaat niet, is het voor u gemaakt.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Hallo-URL van uw installatiekopie kunt u krijgen via Hallo JSON-bestandssjabloon. Ga toohello **resources** > **storageProfile** > **osDisk** > **installatiekopie**  >  **uri** sectie voor het volledige pad Hallo van uw installatiekopie. Hallo-URL van de afbeelding Hallo eruitziet: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
U kunt ook controleren Hallo URI in Hallo-portal. Hallo-installatiekopie is gekopieerde tooa container met de naam **system** in uw opslagaccount. 

## <a name="create-a-vm-from-hello-image"></a>Een virtuele machine uit Hallo installatiekopie maken

Nu kunt u een of meer VM's van niet-beheerde Hallo-installatiekopie.

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
Hallo volgende PowerShell wordt voltooid Hallo virtuele-machineconfiguraties en niet-beheerde installatiekopie als Hallo bron voor de nieuwe installatie Hallo gebruikt.

</br>

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

### <a name="verify-that-hello-vm-was-created"></a>Controleer of deze Hallo die VM is gemaakt
Wanneer voltooid, ziet u VM nieuw wordt gemaakt in Hallo Hallo [Azure-portal](https://portal.azure.com) onder **Bladeren** > **virtuele machines**, of met behulp van de volgende Hallo PowerShell-opdrachten:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Volgende stappen
toomanage uw nieuwe virtuele machine met Azure PowerShell, Zie [virtuele machines beheren met Azure Resource Manager en PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


