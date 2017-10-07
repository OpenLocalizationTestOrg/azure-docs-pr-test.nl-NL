---
title: een beheerde schijf aaaAzure PowerShell-voorbeeldscript - maken van een VHD-bestand in een opslagaccount in dezelfde of verschillende abonnement | Microsoft Docs
description: Azure PowerShell-Script steekproef - maken van een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement
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
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Maak een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of verschillende abonnement met PowerShell

Dit script maakt een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement. Gebruik dit script tooimport een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD toomanaged OS schijf toocreate een virtuele machine. Gebruik tevens het tooimport een gegevensschijf VHD toomanaged gegevens. 

Maak meerdere identieke beheerde schijven van een VHD-bestand in een kleine hoeveelheid tijd. toocreate schijven die worden beheerd vanaf een vhd-bestand, blob-momentopname van Hallo vhd-bestand wordt gemaakt en wordt het gebruikte toocreate beheerd schijven. Slechts één blob momentopname kan worden gemaakt in een minuut dat ervoor zorgt het maken van schijffouten dat vanwege toothrottling. tooavoid deze beperking, maak een [beheerde momentopname van de vhd-bestand Hallo](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) en vervolgens gebruik Hallo beheerd momentopname toocreate meerdere beheerde schijven in korte tijd. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt na opdrachten toocreate een beheerde schijf van een VHD in een ander abonnement. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf. Dit omvat opslagtype, locatie, resource-Id van Hallo opslagaccount waar Hallo bovenliggende VHD wordt opgeslagen, VHD-URI van Hallo bovenliggende VHD. |
| [Nieuwe AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven. |

## <a name="next-steps"></a>Volgende stappen

[Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
