---
title: 'Azure CLI-Script voorbeeld: een beheerde schijven maken vanuit een momentopname | Microsoft Docs'
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
ms.openlocfilehash: 68e17ae9e5d82da7f9be9d36e3e2324a2aeadbc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>Een beheerde schijf maken vanuit een momentopname met CLI

Dit script maakt een beheerde schijf van een momentopname. Gebruik dit voor een virtuele machine herstellen van momentopnamen van het besturingssysteem en gegevensschijven. OS maken en gegevens van de respectieve momentopnamen schijven die worden beheerd en maak vervolgens een nieuwe virtuele machine door het koppelen van beheerde schijven. U kunt ook de gegevensschijven van een bestaande virtuele machine herstellen door het koppelen van gegevensschijven gemaakt op basis van momentopnamen.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[belangrijkste](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "-beheerde schijven maken vanuit een momentopname.")]


## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt na de opdrachten voor het maken van een beheerde schijf vanuit een momentopname. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [AZ momentopname weergeven](https://docs.microsoft.com/cli/azure/snapshot#show) | Hiermee haalt u de eigenschappen van een momentopname met de naam en eigenschappen van de momentopname van de bronnengroep. Id-eigenschap wordt gebruikt om beheerde schijf te maken.  |
| [AZ schijf maken](https://docs.microsoft.com/cli/azure/disk#create) | Hiermee maakt u een beheerde met behulp van schijf-Id van een momentopname van een beheerde momentopname |

## <a name="next-steps"></a>Volgende stappen

[Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
