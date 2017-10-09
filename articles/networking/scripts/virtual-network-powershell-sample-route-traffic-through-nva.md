---
title: aaaAzure PowerShell-voorbeeldscript - routeverkeer via een virtueel netwerkapparaat | Microsoft Docs
description: 'Azure PowerShell - voorbeeldscript: de Route-verkeer via een firewall netwerk virtueel apparaat.'
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="6ebc2-103">-Routeverkeer via een virtueel netwerkapparaat</span><span class="sxs-lookup"><span data-stu-id="6ebc2-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="6ebc2-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="6ebc2-105">Een virtuele machine wordt gemaakt met ingeschakelde tooroute verkeer tussen de twee subnetten Hallo doorsturen via IP.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="6ebc2-106">U kunt na het uitvoeren van script Hallo netwerksoftware, zoals een firewalltoepassing toohello VM implementeren.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="6ebc2-107">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6ebc2-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="6ebc2-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6ebc2-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="6ebc2-109">Clean up deployment</span></span> 

<span data-ttu-id="6ebc2-110">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="6ebc2-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="6ebc2-111">Script explanation</span></span>

<span data-ttu-id="6ebc2-112">Dit script maakt gebruik van Hallo opdrachten toocreate na een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="6ebc2-113">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="6ebc2-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="6ebc2-114">Command</span></span> | <span data-ttu-id="6ebc2-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6ebc2-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6ebc2-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6ebc2-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="6ebc2-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6ebc2-118">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="6ebc2-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="6ebc2-119">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="6ebc2-120">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="6ebc2-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="6ebc2-121">Maakt back-end en DMZ subnetten.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="6ebc2-122">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="6ebc2-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="6ebc2-123">Maakt een openbare IP-adres tooaccess-Hallo VM van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="6ebc2-124">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="6ebc2-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="6ebc2-125">Maakt een virtuele netwerkinterface en doorsturen via IP inschakelen voor deze.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="6ebc2-126">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="6ebc2-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="6ebc2-127">Maakt een netwerkbeveiligingsgroep (NSG).</span><span class="sxs-lookup"><span data-stu-id="6ebc2-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="6ebc2-128">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="6ebc2-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="6ebc2-129">NSG-regels waarmee HTTP en HTTPS-poorten inkomend toohello VM maakt.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="6ebc2-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="6ebc2-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="6ebc2-131">Gekoppeld Hallo nsg's en route toosubnets tabellen.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="6ebc2-132">Nieuwe AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="6ebc2-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="6ebc2-133">Een routetabel voor alle routes maken.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="6ebc2-134">Nieuwe AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="6ebc2-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="6ebc2-135">Routes maakt tooroute verkeer tussen subnetten en Hallo Internet via VM Hallo.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="6ebc2-136">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="6ebc2-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="6ebc2-137">Een virtuele machine maakt en koppelt Hallo NIC tooit.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="6ebc2-138">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toouse en beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="6ebc2-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6ebc2-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="6ebc2-140">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="6ebc2-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ebc2-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6ebc2-141">Next steps</span></span>

<span data-ttu-id="6ebc2-142">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6ebc2-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="6ebc2-143">Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in Hallo [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6ebc2-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
