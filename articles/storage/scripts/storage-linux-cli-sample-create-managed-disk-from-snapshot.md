---
title: een beheerde schijf aaaAzure voorbeeldscript CLI - maken vanuit een momentopname | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een beheerde schijven maken vanuit een momentopname'
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
ms.openlocfilehash: f92059353bfb739cff05213a9d206bfde2829a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="e539d-103">Een beheerde schijf maken vanuit een momentopname met CLI</span><span class="sxs-lookup"><span data-stu-id="e539d-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="e539d-104">Dit script maakt een beheerde schijf van een momentopname.</span><span class="sxs-lookup"><span data-stu-id="e539d-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="e539d-105">Gebruik dit toorestore een virtuele machine van de momentopnamen van het besturingssysteem en gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="e539d-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="e539d-106">OS maken en gegevens van de respectieve momentopnamen schijven die worden beheerd en maak vervolgens een nieuwe virtuele machine door het koppelen van beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="e539d-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="e539d-107">U kunt ook de gegevensschijven van een bestaande virtuele machine herstellen door het koppelen van gegevensschijven gemaakt op basis van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="e539d-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e539d-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="e539d-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="e539d-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="e539d-109">Script explanation</span></span>

<span data-ttu-id="e539d-110">Dit script gebruikt na opdrachten toocreate een beheerde schijf vanuit een momentopname.</span><span class="sxs-lookup"><span data-stu-id="e539d-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="e539d-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="e539d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e539d-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="e539d-112">Command</span></span> | <span data-ttu-id="e539d-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e539d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e539d-114">AZ momentopname weergeven</span><span class="sxs-lookup"><span data-stu-id="e539d-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="e539d-115">Hiermee haalt u alle Hallo eigenschappen van een momentopname met de naam van de Hallo en eigenschappen van de bronnengroep van Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="e539d-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="e539d-116">Id-eigenschap is gebruikte toocreate beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="e539d-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="e539d-117">AZ schijf maken</span><span class="sxs-lookup"><span data-stu-id="e539d-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="e539d-118">Hiermee maakt u een beheerde met behulp van schijf-Id van een momentopname van een beheerde momentopname</span><span class="sxs-lookup"><span data-stu-id="e539d-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e539d-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e539d-119">Next steps</span></span>

[<span data-ttu-id="e539d-120">Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="e539d-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="e539d-121">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e539d-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e539d-122">Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in Hallo [Azure Linux VM documentatie](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e539d-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
