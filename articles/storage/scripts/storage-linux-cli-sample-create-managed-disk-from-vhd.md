---
title: Azure CLI-Script steekproef - maken van een beheerde schijf van een VHD-bestand in een opslagaccount in hetzelfde abonnement | Microsoft Docs
description: Azure CLI-Script steekproef - maken van een beheerde schijf van een VHD-bestand in een opslagaccount in hetzelfde abonnement
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
ms.openlocfilehash: 5022ca23ac2c2e515a9b80d44b1221f3c05fecb1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-the-same-subscription-with-cli"></a><span data-ttu-id="228db-103">Maak een beheerde schijf van een VHD-bestand in een opslagaccount in hetzelfde abonnement met CLI</span><span class="sxs-lookup"><span data-stu-id="228db-103">Create a managed disk from a VHD file in a storage account in the same subscription with CLI</span></span>

<span data-ttu-id="228db-104">Dit script maakt een beheerde schijf van een VHD-bestand in een opslagaccount in hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="228db-104">This script creates a managed disk from a VHD file in a storage account in the same subscription.</span></span> <span data-ttu-id="228db-105">Dit script gebruiken voor het importeren van een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD naar beheerde OS-schijf voor het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="228db-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="228db-106">Of gebruik het importeren van een VHD-gegevens naar beheerde gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="228db-106">Or, use it to import a data VHD to managed data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="228db-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="228db-107">Sample script</span></span>

<span data-ttu-id="228db-108">[!code-azurecli[belangrijkste](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "-beheerde schijven van VHD maken")]</span><span class="sxs-lookup"><span data-stu-id="228db-108">[!code-azurecli[main](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="228db-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="228db-109">Script explanation</span></span>

<span data-ttu-id="228db-110">Dit script gebruikt na de opdrachten voor het maken van een beheerde schijf vanaf een VHD.</span><span class="sxs-lookup"><span data-stu-id="228db-110">This script uses following commands to create a managed disk from a VHD.</span></span> <span data-ttu-id="228db-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="228db-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="228db-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="228db-112">Command</span></span> | <span data-ttu-id="228db-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="228db-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="228db-114">AZ schijf maken</span><span class="sxs-lookup"><span data-stu-id="228db-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="228db-115">Hiermee maakt u een beheerde schijf met de URI van een VHD in een opslagaccount in hetzelfde abonnement</span><span class="sxs-lookup"><span data-stu-id="228db-115">Creates a managed disk using URI of a VHD in a storage account in the same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="228db-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="228db-116">Next steps</span></span>

[<span data-ttu-id="228db-117">Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="228db-117">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="228db-118">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="228db-118">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="228db-119">Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="228db-119">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
