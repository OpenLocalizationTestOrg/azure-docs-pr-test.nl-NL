---
title: aaaCreate VM vanaf een speciale schijf in Azure | Microsoft Docs
description: Maak een nieuwe virtuele machine door het koppelen van een gespecialiseerde onbeheerde schijf Hallo Resource Manager-implementatiemodel.
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>Een virtuele machine vanaf een speciale VHD in een opslagaccount maken

Maak een nieuwe virtuele machine door het koppelen van een gespecialiseerde onbeheerde schijf als Hallo besturingssysteemschijf met behulp van Powershell. Een speciale schijf is een kopie van de VHD van een bestaande virtuele machine die wordt onderhouden door Hallo gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM. 

U hebt hiervoor twee opties:
* [Een VHD uploaden](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [Kopieer Hallo VHD van een bestaande virtuele machine in Azure](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>Voordat u begint
Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt. Voer Hallo na de opdracht tooinstall deze.

```powershell
Install-Module AzureRM.Compute 
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Optie 1: Een gespecialiseerde VHD uploaden

U kunt VHD van een speciale virtuele machine met een lokale virtualisatie hulpprogramma gemaakt, zoals Hyper-V of een virtuele machine die zijn geëxporteerd uit een andere cloud Hallo uploaden.

### <a name="prepare-hello-vm"></a>Hallo VM voorbereiden
U kunt een gespecialiseerde VHD die is gemaakt met een lokale virtuele machine of een VHD die is geëxporteerd uit een andere cloud uploaden. Een speciale VHD onderhoudt Hallo gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM. Als u van plan toouse bent Hallo VHD-toocreate is een nieuwe virtuele machine, Controleer Hallo stappen zijn voltooid. 
  
  * [Voorbereiden van een Windows-VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Geen** generalize Hallo van virtuele machine met behulp van Sysprep.
  * Verwijder eventuele Gast virtualisatie-hulpprogramma's en de agents die zijn geïnstalleerd op Hallo VM (dat wil zeggen VMware tools).
  * Zorg ervoor dat Hallo VM geconfigureerde toopull is het IP-adres en DNS-instellingen via DHCP. Dit zorgt ervoor dat Hallo-server verkrijgt IP-adres binnen Hallo VNet wanneer deze opgestart wordt. 


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
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>Hallo VHD tooyour storage-account uploaden
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


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>Optie 2: Kopieer Hallo VHD van een bestaande virtuele machine in Azure

Bij het maken van een nieuwe, dubbele virtuele machine, kunt u een VHD tooanother storage account toouse kopiëren.

### <a name="before-you-begin"></a>Voordat u begint
Zorg ervoor dat u:

* Informatie over Hallo **bron- en storage-accounts**. Hallo bron-VM moet u toohave Hallo storage-account en de container namen. Normaal gesproken Hallo containernaam worden **VHD's**. U moet ook een doelopslagaccount toohave. Als u dit niet al hebt, kunt u een met een van de portals hello (**meer Services** > opslagaccounts > toevoegen) of met behulp van Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet. 
* Hebt gedownload en geïnstalleerd Hallo [AzCopy hulpprogramma](../../storage/common/storage-use-azcopy.md). 

### <a name="deallocate-hello-vm"></a>Hallo VM ongedaan gemaakt
Toewijzing Hallo virtuele machine vrijgemaakt Hallo VHD toobe gekopieerd wordt. 

* **Portal**: klik op **virtuele machines** > **myVM** > stoppen
* **PowerShell**: Gebruik [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (ongedaan gemaakt) met de naam VM Hallo **myVM** in de resourcegroep **myResourceGroup**.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Hallo **Status** voor Hallo VM in hello Azure portal wordt gewijzigd van **gestopt** te**gestopt (toewijzing opgeheven)**.

### <a name="get-hello-storage-account-urls"></a>Hallo storage-account-URL's ophalen
U moet Hallo-URL's van Hallo bron- en storage-accounts. Hallo URL er als volgt uitzien: `https://<storageaccount>.blob.core.windows.net/<containerName>/`. Als u al Hallo-account en de container Opslagnaam weet, kunt u zojuist hebt vervangen Hallo informatie tussen Hallo haken toocreate uw URL. 

U kunt hello Azure-portal of Azure Powershell tooget Hallo URL gebruiken:

* **Portal**: klik op Hallo  **>**  voor **meer services** > **opslagaccounts**  >   *Storage-account* > **Blobs** en de bron-VHD-bestand is waarschijnlijk in Hallo **VHD's** container. Klik op **eigenschappen** voor Hallo-container en de tekst hello kopiëren met het label **URL**. U moet Hallo-URL's van beide Hallo bron- en doelserver containers. 
* **PowerShell**: Gebruik [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget Hallo-informatie voor de virtuele machine met de naam **myVM** in de resourcegroep Hallo **myResourceGroup**. Hallo-resultaten, kijk in Hallo **archiefprofiel** sectie voor Hallo **Vhd-Uri**. Hallo eerste deel van Hallo Uri is Hallo URL toohello container en het laatste deel Hallo is Hallo OS VHD-naam voor Hallo VM.

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>Hallo opslagtoegangssleutels ophalen
Hallo toegangstoetsen voor Hallo bron- en storage-accounts gevonden. Zie voor meer informatie over toegangstoetsen [over Azure storage-accounts](../../storage/common/storage-create-storage-account.md).

* **Portal**: klik op **meer services** > **opslagaccounts** > *opslagaccount*  >  **Toegangssleutels**. Kopiëren Hallo sleutel aangeduid als **key1**.
* **PowerShell**: Gebruik [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget Hallo-opslagsleutel voor opslagaccount hello **mystorageaccount** in de resourcegroep Hallo  **myResourceGroup**. Kopiëren Hallo sleutel met het label **key1**.

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>Hallo VHD kopiëren
U kunt bestanden kopiëren tussen opslagaccounts met behulp van AzCopy. Voor de doelcontainer hello, als de opgegeven container Hallo niet bestaat, zal deze worden voor u gemaakt. 

toouse AzCopy, open een opdrachtprompt op uw lokale machine en navigeer toohello-map waarin AzCopy is geïnstalleerd. Deze lijken te*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*. 

toocopy alle Hallo bestanden binnen een container, gebruikt u Hallo **/S** overschakelen. Dit kan gebruikte toocopy Hallo OS VHD en alle Hallo gegevensschijven als ze in dezelfde container Hallo. Dit voorbeeld ziet u hoe alle Hallo bestanden in de container Hallo toocopy **mysourcecontainer** in opslagaccount **mysourcestorageaccount** toohello container **mydestinationcontainer**  in Hallo **mydestinationstorageaccount** storage-account. Hallo-namen van opslagaccounts hello en containers vervangen door uw eigen. Vervang `<sourceStorageAccountKey1>` en `<destinationStorageAccountKey1>` met uw eigen sleutels.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

Als u wilt dat alleen toocopy een specifieke VHD in een container met meerdere bestanden, kunt u ook Hallo bestandsnaam met Hallo /Pattern switch opgeven. In dit voorbeeld bestand met de naam alleen Hallo **myFileName.vhd** worden gekopieerd.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


Als dit is voltooid, ontvangt u een bericht dat ongeveer als volgt uitziet:

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>Problemen oplossen
* Wanneer u met AZCopy, als er een fout Hallo 'Server is mislukt tooauthenticate Hallo aanvraag', zorg er dan voor dat Hallo-waarde van de autorisatie-header Hallo correct inclusief Hallo handtekening is samengesteld. Als u sleutel 2 of Hallo secundaire opslagsleutel gebruikt, probeert u de primaire of 1e opslagsleutel Hallo.

## <a name="create-hello-new-vm"></a>Maken van nieuwe virtuele machine Hallo 

U moet toocreate netwerken en andere VM-resources toobe die wordt gebruikt door Hallo nieuwe virtuele machine.

### <a name="create-hello-subnet-and-vnet"></a>Hallo-subNet en een vNet maken

Hallo vNet en subNet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).

1. Hallo subNet maken. In dit voorbeeld wordt een subnet met de naam **mySubNet**, in de resourcegroep Hallo **myResourceGroup**, en stelt Hallo adresvoorvoegsel subnet te**10.0.0.0/24**.
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Hallo vNet maken. In dit voorbeeld sets Hallo virtueel netwerk naam toobe **myVnetName**, locatie te Hallo**VS-West**, en het adresvoorvoegsel voor het virtuele netwerk hello te Hallo**10.0.0.0/16**. 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>Een openbaar IP-adres en NIC maken
tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.

1. Hallo openbare IP-adres maken. In dit voorbeeld Hallo naam openbare IP-adres te ingesteld**myIP**.
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Hallo NIC. maken In dit voorbeeld Hallo NIC naam te is ingesteld**myNicName**.
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Netwerkbeveiligingsgroep hello en een RDP-regel maken
toobe kunnen toolog in tooyour VM met RDP, moet u toohave een beveiligingsregel waarmee op poort 3389 van RDP-toegang. Omdat Hallo VHD voor de nieuwe virtuele machine is gemaakt van een bestaand Hallo gespecialiseerde kunt VM, nadat Hallo VM is gemaakt, moet u een bestaand account van Hallo virtuele bronmachine die machtiging toolog over het gebruik van RDP had gebruiken.
In dit voorbeeld wordt de naam van het NSG te Hallo**myNsg** en Hallo RDP regelnaam te**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Zie voor meer informatie over eindpunten en NSG-regels [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="set-hello-vm-name-and-size"></a>Hallo VM-naam en de grootte instellen

In dit voorbeeld sets Hallo VM-naam te 'myVM' en Hallo VM grootte te 'Standard_A2'.
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Hallo NIC toevoegen
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>Configureer Hallo OS-schijf

1. Stel Hallo URI voor Hallo VHD die u hebt geüpload of gekopieerd. In dit voorbeeld Hallo VHD-bestand met de naam **myOsDisk.vhd** wordt opgeslagen in een opslagaccount met de naam **myStorageAccount** in een container met de naam **myContainer**.

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. Hallo OS-schijf toevoegen. Wanneer Hallo besturingssysteemschijf is gemaakt, is osDisk' hello term' in dit voorbeeld appened toohello VM naam toocreate Hallo naam Besturingssysteemschijf. In dit voorbeeld geeft ook dat deze VHD op basis van Windows gekoppelde toohello VM als Hallo OS-schijf moet worden.
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

Optioneel: Als u gegevensschijven hebt die moeten toobe gekoppeld toohello VM en voeg Hallo gegevensschijven met behulp van URL's van gegevens VHD's Hallo Hallo juiste Logical Unit Number (Lun).

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

Wanneer u een opslagaccount, Hallo gegevens en URL's van besturingssysteem schijf als volgt uitzien: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`. U kunt dit vinden op Hallo portal door bladeren toohello doel storage-container, klikt u op Hallo besturingssysteem of gegevens VHD die is gekopieerd en vervolgens inhoud Hallo van Hallo-URL te kopiëren.


### <a name="complete-hello-vm"></a>Hallo VM voltooien 

Maak Hallo VM die gebruikmaakt van Hallo-configuraties die we zojuist hebben gemaakt.

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
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
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>Volgende stappen
toosign in tooyour nieuwe virtuele machine, bladeren toohello VM in Hallo [portal](https://portal.azure.com), klikt u op **Connect**, en open Hallo Remote Desktop RDP-bestand. Gebruik de accountreferenties op Hallo van uw oorspronkelijke toosign van de virtuele machine in tooyour nieuwe virtuele machine. Zie voor meer informatie [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md).

