---
title: PowerShell-voorbeeldscript - aaaAzure maken van een netwerk voor toepassingen met meerdere lagen | Microsoft Docs
description: 'Azure PowerShell-script voorbeeld: een virtueel netwerk voor toepassingen met meerdere lagen maken.'
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
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="9ac58-103">Een netwerk voor toepassingen met meerdere lagen maken</span><span class="sxs-lookup"><span data-stu-id="9ac58-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="9ac58-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="9ac58-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="9ac58-105">Verkeer toohello front-end-subnet is beperkt tooHTTP en SSH, tijdens het verkeer toohello back-end-subnet is beperkt tooMySQL, poort 3306.</span><span class="sxs-lookup"><span data-stu-id="9ac58-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="9ac58-106">Na het Hallo-script wordt uitgevoerd hebt u twee virtuele machines, één in elk subnet dat u kunt webserver en MySQL-software te implementeren.</span><span class="sxs-lookup"><span data-stu-id="9ac58-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="9ac58-107">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac58-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9ac58-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9ac58-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9ac58-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="9ac58-109">Clean up deployment</span></span> 

<span data-ttu-id="9ac58-110">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ac58-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9ac58-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9ac58-111">Script explanation</span></span>

<span data-ttu-id="9ac58-112">Dit script maakt gebruik van Hallo opdrachten toocreate na een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="9ac58-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="9ac58-113">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="9ac58-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="9ac58-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9ac58-114">Command</span></span> | <span data-ttu-id="9ac58-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9ac58-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9ac58-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9ac58-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9ac58-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9ac58-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9ac58-118">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9ac58-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9ac58-119">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="9ac58-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="9ac58-120">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9ac58-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9ac58-121">Maakt een back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="9ac58-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="9ac58-122">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="9ac58-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9ac58-123">Maakt een openbare IP-adres tooaccess-Hallo VM van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="9ac58-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="9ac58-124">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="9ac58-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9ac58-125">Virtuele netwerkinterfaces maakt en koppelt deze toohello van het virtuele netwerk front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="9ac58-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="9ac58-126">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="9ac58-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="9ac58-127">Netwerkbeveiligingsgroepen (NSG) die gekoppeld toohello front-end en back-end subnetten zijn maakt.</span><span class="sxs-lookup"><span data-stu-id="9ac58-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="9ac58-128">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9ac58-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="9ac58-129">NSG-regels toestaan of blokkeren van bepaalde poorten toospecific subnetten maakt.</span><span class="sxs-lookup"><span data-stu-id="9ac58-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="9ac58-130">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9ac58-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9ac58-131">Virtuele machines maakt en koppelt een NIC tooeach VM.</span><span class="sxs-lookup"><span data-stu-id="9ac58-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="9ac58-132">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toouse en beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="9ac58-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="9ac58-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9ac58-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9ac58-134">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="9ac58-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9ac58-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ac58-135">Next steps</span></span>

<span data-ttu-id="9ac58-136">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9ac58-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="9ac58-137">Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in Hallo [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9ac58-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
