---
title: PowerShell-voorbeeldscript - aaaAzure Peer twee virtuele netwerken | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Peer twee virtuele netwerken
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="1f4d8-103">Peer twee virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="1f4d8-103">Peer two virtual networks</span></span>

<span data-ttu-id="1f4d8-104">Dit script wordt gemaakt en verbinding maakt twee virtuele netwerken in Hallo dezelfde regio trhough hello Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="1f4d8-105">Na het uitvoeren van script hello, maakt u een peering tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="1f4d8-106">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1f4d8-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="1f4d8-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1f4d8-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="1f4d8-108">Clean up deployment</span></span> 

<span data-ttu-id="1f4d8-109">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1f4d8-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="1f4d8-110">Script explanation</span></span>

<span data-ttu-id="1f4d8-111">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1f4d8-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1f4d8-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="1f4d8-113">Command</span></span> | <span data-ttu-id="1f4d8-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1f4d8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1f4d8-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1f4d8-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1f4d8-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="1f4d8-117">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1f4d8-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="1f4d8-118">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="1f4d8-119">Voeg AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="1f4d8-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="1f4d8-120">Maakt een peering tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="1f4d8-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1f4d8-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1f4d8-122">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="1f4d8-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1f4d8-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f4d8-123">Next steps</span></span>

<span data-ttu-id="1f4d8-124">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1f4d8-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="1f4d8-125">Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in Hallo [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f4d8-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
