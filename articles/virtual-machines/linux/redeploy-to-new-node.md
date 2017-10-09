---
title: aaaRedeploy Linux virtuele Machines in Azure | Microsoft Docs
description: Hoe problemen die tooredeploy Linux virtuele machines in Azure toomitigate SSH-verbinding.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a>Linux-virtuele machine toonew Azure knooppunt opnieuw implementeren
Als u problemen bij het oplossen van SSH wordt geconfronteerd of toepassing access tooa Linux virtuele machine (VM) in Azure, kan Hallo VM opnieuw distribueren helpen. Wanneer u een virtuele machine opnieuw implementeert, wordt verplaatst Hallo VM tooa nieuw knooppunt binnen hello Azure-infrastructuur en wordt deze vervolgens weer ingeschakeld. Alle configuratie-opties en bijbehorende bronnen worden bewaard. Dit artikel ziet u hoe tooredeploy een VM die gebruikmaakt van Azure CLI of hello Azure-portal.

> [!NOTE]
> Nadat u een virtuele machine opnieuw implementeren, is Hallo tijdelijke schijf verloren en dynamische IP-adressen die zijn gekoppeld aan virtuele netwerkinterface worden bijgewerkt. 

U kunt een virtuele machine met behulp van een Hallo volgend opties voor opnieuw implementeren. U hoeft alleen toochoose één optie tooredeploy uw virtuele machine:

- [Azure CLI 2.0](#azure-cli-20)
- [Azure CLI 1.0](#azure-cli-10)
- [Azure Portal](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a>Hello Azure CLI 2.0 gebruiken
Meest recente installatie Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).

Implementeren van uw virtuele machine met [az vm opnieuw distribueren](/cli/azure/vm#redeploy). voorbeeld redeploys na Hallo Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a>Gebruik hello Azure CLI 1.0
Hallo installeren [nieuwste Azure CLI 1.0](../../cli-install-nodejs.md)tooan Azure-account aanmelden en zorg ervoor dat u in de modus Resource Manager (`azure config mode arm`).

voorbeeld redeploys na Hallo Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Volgende stappen
Als u verbinding maken met tooyour VM problemen ondervindt, kunt u Help-informatie vinden op [probleemoplossing SSH-verbindingen](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [gedetailleerde stappen voor probleemoplossing SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Als u geen toegang een toepassing die wordt uitgevoerd op de virtuele machine tot, kunt u ook lezen [toepassing het oplossen van problemen](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

