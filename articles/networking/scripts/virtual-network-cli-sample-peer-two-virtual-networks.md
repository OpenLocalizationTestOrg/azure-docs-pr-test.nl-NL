---
title: aaaAzure voorbeeldscript CLI - Peer twee virtuele netwerken | Microsoft Docs
description: Azure CLI-voorbeeldscript - Peer twee virtuele netwerken
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="03808-103">Peer twee virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="03808-103">Peer two virtual networks</span></span>

<span data-ttu-id="03808-104">Dit script wordt gemaakt en verbinding maakt twee virtuele netwerken in Hallo dezelfde regio trhough hello Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="03808-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="03808-105">Na het uitvoeren van script hello, maakt u een peering tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="03808-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="03808-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="03808-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="03808-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="03808-107">Clean up deployment</span></span> 

<span data-ttu-id="03808-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="03808-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="03808-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="03808-109">Script explanation</span></span>

<span data-ttu-id="03808-110">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="03808-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="03808-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="03808-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="03808-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="03808-112">Command</span></span> | <span data-ttu-id="03808-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="03808-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="03808-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="03808-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="03808-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="03808-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="03808-116">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="03808-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="03808-117">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="03808-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="03808-118">AZ network vnet-peering maken</span><span class="sxs-lookup"><span data-stu-id="03808-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="03808-119">Maakt een peering tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="03808-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="03808-120">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="03808-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="03808-121">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="03808-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="03808-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="03808-122">Next steps</span></span>

<span data-ttu-id="03808-123">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="03808-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="03808-124">Aanvullende netwerken CLI scriptvoorbeelden kunnen u vinden in Hallo [overzicht van Azure-netwerken documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="03808-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
