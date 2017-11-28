---
title: een beheerde schijf aaaAzure PowerShell-voorbeeldscript - maken vanuit een momentopname | Microsoft Docs
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
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="9e709-103">Een beheerde schijf maken vanuit een momentopname met PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e709-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="9e709-104">Dit script maakt een beheerde schijf van een momentopname.</span><span class="sxs-lookup"><span data-stu-id="9e709-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="9e709-105">Gebruik dit toorestore een virtuele machine van de momentopnamen van het besturingssysteem en gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="9e709-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="9e709-106">OS maken en gegevens van de respectieve momentopnamen schijven die worden beheerd en maak vervolgens een nieuwe virtuele machine door het koppelen van beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="9e709-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="9e709-107">U kunt ook de gegevensschijven van een bestaande virtuele machine herstellen door het koppelen van gegevensschijven gemaakt op basis van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="9e709-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9e709-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9e709-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="9e709-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9e709-109">Script explanation</span></span>

<span data-ttu-id="9e709-110">Dit script gebruikt na opdrachten toocreate een beheerde schijf vanuit een momentopname.</span><span class="sxs-lookup"><span data-stu-id="9e709-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="9e709-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="9e709-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9e709-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9e709-112">Command</span></span> | <span data-ttu-id="9e709-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9e709-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e709-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="9e709-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="9e709-115">Eigenschappen van de momentopname opgehaald.</span><span class="sxs-lookup"><span data-stu-id="9e709-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="9e709-116">Nieuwe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="9e709-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="9e709-117">Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf.</span><span class="sxs-lookup"><span data-stu-id="9e709-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="9e709-118">Dit omvat Hallo resource-Id van Hallo bovenliggende momentopname, de locatie die is hetzelfde als het Hallo-locatie van het type van bovenliggende momentopnamen en het Hallo-opslag.</span><span class="sxs-lookup"><span data-stu-id="9e709-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="9e709-119">Nieuwe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="9e709-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="9e709-120">Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="9e709-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="9e709-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e709-121">Next steps</span></span>

[<span data-ttu-id="9e709-122">Een virtuele machine maken van een beheerde schijf</span><span class="sxs-lookup"><span data-stu-id="9e709-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="9e709-123">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e709-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9e709-124">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e709-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
