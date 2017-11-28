---
title: 'Azure PowerShell-Script voorbeeld: een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf | Microsoft Docs'
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
ms.openlocfilehash: ec532811e94647c8a04b9faf9474f6749969f83e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="36af2-103">Maak een virtuele machine met behulp van een bestaande beheerde OS-schijf met PowerShell</span><span class="sxs-lookup"><span data-stu-id="36af2-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="36af2-104">Dit script maakt een virtuele machine door het koppelen van een bestaande beheerde schijf als de besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="36af2-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="36af2-105">Gebruik dit script in de voorgaande scenario's:</span><span class="sxs-lookup"><span data-stu-id="36af2-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="36af2-106">Een virtuele machine maken van een bestaande beheerde OS schijf die is opgehaald uit een beheerde schijf in een ander abonnement</span><span class="sxs-lookup"><span data-stu-id="36af2-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="36af2-107">Een virtuele machine maken van een bestaande beheerde schijf dat is gemaakt vanaf een speciale VHD-bestand</span><span class="sxs-lookup"><span data-stu-id="36af2-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="36af2-108">Een virtuele machine maken van een bestaande beheerde OS schijf die is gemaakt vanuit een momentopname</span><span class="sxs-lookup"><span data-stu-id="36af2-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="36af2-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="36af2-109">Sample script</span></span>

<span data-ttu-id="36af2-110">[!code-powershell[belangrijkste](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "VM maken vanuit een momentopname.")]</span><span class="sxs-lookup"><span data-stu-id="36af2-110">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="36af2-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="36af2-111">Clean up deployment</span></span> 

<span data-ttu-id="36af2-112">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="36af2-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="36af2-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="36af2-113">Script explanation</span></span>

<span data-ttu-id="36af2-114">Dit script gebruikt de volgende opdrachten voor het ophalen van beheerde schijfeigenschappen, een beheerde schijf koppelen met een nieuwe virtuele machine en een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="36af2-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="36af2-115">Elk item in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="36af2-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="36af2-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="36af2-116">Command</span></span> | <span data-ttu-id="36af2-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="36af2-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="36af2-118">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="36af2-118">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="36af2-119">Schijfobject op basis van de naam en de resourcegroep van een schijf opgehaald.</span><span class="sxs-lookup"><span data-stu-id="36af2-119">Gets disk object based on the name and the resource group of a disk.</span></span> <span data-ttu-id="36af2-120">Id-eigenschap van het object geretourneerde schijf wordt gebruikt om de schijf koppelen aan een nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="36af2-120">Id property of the returned disk object is used to attach the disk to a new VM</span></span> |
| [<span data-ttu-id="36af2-121">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="36af2-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="36af2-122">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="36af2-122">Creates a VM configuration.</span></span> <span data-ttu-id="36af2-123">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="36af2-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="36af2-124">De configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="36af2-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="36af2-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="36af2-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="36af2-126">Een beheerde schijf met behulp van de eigenschap Id van de schijf als de besturingssysteemschijf voor een nieuwe virtuele machine gekoppeld</span><span class="sxs-lookup"><span data-stu-id="36af2-126">Attaches a managed disk using the Id property of the disk as OS disk to a new virtual machine</span></span> |
| [<span data-ttu-id="36af2-127">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="36af2-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="36af2-128">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="36af2-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="36af2-129">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="36af2-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="36af2-130">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="36af2-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="36af2-131">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="36af2-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="36af2-132">Maak een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="36af2-132">Create a virtual machine.</span></span> |
|[<span data-ttu-id="36af2-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="36af2-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="36af2-134">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="36af2-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="36af2-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36af2-135">Next steps</span></span>

<span data-ttu-id="36af2-136">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="36af2-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="36af2-137">Voorbeelden van extra virtuele machine PowerShell-script kunnen worden gevonden in de [virtuele machine van Windows Azure-documentatie](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36af2-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>