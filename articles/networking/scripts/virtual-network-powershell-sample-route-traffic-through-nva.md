---
title: Azure PowerShell-voorbeeldscript - routeverkeer via een virtueel netwerkapparaat | Microsoft Docs
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
ms.openlocfilehash: 883d28dac72a66c2186d222f72b04d68e532cead
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="2d5c3-103">-Routeverkeer via een virtueel netwerkapparaat</span><span class="sxs-lookup"><span data-stu-id="2d5c3-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="2d5c3-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="2d5c3-105">Een virtuele machine wordt gemaakt met doorsturen via IP is ingeschakeld voor het routeren van netwerkverkeer tussen de twee subnetten.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="2d5c3-106">U kunt na het uitvoeren van het script netwerksoftware, zoals een firewalltoepassing naar de virtuele machine implementeren.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="2d5c3-107">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2d5c3-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="2d5c3-108">Sample script</span></span>


<span data-ttu-id="2d5c3-109">[!code-powershell[belangrijkste](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "verkeer routeren via een virtueel netwerkapparaat")]</span><span class="sxs-lookup"><span data-stu-id="2d5c3-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2d5c3-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="2d5c3-110">Clean up deployment</span></span> 

<span data-ttu-id="2d5c3-111">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="2d5c3-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="2d5c3-112">Script explanation</span></span>

<span data-ttu-id="2d5c3-113">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="2d5c3-114">Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="2d5c3-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="2d5c3-115">Command</span></span> | <span data-ttu-id="2d5c3-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2d5c3-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2d5c3-117">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d5c3-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="2d5c3-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2d5c3-119">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="2d5c3-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="2d5c3-120">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="2d5c3-121">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="2d5c3-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="2d5c3-122">Maakt back-end en DMZ subnetten.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-122">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="2d5c3-123">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="2d5c3-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="2d5c3-124">Hiermee maakt u een openbaar IP-adres voor toegang tot de virtuele machine via het Internet.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="2d5c3-125">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="2d5c3-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="2d5c3-126">Maakt een virtuele netwerkinterface en doorsturen via IP inschakelen voor deze.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-126">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="2d5c3-127">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="2d5c3-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="2d5c3-128">Maakt een netwerkbeveiligingsgroep (NSG).</span><span class="sxs-lookup"><span data-stu-id="2d5c3-128">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="2d5c3-129">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="2d5c3-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="2d5c3-130">NSG-regels waarmee HTTP en HTTPS-poorten inkomend naar de virtuele machine maakt.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-130">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="2d5c3-131">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="2d5c3-131">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="2d5c3-132">Koppelt de nsg's en routetabellen aan subnetten.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-132">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="2d5c3-133">Nieuwe AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="2d5c3-133">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="2d5c3-134">Een routetabel voor alle routes maken.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-134">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="2d5c3-135">Nieuwe AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="2d5c3-135">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="2d5c3-136">Routes naar verkeer leiden tussen subnetten en het Internet via de virtuele machine maakt.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-136">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="2d5c3-137">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="2d5c3-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="2d5c3-138">Hiermee maakt u een virtuele machine en de NIC koppelt aan het.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-138">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="2d5c3-139">Deze opdracht geeft ook aan de installatiekopie van de virtuele machine te gebruiken en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-139">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="2d5c3-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d5c3-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="2d5c3-141">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="2d5c3-141">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2d5c3-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d5c3-142">Next steps</span></span>

<span data-ttu-id="2d5c3-143">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2d5c3-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="2d5c3-144">Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in de [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2d5c3-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>