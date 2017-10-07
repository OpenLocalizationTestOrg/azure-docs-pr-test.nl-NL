---
title: aaaAzure voorbeeldscript CLI - exemplaar (verplaatsen) beheerd toosame schijven of een ander abonnement | Microsoft Docs
description: Azure CLI voorbeeldscript - exemplaar (verplaatsen) beheerd schijven toosame of een ander abonnement
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="87a69-103">Beheerde schijven toosame of een ander abonnement met CLI kopiëren</span><span class="sxs-lookup"><span data-stu-id="87a69-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="87a69-104">Dit script kopieert een beheerde schijf toosame of een ander abonnement maar Hallo in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="87a69-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="87a69-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="87a69-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="87a69-106">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="87a69-106">Script explanation</span></span>

<span data-ttu-id="87a69-107">Dit script maakt gebruik van opdrachten toocreate na een nieuwe beheerde schijf bij het gebruik van Hallo doel abonnement Hallo Hallo bron-Id beheerd schijf.</span><span class="sxs-lookup"><span data-stu-id="87a69-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="87a69-108">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="87a69-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="87a69-109">Opdracht</span><span class="sxs-lookup"><span data-stu-id="87a69-109">Command</span></span> | <span data-ttu-id="87a69-110">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="87a69-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="87a69-111">AZ schijf weergeven</span><span class="sxs-lookup"><span data-stu-id="87a69-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="87a69-112">Hiermee haalt u alle Hallo-eigenschappen van een beheerde schijf met een Hallo groepseigenschappen en de bron van het Hallo-beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="87a69-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="87a69-113">Id-eigenschap is gebruikte toocopy Hallo beheerd schijf toodifferent abonnement.</span><span class="sxs-lookup"><span data-stu-id="87a69-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="87a69-114">AZ schijf maken</span><span class="sxs-lookup"><span data-stu-id="87a69-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="87a69-115">Een beheerde schijf opgehaald door het maken van een nieuwe beheerde schijf in een ander abonnement-Id en naam Hallo bovenliggende schijf worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="87a69-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="87a69-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87a69-116">Next steps</span></span>

[<span data-ttu-id="87a69-117">Een virtuele machine maken van een beheerde schijf</span><span class="sxs-lookup"><span data-stu-id="87a69-117">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="87a69-118">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="87a69-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="87a69-119">Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in Hallo [Azure Linux VM documentatie](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="87a69-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
