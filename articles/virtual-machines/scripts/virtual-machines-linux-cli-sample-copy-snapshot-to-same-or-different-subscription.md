---
title: aaaAzure voorbeeldscript CLI - exemplaar (verplaatsen)-momentopname van een beheerde schijf toosame of een ander abonnement met CLI | Microsoft Docs
description: Azure CLI-voorbeeldscript - exemplaar (verplaatsen)-momentopname van een beheerde schijf toosame of een ander abonnement met CLI
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
ms.openlocfilehash: f214ab1fc1cb2cb42479d82e455f20a8cc55c83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>Kopiëren van de momentopname van een beheerde schijf toosame of een ander abonnement met CLI

Dit script wordt gekopieerd van een momentopname van een beheerde schijf toosame of een ander abonnement. Gebruik dit script toomove een momentopname toodifferent abonnement in Hallo dezelfde regio bevinden als Hallo bovenliggende momentopname.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van opdrachten toocreate na een momentopname aan Hallo doel abonnement met Hallo Hallo bron momentopname-Id. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ momentopname weergeven](https://docs.microsoft.com/cli/azure/snapshot#show) | Hiermee haalt u alle Hallo eigenschappen van een momentopname met de naam van de Hallo en eigenschappen van de bronnengroep van Hallo momentopname. Id-eigenschap is gebruikte toocopy Hallo momentopname toodifferent abonnement.  |
| [AZ momentopname maken](https://docs.microsoft.com/cli/azure/snapshot#create) | Een momentopname van een door het maken van een momentopname bij het gebruik van verschillende abonnement-Id en de naam van Hallo kopieën Hallo bovenliggende momentopname.  |

## <a name="next-steps"></a>Volgende stappen

[Een virtuele machine maken vanuit een momentopname](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in Hallo [Azure Linux VM documentatie](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
