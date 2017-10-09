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
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a><span data-ttu-id="30a39-103">OS-schijf op een Linux-VM hello Azure CLI gebruiken met Azure CLI 1.0 Hallo uitbreiden</span><span class="sxs-lookup"><span data-stu-id="30a39-103">Expand OS disk on a Linux VM using hello Azure CLI with hello Azure CLI 1.0</span></span>
<span data-ttu-id="30a39-104">Hallo standaardgrootte virtuele harde schijf voor Hallo besturingssysteem (OS) is doorgaans 30 GB op een Linux virtuele machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="30a39-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="30a39-105">U kunt [gegevensschijven toevoegen](add-disk.md) tooprovide voor extra opslagruimte, maar u kunt ook desgewenst tooexpand Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="30a39-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand hello OS disk.</span></span> <span data-ttu-id="30a39-106">Dit artikel wordt uitgelegd hoe tooexpand Hallo OS schijf voor een Linux-VM met niet-beheerde schijven Hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="30a39-106">This article details how tooexpand hello OS disk for a Linux VM using unmanaged disks with hello Azure CLI 1.0.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="30a39-107">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="30a39-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="30a39-108">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="30a39-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="30a39-109">[Azure CLI 1.0](#prerequisites) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="30a39-109">[Azure CLI 1.0](#prerequisites) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="30a39-110">[Azure CLI 2.0](expand-disks.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="30a39-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30a39-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="30a39-111">Prerequisites</span></span>
<span data-ttu-id="30a39-112">Moet u Hallo [nieuwste Azure CLI 1.0](../../cli-install-nodejs.md) geïnstalleerd en geregistreerd in tooan [Azure-account](https://azure.microsoft.com/pricing/free-trial/) Hallo Resource Manager-modus als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="30a39-112">You need hello [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in tooan [Azure account](https://azure.microsoft.com/pricing/free-trial/) using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="30a39-113">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="30a39-113">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="30a39-114">De namen van de voorbeeld-parameter *myResourceGroup* en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="30a39-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="30a39-115">Een besturingssysteemschijf uitbreiden</span><span class="sxs-lookup"><span data-stu-id="30a39-115">Expand OS disk</span></span>

1. <span data-ttu-id="30a39-116">Bewerkingen op virtuele harde schijven kunnen niet worden uitgevoerd met Hallo VM uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="30a39-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="30a39-117">Hallo volgende voorbeeld wordt gestopt en Hallo VM met de naam deallocates *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="30a39-117">hello following example stops and deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="30a39-118">`azure vm stop`Geeft de rekenresources Hallo niet vrij.</span><span class="sxs-lookup"><span data-stu-id="30a39-118">`azure vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="30a39-119">toorelease rekenresources, gebruikt u `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="30a39-119">toorelease compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="30a39-120">Hallo VM moet ongedaan tooexpand Hallo virtuele hardeschijf.</span><span class="sxs-lookup"><span data-stu-id="30a39-120">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="30a39-121">Hallo-grootte van de besturingssysteemschijf Hallo zonder begeleiding Hallo met bijwerken `azure vm set` opdracht.</span><span class="sxs-lookup"><span data-stu-id="30a39-121">Update hello size of hello unmanaged OS disk using hello `azure vm set` command.</span></span> <span data-ttu-id="30a39-122">Voorbeeld van updates na Hallo Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup* toobe *50* GB:</span><span class="sxs-lookup"><span data-stu-id="30a39-122">hello following example updates hello VM named *myVM* in hello resource group named *myResourceGroup* toobe *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="30a39-123">Start uw VM als volgt:</span><span class="sxs-lookup"><span data-stu-id="30a39-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="30a39-124">SSH tooyour VM met de juiste referenties Hallo.</span><span class="sxs-lookup"><span data-stu-id="30a39-124">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="30a39-125">tooverify hello OS-schijf is gewijzigd, gebruikt u `df -h`.</span><span class="sxs-lookup"><span data-stu-id="30a39-125">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="30a39-126">Hallo voorbeelduitvoer na ziet u de primaire partitie Hallo (*/dev/sda1*) is nu 50 GB:</span><span class="sxs-lookup"><span data-stu-id="30a39-126">hello following example output shows hello primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="30a39-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="30a39-127">Next steps</span></span>
<span data-ttu-id="30a39-128">Als u extra opslagruimte, moet u ook [gegevens schijven tooa Linux VM toevoegen](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="30a39-128">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="30a39-129">Zie voor meer informatie over schijfversleuteling [versleutelen schijven op een Linux-VM met behulp van Azure CLI Hallo](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="30a39-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
