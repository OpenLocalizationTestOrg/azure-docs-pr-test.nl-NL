---
title: aaaExpand OS-schijf op Linux-VM met hello Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe tooexpand Hallo besturingssysteem (OS) virtuele schijf op een Linux-VM met hello Azure CLI 1.0 en Hallo Resource Manager-implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a>OS-schijf op een Linux-VM hello Azure CLI gebruiken met Azure CLI 1.0 Hallo uitbreiden
Hallo standaardgrootte virtuele harde schijf voor Hallo besturingssysteem (OS) is doorgaans 30 GB op een Linux virtuele machine (VM) in Azure. U kunt [gegevensschijven toevoegen](add-disk.md) tooprovide voor extra opslagruimte, maar u kunt ook desgewenst tooexpand Hallo OS-schijf. Dit artikel wordt uitgelegd hoe tooexpand Hallo OS schijf voor een Linux-VM met niet-beheerde schijven Hello Azure CLI 1.0.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#prerequisites) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](expand-disks.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="prerequisites"></a>Vereisten
Moet u Hallo [nieuwste Azure CLI 1.0](../../cli-install-nodejs.md) geïnstalleerd en geregistreerd in tooan [Azure-account](https://azure.microsoft.com/pricing/free-trial/) Hallo Resource Manager-modus als volgt gebruiken:

```azurecli
azure config mode arm
```

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup* en *myVM*.

## <a name="expand-os-disk"></a>Een besturingssysteemschijf uitbreiden

1. Bewerkingen op virtuele harde schijven kunnen niet worden uitgevoerd met Hallo VM uitgevoerd. Hallo volgende voorbeeld wordt gestopt en Hallo VM met de naam deallocates *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `azure vm stop`Geeft de rekenresources Hallo niet vrij. toorelease rekenresources, gebruikt u `azure vm deallocate`. Hallo VM moet ongedaan tooexpand Hallo virtuele hardeschijf.

2. Hallo-grootte van de besturingssysteemschijf Hallo zonder begeleiding Hallo met bijwerken `azure vm set` opdracht. Voorbeeld van updates na Hallo Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup* toobe *50* GB:

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. Start uw VM als volgt:

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM met de juiste referenties Hallo. tooverify hello OS-schijf is gewijzigd, gebruikt u `df -h`. Hallo voorbeelduitvoer na ziet u de primaire partitie Hallo (*/dev/sda1*) is nu 50 GB:

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a>Volgende stappen
Als u extra opslagruimte, moet u ook [gegevens schijven tooa Linux VM toevoegen](add-disk.md). Zie voor meer informatie over schijfversleuteling [versleutelen schijven op een Linux-VM met behulp van Azure CLI Hallo](encrypt-disks.md).
