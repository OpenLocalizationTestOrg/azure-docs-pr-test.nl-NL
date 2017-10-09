---
title: Voorbeelden van de virtuele Machine PowerShell aaaAzure | Microsoft Docs
description: Voorbeelden van de virtuele Machine van Azure PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Azure virtuele Machine PowerShell-voorbeelden

Hallo bevat volgende tabel koppelingen tooPowerShell scripts steekproeven maken en beheren van virtuele machines van Windows.

| | |
|---|---|
|**Virtuele machines maken**||
| [Een volledig geconfigureerde virtuele machine maken](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Een resourcegroep, virtuele machine en alle gerelateerde resources gemaakt.|
| [Maximaal beschikbare virtuele machines maken](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Maakt verschillende virtuele machines in een maximaal beschikbare en configuratie van taakverdeling.|
| [Een virtuele machine maken en voer het script voor configuratie](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Een virtuele machine maakt en hello Azure aangepast Script extensie tooinstall IIS gebruikt. |
| [Een virtuele machine maken en uitvoeren van de DSC-configuratie](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Een virtuele machine maakt en hello Azure Desired State Configuration (DSC)-extensie tooinstall IIS gebruikt. |
| [Een VHD uploaden en virtuele machines maken](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | Uplaods een lokale VHD tooAzure bestand, maakt en een installatiekopie van Hallo VHD en maakt vervolgens een virtuele machine vanuit die installatiekopie. |
| [Een virtuele machine maken van een beheerde OS-schijf](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Maakt een virtuele machine door het koppelen van een bestaande schijf beheerd als besturingssysteemschijf. |
| [Een virtuele machine maken vanuit een momentopname](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Een virtuele machine maakt vanuit een momentopname eerst een beheerde schijven maken vanuit een momentopname en vervolgens Hallo nieuwe beheerde schijf als besturingssysteemschijf te koppelen. |
|**Opslag beheren**||
| [Beheerde schijf maken vanaf een VHD in hetzelfde of een ander abonnement](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Hiermee maakt een beheerde schijf vanaf een speciale VHD als een besturingssysteemschijf of uit een VHD als gegevensschijf in hetzelfde of een ander abonnement.  |
| [Een beheerde schijf maken vanuit een momentopname](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Maakt een beheerde schijf van een momentopname. |
| [Toosame beheerde schijf of een ander abonnement niet kopiëren](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Exemplaren beheerd schijf toosame of een ander abonnement maar Hallo in dezelfde regio bevinden als Hallo bovenliggende schijf worden beheerd. 
| [Een momentopname exporteren als VHD tooa storage-account](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Exporteert een momentopname van een beheerde als VHD tooa storage-account in andere regio. |
| [Een momentopname maken van een VHD](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Maakt momentopname van een VHD-toocreate meerdere identieke beheerde schijven vanuit een momentopname in korte tijd.  |
| [Momentopname toosame of een ander abonnement kopiëren](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Kopieën momentopname toosame of ander abonnement maar in Hallo dezelfde regio bevinden als Hallo bovenliggende momentopname. |
|**Beveiligde virtuele machines**||
| [Versleutelen van een VM- en gegevensschijven](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | Een Azure Sleutelkluis, de versleutelingssleutel en de service-principal gemaakt en vervolgens een virtuele machine versleutelt. |
|**Virtuele machines bewaken**||
| [Monitor voor een virtuele machine bij Operations Management Suite](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Een virtuele machine maakt, Hallo Operations Management Suite-agent geïnstalleerd en schrijft Hallo VM in een OMS-werkruimte.  |
| | |

