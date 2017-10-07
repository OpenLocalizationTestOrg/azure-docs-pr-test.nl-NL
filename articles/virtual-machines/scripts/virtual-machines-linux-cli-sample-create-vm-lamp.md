---
title: aaaAzure voorbeeldscript CLI - Hallo licht Stack in een Load-Balanced Virtual Machin implementeren | Microsoft Docs
description: Gebruik een aangepast script extensie toodeploy Hallo licht Stack in de belasting = taakverdeling virtuele-machineschaalset ingesteld op Azure.
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Hallo licht stack in een taakverdeling virtuele-machineschaalset implementeren

In dit voorbeeld maakt u een virtuele-machineschaalset en past een uitbreiding die een aangepast script toodeploy Hallo licht stack op elke virtuele machine in de schaalset hello wordt uitgevoerd.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Verbinding maken

Gebruik deze code toosee hoe tooconnect tooyour VM's en schaal ingesteld.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, Hallo schaalset en virtuele machines en alle gerelateerde resources worden uitgevoerd.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ vmss maken](https://docs.microsoft.com/cli/azure/vmss#create) | Hiermee maakt u een virtuele-machineschaalset |
| [AZ network Load Balancer-regel maken](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Een eindpunt met gelijke taakverdeling toevoegen |
| [AZ vmss extensie instellen](https://docs.microsoft.com/cli/azure/vmss/extension#set) | Hallo-extensie die Hallo aangepast script wordt uitgevoerd op de implementatie van een virtuele machine maken |
| [AZ vmss update-exemplaren](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Hallo aangepast script uitvoeren op Hallo VM-exemplaren die zijn geïmplementeerd voordat het Hallo-uitbreiding is toegepast toohello schaalset. |
| [AZ vmss schaal](https://docs.microsoft.com/cli/azure/vmss#scale) | Opschalen Hallo scale ingesteld door meer VM-exemplaren toe te voegen. Hallo aangepast script wordt uitgevoerd op deze wanneer ze zijn geïmplementeerd. |
| [lijst met AZ netwerken openbare-ip](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Hallo IP-adressen van virtuele machines die zijn gemaakt door Hallo voorbeeld Hallo ophalen. |
| [AZ netwerk lb weergeven](https://docs.microsoft.com/cli/azure/network/lb#show) | Hallo frontend en backend poorten die worden gebruikt door Hallo load balancer ophalen. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
