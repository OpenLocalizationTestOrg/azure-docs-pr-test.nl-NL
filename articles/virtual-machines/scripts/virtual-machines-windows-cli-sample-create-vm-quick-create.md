---
title: Azure CLI-voorbeeldscript - snel maken van een Windows Server 2016 VM | Microsoft Docs
description: Azure CLI-voorbeeldscript - snel maken van een virtuele machine van Windows Server 2016
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rickstercdn
ms.openlocfilehash: 084518bf7bc1d01c4a146efe3e0b7fe08149ce35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="14d4f-103">Snel een virtuele machine maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="14d4f-103">Quick Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="14d4f-104">Dit script maakt een Azure-virtuele Machine met Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="14d4f-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="14d4f-105">Nadat het script is uitgevoerd, kunt u de virtuele machine via Extern bureaublad-verbinding openen.</span><span class="sxs-lookup"><span data-stu-id="14d4f-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="14d4f-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="14d4f-106">Sample script</span></span>

<span data-ttu-id="14d4f-107">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "snelle VM maken")]</span><span class="sxs-lookup"><span data-stu-id="14d4f-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="14d4f-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="14d4f-108">Clean up deployment</span></span> 

<span data-ttu-id="14d4f-109">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="14d4f-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="14d4f-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="14d4f-110">Script explanation</span></span>

<span data-ttu-id="14d4f-111">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="14d4f-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="14d4f-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="14d4f-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="14d4f-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="14d4f-113">Command</span></span> | <span data-ttu-id="14d4f-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="14d4f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="14d4f-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="14d4f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="14d4f-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="14d4f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="14d4f-117">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="14d4f-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="14d4f-118">De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en netwerkbeveiligingsgroep is verbonden.</span><span class="sxs-lookup"><span data-stu-id="14d4f-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="14d4f-119">Deze opdracht geeft ook aan de installatiekopie van de virtuele machine om te worden gebruikt en administratieve referenties.</span><span class="sxs-lookup"><span data-stu-id="14d4f-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="14d4f-120">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="14d4f-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="14d4f-121">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="14d4f-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="14d4f-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="14d4f-122">Next steps</span></span>

<span data-ttu-id="14d4f-123">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="14d4f-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="14d4f-124">Extra virtuele machine CLI scriptvoorbeelden vindt u in de [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="14d4f-124">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
