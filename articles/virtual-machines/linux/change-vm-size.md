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
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="925f7-103">Een virtuele Linux-machine met CLI 2.0 vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="925f7-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="925f7-104">Nadat u een virtuele machine (VM) inricht, u kunt Hallo VM omhoog of omlaag schalen door het wijzigen van Hallo [VM-grootte][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="925f7-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="925f7-105">In sommige gevallen moet u eerst Hallo VM ongedaan.</span><span class="sxs-lookup"><span data-stu-id="925f7-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="925f7-106">U moet toodeallocate Hallo VM desgewenst grootte is niet beschikbaar op Hallo hardware cluster die als host voor Hallo VM fungeert Hallo.</span><span class="sxs-lookup"><span data-stu-id="925f7-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="925f7-107">Dit artikel wordt uitgelegd hoe tooresize een Linux-VM met Azure CLI 2.0 Hallo.</span><span class="sxs-lookup"><span data-stu-id="925f7-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="925f7-108">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="925f7-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="925f7-109">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="925f7-109">Resize a VM</span></span>
<span data-ttu-id="925f7-110">tooresize een virtuele machine, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="925f7-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="925f7-111">Lijst met beschikbare virtuele machine Hallo groottes op Hallo hardware cluster waar Hallo VM wordt gehost met [az vm-vm-formaat-opties voor](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="925f7-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="925f7-112">Hallo volgende voorbeeld worden VM-grootten voor virtuele machine met de naam Hallo `myVM` in de resourcegroep Hallo `myResourceGroup` regio:</span><span class="sxs-lookup"><span data-stu-id="925f7-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="925f7-113">Als Hallo VM-grootte wordt vermeld gewenst, de grootte van Hallo VM met [az vm vergroten of verkleinen](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="925f7-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="925f7-114">Hallo volgende voorbeeld wordt het formaat gewijzigd met de naam VM Hallo `myVM` toohello `Standard_DS3_v2` grootte:</span><span class="sxs-lookup"><span data-stu-id="925f7-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="925f7-115">Hallo VM opnieuw wordt opgestart tijdens dit proces.</span><span class="sxs-lookup"><span data-stu-id="925f7-115">hello VM restarts during this process.</span></span> <span data-ttu-id="925f7-116">Na opnieuw opstarten hello wordt worden uw bestaande OS en de gegevensschijven toegewezen.</span><span class="sxs-lookup"><span data-stu-id="925f7-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="925f7-117">Alles op Hallo tijdelijke schijf gaat verloren.</span><span class="sxs-lookup"><span data-stu-id="925f7-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="925f7-118">Desgewenst Hallo VM-grootte niet wordt vermeld, moet u toofirst ongedaan gemaakt met virtuele machine Hallo [az vm ongedaan gemaakt](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="925f7-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="925f7-119">Dit proces kunt Hallo VM toothen formaat is gewijzigd tooany grootte zijn beschikbaar die Hallo regio ondersteunt en vervolgens worden gestart.</span><span class="sxs-lookup"><span data-stu-id="925f7-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="925f7-120">Hallo volgt ongedaan gemaakt, vergroten of verkleinen en start vervolgens Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="925f7-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="925f7-121">Toewijzing Hallo VM versies ook dynamische IP-adressen toegewezen toohello VM.</span><span class="sxs-lookup"><span data-stu-id="925f7-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="925f7-122">Hello OS- en gegevensschijven worden niet getroffen.</span><span class="sxs-lookup"><span data-stu-id="925f7-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="925f7-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="925f7-123">Next steps</span></span>
<span data-ttu-id="925f7-124">Voor extra schaalbaarheid, meerdere exemplaren van de VM uitvoeren en uitbreiden. Zie voor meer informatie [automatisch schalen van Linux-machines in een virtuele-Machineschaalset][scale-set].</span><span class="sxs-lookup"><span data-stu-id="925f7-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
