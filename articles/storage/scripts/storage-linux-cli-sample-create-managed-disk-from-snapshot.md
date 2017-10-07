---
title: een beheerde schijf aaaAzure voorbeeldscript CLI - maken vanuit een momentopname | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een beheerde schijven maken vanuit een momentopname'
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
ms.openlocfilehash: f92059353bfb739cff05213a9d206bfde2829a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>Een beheerde schijf maken vanuit een momentopname met CLI

Dit script maakt een beheerde schijf van een momentopname. Gebruik dit toorestore een virtuele machine van de momentopnamen van het besturingssysteem en gegevensschijven. OS maken en gegevens van de respectieve momentopnamen schijven die worden beheerd en maak vervolgens een nieuwe virtuele machine door het koppelen van beheerde schijven. U kunt ook de gegevensschijven van een bestaande virtuele machine herstellen door het koppelen van gegevensschijven gemaakt op basis van momentopnamen.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt na opdrachten toocreate een beheerde schijf vanuit een momentopname. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ momentopname weergeven](https://docs.microsoft.com/cli/azure/snapshot#show) | Hiermee haalt u alle Hallo eigenschappen van een momentopname met de naam van de Hallo en eigenschappen van de bronnengroep van Hallo momentopname. Id-eigenschap is gebruikte toocreate beheerde schijf.  |
| [AZ schijf maken](https://docs.microsoft.com/cli/azure/disk#create) | Hiermee maakt u een beheerde met behulp van schijf-Id van een momentopname van een beheerde momentopname |

## <a name="next-steps"></a>Volgende stappen

[Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in Hallo [Azure Linux VM documentatie](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
