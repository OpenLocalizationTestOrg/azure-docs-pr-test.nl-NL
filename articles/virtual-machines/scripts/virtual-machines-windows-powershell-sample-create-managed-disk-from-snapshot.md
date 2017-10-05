---
title: 'Azure PowerShell-Script voorbeeld: een beheerde schijven maken vanuit een momentopname | Microsoft Docs'
description: 'Azure PowerShell-Script voorbeeld: een beheerde schijven maken vanuit een momentopname'
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: b475516694d120b7ea05d0892b6789710eec171e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="fed69-103">Een beheerde schijf maken vanuit een momentopname met PowerShell</span><span class="sxs-lookup"><span data-stu-id="fed69-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="fed69-104">Dit script maakt een beheerde schijf van een momentopname.</span><span class="sxs-lookup"><span data-stu-id="fed69-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="fed69-105">Gebruik dit voor een virtuele machine herstellen van momentopnamen van het besturingssysteem en gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="fed69-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="fed69-106">OS maken en gegevens van de respectieve momentopnamen schijven die worden beheerd en maak vervolgens een nieuwe virtuele machine door het koppelen van beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="fed69-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="fed69-107">U kunt ook de gegevensschijven van een bestaande virtuele machine herstellen door het koppelen van gegevensschijven gemaakt op basis van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="fed69-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fed69-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="fed69-108">Sample script</span></span>

<span data-ttu-id="fed69-109">[!code-powershell[belangrijkste](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "-beheerde schijven maken vanuit een momentopname.")]</span><span class="sxs-lookup"><span data-stu-id="fed69-109">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="fed69-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="fed69-110">Script explanation</span></span>

<span data-ttu-id="fed69-111">Dit script gebruikt na de opdrachten voor het maken van een beheerde schijf vanuit een momentopname.</span><span class="sxs-lookup"><span data-stu-id="fed69-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="fed69-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="fed69-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fed69-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="fed69-113">Command</span></span> | <span data-ttu-id="fed69-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="fed69-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fed69-115">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="fed69-115">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="fed69-116">Eigenschappen van de momentopname opgehaald.</span><span class="sxs-lookup"><span data-stu-id="fed69-116">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="fed69-117">Nieuwe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="fed69-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="fed69-118">Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf.</span><span class="sxs-lookup"><span data-stu-id="fed69-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="fed69-119">Dit omvat de resource-Id van de momentopname van de bovenliggende, de locatie die is hetzelfde als de locatie van momentopname van de bovenliggende en een opslagtype.</span><span class="sxs-lookup"><span data-stu-id="fed69-119">It includes the resource Id of the parent snapshot, location that is same as the location of parent snapshot and the storage type.</span></span>  |
| [<span data-ttu-id="fed69-120">Nieuwe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="fed69-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="fed69-121">Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="fed69-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="fed69-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fed69-122">Next steps</span></span>

[<span data-ttu-id="fed69-123">Een virtuele machine maken van een beheerde schijf</span><span class="sxs-lookup"><span data-stu-id="fed69-123">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="fed69-124">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fed69-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fed69-125">Voorbeelden van extra virtuele machine PowerShell-script kunnen worden gevonden in de [virtuele machine van Windows Azure-documentatie](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fed69-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>