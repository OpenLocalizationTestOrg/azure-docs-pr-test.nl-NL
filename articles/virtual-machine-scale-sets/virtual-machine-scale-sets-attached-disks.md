---
title: Virtuele Machine Scale Sets gekoppeld gegevensschijven aaaAzure | Microsoft Docs
description: Meer informatie over hoe toouse gekoppeld gegevensschijven met virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Virtuele-machineschaalsets in Azure en gekoppelde gegevensschijven
[Virtuele-machineschaalsets](/azure/virtual-machine-scale-sets/) in Azure ondersteunen nu virtuele machines met gekoppelde gegevensschijven. Gegevensschijven kunnen worden gedefinieerd in het opslagprofiel Hallo voor schaalsets die zijn gemaakt met beheerde Azure-schijven. Eerder waren hello alleen direct gekoppelde opslag beschikbare opties met virtuele machines in schaalsets Hallo OS station en tijdelijke stations.

> [!NOTE]
>  Wanneer u een schaal bijgesloten gegevensschijven die zijn gedefinieerd in te stellen maakt, moet u nog steeds toomount en indeling Hallo schijven uit binnen een VM-toouse ze (alleen like voor zelfstandige virtuele Azure-machines). Een handige manier toodo die dit toouse een extensie voor aangepaste scripts die een Standaardscript toopartition aanroept en formatteren van alle Hallo gegevensschijven op een virtuele machine is.

## <a name="create-a-scale-set-with-attached-data-disks"></a>Een schaalset maken met gekoppelde gegevensschijven
Een eenvoudige manier toocreate een met gekoppelde schijven schaalset is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss maken_ opdracht. Hallo volgende voorbeeld maakt een Azure-resourcegroep en een VM-schaalset van 10 Ubuntu VM's, elk met 2 bijgesloten gegevensschijven, 50 GB en 100 GB respectievelijk.
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
Houd er rekening mee dat Hallo _vmss maken_ wordt standaard een bepaalde configuratiewaarden als u ze niet opgeven. toosee hello beschikbare opties dat kunt u proberen overschrijven:
```bash
az vmss create --help
```
Een andere manier toocreate een schaal gekoppelde gegevensschijven in te stellen is een schaal in een Azure Resource Manager-sjabloon instellen toodefine bevatten een _dataDisks_ sectie in Hallo _storageProfile_, en Hallo implementeren de sjabloon. Hallo 50 en 100 GB schijf bovenstaande voorbeeld zou als volgt in Hallo sjabloon worden gedefinieerd:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
Ziet u een voorbeeld van een voltooid, gereed toodeploy van een scale set-sjabloon met een gekoppelde schijf hier gedefinieerd: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>Toevoegen van een bestaande schaal voor gegevens schijf tooan instellen
> [!NOTE]
>  U kunt alleen koppelen schijven tooa scale gegevensset die is gemaakt met [Azure beheerd schijven](./virtual-machine-scale-sets-managed-disks.md).

U kunt geen gegevens schijf tooa VM schaal ingesteld met Azure CLI toevoegen _az vmss schijf koppelen_ opdracht. Geef een LUN op die nog niet in gebruik is. Hallo na CLI voorbeeld wordt een 50 GB station toolun 3 toegevoegd:
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

Hallo volgende PowerShell-voorbeeld wordt een 50 GB station toolun 3 toegevoegd:
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> Andere VM-grootten hebben andere beperkingen op Hallo aantal gekoppelde schijven die ze ondersteunen. Controleer Hallo [kenmerken van virtuele machine grootte](../virtual-machines/windows/sizes.md) voordat een nieuwe schijf toe te voegen.

