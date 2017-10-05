---
title: Het formaat van een Linux-VM met de Azure CLI 2.0 | Microsoft Docs
description: Het opschalen of terugschroeven virtuele Linux-machine, door het wijzigen van de VM-grootte.
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
ms.openlocfilehash: 23fc9f7f34732079682857d4ee685fe811751698
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="7b667-103">Een virtuele Linux-machine met CLI 2.0 vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="7b667-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="7b667-104">Nadat u een virtuele machine (VM) inricht, u kunt de virtuele machine omhoog of omlaag schalen door het wijzigen van de [VM-grootte][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="7b667-104">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="7b667-105">In sommige gevallen moet u eerst de VM ongedaan.</span><span class="sxs-lookup"><span data-stu-id="7b667-105">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="7b667-106">U moet de VM ongedaan gemaakt als de gewenste grootte is niet beschikbaar op het cluster hardware die als host voor de virtuele machine fungeert.</span><span class="sxs-lookup"><span data-stu-id="7b667-106">You need to deallocate the VM if the desired size is not available on the hardware cluster that is hosting the VM.</span></span> <span data-ttu-id="7b667-107">Dit artikel wordt uitgelegd hoe u dit moet een Linux-VM met de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="7b667-107">This article details how to resize a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="7b667-108">U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7b667-108">You can also perform these steps with the [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="7b667-109">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="7b667-109">Resize a VM</span></span>
<span data-ttu-id="7b667-110">Als u een virtuele machine, moet u de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in het gebruik van een Azure-account [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="7b667-110">To resize a VM, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="7b667-111">De lijst met beschikbare grootten voor virtuele machine weergeven op de hardware-cluster waarop de virtuele machine wordt gehost met [az vm-vm-formaat-opties voor](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="7b667-111">View the list of available VM sizes on the hardware cluster where the VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="7b667-112">Het volgende voorbeeld worden VM-grootten voor de virtuele machine met de naam `myVM` in de resourcegroep `myResourceGroup` regio:</span><span class="sxs-lookup"><span data-stu-id="7b667-112">The following example lists VM sizes for the VM named `myVM` in the resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="7b667-113">Als de gewenste VM-grootte wordt weergegeven, de grootte van de virtuele machine met [az vm vergroten of verkleinen](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="7b667-113">If the desired VM size is listed, resize the VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="7b667-114">Hiermee het volgende voorbeeld wordt ingesteld voor de virtuele machine met de naam `myVM` naar de `Standard_DS3_v2` grootte:</span><span class="sxs-lookup"><span data-stu-id="7b667-114">The following example resizes the VM named `myVM` to the `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="7b667-115">De virtuele machine opnieuw is opgestart tijdens dit proces.</span><span class="sxs-lookup"><span data-stu-id="7b667-115">The VM restarts during this process.</span></span> <span data-ttu-id="7b667-116">Na het opnieuw opstarten, worden uw bestaande OS en de gegevensschijven toegewezen.</span><span class="sxs-lookup"><span data-stu-id="7b667-116">After the restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="7b667-117">Alles op de tijdelijke schijf gaat verloren.</span><span class="sxs-lookup"><span data-stu-id="7b667-117">Anything on the temporary disk is lost.</span></span>

3. <span data-ttu-id="7b667-118">Als de gewenste VM-grootte niet wordt weergegeven, moet u eerst de virtuele machine met de toewijzing [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="7b667-118">If the desired VM size is not listed, you need to first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="7b667-119">Dit proces kan de virtuele machine vervolgens worden aangepast aan de grootte die beschikbaar is dat de regio ondersteunt en vervolgens worden gestart.</span><span class="sxs-lookup"><span data-stu-id="7b667-119">This process allows the VM to then be resized to any size available that the region supports and then started.</span></span> <span data-ttu-id="7b667-120">De volgende stappen ongedaan gemaakt, vergroten of verkleinen en start vervolgens de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7b667-120">The following steps deallocate, resize, and then start the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="7b667-121">Toewijzing van de virtuele machine ook versies van dynamische IP-adressen toegewezen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7b667-121">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="7b667-122">Het besturingssysteem en de gegevensschijven worden niet getroffen.</span><span class="sxs-lookup"><span data-stu-id="7b667-122">The OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b667-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b667-123">Next steps</span></span>
<span data-ttu-id="7b667-124">Voor extra schaalbaarheid, meerdere exemplaren van de VM uitvoeren en uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="7b667-124">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="7b667-125">Zie voor meer informatie [automatisch schalen van Linux-machines in een virtuele-Machineschaalset][scale-set].</span><span class="sxs-lookup"><span data-stu-id="7b667-125">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
