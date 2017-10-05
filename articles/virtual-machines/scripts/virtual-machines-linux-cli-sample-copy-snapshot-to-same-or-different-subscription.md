---
title: Azure CLI-voorbeeldscript - exemplaar (verplaatsen)-momentopname van een beheerde schijf met dezelfde of verschillende abonnement CLI | Microsoft Docs
description: Azure CLI-voorbeeldscript - exemplaar (verplaatsen)-momentopname van een beheerde schijf met dezelfde of verschillende abonnement CLI
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
ms.openlocfilehash: 6cc0125c08ccb77d014b4642d702c556fffdc8bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="9bda3-103">Momentopname van een beheerde schijf kopiëren naar hetzelfde of een ander abonnement met CLI</span><span class="sxs-lookup"><span data-stu-id="9bda3-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="9bda3-104">Dit script wordt een momentopname van een beheerde schijf gekopieerd naar hetzelfde of een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="9bda3-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="9bda3-105">Dit script gebruiken voor het verplaatsen van een momentopname naar ander abonnement in dezelfde regio bevinden als de momentopname van de bovenliggende.</span><span class="sxs-lookup"><span data-stu-id="9bda3-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9bda3-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9bda3-106">Sample script</span></span>

<span data-ttu-id="9bda3-107">[!code-azurecli[belangrijkste](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "kopie momentopname")]</span><span class="sxs-lookup"><span data-stu-id="9bda3-107">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="9bda3-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9bda3-108">Script explanation</span></span>

<span data-ttu-id="9bda3-109">Dit script gebruikt na de opdrachten voor het maken van een momentopname in het doelabonnement met de Id van de momentopname van de bron.</span><span class="sxs-lookup"><span data-stu-id="9bda3-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="9bda3-110">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="9bda3-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9bda3-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9bda3-111">Command</span></span> | <span data-ttu-id="9bda3-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9bda3-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9bda3-113">AZ momentopname weergeven</span><span class="sxs-lookup"><span data-stu-id="9bda3-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="9bda3-114">Hiermee haalt u de eigenschappen van een momentopname met de naam en eigenschappen van de momentopname van de bronnengroep.</span><span class="sxs-lookup"><span data-stu-id="9bda3-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="9bda3-115">Id-eigenschap wordt gebruikt voor het kopiëren van de momentopname naar ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="9bda3-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="9bda3-116">AZ momentopname maken</span><span class="sxs-lookup"><span data-stu-id="9bda3-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="9bda3-117">Een momentopname opgehaald door het maken van een momentopname in een ander abonnement met de Id en de naam van de momentopname van de bovenliggende.</span><span class="sxs-lookup"><span data-stu-id="9bda3-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="9bda3-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9bda3-118">Next steps</span></span>

[<span data-ttu-id="9bda3-119">Een virtuele machine maken vanuit een momentopname</span><span class="sxs-lookup"><span data-stu-id="9bda3-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="9bda3-120">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9bda3-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9bda3-121">Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9bda3-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
