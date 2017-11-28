---
title: aaaAzure PowerShell-voorbeeldscript - exemplaar (verplaatsen) beheerd toosame schijven of een ander abonnement | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - exemplaar (verplaatsen) beheerd schijven toosame of een ander abonnement
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 5a92118e10a14615e5b1713f1b90188b37b05305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="401be-103">Schijven kopiëren die worden beheerd in de Hallo dezelfde abonnement of een ander abonnement met PowerShell</span><span class="sxs-lookup"><span data-stu-id="401be-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="401be-104">Dit script maakt een kopie van een bestaande beheerde schijf in Hallo hetzelfde abonnement of een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="401be-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="401be-105">Hallo nieuwe schijf wordt gemaakt in Hallo dezelfde regio bevinden als Hallo bovenliggende schijf worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="401be-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="401be-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="401be-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="401be-107">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="401be-107">Script explanation</span></span>

<span data-ttu-id="401be-108">Dit script maakt gebruik van opdrachten toocreate na een nieuwe beheerde schijf bij het gebruik van Hallo doel abonnement Hallo Hallo bron-Id beheerd schijf.</span><span class="sxs-lookup"><span data-stu-id="401be-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="401be-109">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="401be-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="401be-110">Opdracht</span><span class="sxs-lookup"><span data-stu-id="401be-110">Command</span></span> | <span data-ttu-id="401be-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="401be-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="401be-112">Nieuwe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="401be-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="401be-113">Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf.</span><span class="sxs-lookup"><span data-stu-id="401be-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="401be-114">Dit omvat Hallo resource-Id van Hallo bovenliggende schijf en de locatie die is hetzelfde als het Hallo-locatie van de bovenliggende schijf.</span><span class="sxs-lookup"><span data-stu-id="401be-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="401be-115">Nieuwe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="401be-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="401be-116">Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="401be-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="401be-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="401be-117">Next steps</span></span>

[<span data-ttu-id="401be-118">Een virtuele machine maken van een beheerde schijf</span><span class="sxs-lookup"><span data-stu-id="401be-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="401be-119">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="401be-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="401be-120">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="401be-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
