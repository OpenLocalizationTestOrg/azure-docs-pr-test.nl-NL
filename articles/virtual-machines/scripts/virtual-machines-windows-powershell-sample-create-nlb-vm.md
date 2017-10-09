---
title: aaaAzure PowerShell-voorbeeldscript - Maak een VM van Windows NLB | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: Maak een VM van Windows NLB'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="359eb-103">Load balance verkeer tussen de maximaal beschikbare virtuele machines</span><span class="sxs-lookup"><span data-stu-id="359eb-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="359eb-104">Dit voorbeeldscript wordt gemaakt van alles wat u nodig toorun verschillende virtuele machines van Windows Server 2016 geconfigureerd in een maximaal beschikbare en load balanced configuratie.</span><span class="sxs-lookup"><span data-stu-id="359eb-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="359eb-105">Nadat het Hallo-script wordt uitgevoerd, hebt u drie virtuele machines, gekoppelde tooan Beschikbaarheidsset Azure en zijn toegankelijk via een Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="359eb-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="359eb-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="359eb-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="359eb-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="359eb-107">Clean up deployment</span></span> 

<span data-ttu-id="359eb-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="359eb-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="359eb-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="359eb-109">Script explanation</span></span>

<span data-ttu-id="359eb-110">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="359eb-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="359eb-111">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="359eb-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="359eb-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="359eb-112">Command</span></span> | <span data-ttu-id="359eb-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="359eb-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="359eb-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="359eb-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="359eb-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="359eb-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="359eb-116">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="359eb-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="359eb-117">Hiermee maakt u de subnetconfiguratie van een.</span><span class="sxs-lookup"><span data-stu-id="359eb-117">Creates a subnet configuration.</span></span> <span data-ttu-id="359eb-118">Deze configuratie wordt gebruikt met Hallo-proces voor het maken van virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="359eb-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="359eb-119">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="359eb-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="359eb-120">Hiermee maakt u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="359eb-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="359eb-121">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="359eb-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="359eb-122">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="359eb-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="359eb-123">Nieuwe AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="359eb-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="359eb-124">Maakt een front-end-IP-configuratie voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="359eb-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="359eb-125">Nieuwe AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="359eb-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="359eb-126">Maakt een back-end-pool-adresconfiguratie voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="359eb-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="359eb-127">Nieuwe AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="359eb-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="359eb-128">Maakt een test-configuratie voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="359eb-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="359eb-129">Nieuwe AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="359eb-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="359eb-130">Maakt de regelconfiguratie van een voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="359eb-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="359eb-131">Nieuwe AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="359eb-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="359eb-132">Maakt een binnenkomende NAT-regelconfiguratie voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="359eb-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="359eb-133">Nieuwe AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="359eb-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="359eb-134">Hiermee maakt u een load balancer.</span><span class="sxs-lookup"><span data-stu-id="359eb-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="359eb-135">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="359eb-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="359eb-136">Maakt een groep regel de netwerkbeveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="359eb-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="359eb-137">Deze configuratie is gebruikte toocreate een regel voor het NSG wanneer Hallo NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="359eb-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="359eb-138">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="359eb-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="359eb-139">Een netwerkbeveiligingsgroep maakt.</span><span class="sxs-lookup"><span data-stu-id="359eb-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="359eb-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="359eb-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="359eb-141">Hiermee haalt u informatie over het subnet.</span><span class="sxs-lookup"><span data-stu-id="359eb-141">Gets subnet information.</span></span> <span data-ttu-id="359eb-142">Deze informatie wordt gebruikt bij het maken van een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="359eb-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="359eb-143">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="359eb-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="359eb-144">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="359eb-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="359eb-145">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="359eb-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="359eb-146">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="359eb-146">Creates a VM configuration.</span></span> <span data-ttu-id="359eb-147">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="359eb-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="359eb-148">Hallo-configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="359eb-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="359eb-149">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="359eb-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="359eb-150">Maak een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="359eb-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="359eb-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="359eb-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="359eb-152">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="359eb-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="359eb-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="359eb-153">Next steps</span></span>

<span data-ttu-id="359eb-154">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="359eb-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="359eb-155">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="359eb-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
