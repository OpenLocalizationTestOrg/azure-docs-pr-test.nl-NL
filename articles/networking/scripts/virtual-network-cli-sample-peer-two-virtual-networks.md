---
title: Azure CLI-voorbeeldscript - Peer twee virtuele netwerken | Microsoft Docs
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
ms.openlocfilehash: a2b8fda288072e2fb0087988bbd68d3e4d9031d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="227a3-103">Peer twee virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="227a3-103">Peer two virtual networks</span></span>

<span data-ttu-id="227a3-104">Dit script wordt gemaakt en twee virtuele netwerken in de dezelfde regio trhough het Azure-netwerk met elkaar verbindt.</span><span class="sxs-lookup"><span data-stu-id="227a3-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="227a3-105">Nadat het script is uitgevoerd, maakt u een peering tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="227a3-105">After running the script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="227a3-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="227a3-106">Sample script</span></span>

<span data-ttu-id="227a3-107">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "twee netwerken op hetzelfde niveau")]</span><span class="sxs-lookup"><span data-stu-id="227a3-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="227a3-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="227a3-108">Clean up deployment</span></span> 

<span data-ttu-id="227a3-109">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="227a3-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="227a3-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="227a3-110">Script explanation</span></span>

<span data-ttu-id="227a3-111">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="227a3-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="227a3-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="227a3-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="227a3-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="227a3-113">Command</span></span> | <span data-ttu-id="227a3-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="227a3-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="227a3-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="227a3-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="227a3-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="227a3-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="227a3-117">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="227a3-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="227a3-118">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="227a3-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="227a3-119">AZ network vnet-peering maken</span><span class="sxs-lookup"><span data-stu-id="227a3-119">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="227a3-120">Maakt een peering tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="227a3-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="227a3-121">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="227a3-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="227a3-122">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="227a3-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="227a3-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="227a3-123">Next steps</span></span>

<span data-ttu-id="227a3-124">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="227a3-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="227a3-125">Aanvullende netwerken CLI scriptvoorbeelden vindt u in de [overzicht van Azure-netwerken documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="227a3-125">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).</span></span>
