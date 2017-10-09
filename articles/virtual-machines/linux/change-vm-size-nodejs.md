---
title: aaaHow tooresize een Linux-VM met hello Azure CLI 1.0 | Microsoft Docs
description: Hoe Hallo tooscale omhoog of schaal omlaag virtuele Linux-machine, door het wijzigen van de VM-grootte.
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>Een virtuele Linux-machine met Azure CLI 1.0 vergroten of verkleinen

## <a name="overview"></a>Overzicht

Nadat u een virtuele machine (VM) inricht, u kunt Hallo VM omhoog of omlaag schalen door het wijzigen van Hallo [VM-grootte][vm-sizes]. In sommige gevallen moet u eerst Hallo VM ongedaan. Dit kan gebeuren als de nieuwe grootte voor het Hallo is niet beschikbaar op Hallo hardware cluster die als host voor Hallo VM fungeert.

Dit artikel laat zien hoe tooresize een Linux-VM met Hallo [Azure CLI][azure-cli].

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#resize-a-linux-vm) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="resize-a-linux-vm"></a>Een virtuele Linux-machine vergroten of verkleinen
een VM tooresize uitvoeren Hallo stappen te volgen.

1. Hallo na CLI-opdracht wordt uitgevoerd. Met deze opdracht worden Hallo VM-grootten die beschikbaar zijn op Hallo hardware cluster waar hello VM wordt gehost.
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. Als Hallo grootte wordt vermeld gewenst, voert u Hallo opdracht tooresize Hallo VM te volgen.
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    Hallo VM wordt opnieuw opgestart tijdens dit proces. Na opnieuw opstarten hello wordt uw bestaande besturingssysteem en gegevensschijven zal opnieuw worden toegewezen. Alles op Hallo tijdelijke schijf zijn verloren.
   
    Gebruik Hallo `--enable-boot-diagnostics` optie schakelt [opstarten diagnostics][boot-diagnostics], toolog eventuele gerelateerde fouten-toostartup.
3. Anders uitvoeren desgewenst Hallo formaat niet wordt vermeld, Hallo opdrachten toodeallocate Hallo VM, het formaat en Hallo VM start opnieuw op te volgen.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > Toewijzing Hallo VM versies ook dynamische IP-adressen toegewezen toohello VM. Hello OS- en gegevensschijven worden niet getroffen.
   > 
   > 

## <a name="next-steps"></a>Volgende stappen
Voor extra schaalbaarheid, meerdere exemplaren van de VM uitvoeren en uitbreiden. Zie voor meer informatie [automatisch schalen van Linux-machines in een virtuele-Machineschaalset][scale-set]. 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
