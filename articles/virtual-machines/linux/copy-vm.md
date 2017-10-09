---
title: een Linux-VM met behulp van Azure CLI 2.0 aaaCopy | Microsoft Docs
description: Meer informatie over hoe toocreate een kopie van uw Azure Linux virtuele machine met behulp van Azure CLI 2.0 en schijven beheerd.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>Maak een kopie van een Linux-VM met behulp van Azure CLI 2.0 en schijven beheerd


Dit artikel laat zien hoe een kopie van uw Azure virtuele machine (VM) met behulp van Linux toocreate hello Azure CLI 2.0 en hello Azure Resource Manager-implementatiemodel. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

U kunt ook [uploaden en een virtuele machine maken vanaf een VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Vereisten


-   Installeer [Azure CLI 2.0](/cli/azure/install-az-cli2)

-   Meld u aan tooan Azure-account met [az aanmelding](/cli/azure/#login).

-   Een virtuele machine van Azure toouse als Hallo bron voor uw exemplaar hebben.

## <a name="step-1-stop-hello-source-vm"></a>Stap 1: Hallo bron-VM stoppen


Hallo bron-VM met behulp van toewijzing [az vm ongedaan](/cli/azure/vm#deallocate).
Hallo volgende voorbeeld deallocates Hallo VM met de naam **myVM** in de resourcegroep Hallo **myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>Stap 2: Kopieer Hallo bron-VM


toocopy een virtuele machine, maakt u een kopie van Hallo onderliggende virtuele harde schijf. Dit proces maakt een gespecialiseerde VHD als een schijf beheerd Hallo met dezelfde configuratie en instellingen als Hallo bron-VM.

Zie [Overzicht van Azure Managed Disks](../windows/managed-disks-overview.md) voor meer informatie over Azure Managed Disks. 

1.  Lijst van de OS-schijf met de naam van elke virtuele machine en Hallo [az vm lijst](/cli/azure/vm#list). Hallo volgende voorbeeld worden alle virtuele machines in de resourcegroep met de naam **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  Hallo diskette kopiëren door het maken van een nieuwe schijf met beheerd [az schijf maken](/cli/azure/disk#create). Hallo volgende voorbeeld wordt een schijf met de naam **myCopiedDisk** beheerd schijf met de naam van Hallo **myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  Hallo beheerd schijven nu in de resourcegroep controleren met behulp van [az Schijflijst](/cli/azure/disk#list). Hallo volgende voorbeeld worden beheerd Hallo schijven in de resourcegroep Hallo met de naam **myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  Overslaan te[' stap 3: een virtueel netwerk instellen '](#step-3-set-up-a-virtual-network).


## <a name="step-3-set-up-a-virtual-network"></a>Stap 3: Een virtueel netwerk instellen


Hallo Maak volgende optionele stappen een nieuw virtueel netwerk, subnet, openbare IP-adres en virtuele netwerkinterfacekaart (NIC).

Als u een virtuele machine voor het oplossen van problemen of aanvullende implementaties kopieert, wilt u mogelijk niet toouse een virtuele machine in een bestaand virtueel netwerk.

Als u een virtuele-netwerkinfrastructuur toocreate wilt voor de gekopieerde virtuele machines, Hallo Volg volgende stappen. Als u een virtueel netwerk toocreate niet wilt, gaat u verder te[stap 4: een virtuele machine maken](#step-4-create-a-vm).

1.  Hallo virtueel netwerk maken met behulp van [az network vnet maken](/cli/azure/network/vnet#create). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam **myVnet** en een subnet met de naam **mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  Maken van een openbaar IP-adres met behulp van [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create). Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam **myPublicIP** met Hallo DNS-naam van **mypublicdns**. (Hallo DNS-naam moet uniek zijn, dus een unieke naam opgeven.)

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  Maak Hallo NIC met [az netwerk nic maken](/cli/azure/network/nic#create).
    Hallo volgende voorbeeld wordt een NIC met de naam **myNic** die gekoppelde toothe **mySubnet** subnet:

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>Stap 4: Een virtuele machine maken

U kunt nu een virtuele machine maken met behulp van [az vm maken](/cli/azure/vm#create).

Geef Hallo gekopieerd toouse als Hallo OS-schijf beheerde schijven (--koppelen-os-schijf), als volgt:

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>Volgende stappen

toolearn hoe toouse Azure CLI toomanage uw nieuwe VM Zie [Azure CLI-opdrachten voor hello Azure Resource Manager](../azure-cli-arm-commands.md).
