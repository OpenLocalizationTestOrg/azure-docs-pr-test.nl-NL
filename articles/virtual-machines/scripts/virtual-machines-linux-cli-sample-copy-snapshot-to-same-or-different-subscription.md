---
title: aaaAzure voorbeeldscript CLI - exemplaar (verplaatsen)-momentopname van een beheerde schijf toosame of een ander abonnement met CLI | Microsoft Docs
description: Azure CLI-voorbeeldscript - exemplaar (verplaatsen)-momentopname van een beheerde schijf toosame of een ander abonnement met CLI
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
ms.openlocfilehash: f214ab1fc1cb2cb42479d82e455f20a8cc55c83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="dd2c2-103">Kopiëren van de momentopname van een beheerde schijf toosame of een ander abonnement met CLI</span><span class="sxs-lookup"><span data-stu-id="dd2c2-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="dd2c2-104">Dit script wordt gekopieerd van een momentopname van een beheerde schijf toosame of een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="dd2c2-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="dd2c2-105">Gebruik dit script toomove een momentopname toodifferent abonnement in Hallo dezelfde regio bevinden als Hallo bovenliggende momentopname.</span><span class="sxs-lookup"><span data-stu-id="dd2c2-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dd2c2-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="dd2c2-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="dd2c2-107">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="dd2c2-107">Script explanation</span></span>

<span data-ttu-id="dd2c2-108">Dit script maakt gebruik van opdrachten toocreate na een momentopname aan Hallo doel abonnement met Hallo Hallo bron momentopname-Id.</span><span class="sxs-lookup"><span data-stu-id="dd2c2-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="dd2c2-109">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="dd2c2-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dd2c2-110">Opdracht</span><span class="sxs-lookup"><span data-stu-id="dd2c2-110">Command</span></span> | <span data-ttu-id="dd2c2-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="dd2c2-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dd2c2-112">AZ momentopname weergeven</span><span class="sxs-lookup"><span data-stu-id="dd2c2-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="dd2c2-113">Hiermee haalt u alle Hallo eigenschappen van een momentopname met de naam van de Hallo en eigenschappen van de bronnengroep van Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="dd2c2-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="dd2c2-114">Id-eigenschap is gebruikte toocopy Hallo momentopname toodifferent abonnement.</span><span class="sxs-lookup"><span data-stu-id="dd2c2-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="dd2c2-115">AZ momentopname maken</span><span class="sxs-lookup"><span data-stu-id="dd2c2-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="dd2c2-116">Een momentopname van een door het maken van een momentopname bij het gebruik van verschillende abonnement-Id en de naam van Hallo kopieën Hallo bovenliggende momentopname.</span><span class="sxs-lookup"><span data-stu-id="dd2c2-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="dd2c2-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dd2c2-117">Next steps</span></span>

[<span data-ttu-id="dd2c2-118">Een virtuele machine maken vanuit een momentopname</span><span class="sxs-lookup"><span data-stu-id="dd2c2-118">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="dd2c2-119">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dd2c2-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dd2c2-120">Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in Hallo [Azure Linux VM documentatie](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd2c2-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
