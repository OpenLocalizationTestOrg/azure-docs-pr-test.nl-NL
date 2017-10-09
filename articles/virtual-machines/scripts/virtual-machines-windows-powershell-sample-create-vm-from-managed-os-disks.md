---
title: aaaAzure PowerShell-voorbeeldscript - een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf'
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
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="e351b-103">Maak een virtuele machine met behulp van een bestaande beheerde OS-schijf met PowerShell</span><span class="sxs-lookup"><span data-stu-id="e351b-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="e351b-104">Dit script maakt een virtuele machine door het koppelen van een bestaande beheerde schijf als de besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="e351b-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="e351b-105">Gebruik dit script in de voorgaande scenario's:</span><span class="sxs-lookup"><span data-stu-id="e351b-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="e351b-106">Een virtuele machine maken van een bestaande beheerde OS schijf die is opgehaald uit een beheerde schijf in een ander abonnement</span><span class="sxs-lookup"><span data-stu-id="e351b-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="e351b-107">Een virtuele machine maken van een bestaande beheerde schijf dat is gemaakt vanaf een speciale VHD-bestand</span><span class="sxs-lookup"><span data-stu-id="e351b-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="e351b-108">Een virtuele machine maken van een bestaande beheerde OS schijf die is gemaakt vanuit een momentopname</span><span class="sxs-lookup"><span data-stu-id="e351b-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e351b-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="e351b-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e351b-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="e351b-110">Clean up deployment</span></span> 

<span data-ttu-id="e351b-111">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e351b-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e351b-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="e351b-112">Script explanation</span></span>

<span data-ttu-id="e351b-113">Dit script maakt gebruik van Hallo opdrachten tooget beheerd schijfeigenschappen te volgen, een tooa beheerde schijf koppelen nieuwe virtuele machine en een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="e351b-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="e351b-114">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="e351b-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e351b-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="e351b-115">Command</span></span> | <span data-ttu-id="e351b-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e351b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e351b-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="e351b-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="e351b-118">Schijfobject op basis van Hallo naam en het Hallo-resourcegroep van een schijf opgehaald.</span><span class="sxs-lookup"><span data-stu-id="e351b-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="e351b-119">De eigenschap id van Hallo geretourneerd schijfobject is gebruikte tooattach Hallo schijf tooa nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e351b-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="e351b-120">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="e351b-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="e351b-121">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="e351b-121">Creates a VM configuration.</span></span> <span data-ttu-id="e351b-122">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="e351b-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e351b-123">Hallo-configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="e351b-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e351b-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="e351b-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="e351b-125">Een beheerde schijf met een Id-eigenschap Hallo van Hallo schijf als OS schijf tooa nieuwe virtuele machine gekoppeld</span><span class="sxs-lookup"><span data-stu-id="e351b-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="e351b-126">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e351b-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="e351b-127">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="e351b-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="e351b-128">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e351b-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="e351b-129">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="e351b-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="e351b-130">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e351b-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="e351b-131">Maak een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e351b-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="e351b-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e351b-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e351b-133">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="e351b-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e351b-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e351b-134">Next steps</span></span>

<span data-ttu-id="e351b-135">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e351b-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e351b-136">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e351b-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
