---
title: een kopie van uw Linux-VM met hello Azure CLI 1.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een kopie van uw Azure Linux virtuele machine met Azure CLI 1.0 Hallo Hallo Resource Manager-implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>Maak een kopie van een virtuele Linux-machine uitgevoerd op Azure Hello Azure CLI 1.0
Dit artikel laat zien hoe een exemplaar van uw virtuele Azure-machine (VM) actieve Linux met toocreate Hallo Resource Manager-implementatiemodel. Eerst u Hallo-besturingssysteem en gegevens schijven tooa nieuwe container, worden overschreven klikt en vervolgens Hallo netwerkbronnen instellen en Hallo nieuwe virtuele machine maken.

U kunt ook [uploaden en een virtuele machine maken van aangepaste schijfimage](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- Azure CLI 1.0 – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="before-you-begin"></a>Voordat u begint
Zorg ervoor dat u voldoet aan de volgende vereisten voordat u de stappen Hallo Hallo:

* U hebt Hallo [Azure CLI](../../cli-install-nodejs.md) gedownload en geïnstalleerd op uw computer. 
* Ook moet u enkele gegevens over uw bestaande Azure Linux VM:

| Informatie over het bron-VM | Waar tooget deze |
| --- | --- |
| VM-naam |`azure vm list` |
| De naam van resourcegroep |`azure vm list` |
| Locatie |`azure vm list` |
| Naam van het opslagaccount |`azure storage account list -g <resourceGroup>` |
| Containernaam |`azure storage container list -a <sourcestorageaccountname>` |
| Bronnaam VM VHD-bestand |`azure storage blob list --container <containerName>` |

* U moet toomake enkele mogelijkheden over de nieuwe virtuele machine:   <br> -Containernaam   <br> VM - naam   <br> VM - grootte   <br> -vNet-naam   <br> -Subnetnaam   <br> -IP-naam   <br> De naam van de - NIC

## <a name="login-and-set-your-subscription"></a>Aanmelding en stel uw abonnement
1. Aanmelding toohello CLI.

    ```azurecli
    azure login
    ```
2. Zorg ervoor dat u in de modus Resource Manager.

    ```azurecli
    azure config mode arm
    ```
3. Het juiste abonnement Hallo ingesteld. U kunt een lijst met azure-account toosee al uw abonnementen.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>Hallo VM stoppen
Stop en Hallo bron-VM ongedaan gemaakt. Lijst met azure vm tooget een lijst met alle Hallo VM's kunt u in uw abonnement en de namen van resourcegroepen.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>Hallo VHD kopiëren
U kunt VHD Hallo kopiëren van Hallo bron toohello opslaglocatie Hallo met `azure storage blob copy start`. In dit voorbeeld gaan we toocopy Hallo VHD toohello hetzelfde opslagaccount, maar een andere container.

toocopy hello VHD tooanother container in Hallo hetzelfde opslagaccount, type:

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>Hallo virtueel netwerk instellen voor uw nieuwe virtuele machine
Stel een virtueel netwerk en de NIC in voor uw nieuwe virtuele machine. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>Maken van nieuwe virtuele machine Hallo
U kunt nu een virtuele machine maken van de geüploade virtuele schijf [met behulp van een resource manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) of via Hallo CLI door te geven Hallo URI tooyour schijf gekopieerd door te typen:

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>Volgende stappen
toolearn hoe toouse Azure CLI toomanage uw nieuwe virtuele machine, Zie [Azure CLI-opdrachten voor hello Azure Resource Manager](../azure-cli-arm-commands.md).