U kunt ook een schijf toevoegen door het toevoegen van een nieuwe vermelding toohello _dataDisks_ eigenschap in Hallo _storageProfile_ instellen van een scale-definitie en het toepassen van Hallo wijzigen. tootest deze, zoeken naar een bestaande scale setdefinitie in Hallo [Azure Resource Explorer](https://resources.azure.com/). Selecteer _bewerken_ en een nieuwe schijf toohello lijst met gegevensschijven toe te voegen. Bijvoorbeeld bovenstaande Hallo-voorbeeld gebruikt:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

Selecteer vervolgens _plaatsen_ tooapply hello tooyour scale set wordt gewijzigd. Dit voorbeeld zou moeten werken als u gebruikmaakt van een VM-formaat dat meer dan twee gekoppelde gegevensschijven ondersteunt.

> [!NOTE]
> Wanneer u een wijziging tooa schaal definitie zoals het toevoegen of verwijderen van een gegevensschijf ingesteld, is van toepassing tooall nieuw gemaakte virtuele machines, maar is alleen van toepassing tooexisting VMs hello _upgradePolicy_ eigenschap te 'automatisch' is ingesteld. Als deze optie is ingesteld te 'handmatig', moet u toomanually Hallo nieuwe model tooexisting VM's van toepassing. U kunt dit doen in Hallo-portal met Hallo _Update AzureRmVmssInstance_ PowerShell-opdracht of met behulp van Hallo _az vmss update-exemplaren_ CLI-opdracht.

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>Toe te voegen vooraf ingestelde schijven tooan scale-bestaande gegevensset 
> Wanneer u schijven tooan bestaande toevoegt schaalset model ontwikkeld, Hallo schijf wordt altijd gemaakt leeg. Dit scenario omvat ook nieuwe exemplaren gemaakt door Hallo schaalset. Dit gedrag is omdat Hallo scaleset definitie een lege gegevensschijf heeft. In de volgorde toocreate vooraf ingestelde gegevensstations voor een bestaand scale set-model, kunt u een van de volgende twee opties kiezen:

* Gegevens kopiëren van Hallo exemplaar 0 VM toohello gegevens een of meer schijven in Hallo andere virtuele machines door het uitvoeren van een aangepast script.
* Maken van een begeleide afbeelding met schijf Hallo OS plus gegevensschijf (met gegevens Hallo vereist) en maak een nieuwe scaleset met Hallo-installatiekopie. Op deze manier om nieuwe virtuele machine gemaakt heeft een schijf die die is opgegeven in de definitie Hallo van Hallo scaleset. Aangezien deze definitie tooan afbeelding met een gegevensschijf die gegevens aangepast verwijzen wordt, terug elke virtuele machine op Hallo scaleset automatisch met deze wijzigingen.

> Hallo manier toocreate een aangepaste installatiekopie u hier vindt: [een begeleide afbeelding van een gegeneraliseerde virtuele machine in Azure maken](/azure/virtual-machines/windows/capture-image-resource/) 

> Hallo gebruiker moet toocapture Hallo 0 virtuele die vereiste gegevens heeft Hallo-instantie en gebruik vervolgens deze vhd voor Hallo installatiekopie definitie.

## <a name="removing-a-data-disk-from-a-scale-set"></a>Een gegevensschijf verwijderen uit een schaalset
U kunt een gegevensschijf verwijderen uit een VM-schaalset met behulp van de Azure CLI-opdracht _az vmss disk detach_. Bijvoorbeeld hello volgende opdracht wordt gedefinieerd op lun 2 Hallo-schijf:
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
Op dezelfde manier kunt u ook een schijf verwijderen uit een schaal ingesteld door het verwijderen van een item uit Hallo _dataDisks_ eigenschap in Hallo _storageProfile_ en Hallo wijziging toe te passen. 

## <a name="additional-notes"></a>Aanvullende opmerkingen
Ondersteuning voor Azure Managed schijven en schaal ingesteld gekoppelde gegevensschijven is beschikbaar in de API-versie [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) of hoger van Hallo Microsoft.Compute-API.

In de aanvankelijke implementatie van de gekoppelde schijfondersteuning voor schaalsets Hallo kan niet u koppelen of ontkoppelen van gegevensschijven van afzonderlijke virtuele machines in een schaalset.

De ondersteuning in Azure Portal voor gekoppelde gegevensschijven in schaalsets is oorspronkelijk beperkt. Afhankelijk van uw vereisten dat kunt u Azure-sjablonen, CLI, PowerShell SDK's en REST-API toomanage gekoppelde schijven.


