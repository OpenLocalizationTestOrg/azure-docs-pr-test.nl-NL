---
title: een beheerde schijf van een VHD in Azure aaaCreate | Microsoft Docs
description: Een beheerde schijf maken vanaf een VHD die momenteel is in een Azure storage-account met Hallo Resource Manager-implementatiemodel.
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
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Beheerde schijven van niet-beheerde schijven in een opslagaccount maken

Een beheerde schijf kan worden gemaakt vanuit een bestaande gegevensschijf of een besturingssysteemschijf die zich in een Azure storage-account. U kunt ook een lege schijf die kan worden gebruikt als een nieuwe gegevensschijf voor een virtuele machine maken. 

## <a name="before-you-begin"></a>Voordat u begint
Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt. Voer Hallo na de opdracht tooinstall deze.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Een beheerde schijf vanaf een VHD in Azure storage-account maken

In voorbeeld Hallo we een schijf van een VHD als beheerde schijf maken en toewijzen toohello parameter **diskette $1** toouse later. 

Hallo beheerde schijf wordt gemaakt in Hallo **West VS** locatie in een resourcegroep met de naam **myResourceGroup**. Hallo schijf worden benoemd **myDisk** en deze wordt gemaakt van een VHD-bestand met de naam **myDisk.vhd** we eerder tooa opslagaccount met de naam geüpload **mystorageaccount**. Hallo-beheerde schijven wordt gemaakt in premium lokaal redundante opslag (LRS). StandardLRS en PremiumLRS zijn alleen Hallo **- AccountType** beschikbare opties voor schijven die worden beheerd. 

1.  Sommige parameters instellen

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Hallo gegevensschijf maken. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Een lege gegevensschijf als een beheerde schijf maken

In voorbeeld Hallo we een lege gegevensschijf als beheerde schijf maken en toewijzen toohello parameter **$dataDisk2** toouse later. Een lege gegevensschijf moet toobe geïnitialiseerd toohello VM aanmelden en het gebruik van diskmgmt.msc of [op afstand met WinRM en een script](attach-disk-ps.md#initialize-the-disk), wanneer het bijgevoegde tooa VM uitgevoerd.

Hallo lege gegevensschijf worden aangemaakt in Hallo **West-Centraal VS** locatie in een resourcegroep met de naam **myResourceGroup**. Hallo schijf worden benoemd **myEmptyDataDisk**. Hallo lege schijf wordt gemaakt in premium lokaal redundante opslag (LRS). StandardLRS en PremiumLRS zijn alleen Hallo **- AccountType** beschikbare opties voor schijven die worden beheerd.

Hallo-schijfgrootte in dit voorbeeld is 128GB, maar moet u een grootte die voldoet aan de behoeften Hallo van alle toepassingen die op de virtuele machine.

1.  Sommige parameters instellen

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Hallo gegevensschijf maken.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Volgende stappen   
- Als u al een virtuele machine hebt, kunt u [een gegevensschijf koppelen](attach-disk-portal.md).
