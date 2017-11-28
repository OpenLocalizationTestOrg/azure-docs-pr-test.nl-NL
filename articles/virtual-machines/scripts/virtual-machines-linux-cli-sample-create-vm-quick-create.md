---
title: aaaAzure voorbeeldscript CLI - snel maken een Linux-VM | Microsoft Docs
description: Azure CLI-voorbeeldscript - snel een virtuele Linux-machine maken
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: edecf274f4e401af3603e5be37a989e2e0eb22c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="26581-103">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="26581-103">Create a virtual machine</span></span>

<span data-ttu-id="26581-104">Dit script maakt een virtuele Machine van Azure met een besturingssysteem Ubuntu en verwante netwerkresources.</span><span class="sxs-lookup"><span data-stu-id="26581-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="26581-105">Na het uitvoeren van script hello, kunt u toegang tot de Hallo virtuele machine via SSH.</span><span class="sxs-lookup"><span data-stu-id="26581-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="26581-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="26581-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="26581-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="26581-107">Clean up deployment</span></span> 

<span data-ttu-id="26581-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="26581-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="26581-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="26581-109">Script explanation</span></span>

<span data-ttu-id="26581-110">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="26581-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="26581-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="26581-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="26581-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="26581-112">Command</span></span> | <span data-ttu-id="26581-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="26581-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="26581-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="26581-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="26581-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="26581-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="26581-116">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="26581-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="26581-117">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en netwerkbeveiligingsgroep is verbonden.</span><span class="sxs-lookup"><span data-stu-id="26581-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="26581-118">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="26581-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="26581-119">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="26581-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="26581-120">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="26581-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="26581-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="26581-121">Next steps</span></span>

<span data-ttu-id="26581-122">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="26581-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="26581-123">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26581-123">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
