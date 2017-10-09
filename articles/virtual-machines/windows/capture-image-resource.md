---
title: aaaCreate een begeleide afbeelding in Azure | Microsoft Docs
description: "Maak een begeleide afbeelding van een gegeneraliseerde virtuele machine of VHD in Azure. Installatiekopieën van het gebruikte toocreate meerdere virtuele machines die gebruikmaken van beheerde schijven kan worden."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Maken van een begeleide afbeelding van een gegeneraliseerde virtuele machine in Azure

Een beheerde Afbeeldingsbron kan worden gemaakt vanuit een gegeneraliseerde virtuele machine die wordt opgeslagen als een beheerde schijf of een niet-beheerde schijf in een opslagaccount. Hallo installatiekopie kan vervolgens worden de gebruikte toocreate meerdere virtuele machines. 


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


## <a name="create-a-managed-image-in-hello-portal"></a>Maken van een begeleide afbeelding in Hallo-portal 

1. Open Hallo [portal](https://portal.azure.com).
2. Klik op Hallo plusteken toocreate een nieuwe resource.
3. Typ in Hallo filter zoeken **installatiekopie**.
4. Selecteer **installatiekopie** uit Hallo resultaten.
5. In Hallo **installatiekopie** blade, klikt u op **maken**.
6. In **naam**, typ een naam voor het Hallo-installatiekopie.
7. Als u meer dan één abonnement hebt, selecteer juiste paneel van Hallo Hallo **abonnement** vervolgkeuzelijst.
7. In **resourcegroep** select **nieuw** en typ een naam in of selecteer **uit bestaande** en selecteert u een groep resource toouse in de vervolgkeuzelijst Hallo.
8. In **locatie**, kies Hallo-locatie van de resourcegroep.
9. In **type besturingssysteem** Hallo-type van Windows of Linux-besturingssysteem selecteert.
11. In **Storage-blob**, klikt u op **Bladeren** toolook voor Hallo VHD in uw Azure-opslag.
12. In **accounttype** Standard_LRS of Premium_LRS kiezen. Standaard harde schijven en Premium SSD-schijven gebruikt. Beide lokaal redundante opslag gebruiken.
13. In **schijfcache** Selecteer Hallo geschikte schijf opslaan in cache optie. Hallo-opties zijn **geen**, **alleen-lezen** en **alleen-lezen**.
14. Optioneel: U kunt ook een bestaande gegevens schijf toohello afbeelding toevoegen door te klikken op **+ gegevensschijf toevoegen**.  
15. Wanneer u klaar bent u deze hebt geselecteerd, klikt u op **maken**.
16. Nadat het Hallo-installatiekopie is gemaakt, ziet u dit als een **installatiekopie** resource in Hallo lijst met resources in Hallo-resourcegroep die u hebt gekozen.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Maken van een begeleide afbeelding van een virtuele machine met behulp van Powershell

Het maken van een installatiekopie van een rechtstreeks vanuit Hallo die VM zorgt ervoor dat Hallo-installatiekopie bevat alle Hallo schijven die zijn gekoppeld aan virtuele machine, met inbegrip van Hallo Besturingssysteemschijf en alle gegevensschijven Hallo.


Voordat u begint, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt. Voer Hallo na de opdracht tooinstall deze.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).


1. Sommige variabelen maken.

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. Zorg ervoor dat Hallo die VM is opgeheven.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Hallo-status van Hallo virtuele machine te instellen**gegeneraliseerd**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Hallo virtuele machine worden opgehaald. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Hallo imageconfiguratie maken.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Hallo-installatiekopie kan maken.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>Maken van een begeleide afbeelding van een VHD in PowerShell

Maak een begeleide afbeelding met behulp van uw algemene besturingssysteem-VHD.


1.  Stel eerst Hallo algemene parameters:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Step\deallocate hello VM.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Hallo VM zoals gegeneraliseerd markeren.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Hallo-installatiekopie met behulp van uw algemene besturingssysteem-VHD maken.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Een begeleide afbeelding maken vanuit een momentopname met behulp van Powershell

U kunt ook een begeleide afbeelding maken vanuit een momentopname van Hallo VHD van een gegeneraliseerde virtuele machine.

    
1. Sommige variabelen maken. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Hallo-momentopname ophalen.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Hallo imageconfiguratie maken.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Hallo-installatiekopie kan maken.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Volgende stappen
- Nu u kunt [een virtuele machine maken van Hallo gegeneraliseerd begeleide afbeelding](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).    

