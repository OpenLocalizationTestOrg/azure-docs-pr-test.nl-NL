---
title: aaaAzure PowerShell-voorbeeldscript - een virtuele machine maken vanuit een momentopname | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een virtuele machine maken vanuit een momentopname'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="ad5cb-103">Een virtuele machine maken vanuit een momentopname met PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad5cb-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="ad5cb-104">Dit script maakt een virtuele machine van een momentopname van een besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ad5cb-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="ad5cb-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ad5cb-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="ad5cb-106">Clean up deployment</span></span> 

<span data-ttu-id="ad5cb-107">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ad5cb-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="ad5cb-108">Script explanation</span></span>

<span data-ttu-id="ad5cb-109">Dit script maakt gebruik van Hallo opdrachten tooget momentopname eigenschappen, een beheerde schijf maken vanuit een momentopname en maak een VM te volgen.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="ad5cb-110">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ad5cb-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="ad5cb-111">Command</span></span> | <span data-ttu-id="ad5cb-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="ad5cb-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ad5cb-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="ad5cb-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="ad5cb-114">Hiermee haalt u een momentopname met de naam van de momentopname.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="ad5cb-115">Nieuwe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="ad5cb-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="ad5cb-116">De configuratie van een schijf maakt.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-116">Creates a disk configuration.</span></span> <span data-ttu-id="ad5cb-117">Deze configuratie wordt gebruikt met Hallo-proces voor het maken van schijf.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="ad5cb-118">Nieuwe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="ad5cb-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="ad5cb-119">Hiermee maakt u een beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="ad5cb-120">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ad5cb-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="ad5cb-121">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-121">Creates a VM configuration.</span></span> <span data-ttu-id="ad5cb-122">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ad5cb-123">Hallo-configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ad5cb-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="ad5cb-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="ad5cb-125">Hallo-beheerde schijven als OS schijf toohello virtuele machine gekoppeld</span><span class="sxs-lookup"><span data-stu-id="ad5cb-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="ad5cb-126">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ad5cb-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ad5cb-127">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ad5cb-128">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ad5cb-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ad5cb-129">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="ad5cb-130">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ad5cb-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ad5cb-131">Hiermee maakt u een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="ad5cb-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ad5cb-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ad5cb-133">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="ad5cb-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad5cb-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad5cb-134">Next steps</span></span>

<span data-ttu-id="ad5cb-135">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ad5cb-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ad5cb-136">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad5cb-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
