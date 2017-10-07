---
title: aaaAzure voorbeeldscript CLI - een virtuele machine maken vanuit een momentopname | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een virtuele machine maken vanuit een momentopname'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a>Een virtuele machine maken vanuit een momentopname met CLI

Dit script maakt een virtuele machine van een momentopname van een besturingssysteemschijf.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate een beheerde schijf virtuele machine te volgen en alle bijbehorende resources. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ momentopname weergeven](https://docs.microsoft.com/cli/azure/snapshot#show) | Opgehaald momentopname met behulp van de naam van de momentopname en de naam van resourcegroep. Id-eigenschap van Hallo geretourneerde object is gebruikte toocreate een beheerde schijf.  |
| [AZ schijf maken](https://docs.microsoft.com/cli/azure/disk#create) | Beheerde schijven vanuit een momentopname maakt met behulp van een momentopname van Id, de schijfnaam van de, opslagtype en grootte  |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm#create) | Hiermee maakt u een VM die gebruikmaakt van een beheerde besturingssysteemschijf |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
