---
title: Voorbeeld van Azure PowerShell-Script - OMS | Microsoft Docs
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
ms.openlocfilehash: 9f876be46f5214b12d6a46e54509ba3541f819c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="dcfee-103">Maak een Operations Management Suite bewaakt VM met PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcfee-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="dcfee-104">Dit script maakt een virtuele Machine in Azure, installeert de agent Operations Management Suite (OMS) en registreert het systeem met een OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="dcfee-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="dcfee-105">Nadat het script is uitgevoerd, is de virtuele machine worden weergegeven in de OMS-console.</span><span class="sxs-lookup"><span data-stu-id="dcfee-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span> <span data-ttu-id="dcfee-106">U moet ook de OMS-werkruimte-ID en de werkruimte-sleutel bijwerken.</span><span class="sxs-lookup"><span data-stu-id="dcfee-106">Also, you need to update the OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dcfee-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="dcfee-107">Sample script</span></span>

<span data-ttu-id="dcfee-108">[!code-powershell[belangrijkste](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "VM OMS maken")]</span><span class="sxs-lookup"><span data-stu-id="dcfee-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="dcfee-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="dcfee-109">Clean up deployment</span></span> 

<span data-ttu-id="dcfee-110">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="dcfee-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dcfee-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="dcfee-111">Script explanation</span></span>

<span data-ttu-id="dcfee-112">Dit script maakt gebruik van de volgende opdrachten om de implementatie te maken.</span><span class="sxs-lookup"><span data-stu-id="dcfee-112">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="dcfee-113">Elk item in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="dcfee-113">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dcfee-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="dcfee-114">Command</span></span> | <span data-ttu-id="dcfee-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="dcfee-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dcfee-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dcfee-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="dcfee-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="dcfee-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dcfee-118">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="dcfee-118">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="dcfee-119">Hiermee maakt u de subnetconfiguratie van een.</span><span class="sxs-lookup"><span data-stu-id="dcfee-119">Creates a subnet configuration.</span></span> <span data-ttu-id="dcfee-120">Deze configuratie wordt gebruikt met het proces voor het virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="dcfee-120">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="dcfee-121">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="dcfee-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="dcfee-122">Hiermee maakt u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="dcfee-122">Creates a virtual network.</span></span> |
| [<span data-ttu-id="dcfee-123">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="dcfee-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="dcfee-124">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="dcfee-124">Creates a public IP address.</span></span> |
| [<span data-ttu-id="dcfee-125">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="dcfee-125">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="dcfee-126">Maakt een groep regel de netwerkbeveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="dcfee-126">Creates a network security group rule configuration.</span></span> <span data-ttu-id="dcfee-127">Deze configuratie wordt gebruikt voor het maken van een regel voor het NSG wanneer het NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dcfee-127">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="dcfee-128">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="dcfee-128">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="dcfee-129">Een netwerkbeveiligingsgroep maakt.</span><span class="sxs-lookup"><span data-stu-id="dcfee-129">Creates a network security group.</span></span> |
| [<span data-ttu-id="dcfee-130">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="dcfee-130">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="dcfee-131">Hiermee haalt u informatie over het subnet.</span><span class="sxs-lookup"><span data-stu-id="dcfee-131">Gets subnet information.</span></span> <span data-ttu-id="dcfee-132">Deze informatie wordt gebruikt bij het maken van een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="dcfee-132">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="dcfee-133">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="dcfee-133">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="dcfee-134">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="dcfee-134">Creates a network interface.</span></span> |
| [<span data-ttu-id="dcfee-135">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="dcfee-135">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="dcfee-136">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="dcfee-136">Creates a VM configuration.</span></span> <span data-ttu-id="dcfee-137">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="dcfee-137">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="dcfee-138">De configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="dcfee-138">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="dcfee-139">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="dcfee-139">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="dcfee-140">Maak een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="dcfee-140">Create a virtual machine.</span></span> |
| [<span data-ttu-id="dcfee-141">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="dcfee-141">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="dcfee-142">Een VM-extensie toevoegen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="dcfee-142">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="dcfee-143">In dit geval wordt de extensie van de agent Operations Management Suite gebruikt de OMS-agent installeren en het inschrijven van de virtuele machine in een OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="dcfee-143">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="dcfee-144">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dcfee-144">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="dcfee-145">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="dcfee-145">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dcfee-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dcfee-146">Next steps</span></span>

<span data-ttu-id="dcfee-147">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcfee-147">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dcfee-148">Voorbeelden van extra virtuele machine PowerShell-script kunnen worden gevonden in de [virtuele machine van Windows Azure-documentatie](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dcfee-148">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
