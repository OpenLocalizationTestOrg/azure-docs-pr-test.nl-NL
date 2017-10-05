---
title: Azure CLI-voorbeeldscript - koppelpunt besturingssysteemschijf | Microsoft Docs
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
ms.openlocfilehash: b54a94d833644ebfae4c1fac59e4753ab723ced4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="9b88d-103">Problemen met een besturingssysteemschijf virtuele machines</span><span class="sxs-lookup"><span data-stu-id="9b88d-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="9b88d-104">Dit script koppelt u de schijf van het besturingssysteem van een mislukte of problematisch virtuele machine als een gegevensschijf aan een tweede virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9b88d-104">This script mounts the operating system disk of a failed or problematic virtual machine as a data disk to a second virtual machine.</span></span> <span data-ttu-id="9b88d-105">Dit kan nuttig zijn bij het oplossen van problemen of -gegevens herstellen schijf.</span><span class="sxs-lookup"><span data-stu-id="9b88d-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9b88d-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9b88d-106">Sample script</span></span>

<span data-ttu-id="9b88d-107">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "snelle VM maken")]</span><span class="sxs-lookup"><span data-stu-id="9b88d-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="9b88d-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9b88d-108">Script explanation</span></span>

<span data-ttu-id="9b88d-109">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="9b88d-109">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9b88d-110">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="9b88d-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9b88d-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9b88d-111">Command</span></span> | <span data-ttu-id="9b88d-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9b88d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9b88d-113">AZ vm weergeven</span><span class="sxs-lookup"><span data-stu-id="9b88d-113">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="9b88d-114">Retourneert een lijst met virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9b88d-114">Return a list of virtual machines.</span></span> <span data-ttu-id="9b88d-115">In dit geval wordt de query-optie gebruikt om te retourneren van de schijf van de virtuele machine-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="9b88d-115">In this case, the query option is used to return the virtual machine operating system disk.</span></span> <span data-ttu-id="9b88d-116">Deze waarde wordt vervolgens toegevoegd aan de naam van een variabele 'uri'.</span><span class="sxs-lookup"><span data-stu-id="9b88d-116">This value is then added to a variable name ‘uri’.</span></span> |
| [<span data-ttu-id="9b88d-117">AZ vm verwijderen</span><span class="sxs-lookup"><span data-stu-id="9b88d-117">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="9b88d-118">Hiermee verwijdert u een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9b88d-118">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="9b88d-119">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="9b88d-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9b88d-120">Hiermee maakt u een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9b88d-120">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="9b88d-121">AZ vm schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="9b88d-121">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="9b88d-122">Er wordt een schijf aan een virtuele machine toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9b88d-122">Attaches a disk to a virtual machine.</span></span> |
| [<span data-ttu-id="9b88d-123">AZ vm lijst-ip-adressen</span><span class="sxs-lookup"><span data-stu-id="9b88d-123">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="9b88d-124">Retourneert de IP-adressen van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9b88d-124">Returns the IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9b88d-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b88d-125">Next steps</span></span>

<span data-ttu-id="9b88d-126">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b88d-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9b88d-127">Extra virtuele machine CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b88d-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
