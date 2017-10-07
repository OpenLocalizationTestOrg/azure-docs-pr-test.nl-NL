---
title: aaaHow tooresize een Linux-VM met hello Azure CLI 2.0 | Microsoft Docs
description: Hoe Hallo tooscale omhoog of schaal omlaag virtuele Linux-machine, door het wijzigen van de VM-grootte.
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>Een virtuele Linux-machine met CLI 2.0 vergroten of verkleinen

Nadat u een virtuele machine (VM) inricht, u kunt Hallo VM omhoog of omlaag schalen door het wijzigen van Hallo [VM-grootte][vm-sizes]. In sommige gevallen moet u eerst Hallo VM ongedaan. U moet toodeallocate Hallo VM desgewenst grootte is niet beschikbaar op Hallo hardware cluster die als host voor Hallo VM fungeert Hallo. Dit artikel wordt uitgelegd hoe tooresize een Linux-VM met Azure CLI 2.0 Hallo. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="resize-a-vm"></a>De grootte van een virtuele machine wijzigen
tooresize een virtuele machine, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

1. Lijst met beschikbare virtuele machine Hallo groottes op Hallo hardware cluster waar Hallo VM wordt gehost met [az vm-vm-formaat-opties voor](/cli/azure/vm#list-vm-resize-options). Hallo volgende voorbeeld worden VM-grootten voor virtuele machine met de naam Hallo `myVM` in de resourcegroep Hallo `myResourceGroup` regio:
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. Als Hallo VM-grootte wordt vermeld gewenst, de grootte van Hallo VM met [az vm vergroten of verkleinen](/cli/azure/vm#resize). Hallo volgende voorbeeld wordt het formaat gewijzigd met de naam VM Hallo `myVM` toohello `Standard_DS3_v2` grootte:
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    Hallo VM opnieuw wordt opgestart tijdens dit proces. Na opnieuw opstarten hello wordt worden uw bestaande OS en de gegevensschijven toegewezen. Alles op Hallo tijdelijke schijf gaat verloren.

3. Desgewenst Hallo VM-grootte niet wordt vermeld, moet u toofirst ongedaan gemaakt met virtuele machine Hallo [az vm ongedaan gemaakt](/cli/azure/vm#deallocate). Dit proces kunt Hallo VM toothen formaat is gewijzigd tooany grootte zijn beschikbaar die Hallo regio ondersteunt en vervolgens worden gestart. Hallo volgt ongedaan gemaakt, vergroten of verkleinen en start vervolgens Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > Toewijzing Hallo VM versies ook dynamische IP-adressen toegewezen toohello VM. Hello OS- en gegevensschijven worden niet getroffen.

## <a name="next-steps"></a>Volgende stappen
Voor extra schaalbaarheid, meerdere exemplaren van de VM uitvoeren en uitbreiden. Zie voor meer informatie [automatisch schalen van Linux-machines in een virtuele-Machineschaalset][scale-set]. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
