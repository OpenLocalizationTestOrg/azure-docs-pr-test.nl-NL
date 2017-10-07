---
title: aaaConvert virtuele Linux-machine in Azure uit niet-beheerde schijven toomanaged schijven - beheerde Azure-schijven | Microsoft Docs
description: Hoe een Linux-VM uit niet-beheerde schijven toomanaged tooconvert schijven met behulp van Azure CLI 2.0 Hallo Resource Manager-implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Een virtuele Linux-machine converteren van niet-beheerde schijven toomanaged schijven

Als u bestaande Linux virtuele machines (VM's) die gebruikmaken van niet-beheerde schijven hebt, Hallo VMs toouse beheerd schijven via hello, kunnen worden geconverteerd [Azure beheerd schijven](../windows/managed-disks-overview.md) service. Dit proces converteert Hallo OS-schijven en schijven bijgesloten gegevens.

Dit artikel laat zien hoe tooconvert virtuele machines met behulp van Azure CLI Hallo. Als u tooinstall moet of een upgrade uitvoeren, Zie [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Voordat u begint

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Single instance VMs converteren
Deze sectie bevat informatie over hoe tooconvert single instance Azure virtuele machines van niet-beheerde schijven toomanaged schijven. (Als uw virtuele machines zich in een beschikbaarheidsset, Zie de volgende sectie Hallo.) U kunt dit proces tooconvert Hallo VM's van premium (SSD) zonder begeleiding schijven toopremium beheerd-schijven, of van standaard (HDD) zonder begeleiding schijven toostandard beheerd schijven gebruiken.

1. Hallo VM ongedaan met behulp van [az vm ongedaan](/cli/azure/vm#deallocate). Hallo volgende voorbeeld deallocates Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Hallo VM toomanaged schijven worden geconverteerd met behulp van [az vm converteren](/cli/azure/vm#convert). Hallo na proces zet virtuele machine met de naam Hallo `myVM`, waaronder Hallo OS-schijf en eventuele gegevensschijven:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Hallo VM starten na Hallo conversie toomanaged schijven met behulp van [az vm start](/cli/azure/vm#start). Hallo volgende voorbeeld wordt gestart met de naam VM Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Converteren van virtuele machines in een beschikbaarheidsset

Als Hallo VM's die u wilt dat tooconvert toomanaged schijven zich bevinden in een beschikbaarheidsset, u eerst tooconvert Hallo beschikbaarheid set tooa beheerd moet beschikbaarheidsset.

Alle virtuele machines in de beschikbaarheidsset Hallo moeten ongedaan voordat u de beschikbaarheidsset Hallo converteert. Plan tooconvert alle schijven van virtuele machines toomanaged na Hallo beschikbaarheid zelf instellen is beschikbaarheidsset geconverteerde tooa beheerd. Vervolgens start alle Hallo VM's en verder te werken die normaal werken.

1. Lijst van alle virtuele machines in een beschikbaarheidsset met behulp van [az vm beschikbaarheidsset lijst](/cli/azure/vm/availability-set#list). Hallo volgende voorbeeld worden alle virtuele machines in Hallo beschikbaarheidsset benoemde `myAvailabilitySet` in Hallo resourcegroep met de naam `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Toewijzing van alle Hallo VM's met behulp van [az vm ongedaan](/cli/azure/vm#deallocate). Hallo volgende voorbeeld deallocates Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Hallo beschikbaarheid instellen via converteren [az vm-beschikbaarheidsset converteren](/cli/azure/vm/availability-set#convert). Hallo volgende voorbeeld wordt geconverteerd Hallo beschikbaarheidsset benoemde `myAvailabilitySet` in Hallo resourcegroep met de naam `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Converteert alle Hallo VMs toomanaged schijven met behulp van [az vm converteren](/cli/azure/vm#convert). Hallo na proces zet virtuele machine met de naam Hallo `myVM`, waaronder Hallo OS-schijf en eventuele gegevensschijven:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Start alle Hallo VM's na Hallo conversie toomanaged schijven met behulp van [az vm start](/cli/azure/vm#start). Hallo volgende voorbeeld wordt gestart met de naam VM Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over opties voor opslag, [Azure beheerd schijven overzicht](../windows/managed-disks-overview.md).
