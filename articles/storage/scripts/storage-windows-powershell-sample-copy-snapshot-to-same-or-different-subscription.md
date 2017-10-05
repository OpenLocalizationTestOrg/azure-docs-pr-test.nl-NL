---
title: Azure PowerShell-Script voorbeeld - exemplaar (verplaatsen)-momentopname van een beheerde schijf naar hetzelfde of een ander abonnement | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - exemplaar (verplaatsen)-momentopname van een beheerde schijf naar hetzelfde of een ander abonnement
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
ms.openlocfilehash: 69b9b4ed86117f7fe561e7e70227e60e6a9d858e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a>Momentopname van een beheerde schijf kopiëren in hetzelfde abonnement of een ander abonnement met PowerShell

Dit script maakt een kopie van een momentopname in de dezelfde hetzelfde abonnement of een ander abonnement. Dit script gebruiken voor het verplaatsen van een momentopname naar ander abonnement voor het bewaren van gegevens. Opslag-momentopnamen in een ander abonnement bescherming tegen onopzettelijk verwijderen van momentopnamen in uw belangrijkste abonnement. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[belangrijkste](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "kopie momentopname")]


## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt na de opdrachten voor het maken van een momentopname in het doelabonnement met de Id van de momentopname van de bron. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmSnapshotConfig](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | Maakt de configuratie van de momentopnamen die wordt gebruikt voor het maken van momentopnamen. Dit omvat de resource-Id van de momentopname van de bovenliggende en de locatie die is hetzelfde als de momentopname van de bovenliggende.  |
| [Nieuwe AzureRmSnapshot](/powershell/module/azurerm.compute/New-AzureRmDisk) | Maakt een momentopname met configuratie van de momentopnamen, naam van de momentopname en de Resourcegroepnaam als parameters doorgegeven. |


## <a name="next-steps"></a>Volgende stappen

[Een virtuele machine maken vanuit een momentopname](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Voorbeelden van extra virtuele machine PowerShell-script kunnen worden gevonden in de [virtuele machine van Windows Azure-documentatie](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).