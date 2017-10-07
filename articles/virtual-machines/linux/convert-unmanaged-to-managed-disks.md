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
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="45ecc-103">Een virtuele Linux-machine converteren van niet-beheerde schijven toomanaged schijven</span><span class="sxs-lookup"><span data-stu-id="45ecc-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="45ecc-104">Als u bestaande Linux virtuele machines (VM's) die gebruikmaken van niet-beheerde schijven hebt, Hallo VMs toouse beheerd schijven via hello, kunnen worden geconverteerd [Azure beheerd schijven](../windows/managed-disks-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="45ecc-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="45ecc-105">Dit proces converteert Hallo OS-schijven en schijven bijgesloten gegevens.</span><span class="sxs-lookup"><span data-stu-id="45ecc-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="45ecc-106">Dit artikel laat zien hoe tooconvert virtuele machines met behulp van Azure CLI Hallo.</span><span class="sxs-lookup"><span data-stu-id="45ecc-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="45ecc-107">Als u tooinstall moet of een upgrade uitvoeren, Zie [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="45ecc-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="45ecc-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="45ecc-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="45ecc-109">Single instance VMs converteren</span><span class="sxs-lookup"><span data-stu-id="45ecc-109">Convert single-instance VMs</span></span>
<span data-ttu-id="45ecc-110">Deze sectie bevat informatie over hoe tooconvert single instance Azure virtuele machines van niet-beheerde schijven toomanaged schijven.</span><span class="sxs-lookup"><span data-stu-id="45ecc-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="45ecc-111">(Als uw virtuele machines zich in een beschikbaarheidsset, Zie de volgende sectie Hallo.) U kunt dit proces tooconvert Hallo VM's van premium (SSD) zonder begeleiding schijven toopremium beheerd-schijven, of van standaard (HDD) zonder begeleiding schijven toostandard beheerd schijven gebruiken.</span><span class="sxs-lookup"><span data-stu-id="45ecc-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="45ecc-112">Hallo VM ongedaan met behulp van [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="45ecc-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="45ecc-113">Hallo volgende voorbeeld deallocates Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="45ecc-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="45ecc-114">Hallo VM toomanaged schijven worden geconverteerd met behulp van [az vm converteren](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="45ecc-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="45ecc-115">Hallo na proces zet virtuele machine met de naam Hallo `myVM`, waaronder Hallo OS-schijf en eventuele gegevensschijven:</span><span class="sxs-lookup"><span data-stu-id="45ecc-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="45ecc-116">Hallo VM starten na Hallo conversie toomanaged schijven met behulp van [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="45ecc-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="45ecc-117">Hallo volgende voorbeeld wordt gestart met de naam VM Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="45ecc-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="45ecc-118">Converteren van virtuele machines in een beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="45ecc-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="45ecc-119">Als Hallo VM's die u wilt dat tooconvert toomanaged schijven zich bevinden in een beschikbaarheidsset, u eerst tooconvert Hallo beschikbaarheid set tooa beheerd moet beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="45ecc-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="45ecc-120">Alle virtuele machines in de beschikbaarheidsset Hallo moeten ongedaan voordat u de beschikbaarheidsset Hallo converteert.</span><span class="sxs-lookup"><span data-stu-id="45ecc-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="45ecc-121">Plan tooconvert alle schijven van virtuele machines toomanaged na Hallo beschikbaarheid zelf instellen is beschikbaarheidsset geconverteerde tooa beheerd.</span><span class="sxs-lookup"><span data-stu-id="45ecc-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="45ecc-122">Vervolgens start alle Hallo VM's en verder te werken die normaal werken.</span><span class="sxs-lookup"><span data-stu-id="45ecc-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="45ecc-123">Lijst van alle virtuele machines in een beschikbaarheidsset met behulp van [az vm beschikbaarheidsset lijst](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="45ecc-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="45ecc-124">Hallo volgende voorbeeld worden alle virtuele machines in Hallo beschikbaarheidsset benoemde `myAvailabilitySet` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="45ecc-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="45ecc-125">Toewijzing van alle Hallo VM's met behulp van [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="45ecc-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="45ecc-126">Hallo volgende voorbeeld deallocates Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="45ecc-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="45ecc-127">Hallo beschikbaarheid instellen via converteren [az vm-beschikbaarheidsset converteren](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="45ecc-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="45ecc-128">Hallo volgende voorbeeld wordt geconverteerd Hallo beschikbaarheidsset benoemde `myAvailabilitySet` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="45ecc-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="45ecc-129">Converteert alle Hallo VMs toomanaged schijven met behulp van [az vm converteren](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="45ecc-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="45ecc-130">Hallo na proces zet virtuele machine met de naam Hallo `myVM`, waaronder Hallo OS-schijf en eventuele gegevensschijven:</span><span class="sxs-lookup"><span data-stu-id="45ecc-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="45ecc-131">Start alle Hallo VM's na Hallo conversie toomanaged schijven met behulp van [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="45ecc-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="45ecc-132">Hallo volgende voorbeeld wordt gestart met de naam VM Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="45ecc-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="45ecc-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45ecc-133">Next steps</span></span>
<span data-ttu-id="45ecc-134">Zie voor meer informatie over opties voor opslag, [Azure beheerd schijven overzicht](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45ecc-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
