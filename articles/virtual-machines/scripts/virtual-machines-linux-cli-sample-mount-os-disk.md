---
title: aaaAzure voorbeeldscript CLI - koppelpunt besturingssysteemschijf | Microsoft Docs
description: Azure CLI-voorbeeldscript - schijf koppelen-besturingssysteem
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="7a3a9-103">Problemen met een besturingssysteemschijf virtuele machines</span><span class="sxs-lookup"><span data-stu-id="7a3a9-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="7a3a9-104">Dit script koppelt Hallo besturingssysteemschijf van een virtuele machine is mislukt of problemen veroorzaken als gegevens schijf tooa tweede virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="7a3a9-105">Dit kan nuttig zijn bij het oplossen van problemen of -gegevens herstellen schijf.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7a3a9-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="7a3a9-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="7a3a9-107">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="7a3a9-107">Script explanation</span></span>

<span data-ttu-id="7a3a9-108">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="7a3a9-109">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7a3a9-110">Opdracht</span><span class="sxs-lookup"><span data-stu-id="7a3a9-110">Command</span></span> | <span data-ttu-id="7a3a9-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7a3a9-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a3a9-112">AZ vm weergeven</span><span class="sxs-lookup"><span data-stu-id="7a3a9-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="7a3a9-113">Retourneert een lijst met virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-113">Return a list of virtual machines.</span></span> <span data-ttu-id="7a3a9-114">In dit geval is Hallo query-optie schijf besturingssysteem gebruikte tooreturn Hallo-virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="7a3a9-115">Deze waarde wordt vervolgens toegevoegd aan tooa variabelenaam 'uri'.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="7a3a9-116">AZ vm verwijderen</span><span class="sxs-lookup"><span data-stu-id="7a3a9-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="7a3a9-117">Hiermee verwijdert u een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="7a3a9-118">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="7a3a9-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7a3a9-119">Hiermee maakt u een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="7a3a9-120">AZ vm schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="7a3a9-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="7a3a9-121">Er wordt een schijf tooa virtuele machine toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="7a3a9-122">AZ vm lijst-ip-adressen</span><span class="sxs-lookup"><span data-stu-id="7a3a9-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="7a3a9-123">Retourneert Hallo IP-adressen van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a3a9-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a3a9-124">Next steps</span></span>

<span data-ttu-id="7a3a9-125">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a3a9-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7a3a9-126">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a3a9-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
