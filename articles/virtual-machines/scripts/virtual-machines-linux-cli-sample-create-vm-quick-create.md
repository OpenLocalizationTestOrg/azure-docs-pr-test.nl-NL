---
title: Azure CLI-voorbeeldscript - snel een virtuele Linux-machine maken | Microsoft Docs
description: Azure CLI-voorbeeldscript - snel een virtuele Linux-machine maken
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
ms.openlocfilehash: 3df3affcedf9edbe6e548d881a877f14204ec280
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="d5cee-103">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="d5cee-103">Create a virtual machine</span></span>

<span data-ttu-id="d5cee-104">Dit script maakt een virtuele Machine van Azure met een besturingssysteem Ubuntu en verwante netwerkresources.</span><span class="sxs-lookup"><span data-stu-id="d5cee-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="d5cee-105">Nadat het script is uitgevoerd, kunt u de virtuele machine via SSH te openen.</span><span class="sxs-lookup"><span data-stu-id="d5cee-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d5cee-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="d5cee-106">Sample script</span></span>

<span data-ttu-id="d5cee-107">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "snelle VM maken")]</span><span class="sxs-lookup"><span data-stu-id="d5cee-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d5cee-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="d5cee-108">Clean up deployment</span></span> 

<span data-ttu-id="d5cee-109">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d5cee-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d5cee-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="d5cee-110">Script explanation</span></span>

<span data-ttu-id="d5cee-111">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="d5cee-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d5cee-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="d5cee-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d5cee-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="d5cee-113">Command</span></span> | <span data-ttu-id="d5cee-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d5cee-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d5cee-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="d5cee-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d5cee-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d5cee-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d5cee-117">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="d5cee-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d5cee-118">De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en netwerkbeveiligingsgroep is verbonden.</span><span class="sxs-lookup"><span data-stu-id="d5cee-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="d5cee-119">Deze opdracht geeft ook aan de installatiekopie van de virtuele machine om te worden gebruikt en administratieve referenties.</span><span class="sxs-lookup"><span data-stu-id="d5cee-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="d5cee-120">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="d5cee-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d5cee-121">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="d5cee-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d5cee-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d5cee-122">Next steps</span></span>

<span data-ttu-id="d5cee-123">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d5cee-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d5cee-124">Extra virtuele machine CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d5cee-124">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
