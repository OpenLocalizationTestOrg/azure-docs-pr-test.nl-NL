---
title: aaaAzure voorbeeldscript CLI - een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf'
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="9e039-103">Maak een virtuele machine met behulp van een bestaande beheerde OS-schijf met CLI</span><span class="sxs-lookup"><span data-stu-id="9e039-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="9e039-104">Dit script maakt een virtuele machine door het koppelen van een bestaande beheerde schijf als de besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="9e039-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="9e039-105">Gebruik dit script in de voorgaande scenario's:</span><span class="sxs-lookup"><span data-stu-id="9e039-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="9e039-106">Een virtuele machine maken van een bestaande beheerde OS schijf die is opgehaald uit een beheerde schijf in een ander abonnement</span><span class="sxs-lookup"><span data-stu-id="9e039-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="9e039-107">Een virtuele machine maken van een bestaande beheerde schijf dat is gemaakt vanaf een speciale VHD-bestand</span><span class="sxs-lookup"><span data-stu-id="9e039-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="9e039-108">Een virtuele machine maken van een bestaande beheerde OS schijf die is gemaakt vanuit een momentopname</span><span class="sxs-lookup"><span data-stu-id="9e039-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9e039-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9e039-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9e039-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="9e039-110">Clean up deployment</span></span> 

<span data-ttu-id="9e039-111">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9e039-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9e039-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9e039-112">Script explanation</span></span>

<span data-ttu-id="9e039-113">Dit script maakt gebruik van Hallo opdrachten tooget beheerd schijfeigenschappen te volgen, een tooa beheerde schijf koppelen nieuwe virtuele machine en een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="9e039-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="9e039-114">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="9e039-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9e039-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9e039-115">Command</span></span> | <span data-ttu-id="9e039-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9e039-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e039-117">AZ schijf weergeven</span><span class="sxs-lookup"><span data-stu-id="9e039-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="9e039-118">Haalt de eigenschappen van de schijf met de naam van schijf en de naam van resourcegroep beheerd.</span><span class="sxs-lookup"><span data-stu-id="9e039-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="9e039-119">Id-eigenschap is gebruikte tooattach een beheerde schijf tooa nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9e039-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="9e039-120">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="9e039-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9e039-121">Hiermee maakt u een VM die gebruikmaakt van een beheerde besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="9e039-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="9e039-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e039-122">Next steps</span></span>

<span data-ttu-id="9e039-123">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e039-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9e039-124">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e039-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
