---
title: 'Azure CLI-Script voorbeeld: een beheerde schijven maken vanuit een momentopname | Microsoft Docs'
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
ms.openlocfilehash: 030fa06bc5819443dac5832172a93c2dca28d1ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="9a042-103">Een beheerde schijf maken vanuit een momentopname met CLI</span><span class="sxs-lookup"><span data-stu-id="9a042-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="9a042-104">Dit script maakt een beheerde schijf van een momentopname.</span><span class="sxs-lookup"><span data-stu-id="9a042-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="9a042-105">Gebruik dit voor een virtuele machine herstellen van momentopnamen van het besturingssysteem en gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="9a042-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="9a042-106">OS maken en gegevens van de respectieve momentopnamen schijven die worden beheerd en maak vervolgens een nieuwe virtuele machine door het koppelen van beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="9a042-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="9a042-107">U kunt ook de gegevensschijven van een bestaande virtuele machine herstellen door het koppelen van gegevensschijven gemaakt op basis van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="9a042-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9a042-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9a042-108">Sample script</span></span>

<span data-ttu-id="9a042-109">[!code-azurecli[belangrijkste](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "-beheerde schijven maken vanuit een momentopname.")]</span><span class="sxs-lookup"><span data-stu-id="9a042-109">[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="9a042-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9a042-110">Script explanation</span></span>

<span data-ttu-id="9a042-111">Dit script gebruikt na de opdrachten voor het maken van een beheerde schijf vanuit een momentopname.</span><span class="sxs-lookup"><span data-stu-id="9a042-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="9a042-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="9a042-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9a042-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9a042-113">Command</span></span> | <span data-ttu-id="9a042-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9a042-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9a042-115">AZ momentopname weergeven</span><span class="sxs-lookup"><span data-stu-id="9a042-115">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="9a042-116">Hiermee haalt u de eigenschappen van een momentopname met de naam en eigenschappen van de momentopname van de bronnengroep.</span><span class="sxs-lookup"><span data-stu-id="9a042-116">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="9a042-117">Id-eigenschap wordt gebruikt om beheerde schijf te maken.</span><span class="sxs-lookup"><span data-stu-id="9a042-117">Id property is used to create managed disk.</span></span>  |
| [<span data-ttu-id="9a042-118">AZ schijf maken</span><span class="sxs-lookup"><span data-stu-id="9a042-118">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="9a042-119">Hiermee maakt u een beheerde met behulp van schijf-Id van een momentopname van een beheerde momentopname</span><span class="sxs-lookup"><span data-stu-id="9a042-119">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9a042-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a042-120">Next steps</span></span>

[<span data-ttu-id="9a042-121">Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="9a042-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="9a042-122">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9a042-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9a042-123">Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a042-123">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
