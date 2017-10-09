---
title: aaaAzure voorbeeldscript CLI - snel maken van een Windows Server 2016 VM | Microsoft Docs
description: Azure CLI-voorbeeldscript - snel maken van een virtuele machine van Windows Server 2016
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rickstercdn
ms.openlocfilehash: 4c736ce9e2ecc9ee75b34f903cad52c9c0ee0707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="77023-103">Snel een virtuele machine maken met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="77023-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="77023-104">Dit script maakt een Azure-virtuele Machine met Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="77023-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="77023-105">Na het uitvoeren van script hello, kunt u Hallo virtuele machine via Extern bureaublad-verbinding openen.</span><span class="sxs-lookup"><span data-stu-id="77023-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="77023-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="77023-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="77023-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="77023-107">Clean up deployment</span></span> 

<span data-ttu-id="77023-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="77023-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="77023-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="77023-109">Script explanation</span></span>

<span data-ttu-id="77023-110">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="77023-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="77023-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="77023-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="77023-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="77023-112">Command</span></span> | <span data-ttu-id="77023-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="77023-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="77023-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="77023-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="77023-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="77023-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="77023-116">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="77023-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="77023-117">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en netwerkbeveiligingsgroep is verbonden.</span><span class="sxs-lookup"><span data-stu-id="77023-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="77023-118">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="77023-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="77023-119">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="77023-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="77023-120">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="77023-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="77023-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="77023-121">Next steps</span></span>

<span data-ttu-id="77023-122">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77023-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="77023-123">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="77023-123">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
