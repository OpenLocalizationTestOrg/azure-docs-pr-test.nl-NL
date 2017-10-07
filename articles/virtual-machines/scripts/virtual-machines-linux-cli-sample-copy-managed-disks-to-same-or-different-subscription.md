---
title: aaaAzure voorbeeldscript CLI - exemplaar (verplaatsen) beheerd toosame schijven of een ander abonnement | Microsoft Docs
description: Azure CLI voorbeeldscript - exemplaar (verplaatsen) beheerd schijven toosame of een ander abonnement
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: b1fa207bd6e05d7094be08855e7823e3b7686013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>Beheerde schijven toosame of een ander abonnement met CLI kopiëren

Dit script kopieert een beheerde schijf toosame of een ander abonnement maar Hallo in dezelfde regio. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van opdrachten toocreate na een nieuwe beheerde schijf bij het gebruik van Hallo doel abonnement Hallo Hallo bron-Id beheerd schijf. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ schijf weergeven](https://docs.microsoft.com/cli/azure/disk#show) | Hiermee haalt u alle Hallo-eigenschappen van een beheerde schijf met een Hallo groepseigenschappen en de bron van het Hallo-beheerde schijven. Id-eigenschap is gebruikte toocopy Hallo beheerd schijf toodifferent abonnement.  |
| [AZ schijf maken](https://docs.microsoft.com/cli/azure/disk#create) | Een beheerde schijf opgehaald door het maken van een nieuwe beheerde schijf in een ander abonnement-Id en naam Hallo bovenliggende schijf worden beheerd.  |

## <a name="next-steps"></a>Volgende stappen

[Een virtuele machine maken van een beheerde schijf](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in Hallo [Azure Linux VM documentatie](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
