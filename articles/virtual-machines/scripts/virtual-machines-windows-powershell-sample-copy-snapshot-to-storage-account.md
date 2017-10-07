---
title: "PowerShell-voorbeeldscript - momentopname exporteren/kopiëren als VHD tooa storage-account in andere regio aaaAzure | Microsoft Docs"
description: "Azure PowerShell-Script voorbeeld - momentopname exporteren/kopiëren als VHD tooa opslagaccount in dezelfde andere regio"
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
ms.openlocfilehash: c18ad4fa0bf12033fafe941a807e7b4c8d233a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>Export/exemplaar beheerde momentopnamen als VHD tooa storage-account in andere regio met PowerShell

Dit script exporteert u een beheerde momentopname tooa storage-account in andere regio. Deze genereert eerst Hallo SAS-URI van de momentopname Hallo en gebruikt vervolgens toocopy het tooa storage-account in andere regio. Gebruik deze back-up toomaintain script beheerde schijven in andere regio voor herstel na noodgevallen.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van opdrachten toogenerate na SAS-URI voor een beheerde momentopnamen en kopieën op Hallo momentopname tooa storage-account met behulp van SAS-URI. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Verleen AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | De SAS-URI voor een momentopname die is gebruikt toocopy genereert het tooa storage-account. |
| [Nieuwe AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Maakt een storage account context Hallo-accountnaam en-sleutel. Deze context kan worden gebruikt tooperform lezen/schrijven-bewerkingen op Hallo storage-account. |
| [Start AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Kopieën Hallo onderliggende VHD van een momentopname tooa storage-account |

## <a name="next-steps"></a>Volgende stappen

[Een beheerde schijf vanaf een VHD maken](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Een virtuele machine maken van een beheerde schijf](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
