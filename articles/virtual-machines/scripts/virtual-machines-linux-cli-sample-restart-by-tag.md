---
title: aaaAzure voorbeeldscript CLI - virtuele machines opnieuw opstarten | Microsoft Docs
description: Azure CLI-voorbeeldscript - virtuele machines opnieuw starten door de tag en -ID
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>Opnieuw opstarten van virtuele machines

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

Dit voorbeeld toont een aantal manieren tooget sommige virtuele machines en deze opnieuw opstarten.

Hallo eerst opnieuw wordt opgestart alle Hallo VM's in de resourcegroep Hallo.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

Hallo tweede opgehaald Hallo gelabeld virtuele machines met `az resouce list` filtert toohello resources die virtuele machines en deze VMs opnieuw wordt opgestart.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Dit voorbeeld werkt in een Bash-shell. Zie voor opties op Azure CLI-scripts die worden uitgevoerd op Windows-client [hello Azure CLI uitvoeren in Windows](../windows/cli-options.md).


## <a name="sample-script"></a>Voorbeeld van een script

Hallo voorbeeld heeft drie scripts.
Hallo eerst een bepaalde Hallo virtuele machines.
Hallo Nee-wait-optie wordt gebruikt zodat Hallo-opdracht geretourneerd zonder te wachten op elke virtuele machine toobe ingericht.
Hallo wacht tweede Hallo VMs toobe volledig is ingericht.
Hallo derde script start opnieuw alle Hallo VM's die zijn ingericht en vervolgens alleen Hallo label voor virtuele machines.

### <a name="provision-hello-vms"></a>Hallo virtuele machines inrichten

Dit script maakt een resourcegroep en maakt vervolgens het toorestart van drie virtuele machines.
Twee van deze zijn gelabeld.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Wait

Dit script wordt gecontroleerd op Hallo Inrichtingsstatus elke 20 seconden totdat alle drie virtuele machines zijn ingericht, of een van beide tooprovision is mislukt.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Hallo virtuele machines opnieuw opstarten

Dit script in de resourcegroep Hallo alle Hallo VM opnieuw wordt opgestart en het zojuist Hallo gelabeld virtuele machines opnieuw wordt opgestart.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Na het uitvoeren van het voorbeeldscript Hallo mag Hallo opdracht volgende gebruikte tooremove Hallo resourcegroepen, virtuele machines en alle gerelateerde bronnen.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Hallo virtuele machines maakt.  |
| [AZ vm lijst](https://docs.microsoft.com/cli/azure/vm#list) | Gebruikt met `--query` tooensure Hallo virtuele machines zijn ingericht voordat u ze opnieuw start en vervolgens tooget Hallo-id's van Hallo VMs toorestart ze. |
| [lijst met resources AZ](https://docs.microsoft.com/cli/azure/vm#list) | Gebruikt met `--query` tooget Hallo-id's van Hallo virtuele machines met behulp van Hallo-tag. |
| [AZ vm opnieuw opstarten](https://docs.microsoft.com/cli/azure/vm#list) | Hallo virtuele machines opnieuw is opgestart. |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
