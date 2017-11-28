---
title: aaaAzure PowerShell-voorbeeldscript - Maak een Linux-VM | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een virtuele Linux-machine maken'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8ee2ee42aa68ee135a859b7eaead25811cf54095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="42fc2-103">Een volledig geconfigureerde virtuele machine maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="42fc2-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="42fc2-104">Dit script maakt een virtuele Machine van Azure met een virtuele Ubuntu-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="42fc2-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="42fc2-105">Na het uitvoeren van script hello, kunt u toegang tot de Hallo virtuele machine via SSH.</span><span class="sxs-lookup"><span data-stu-id="42fc2-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="42fc2-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="42fc2-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.ps1 "Create VM detailed")]

## <a name="clean-up-deployment"></a><span data-ttu-id="42fc2-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="42fc2-107">Clean up deployment</span></span> 

<span data-ttu-id="42fc2-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="42fc2-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="42fc2-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="42fc2-109">Script explanation</span></span>

<span data-ttu-id="42fc2-110">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="42fc2-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="42fc2-111">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="42fc2-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="42fc2-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="42fc2-112">Command</span></span> | <span data-ttu-id="42fc2-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="42fc2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="42fc2-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="42fc2-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="42fc2-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="42fc2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="42fc2-116">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="42fc2-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="42fc2-117">Hiermee maakt u de subnetconfiguratie van een.</span><span class="sxs-lookup"><span data-stu-id="42fc2-117">Creates a subnet configuration.</span></span> <span data-ttu-id="42fc2-118">Deze configuratie wordt gebruikt met Hallo-proces voor het maken van virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="42fc2-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="42fc2-119">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="42fc2-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="42fc2-120">Hiermee maakt u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="42fc2-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="42fc2-121">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="42fc2-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="42fc2-122">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="42fc2-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="42fc2-123">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="42fc2-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="42fc2-124">Maakt een groep regel de netwerkbeveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="42fc2-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="42fc2-125">Deze configuratie is gebruikte toocreate een regel voor het NSG wanneer Hallo NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="42fc2-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="42fc2-126">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="42fc2-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="42fc2-127">Een netwerkbeveiligingsgroep maakt.</span><span class="sxs-lookup"><span data-stu-id="42fc2-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="42fc2-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="42fc2-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="42fc2-129">Hiermee haalt u informatie over het subnet.</span><span class="sxs-lookup"><span data-stu-id="42fc2-129">Gets subnet information.</span></span> <span data-ttu-id="42fc2-130">Deze informatie wordt gebruikt bij het maken van een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="42fc2-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="42fc2-131">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="42fc2-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="42fc2-132">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="42fc2-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="42fc2-133">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="42fc2-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="42fc2-134">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="42fc2-134">Creates a VM configuration.</span></span> <span data-ttu-id="42fc2-135">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="42fc2-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="42fc2-136">Hallo-configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="42fc2-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="42fc2-137">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="42fc2-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="42fc2-138">Maak een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="42fc2-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="42fc2-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="42fc2-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="42fc2-140">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="42fc2-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="42fc2-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="42fc2-141">Next steps</span></span>

<span data-ttu-id="42fc2-142">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="42fc2-142">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="42fc2-143">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42fc2-143">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
