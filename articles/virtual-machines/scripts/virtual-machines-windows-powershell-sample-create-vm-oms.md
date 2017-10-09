---
title: aaaAzure PowerShell-voorbeeldscript - OMS | Microsoft Docs
description: Voorbeeld van Azure PowerShell-Script - OMS
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
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eeafbe743013e97bf3fcefb5ce87f72cb503a4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="a6b99-103">Maak een Operations Management Suite bewaakt VM met PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6b99-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="a6b99-104">Dit script maakt een virtuele Machine van Azure, Hallo Operations Management Suite (OMS)-agent geïnstalleerd en schrijft Hallo-systeem met een OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="a6b99-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="a6b99-105">Zodra het Hallo-script is uitgevoerd, is de optie Hallo virtuele machine zijn zichtbaar in Hallo OMS-console.</span><span class="sxs-lookup"><span data-stu-id="a6b99-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span> <span data-ttu-id="a6b99-106">U moet ook tooupdate Hallo OMS-ID en werkruimte werkruimtesleutel.</span><span class="sxs-lookup"><span data-stu-id="a6b99-106">Also, you need tooupdate hello OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a6b99-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a6b99-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a6b99-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="a6b99-108">Clean up deployment</span></span> 

<span data-ttu-id="a6b99-109">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a6b99-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a6b99-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a6b99-110">Script explanation</span></span>

<span data-ttu-id="a6b99-111">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="a6b99-111">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="a6b99-112">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="a6b99-112">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a6b99-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a6b99-113">Command</span></span> | <span data-ttu-id="a6b99-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a6b99-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a6b99-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a6b99-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a6b99-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a6b99-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a6b99-117">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="a6b99-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="a6b99-118">Hiermee maakt u de subnetconfiguratie van een.</span><span class="sxs-lookup"><span data-stu-id="a6b99-118">Creates a subnet configuration.</span></span> <span data-ttu-id="a6b99-119">Deze configuratie wordt gebruikt met Hallo-proces voor het maken van virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="a6b99-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="a6b99-120">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a6b99-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="a6b99-121">Hiermee maakt u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="a6b99-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="a6b99-122">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="a6b99-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="a6b99-123">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a6b99-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="a6b99-124">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="a6b99-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="a6b99-125">Maakt een groep regel de netwerkbeveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="a6b99-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="a6b99-126">Deze configuratie is gebruikte toocreate een regel voor het NSG wanneer Hallo NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a6b99-126">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="a6b99-127">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="a6b99-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="a6b99-128">Een netwerkbeveiligingsgroep maakt.</span><span class="sxs-lookup"><span data-stu-id="a6b99-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="a6b99-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="a6b99-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="a6b99-130">Hiermee haalt u informatie over het subnet.</span><span class="sxs-lookup"><span data-stu-id="a6b99-130">Gets subnet information.</span></span> <span data-ttu-id="a6b99-131">Deze informatie wordt gebruikt bij het maken van een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="a6b99-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="a6b99-132">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="a6b99-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="a6b99-133">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="a6b99-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="a6b99-134">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="a6b99-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="a6b99-135">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="a6b99-135">Creates a VM configuration.</span></span> <span data-ttu-id="a6b99-136">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="a6b99-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="a6b99-137">Hallo-configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="a6b99-137">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="a6b99-138">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="a6b99-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="a6b99-139">Maak een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a6b99-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="a6b99-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="a6b99-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="a6b99-141">Een VM-extensie toohello virtuele machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a6b99-141">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="a6b99-142">In dit geval Hallo Operations Management Suite-agentextensie gebruikte tooinstall Hallo OMS-agent is en inschrijven Hallo VM in een OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="a6b99-142">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="a6b99-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a6b99-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a6b99-144">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="a6b99-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a6b99-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6b99-145">Next steps</span></span>

<span data-ttu-id="a6b99-146">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6b99-146">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a6b99-147">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6b99-147">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
