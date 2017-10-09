---
title: aaaAzure voorbeeldscript CLI - koppelpunt besturingssysteemschijf | Microsoft Docs
description: Azure CLI-voorbeeldscript - schijf koppelen-besturingssysteem
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>Problemen met een besturingssysteemschijf virtuele machines

Dit script koppelt Hallo besturingssysteemschijf van een virtuele machine is mislukt of problemen veroorzaken als gegevens schijf tooa tweede virtuele machine. Dit kan nuttig zijn bij het oplossen van problemen of -gegevens herstellen schijf. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ vm weergeven](https://docs.microsoft.com/cli/azure/vm#show) | Retourneert een lijst met virtuele machines. In dit geval is Hallo query-optie schijf besturingssysteem gebruikte tooreturn Hallo-virtuele machine. Deze waarde wordt vervolgens toegevoegd aan tooa variabelenaam 'uri'. |
| [AZ vm verwijderen](https://docs.microsoft.com/cli/azure/vm#delete) | Hiermee verwijdert u een virtuele machine. |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm#create) | Hiermee maakt u een virtuele machine.  |
| [AZ vm schijf koppelen](https://docs.microsoft.com/cli/azure/vm/disk#attach) | Er wordt een schijf tooa virtuele machine toegevoegd. |
| [AZ vm lijst-ip-adressen](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Retourneert Hallo IP-adressen van een virtuele machine. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
