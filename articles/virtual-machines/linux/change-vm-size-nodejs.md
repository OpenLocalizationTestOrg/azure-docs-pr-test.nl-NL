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
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="63991-103">Een virtuele Linux-machine met Azure CLI 1.0 vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="63991-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="63991-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="63991-104">Overview</span></span>

<span data-ttu-id="63991-105">Nadat u een virtuele machine (VM) inricht, u kunt Hallo VM omhoog of omlaag schalen door het wijzigen van Hallo [VM-grootte][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="63991-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="63991-106">In sommige gevallen moet u eerst Hallo VM ongedaan.</span><span class="sxs-lookup"><span data-stu-id="63991-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="63991-107">Dit kan gebeuren als de nieuwe grootte voor het Hallo is niet beschikbaar op Hallo hardware cluster die als host voor Hallo VM fungeert.</span><span class="sxs-lookup"><span data-stu-id="63991-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="63991-108">Dit artikel laat zien hoe tooresize een Linux-VM met Hallo [Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="63991-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="63991-109">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="63991-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="63991-110">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63991-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="63991-111">[Azure CLI 1.0](#resize-a-linux-vm) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="63991-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="63991-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="63991-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="63991-113">Een virtuele Linux-machine vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="63991-113">Resize a Linux VM</span></span>
<span data-ttu-id="63991-114">een VM tooresize uitvoeren Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="63991-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="63991-115">Hallo na CLI-opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="63991-115">Run hello following CLI command.</span></span> <span data-ttu-id="63991-116">Met deze opdracht worden Hallo VM-grootten die beschikbaar zijn op Hallo hardware cluster waar hello VM wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="63991-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="63991-117">Als Hallo grootte wordt vermeld gewenst, voert u Hallo opdracht tooresize Hallo VM te volgen.</span><span class="sxs-lookup"><span data-stu-id="63991-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="63991-118">Hallo VM wordt opnieuw opgestart tijdens dit proces.</span><span class="sxs-lookup"><span data-stu-id="63991-118">hello VM will restart during this process.</span></span> <span data-ttu-id="63991-119">Na opnieuw opstarten hello wordt uw bestaande besturingssysteem en gegevensschijven zal opnieuw worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="63991-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="63991-120">Alles op Hallo tijdelijke schijf zijn verloren.</span><span class="sxs-lookup"><span data-stu-id="63991-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="63991-121">Gebruik Hallo `--enable-boot-diagnostics` optie schakelt [opstarten diagnostics][boot-diagnostics], toolog eventuele gerelateerde fouten-toostartup.</span><span class="sxs-lookup"><span data-stu-id="63991-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="63991-122">Anders uitvoeren desgewenst Hallo formaat niet wordt vermeld, Hallo opdrachten toodeallocate Hallo VM, het formaat en Hallo VM start opnieuw op te volgen.</span><span class="sxs-lookup"><span data-stu-id="63991-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="63991-123">Toewijzing Hallo VM versies ook dynamische IP-adressen toegewezen toohello VM.</span><span class="sxs-lookup"><span data-stu-id="63991-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="63991-124">Hello OS- en gegevensschijven worden niet getroffen.</span><span class="sxs-lookup"><span data-stu-id="63991-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="63991-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63991-125">Next steps</span></span>
<span data-ttu-id="63991-126">Voor extra schaalbaarheid, meerdere exemplaren van de VM uitvoeren en uitbreiden. Zie voor meer informatie [automatisch schalen van Linux-machines in een virtuele-Machineschaalset][scale-set].</span><span class="sxs-lookup"><span data-stu-id="63991-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
