---
title: Azure-schijven met de Azure PowerShell beheren | Microsoft Docs
description: Zelfstudie - schijven van Azure met Azure PowerShell beheren
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
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a>Azure-schijven met PowerShell beheren

Virtuele machines in Azure schijven gebruiken voor het opslaan van het besturingssysteem, toepassingen en gegevens van virtuele machines. Bij het maken van een virtuele machine is het van belang dat u kiest een grootte van de schijf en de configuratie geschikt is voor de verwachte werkbelasting. Deze zelfstudie bevat informatie over het implementeren en beheren van VM-schijven. U meer informatie over:

> [!div class="checklist"]
> * OS-schijven en tijdelijke schijven
> * Gegevensschijven
> * Standard en Premium-schijven
> * Prestaties van de schijf
> * Koppelen en gegevensschijven voorbereiden

Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist. Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken. Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Standaard Azure-schijven

Wanneer een virtuele machine van Azure is gemaakt, worden twee schijven automatisch gekoppeld aan de virtuele machine. 

**Besturingssysteemschijf** -systeemschijven kan worden verkleind tot 1 terabyte is, en fungeert als host voor het besturingssysteem van de virtuele machines.  De besturingssysteemschijf is toegewezen stationsletter van *c:* standaard. De configuratie van de besturingssysteemschijf van de schijfcache is geoptimaliseerd voor OS-prestaties. De besturingssysteemschijf **beter niet** toepassingen of gegevens hosten. Gebruik een gegevensschijf, die verderop in dit artikel wordt beschreven voor toepassingen en gegevens.

**Tijdelijke schijf** -tijdelijke schijven gebruiken een SSD-schijf die zich op dezelfde Azure host als de virtuele machine. Tijdelijke schijven zijn maximaal zodat en kunnen worden gebruikt voor bewerkingen, zoals tijdelijke gegevensverwerking. Als de virtuele machine wordt verplaatst naar een nieuwe host, wordt echter gegevens die zijn opgeslagen op een tijdelijke schijf verwijderd. De grootte van de tijdelijke schijf wordt bepaald door de VM-grootte. Tijdelijke schijven zijn toegewezen stationsletter van *d:* standaard.

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

Extra gegevensschijven kunnen worden toegevoegd voor het installeren van toepassingen en gegevens op te slaan. Gegevensschijven moeten worden gebruikt in een situatie waarin de opslag van gegevens duurzaam en responsief gewenst is. Elke gegevensschijf heeft een maximale capaciteit van 1 terabyte. De grootte van de virtuele machine bepaalt hoeveel gegevensschijven kunnen worden gekoppeld aan een virtuele machine. Voor elke VM-core, kunnen twee schijven worden gekoppeld. 

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

Premium-schijven worden ondersteund door de hoge prestaties, lage latentie SSD-schijf. Ideaal voor virtuele machines met productie werkbelasting. Premium-opslag ondersteunt DS-serie, DSv2-serie GS-serie en virtuele machines FS-serie. Premium-schijven zijn drie typen (P10, P20, P30), de grootte van de schijf bepaalt het schijftype. Wanneer u selecteert, wordt de een de waarde van de schijfgrootte afgerond naar het volgende type. Bijvoorbeeld, als de grootte lager dan 128 GB is wordt het schijftype P10, worden tussen 129 512 P20 en meer dan 512 P30. 

### <a name="premium-disk-performance"></a>Premium-schijfprestaties

|Premium-opslag schijftype | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Grootte van de schijf (afronden) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| IOP's per schijf | 500 | 2,300 | 5,000 |
Doorvoer per schijf | 100 MB/s | 150 MB/s | 200 MB/s |

Terwijl de bovenstaande tabel max. IOP's per schijf identificeert, kan een hoger niveau van de prestaties worden bereikt door meerdere gegevensschijven te verwijderen. 64 gegevensschijven kunnen bijvoorbeeld worden gekoppeld aan Standard_GS5 VM. Als u elk van deze schijven worden aangepast als een P30, kan een maximum van 80.000 IOP's kan worden bereikt. Zie voor gedetailleerde informatie over max. IOP's per VM [Linux VM-grootten](./sizes.md).

## <a name="create-and-attach-disks"></a>Maken en koppelen van schijven

Als u het voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben. Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) kunt maken voor u. Wanneer het uitvoeren van de zelfstudie vervangt benoemt de resourcegroep en de virtuele machine waar nodig.

Maken van de eerste configuratie met [nieuw AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig). Het volgende voorbeeld wordt een schijf die 128 GB groot is geconfigureerd.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Maken van de gegevensschijf met de [nieuw AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) opdracht.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Ophalen van de virtuele machine die u wilt toevoegen de gegevensschijf aan met de [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) opdracht.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

De gegevensschijf toevoegen aan de virtuele-machineconfiguratie met de [toevoegen AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) opdracht.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Werk de virtuele machine met de [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) opdracht.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Gegevensschijven voorbereiden

Zodra een schijf is gekoppeld aan de virtuele machine, moet het besturingssysteem worden geconfigureerd voor gebruik van de schijf. Het volgende voorbeeld laat zien hoe de eerste schijf die is toegevoegd aan de virtuele machine handmatig configureren. Dit proces kan ook worden geautomatiseerd met behulp van de [extensie voor aangepaste scripts](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Handmatige configuratie

Een RDP-verbinding maken met de virtuele machine. Opent u PowerShell en voer dit script.

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

Ga naar de volgende zelfstudie voor meer informatie over het automatiseren van VM-configuratie.

> [!div class="nextstepaction"]
> [VM-configuratie automatiseren](./tutorial-automate-vm-deployment.md)
