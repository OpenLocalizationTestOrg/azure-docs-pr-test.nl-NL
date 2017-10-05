---
title: Azure PowerShell-Script steekproef - maken van een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of verschillende abonnement | Microsoft Docs
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
ms.openlocfilehash: 728def40a3eb132537decbd099fa71f4544c6b87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Maak een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of verschillende abonnement met PowerShell

Dit script maakt een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement. Dit script gebruiken voor het importeren van een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD naar beheerde OS-schijf voor het maken van een virtuele machine. Deze ook gebruiken voor het importeren van een VHD-gegevens naar beheerde gegevensschijf. 

Maak meerdere identieke beheerde schijven van een VHD-bestand in een kleine hoeveelheid tijd. Als u wilt maken beheerde schijven van een vhd-bestand, blob-momentopname van het vhd-bestand wordt gemaakt en wordt vervolgens gebruikt om beheerde schijven te maken. Slechts één blob momentopname kan worden gemaakt in een minuut dat ervoor zorgt het maken van schijffouten vanwege een beperking dat. Om te voorkomen dat deze beperking, maakt u een [beheerde momentopname van het vhd-bestand](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) en gebruik beheerd voor de beheerde momentopname maken van meerdere schijven vervolgens in korte tijd. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[belangrijkste](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "-beheerde schijven van VHD maken")]


## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt na de opdrachten voor het maken van een beheerde schijf vanaf een VHD in een ander abonnement. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf. Dit omvat opslagtype, locatie, resource-Id van het opslagaccount waarin de bovenliggende VHD is opgeslagen, VHD-URI van de bovenliggende VHD. |
| [Nieuwe AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven. |

## <a name="next-steps"></a>Volgende stappen

[Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Voorbeelden van extra virtuele machine PowerShell-script kunnen worden gevonden in de [virtuele machine van Windows Azure-documentatie](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).