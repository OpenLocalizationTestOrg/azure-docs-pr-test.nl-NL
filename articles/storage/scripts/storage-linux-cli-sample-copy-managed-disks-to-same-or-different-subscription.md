---
title: "Azure CLI-voorbeeldscript - schijven op dezelfde of verschillende abonnement die worden beheerd kopiëren (verplaatsen) | Microsoft Docs"
description: Azure CLI-voorbeeldscript - exemplaar (verplaatsen) beheerd schijven met hetzelfde of een ander abonnement
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 784ad81db2c83da14665fa926425928f12a15c27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="copy-managed-disks-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="d457b-103">Beheerde schijven met hetzelfde of een ander abonnement CLI kopiëren</span><span class="sxs-lookup"><span data-stu-id="d457b-103">Copy managed disks to same or different subscription with CLI</span></span>

<span data-ttu-id="d457b-104">Dit script wordt een beheerde schijf gekopieerd naar hetzelfde of een ander abonnement, maar in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="d457b-104">This script copies a managed disk to same or different subscription but in the same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d457b-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="d457b-105">Sample script</span></span>

<span data-ttu-id="d457b-106">[!code-azurecli[belangrijkste](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "kopie beheerd schijf")]</span><span class="sxs-lookup"><span data-stu-id="d457b-106">[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="d457b-107">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="d457b-107">Script explanation</span></span>

<span data-ttu-id="d457b-108">Dit script gebruikt na de opdrachten voor het maken van een nieuwe beheerde schijf in het doelabonnement met de Id van de beheerde bronschijf.</span><span class="sxs-lookup"><span data-stu-id="d457b-108">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="d457b-109">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="d457b-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d457b-110">Opdracht</span><span class="sxs-lookup"><span data-stu-id="d457b-110">Command</span></span> | <span data-ttu-id="d457b-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d457b-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d457b-112">AZ schijf weergeven</span><span class="sxs-lookup"><span data-stu-id="d457b-112">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="d457b-113">Hiermee haalt u de eigenschappen van een beheerde schijf met de naam en eigenschappen van de bronnengroep van de beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="d457b-113">Gets all the properties of a managed disk using the name and resource group properties of the managed disk.</span></span> <span data-ttu-id="d457b-114">Id-eigenschap wordt gebruikt voor de beheerde schijf kopiëren naar een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="d457b-114">Id property is used to copy the managed disk to different subscription.</span></span>  |
| [<span data-ttu-id="d457b-115">AZ schijf maken</span><span class="sxs-lookup"><span data-stu-id="d457b-115">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="d457b-116">Kopieën een beheerde schijf door het maken van een nieuwe schijf in een ander abonnement met behulp van Id beheerd en de naam van de bovenliggende beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="d457b-116">Copies a managed disk by creating a new managed disk in different subscription using Id and name the parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="d457b-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d457b-117">Next steps</span></span>

[<span data-ttu-id="d457b-118">Een virtuele machine maken van een beheerde schijf</span><span class="sxs-lookup"><span data-stu-id="d457b-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="d457b-119">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d457b-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d457b-120">Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d457b-120">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
