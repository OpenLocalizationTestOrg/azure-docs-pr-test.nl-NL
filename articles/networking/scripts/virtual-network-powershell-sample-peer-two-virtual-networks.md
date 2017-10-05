---
title: Azure PowerShell-Script voorbeeld - Peer twee virtuele netwerken | Microsoft Docs
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
ms.openlocfilehash: 51c0b98727e148671cfd7ab2b31ffd1c705d8a4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="5f029-103">Peer twee virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="5f029-103">Peer two virtual networks</span></span>

<span data-ttu-id="5f029-104">Dit script wordt gemaakt en twee virtuele netwerken in de dezelfde regio trhough het Azure-netwerk met elkaar verbindt.</span><span class="sxs-lookup"><span data-stu-id="5f029-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="5f029-105">Nadat het script is uitgevoerd, maakt u een peering tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="5f029-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="5f029-106">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="5f029-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5f029-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="5f029-107">Sample script</span></span>

<span data-ttu-id="5f029-108">[!code-azurepowershell[belangrijkste](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "twee netwerken op hetzelfde niveau")]</span><span class="sxs-lookup"><span data-stu-id="5f029-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5f029-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="5f029-109">Clean up deployment</span></span> 

<span data-ttu-id="5f029-110">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5f029-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5f029-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="5f029-111">Script explanation</span></span>

<span data-ttu-id="5f029-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="5f029-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="5f029-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="5f029-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5f029-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="5f029-114">Command</span></span> | <span data-ttu-id="5f029-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5f029-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5f029-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f029-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5f029-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5f029-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="5f029-118">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5f029-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="5f029-119">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="5f029-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="5f029-120">Voeg AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="5f029-120">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="5f029-121">Maakt een peering tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="5f029-121">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="5f029-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f029-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5f029-123">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="5f029-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5f029-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f029-124">Next steps</span></span>

<span data-ttu-id="5f029-125">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f029-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="5f029-126">Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in de [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f029-126">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>