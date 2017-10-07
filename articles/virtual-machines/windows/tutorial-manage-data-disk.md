---
title: aaaManage Azure schijven Hello Azure PowerShell | Microsoft Docs
description: Zelfstudie - Azure-schijven Hello Azure PowerShell beheren
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>Azure-schijven met PowerShell beheren

Azure virtuele machines gebruiken schijven toostore Hallo VMs-besturingssysteem, toepassingen en gegevens. Bij het maken van een virtuele machine is het belangrijk toochoose een schijfgrootte en configuratie juiste toohello verwacht werkbelasting. Deze zelfstudie bevat informatie over het implementeren en beheren van VM-schijven. U meer informatie over:

> [!div class="checklist"]
> * OS-schijven en tijdelijke schijven
> * Gegevensschijven
> * Standard en Premium-schijven
> * Prestaties van de schijf
> * Koppelen en gegevensschijven voorbereiden

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Standaard Azure-schijven

Wanneer een virtuele machine van Azure is gemaakt, zijn twee schijven automatisch gekoppelde toohello virtuele machine. 

**Besturingssysteemschijf** - besturingssysteem schijven kunnen worden verkleind up too1 terabyte en hosts Hallo VMs-besturingssysteem.  Hallo OS-schijf is toegewezen stationsletter van *c:* standaard. configuratie van de besturingssysteemschijf Hallo van de schijfcache Hallo is geoptimaliseerd voor OS-prestaties. Hallo OS-schijf **beter niet** toepassingen of gegevens hosten. Gebruik een gegevensschijf, die verderop in dit artikel wordt beschreven voor toepassingen en gegevens.

**Tijdelijke schijf** -tijdelijke schijven gebruiken een SSD-schijf die zich bevindt op Hallo dezelfde Azure-host als Hallo VM. Tijdelijke schijven zijn maximaal zodat en kunnen worden gebruikt voor bewerkingen, zoals tijdelijke gegevensverwerking. Als Hallo VM verplaatste tooa nieuwe host is, wordt echter gegevens die zijn opgeslagen op een tijdelijke schijf verwijderd. Hallo-grootte van de tijdelijke schijf hello wordt bepaald door Hallo VM-grootte. Tijdelijke schijven zijn toegewezen stationsletter van *d:* standaard.

### <a name="temporary-disk-sizes"></a>Tijdelijke schijfgrootten

| Type | VM-grootte | Maximumgrootte van tijdelijke schijf (GB) |
|----|----|----|
| [Algemeen doel](sizes-general.md) | A en D-reeks | 800 |
| [Geoptimaliseerde rekenkracht](sizes-compute.md) | F-serie | 800 |
| [Geoptimaliseerd geheugen](../virtual-machines-windows-sizes-memory.md) | D en G-serie | 6144 |
| [Geoptimaliseerde opslag](../virtual-machines-windows-sizes-storage.md) | L-reeks | 5630 |
| [GPU](sizes-gpu.md) | N reeks | 1440 |
| [Hoge prestaties](sizes-hpc.md) | A en H reeks | 2000 |

## <a name="azure-data-disks"></a>Azure gegevensschijven

Extra gegevensschijven kunnen worden toegevoegd voor het installeren van toepassingen en gegevens op te slaan. Gegevensschijven moeten worden gebruikt in een situatie waarin de opslag van gegevens duurzaam en responsief gewenst is. Elke gegevensschijf heeft een maximale capaciteit van 1 terabyte. Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven kunnen worden aangesloten tooa VM. Voor elke VM-core, kunnen twee schijven worden gekoppeld. 

### <a name="max-data-disks-per-vm"></a>Maximum aantal gegevensschijven per VM

| Type | VM-grootte | Maximum aantal gegevensschijven per VM |
|----|----|----|
| [Algemeen doel](sizes-general.md) | A en D-reeks | 32 |
| [Geoptimaliseerde rekenkracht](sizes-compute.md) | F-serie | 32 |
| [Geoptimaliseerd geheugen](../virtual-machines-windows-sizes-memory.md) | D en G-serie | 64 |
| [Geoptimaliseerde opslag](../virtual-machines-windows-sizes-storage.md) | L-reeks | 64 |
| [GPU](sizes-gpu.md) | N reeks | 48 |
| [Hoge prestaties](sizes-hpc.md) | A en H reeks | 32 |

