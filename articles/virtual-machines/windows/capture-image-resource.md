---
title: Een begeleide afbeelding maken in Azure | Microsoft Docs
description: Maak een begeleide afbeelding van een gegeneraliseerde virtuele machine of VHD in Azure. Afbeeldingen kunnen worden gebruikt voor het maken van meerdere virtuele machines die gebruikmaken van beheerde schijven.
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
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Maken van een begeleide afbeelding van een gegeneraliseerde virtuele machine in Azure

Een beheerde Afbeeldingsbron kan worden gemaakt vanuit een gegeneraliseerde virtuele machine die wordt opgeslagen als een beheerde schijf of een niet-beheerde schijf in een opslagaccount. De installatiekopie kan vervolgens worden gebruikt voor het maken van meerdere virtuele machines. 


## <a name="generalize-the-windows-vm-using-sysprep"></a>De virtuele machine van Windows met behulp van Sysprep generalize

Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en voorbereiden van de machine moet worden gebruikt als een afbeelding. Zie voor meer informatie over Sysprep [hoe gebruik Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Zorg ervoor dat de serverfuncties die op de computer uitgevoerd worden ondersteund door Sysprep. Zie voor meer informatie [Sysprep-ondersteuning voor serverfuncties](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Als u Sysprep voordat u uw VHD uploadt naar Azure voor het eerst uitvoert, controleert u of u hebt [uw virtuele machine voorbereid](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat Sysprep wordt uitgevoerd. 
> 
> 

1. Meld u aan de virtuele machine van Windows.
2. Open het venster opdrachtprompt als beheerder. Wijzig de map in **%windir%\system32\sysprep**, en voer vervolgens `sysprep.exe`.
3. In de **hulpprogramma voor systeemvoorbereiding** dialoogvenster, **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat de **Generalize** selectievakje is ingeschakeld.
4. In **afsluitopties**, selecteer **afsluiten**.
5. Klik op **OK**.
   
    ![Sysprep starten](./media/upload-generalized-managed/sysprepgeneral.png)
6. Wanneer Sysprep is voltooid, afgesloten de virtuele machine. Start de virtuele machine niet opnieuw.


## <a name="create-a-managed-image-in-the-portal"></a>Een begeleide afbeelding maken in de portal 

1. Open de [portal](https://portal.azure.com).
2. Klik op het plusteken om een nieuwe resource te maken.
3. Typ in het zoeken filter **installatiekopie**.
4. Selecteer **installatiekopie** uit de resultaten.
5. In de **installatiekopie** blade, klikt u op **maken**.
6. In **naam**, typ een naam voor de installatiekopie.
7. Als u meer dan één abonnement hebt, selecteert u de juiste versie van de **abonnement** vervolgkeuzelijst.
7. In **resourcegroep** select **nieuw** en typ een naam in of selecteer **uit bestaande** en selecteer een resourcegroep te gebruiken uit de vervolgkeuzelijst.
8. In **locatie**, kies de locatie van de resourcegroep.
9. In **type besturingssysteem** Selecteer het type van Windows of Linux-besturingssysteem.
11. In **Storage-blob**, klikt u op **Bladeren** om te zoeken voor de VHD in uw Azure-opslag.
12. In **accounttype** Standard_LRS of Premium_LRS kiezen. Standaard harde schijven en Premium SSD-schijven gebruikt. Beide lokaal redundante opslag gebruiken.
13. In **schijfcache** selecteert u de juiste optie voor de schijfcache. De opties zijn **geen**, **alleen-lezen** en **alleen-lezen**.
14. Optioneel: U kunt ook een bestaande gegevensschijf toevoegen op de installatiekopie door te klikken op **+ gegevensschijf toevoegen**.  
15. Wanneer u klaar bent u deze hebt geselecteerd, klikt u op **maken**.
16. Nadat de installatiekopie is gemaakt, ziet u dit als een **installatiekopie** resource in de lijst met resources in de resourcegroep die u hebt gekozen.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Maken van een begeleide afbeelding van een virtuele machine met behulp van Powershell

Het maken van een installatiekopie van een rechtstreeks vanuit de virtuele machine, zorgt u ervoor dat de installatiekopie alle schijven die zijn gekoppeld aan de virtuele machine bevat, inclusief de Besturingssysteemschijf en alle gegevensschijven.


Voordat u begint, zorg ervoor dat u de nieuwste versie van de AzureRM.Compute PowerShell-module hebt. Voer de volgende opdracht om deze te installeren.

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
2. Zorg ervoor dat de virtuele machine is opgeheven.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Zet de status van de virtuele machine **gegeneraliseerd**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Zorg dat de virtuele machine. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Maak de configuratie van de installatiekopie.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Maken van de installatiekopie.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>Maken van een begeleide afbeelding van een VHD in PowerShell

Maak een begeleide afbeelding met behulp van uw algemene besturingssysteem-VHD.


1.  Stel eerst de algemene parameters:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Step\deallocate de virtuele machine.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. De virtuele machine niet markeren als gegeneraliseerd.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  De installatiekopie via uw algemene besturingssysteem-VHD maken.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Een begeleide afbeelding maken vanuit een momentopname met behulp van Powershell

U kunt ook een begeleide afbeelding maken vanuit een momentopname van de VHD van een gegeneraliseerde virtuele machine.

    
1. Sommige variabelen maken. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Ophalen van de momentopname.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Maak de configuratie van de installatiekopie.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Maken van de installatiekopie.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Volgende stappen
- Nu u kunt [een virtuele machine maken van de installatiekopie van het algemene beheerde](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).  

