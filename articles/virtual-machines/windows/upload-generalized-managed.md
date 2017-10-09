---
title: een beheerde Azure-virtuele machine vanaf een VHD gegeneraliseerde lokale aaaCreate | Microsoft Docs
description: Uploaden van een gegeneraliseerde VHD tooAzure en gebruik deze toocreate nieuwe virtuele machines in Hallo Resource Manager-implementatiemodel.
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>Een gegeneraliseerde VHD uploaden en gebruik deze toocreate nieuwe virtuele machines in Azure

In dit onderwerp leert u met behulp van PowerShell tooupload een VHD van een gegeneraliseerde VM tooAzure, een installatiekopie van Hallo VHD maken en een nieuwe virtuele machine maken vanuit die installatiekopie. U kunt een VHD die is geëxporteerd vanuit een hulpprogramma voor het virtualisatie lokale of vanuit een andere cloud uploaden. Met behulp van [schijven beheerd](managed-disks-overview.md) voor Hallo nieuwe virtuele machine vereenvoudigt het beheer van Hallo-VM en zorgt voor betere beschikbaarheid als Hallo VM wordt geplaatst in een beschikbaarheidsset. 

Als u een voorbeeldscript toouse wilt, Zie [Sample script tooupload een VHD-tooAzure en maak een nieuwe virtuele machine](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>Voordat u begint

- Voordat u een VHD-tooAzure uploadt, u moet volgen [voorbereiden van een Windows-VHD of VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- Bekijk [Hallo-migratie plannen tooManaged schijven](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) voordat u uw migratie te[schijven beheerd](managed-disks-overview.md).
- Zorg ervoor dat u beschikt over de nieuwste versie van de Hallo Hallo AzureRM.Compute PowerShell-module. Voer Hallo na de opdracht tooinstall deze.

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalize Hallo van virtuele machine van Windows met behulp van Sysprep

Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en bereidt Hallo machine toobe gebruikt als een installatiekopie. Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).

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
6. Wanneer Sysprep is voltooid, afgesloten Hallo virtuele machine. Hallo VM niet opnieuw.



## <a name="log-in-tooazure"></a>Meld u bij tooAzure
Als er geen PowerShell-versie 1.4 al of hoger is geïnstalleerd, lezen [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

1. Open Azure PowerShell en meld tooyour Azure-account. Een pop-upvenster wordt geopend voor tooenter u de referenties van uw Azure-account.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Hallo abonnement-id's voor uw beschikbare abonnementen ophalen.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Set Hallo juiste abonnement Hallo abonnement-id. Vervang  *<subscriptionID>*  corrigeren abonnement met de Hallo Hallo-ID.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>Hallo storage-account ophalen
U moet een opslagaccount in Azure toostore Hallo geüpload VM-installatiekopie. U kunt een bestaand opslagaccount gebruiken of een nieuwe maken. 

Als u Hallo VHD toocreate een beheerde schijf voor een virtuele machine gebruikt, moet Hallo opslagaccountlocatie dezelfde Hallo locatie waar u Hallo VM maakt.

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

    een resourcegroep met de naam toocreate **myResourceGroup** in Hallo **VS-Oost** regio, type:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. Maken van een opslagaccount met de naam **mystorageaccount** in deze resourcegroep via Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    Geldige waarden voor - SkuName zijn:
   
   * **Standard_LRS** -lokaal redundante opslag. 
   * **Standard_ZRS** -Zone-redundante opslag.
   * **Standard_GRS** -geografisch redundante opslag. 
   * **Standard_RAGRS** -geografisch redundante opslag met leestoegang. 
   * **Premium_LRS** -Premium lokaal redundante opslag. 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>Hallo VHD tooyour storage-account uploaden

Gebruik Hallo [toevoegen AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload Hallo VHD tooa container in uw opslagaccount. In dit voorbeeld uploads Hallo bestand *myVHD.vhd* van *' C:\Users\Public\Documents\Virtual harde schijven\"*  tooa opslagaccount met de naam *mystorageaccount*in Hallo *myResourceGroup* resourcegroep. Hallo-bestand worden opgenomen in het Hallo-container met de naam *mycontainer* en worden nieuwe bestandsnaam Hallo *myUploadedVHD.vhd*.

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

Afhankelijk van uw netwerkverbinding en het Hallo-grootte van het VHD-bestand met deze opdracht kan een tijdje duren toocomplete

Hallo opslaan **bestemmings-URI** pad toouse later als u een beheerde schijf toocreate gaat of een nieuwe virtuele machine met behulp van Hallo VHD geüpload.

### <a name="other-options-for-uploading-a-vhd"></a>Andere opties voor het uploaden van een VHD
 
 
U kunt ook een VHD tooyour storage-account met behulp van een van de volgende Hallo uploaden:

- [AzCopy](http://aka.ms/downloadazcopy)
- [API voor Azure Storage kopiëren-Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Azure Storage Explorer uploaden van BLOB 's](https://azurestorageexplorer.codeplex.com/)
- [Opslag voor importeren/exporteren Service REST API-verwijzing](https://msdn.microsoft.com/library/dn529096.aspx)
-   U kunt het beste Import/Export-Service gebruikt als de geschatte tijd uploaden is langer dan zeven dagen. U kunt [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate Hallo tijd van de grootte en de overdracht van gegevenseenheid. 
    Import/Export kan worden gebruikt toocopy tooa standard-opslagaccount. U moet toocopy van standaardopslag toopremium storage-account met behulp van een hulpprogramma zoals AzCopy.


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>Maak een beheerde afbeelding van Hallo VHD geüpload 

Maak een begeleide afbeelding met behulp van uw algemene besturingssysteem-VHD. Hallo waarden vervangt door uw eigen gegevens.


1.  Stel eerst Hallo algemene parameters:

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  Hallo-installatiekopie met behulp van uw algemene besturingssysteem-VHD maken.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>Een virtueel netwerk maken
Hallo vNet en subnet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).

1. Hallo subnet maken. In dit voorbeeld wordt een subnet met de naam *mySubnet* met het Hallo-adresvoorvoegsel van *10.0.0.0/24*.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Hallo virtueel netwerk maken. In dit voorbeeld wordt een virtueel netwerk met de naam *myVnet* met het Hallo-adresvoorvoegsel van *10.0.0.0/16*.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Een openbaar IP-adres en een netwerkinterface maken

tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.

1. Een openbaar IP-adres maken. In dit voorbeeld wordt een openbaar IP-adres met de naam *myPip*. 
   
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

In dit voorbeeld maakt u een NSG met de naam *myNsg* die een regel aangeroepen bevat *myRdpRule* waarmee RDP-verkeer via poort 3389. Zie voor meer informatie over Nsg [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

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

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>Hallo VM-naam en de grootte van toohello VM-configuratie toevoegen.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Set Hallo VM-installatiekopie als bronafbeelding voor Hallo nieuwe virtuele machine

Stel broninstallatiekopie Hallo Hallo-id van VM-installatiekopie Hallo beheerd.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Configuratie van het besturingssysteem Hallo en toevoegen van Hallo NIC.

Hallo opslagtype (PremiumLRS of StandardLRS) en het Hallo-grootte van de besturingssysteemschijf Hallo invoeren. In dit voorbeeld wordt het accounttype hello te*PremiumLRS*, schijfgrootte te Hallo*128 GB* en schijfcache te*ReadWrite*.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Hallo VM maken

Maken van nieuwe virtuele machine met behulp van Hallo-configuratie is opgeslagen in Hallo Hallo **$vm** variabele.

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

toosign in tooyour nieuwe virtuele machine, bladeren toohello VM in Hallo [portal](https://portal.azure.com), klikt u op **Connect**, en open Hallo Remote Desktop RDP-bestand. Gebruik de accountreferenties op Hallo van uw oorspronkelijke toosign van de virtuele machine in tooyour nieuwe virtuele machine. Zie voor meer informatie [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

