---
title: Azure PowerShell-Script voorbeeld - exemplaar (verplaatsen)-momentopname van een beheerde schijf naar hetzelfde of een ander abonnement | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - exemplaar (verplaatsen)-momentopname van een beheerde schijf naar hetzelfde of een ander abonnement
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
ms.openlocfilehash: 69b9b4ed86117f7fe561e7e70227e60e6a9d858e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="b94a6-103">Momentopname van een beheerde schijf kopiëren in hetzelfde abonnement of een ander abonnement met PowerShell</span><span class="sxs-lookup"><span data-stu-id="b94a6-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="b94a6-104">Dit script maakt een kopie van een momentopname in de dezelfde hetzelfde abonnement of een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="b94a6-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="b94a6-105">Dit script gebruiken voor het verplaatsen van een momentopname naar ander abonnement voor het bewaren van gegevens.</span><span class="sxs-lookup"><span data-stu-id="b94a6-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="b94a6-106">Opslag-momentopnamen in een ander abonnement bescherming tegen onopzettelijk verwijderen van momentopnamen in uw belangrijkste abonnement.</span><span class="sxs-lookup"><span data-stu-id="b94a6-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b94a6-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="b94a6-107">Sample script</span></span>

<span data-ttu-id="b94a6-108">[!code-powershell[belangrijkste](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "kopie momentopname")]</span><span class="sxs-lookup"><span data-stu-id="b94a6-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="b94a6-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="b94a6-109">Script explanation</span></span>

<span data-ttu-id="b94a6-110">Dit script gebruikt na de opdrachten voor het maken van een momentopname in het doelabonnement met de Id van de momentopname van de bron.</span><span class="sxs-lookup"><span data-stu-id="b94a6-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="b94a6-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="b94a6-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b94a6-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="b94a6-112">Command</span></span> | <span data-ttu-id="b94a6-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b94a6-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b94a6-114">Nieuwe AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="b94a6-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="b94a6-115">Maakt de configuratie van de momentopnamen die wordt gebruikt voor het maken van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="b94a6-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="b94a6-116">Dit omvat de resource-Id van de momentopname van de bovenliggende en de locatie die is hetzelfde als de momentopname van de bovenliggende.</span><span class="sxs-lookup"><span data-stu-id="b94a6-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="b94a6-117">Nieuwe AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="b94a6-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="b94a6-118">Maakt een momentopname met configuratie van de momentopnamen, naam van de momentopname en de Resourcegroepnaam als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="b94a6-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b94a6-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b94a6-119">Next steps</span></span>

[<span data-ttu-id="b94a6-120">Een virtuele machine maken vanuit een momentopname</span><span class="sxs-lookup"><span data-stu-id="b94a6-120">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="b94a6-121">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b94a6-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b94a6-122">Voorbeelden van extra virtuele machine PowerShell-script kunnen worden gevonden in de [virtuele machine van Windows Azure-documentatie](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b94a6-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>