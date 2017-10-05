---
title: 'Azure PowerShell-Script voorbeeld: een momentopname maken van een VHD voor het maken van meerdere identieke beheerde schijven in een kleine hoeveelheid tijd | Microsoft Docs'
description: 'Azure PowerShell-Script voorbeeld: een momentopname maken van een VHD voor het maken van meerdere identieke beheerde schijven in een kleine hoeveelheid tijd'
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
ms.openlocfilehash: 02a69abd6c17ce765996379309e22afad82c4e10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Een momentopname maken van een VHD voor het maken van meerdere identieke beheerde schijven in een kleine hoeveelheid tijd met PowerShell

Dit script maakt een momentopname van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement. Dit script gebruiken voor het importeren van een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD naar een momentopname en gebruik vervolgens de momentopname voor het maken van meerdere identieke schijven die worden beheerd in een kleine hoeveelheid tijd. Ook gebruikt om een VHD-gegevens importeren in een momentopname en gebruik vervolgens de momentopname maken van meerdere beheerde schijven in een kleine hoeveelheid tijd. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[belangrijkste](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "momentopname maken van VHD")]


## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt na de opdrachten voor het maken van een beheerde schijf vanaf een VHD in een ander abonnement. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf. Dit omvat opslagtype, locatie, resource-Id van het opslagaccount waarin de bovenliggende VHD wordt opgeslagen en VHD-URI van de bovenliggende VHD. |
| [Nieuwe AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven. |

## <a name="next-steps"></a>Volgende stappen

[Een beheerde schijf maken vanuit een momentopname.](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Voorbeelden van extra virtuele machine PowerShell-script kunnen worden gevonden in de [virtuele machine van Windows Azure-documentatie](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).