---
title: PowerShell-voorbeeldscript - aaaAzure een momentopname maken van een VHD-toocreate meerdere identieke beheerde schijven in een kleine hoeveelheid tijd | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een momentopname maken van een VHD-toocreate meerdere identieke beheerde schijven in een kleine hoeveelheid tijd'
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 0a13e399b692f32b3772add39fe5b5c023808c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Een momentopname maken van een VHD-toocreate meerdere identieke beheerde schijven in een kleine hoeveelheid tijd met PowerShell

Dit script maakt een momentopname van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement. Gebruik dit script tooimport een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD tooa momentopname en gebruik vervolgens Hallo momentopname toocreate meerdere identieke beheerde schijven in een kleine hoeveelheid tijd. Gebruik tevens een momentopname van de VHD gegevens tooa tooimport en gebruik vervolgens Hallo momentopname toocreate meerdere beheerde schijven in een kleine hoeveelheid tijd. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt na opdrachten toocreate een beheerde schijf van een VHD in een ander abonnement. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf. Dit omvat opslagtype, locatie, resource-Id van het opslagaccount Hallo waar Hallo bovenliggende VHD wordt opgeslagen en VHD-URI van Hallo bovenliggende VHD. |
| [Nieuwe AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven. |

## <a name="next-steps"></a>Volgende stappen

[Een beheerde schijf maken vanuit een momentopname.](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
