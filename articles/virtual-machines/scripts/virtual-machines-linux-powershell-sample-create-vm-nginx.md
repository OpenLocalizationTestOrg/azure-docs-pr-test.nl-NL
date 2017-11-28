---
title: aaaAzure PowerShell-voorbeeldscript - NGINX | Microsoft Docs
description: Azure PowerShell-Script - NGINX-voorbeeld
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
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 017a4853e400f8f544a3f92771adaf468b5dee76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-nginx-vm-with-powershell"></a><span data-ttu-id="36215-103">Een NGINX-virtuele machine maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="36215-103">Create an NGINX VM with PowerShell</span></span>

<span data-ttu-id="36215-104">Dit script wordt een Azure virtuele Machine gemaakt en gebruikt vervolgens hello Azure virtuele Machine aangepaste Scriptextensie tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="36215-104">This script creates an Azure Virtual Machine and then uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="36215-105">Na het uitvoeren van script hello, kunt u toegang tot een demo-website op Hallo openbare IP-adres van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="36215-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="36215-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="36215-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.ps1 "Create VM NGINX")]

## <a name="clean-up-deployment"></a><span data-ttu-id="36215-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="36215-107">Clean up deployment</span></span> 

<span data-ttu-id="36215-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="36215-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="36215-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="36215-109">Script explanation</span></span>

<span data-ttu-id="36215-110">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="36215-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="36215-111">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="36215-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="36215-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="36215-112">Command</span></span> | <span data-ttu-id="36215-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="36215-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="36215-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="36215-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="36215-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="36215-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="36215-116">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="36215-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="36215-117">Hiermee maakt u de subnetconfiguratie van een.</span><span class="sxs-lookup"><span data-stu-id="36215-117">Creates a subnet configuration.</span></span> <span data-ttu-id="36215-118">Deze configuratie wordt gebruikt met Hallo-proces voor het maken van virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="36215-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="36215-119">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="36215-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="36215-120">Hiermee maakt u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="36215-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="36215-121">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="36215-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="36215-122">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="36215-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="36215-123">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="36215-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="36215-124">Maakt een groep regel de netwerkbeveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="36215-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="36215-125">Deze configuratie is gebruikte toocreate een regel voor het NSG wanneer Hallo NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="36215-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="36215-126">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="36215-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="36215-127">Een netwerkbeveiligingsgroep maakt.</span><span class="sxs-lookup"><span data-stu-id="36215-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="36215-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="36215-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="36215-129">Hiermee haalt u informatie over het subnet.</span><span class="sxs-lookup"><span data-stu-id="36215-129">Gets subnet information.</span></span> <span data-ttu-id="36215-130">Deze informatie wordt gebruikt bij het maken van een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="36215-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="36215-131">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="36215-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="36215-132">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="36215-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="36215-133">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="36215-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="36215-134">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="36215-134">Creates a VM configuration.</span></span> <span data-ttu-id="36215-135">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="36215-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="36215-136">Hallo-configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="36215-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="36215-137">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="36215-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="36215-138">Maak een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="36215-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="36215-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="36215-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="36215-140">Een VM-extensie toohello virtuele machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="36215-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="36215-141">In dit voorbeeld is de aangepaste scriptextensie Hallo gebruikte tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="36215-141">In this sample, hello custom script extension is used tooinstall NGINX.</span></span> |
|[<span data-ttu-id="36215-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="36215-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="36215-143">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="36215-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="36215-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36215-144">Next steps</span></span>

<span data-ttu-id="36215-145">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="36215-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="36215-146">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36215-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