## <a name="vm-disk-types"></a>VM-schijftypen

Azure biedt twee typen van de schijf.

### <a name="standard-disk"></a>Standard-schijven

Standard Storage wordt ondersteund door HDD's en biedt voordelige en hoogwaardige opslag. Standaardschijven zijn ideaal voor een voordelige ontwikkelen en testen werkbelasting.

### <a name="premium-disk"></a>Premium-schijf

Premium-schijven worden ondersteund door de hoge prestaties, lage latentie SSD-schijf. Ideaal voor virtuele machines met productie werkbelasting. Premium-opslag ondersteunt DS-serie, DSv2-serie GS-serie en virtuele machines FS-serie. Premium-schijven zijn drie typen (P10, P20, P30), Hallo grootte van Hallo schijf Hallo schijftype bepaalt. Wanneer u selecteert, wordt de waarde van een schijf grootte Hallo toohello volgende type afgerond. Bijvoorbeeld, als Hallo grootte lager dan 128 GB Hallo schijftype is worden P10, tussen 129 512 P20 en meer dan 512 P30. 

### <a name="premium-disk-performance"></a>Premium-schijfprestaties

|Premium-opslag schijftype | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Grootte van de schijf (afronden) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| IOP's per schijf | 500 | 2,300 | 5,000 |
Doorvoer per schijf | 100 MB/s | 150 MB/s | 200 MB/s |

Tijdens het Hallo boven tabel identificeert max. IOP's per schijf, kan een hoger niveau van de prestaties van worden bereikt door meerdere gegevensschijven te verwijderen. 64 gegevens schijven kunnen worden gekoppeld voor het exemplaar tooStandard_GS5 VM. Als u elk van deze schijven worden aangepast als een P30, kan een maximum van 80.000 IOP's kan worden bereikt. Zie voor gedetailleerde informatie over max. IOP's per VM [Linux VM-grootten](./sizes.md).

## <a name="create-and-attach-disks"></a>Maken en koppelen van schijven

toocomplete hello voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben. Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) kunt maken voor u. Wanneer werkende Hallo-zelfstudie vervangt benoemt Hallo resourcegroep en de VM waar nodig.

Maken van de eerste configuratie Hallo met [nieuw AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig). Hallo volgt configureert u een schijf die 128 GB groot is.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Hallo gegevensschijf maken met de Hallo [nieuw AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) opdracht.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Get Hallo virtuele machine die u wilt dat tooadd Hallo gegevens schijf toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) opdracht.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Add Hallo gegevens schijf toohello Virtuele-machineconfiguratie Hello [toevoegen AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) opdracht.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Hallo virtuele machine bijwerken met Hallo [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) opdracht.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Gegevensschijven voorbereiden

Als een schijf is aangesloten toohello virtuele machine, moet Hallo besturingssysteem geconfigureerd toobe toouse Hallo schijf. Hallo volgende voorbeeld ziet u hoe de eerste Hallo-schijf toegevoegd voor het configureren van toomanually toohello VM. Dit proces kan ook worden geautomatiseerd met Hallo [extensie voor aangepaste scripts](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Handmatige configuratie

Maak een RDP-verbinding met de Hallo virtuele machine. Opent u PowerShell en voer dit script.

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd over VM schijven onderwerpen, zoals:

> [!div class="checklist"]
> * OS-schijven en tijdelijke schijven
> * Gegevensschijven
> * Standard en Premium-schijven
> * Prestaties van de schijf
> * Koppelen en gegevensschijven voorbereiden

Ga toohello volgende zelfstudie toolearn over het automatiseren van VM-configuratie.

> [!div class="nextstepaction"]
> [VM-configuratie automatiseren](./tutorial-automate-vm-deployment.md)
