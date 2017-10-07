---
title: "aaaAzure PowerShell-voorbeeldscript - momentopname van een beheerde schijf toosame of een ander abonnement kopiëren (verplaatsen) | Microsoft Docs"
description: Azure PowerShell-Script voorbeeld - exemplaar (verplaatsen)-momentopname van een beheerde schijf toosame of een ander abonnement
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 7a3565356f13cb93759dec7ef9d0357e04c3410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a>Momentopname van een beheerde schijf kopiëren in hetzelfde abonnement of een ander abonnement met PowerShell

Dit script maakt een kopie van een momentopname in Hallo dezelfde hetzelfde abonnement of een ander abonnement. Gebruik dit script toomove een momentopname toodifferent abonnement voor bewaren van gegevens. Opslag-momentopnamen in een ander abonnement bescherming tegen onopzettelijk verwijderen van momentopnamen in uw belangrijkste abonnement. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van opdrachten toocreate na een momentopname aan Hallo doel abonnement met Hallo Hallo bron momentopname-Id. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmSnapshotConfig](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | Maakt de configuratie van de momentopnamen die wordt gebruikt voor het maken van momentopnamen. Het bevat Hallo-resource-Id van de momentopname van de bovenliggende Hallo en de locatie die is hetzelfde als Hallo bovenliggende momentopname.  |
| [Nieuwe AzureRmSnapshot](/powershell/module/azurerm.compute/New-AzureRmDisk) | Maakt een momentopname met configuratie van de momentopnamen, naam van de momentopname en de Resourcegroepnaam als parameters doorgegeven. |


## <a name="next-steps"></a>Volgende stappen

[Een virtuele machine maken vanuit een momentopname](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
