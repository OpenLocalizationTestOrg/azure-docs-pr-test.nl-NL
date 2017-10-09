---
title: "aaaAzure PowerShell-voorbeeldscript - momentopname van een beheerde schijf toosame of een ander abonnement kopiëren (verplaatsen) | Microsoft Docs"
description: Azure PowerShell-Script voorbeeld - exemplaar (verplaatsen)-momentopname van een beheerde schijf toosame of een ander abonnement
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
ms.openlocfilehash: d7b8a71cc09d1950271f472e89b95bb551323be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="9b2c5-103">Momentopname van een beheerde schijf kopiëren in hetzelfde abonnement of een ander abonnement met PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b2c5-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="9b2c5-104">Dit script maakt een kopie van een momentopname in Hallo dezelfde hetzelfde abonnement of een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="9b2c5-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="9b2c5-105">Gebruik dit script toomove een momentopname toodifferent abonnement voor bewaren van gegevens.</span><span class="sxs-lookup"><span data-stu-id="9b2c5-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="9b2c5-106">Opslag-momentopnamen in een ander abonnement bescherming tegen onopzettelijk verwijderen van momentopnamen in uw belangrijkste abonnement.</span><span class="sxs-lookup"><span data-stu-id="9b2c5-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9b2c5-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9b2c5-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="9b2c5-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9b2c5-108">Script explanation</span></span>

<span data-ttu-id="9b2c5-109">Dit script maakt gebruik van opdrachten toocreate na een momentopname aan Hallo doel abonnement met Hallo Hallo bron momentopname-Id.</span><span class="sxs-lookup"><span data-stu-id="9b2c5-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="9b2c5-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="9b2c5-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9b2c5-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9b2c5-111">Command</span></span> | <span data-ttu-id="9b2c5-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9b2c5-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9b2c5-113">Nieuwe AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="9b2c5-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="9b2c5-114">Maakt de configuratie van de momentopnamen die wordt gebruikt voor het maken van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="9b2c5-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="9b2c5-115">Het bevat Hallo-resource-Id van de momentopname van de bovenliggende Hallo en de locatie die is hetzelfde als Hallo bovenliggende momentopname.</span><span class="sxs-lookup"><span data-stu-id="9b2c5-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="9b2c5-116">Nieuwe AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="9b2c5-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="9b2c5-117">Maakt een momentopname met configuratie van de momentopnamen, naam van de momentopname en de Resourcegroepnaam als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="9b2c5-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="9b2c5-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b2c5-118">Next steps</span></span>

[<span data-ttu-id="9b2c5-119">Een virtuele machine maken vanuit een momentopname</span><span class="sxs-lookup"><span data-stu-id="9b2c5-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="9b2c5-120">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b2c5-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9b2c5-121">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b2c5-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
