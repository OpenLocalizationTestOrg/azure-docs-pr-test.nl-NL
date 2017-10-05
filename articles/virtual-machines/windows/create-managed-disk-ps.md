---
title: Een beheerde schijf maken vanaf een VHD in Azure | Microsoft Docs
description: Een beheerde schijf maken vanaf een VHD die momenteel is in een Azure storage-account met het implementatiemodel van Resource Manager.
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
ms.openlocfilehash: c03ebf73f1090b595149daf2eb3e274b05822f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Beheerde schijven van niet-beheerde schijven in een opslagaccount maken

Een beheerde schijf kan worden gemaakt vanuit een bestaande gegevensschijf of een besturingssysteemschijf die zich in een Azure storage-account. U kunt ook een lege schijf die kan worden gebruikt als een nieuwe gegevensschijf voor een virtuele machine maken. 

## <a name="before-you-begin"></a>Voordat u begint
Als u PowerShell gebruikt, zorg ervoor dat u de nieuwste versie van de AzureRM.Compute PowerShell-module hebt. Voer de volgende opdracht om deze te installeren.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Een beheerde schijf vanaf een VHD in Azure storage-account maken

In het voorbeeld wordt een schijf maken vanaf een VHD als beheerde schijf en deze toewijzen aan de parameter **diskette $1** voor later gebruik. 

De beheerde schijf wordt gemaakt in de **West VS** locatie in een resourcegroep met de naam **myResourceGroup**. De schijf worden benoemd **myDisk** en deze wordt gemaakt van een VHD-bestand met de naam **myDisk.vhd** we eerder hebt geüpload naar een opslagaccount met de naam **mystorageaccount**. De beheerde schijf wordt gemaakt in premium lokaal redundante opslag (LRS). StandardLRS en PremiumLRS zijn de enige **- AccountType** beschikbare opties voor schijven die worden beheerd. 

1.  Sommige parameters instellen

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. De gegevensschijf maken. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Een lege gegevensschijf als een beheerde schijf maken

In het voorbeeld wordt een lege gegevensschijf als beheerde schijf maken en toewijzen aan de parameter **$dataDisk2** voor later gebruik. Een lege gegevensschijf moet worden geïnitialiseerd aanmelden bij de virtuele machine en het gebruik van diskmgmt.msc of [op afstand met WinRM en een script](attach-disk-ps.md#initialize-the-disk), zodra deze is gekoppeld aan een actieve virtuele machine.

De lege gegevensschijf wordt gemaakt in de **West-Centraal VS** locatie in een resourcegroep met de naam **myResourceGroup**. De schijf worden benoemd **myEmptyDataDisk**. De lege schijf wordt gemaakt in premium lokaal redundante opslag (LRS). StandardLRS en PremiumLRS zijn de enige **- AccountType** beschikbare opties voor schijven die worden beheerd.

De schijfgrootte in dit voorbeeld is 128GB, maar moet u een grootte die voldoet aan de behoeften van alle toepassingen die op de virtuele machine.

1.  Sommige parameters instellen

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. De gegevensschijf maken.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Volgende stappen   
- Als u al een virtuele machine hebt, kunt u [een gegevensschijf koppelen](attach-disk-portal.md).
