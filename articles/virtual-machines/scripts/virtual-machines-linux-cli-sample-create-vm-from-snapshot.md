---
title: aaaAzure voorbeeldscript CLI - een virtuele machine maken vanuit een momentopname | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een virtuele machine maken vanuit een momentopname'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="4c4f8-103">Een virtuele machine maken vanuit een momentopname met CLI</span><span class="sxs-lookup"><span data-stu-id="4c4f8-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="4c4f8-104">Dit script maakt een virtuele machine van een momentopname van een besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="4c4f8-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4c4f8-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4c4f8-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4c4f8-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="4c4f8-106">Clean up deployment</span></span> 

<span data-ttu-id="4c4f8-107">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4c4f8-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4c4f8-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4c4f8-108">Script explanation</span></span>

<span data-ttu-id="4c4f8-109">Dit script gebruikt Hallo opdrachten toocreate een beheerde schijf virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="4c4f8-109">This script uses hello following commands toocreate a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="4c4f8-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="4c4f8-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4c4f8-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4c4f8-111">Command</span></span> | <span data-ttu-id="4c4f8-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4c4f8-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4c4f8-113">AZ momentopname weergeven</span><span class="sxs-lookup"><span data-stu-id="4c4f8-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="4c4f8-114">Opgehaald momentopname met behulp van de naam van de momentopname en de naam van resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="4c4f8-114">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="4c4f8-115">Id-eigenschap van Hallo geretourneerde object is gebruikte toocreate een beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="4c4f8-115">Id property of hello returned object is used toocreate a managed disk.</span></span>  |
| [<span data-ttu-id="4c4f8-116">AZ schijf maken</span><span class="sxs-lookup"><span data-stu-id="4c4f8-116">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="4c4f8-117">Beheerde schijven vanuit een momentopname maakt met behulp van een momentopname van Id, de schijfnaam van de, opslagtype en grootte</span><span class="sxs-lookup"><span data-stu-id="4c4f8-117">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="4c4f8-118">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="4c4f8-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="4c4f8-119">Hiermee maakt u een VM die gebruikmaakt van een beheerde besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="4c4f8-119">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4c4f8-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4c4f8-120">Next steps</span></span>

<span data-ttu-id="4c4f8-121">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4c4f8-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4c4f8-122">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4c4f8-122">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
