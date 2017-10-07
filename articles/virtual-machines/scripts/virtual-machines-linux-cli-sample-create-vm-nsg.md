---
title: aaaAzure voorbeeldscript CLI - twee virtuele machines maken met een interne en externe NSG | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: twee virtuele machines maken met de interne en externe NSG'
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
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="3d61b-103">Beveiligen van netwerkverkeer tussen virtuele machines</span><span class="sxs-lookup"><span data-stu-id="3d61b-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="3d61b-104">Dit script maakt twee virtuele machines en binnenkomende verkeer tooboth beveiligt.</span><span class="sxs-lookup"><span data-stu-id="3d61b-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="3d61b-105">Een virtuele machine is toegankelijk op Hallo van internet en is een netwerkbeveiligingsgroep (NSG) tooallow verkeer geconfigureerd op poort 22 en 80.</span><span class="sxs-lookup"><span data-stu-id="3d61b-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 22 and port 80.</span></span> <span data-ttu-id="3d61b-106">Hallo tweede virtuele machine is niet toegankelijk op Hallo van internet en is een NSG geconfigureerd tooonly verkeer van de eerste virtuele machine Hallo toestaan.</span><span class="sxs-lookup"><span data-stu-id="3d61b-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3d61b-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="3d61b-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3d61b-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="3d61b-108">Clean up deployment</span></span> 

<span data-ttu-id="3d61b-109">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3d61b-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3d61b-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="3d61b-110">Script explanation</span></span>

<span data-ttu-id="3d61b-111">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="3d61b-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="3d61b-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="3d61b-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3d61b-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="3d61b-113">Command</span></span> | <span data-ttu-id="3d61b-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3d61b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d61b-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="3d61b-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3d61b-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3d61b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3d61b-117">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="3d61b-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="3d61b-118">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="3d61b-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="3d61b-119">AZ network vnet subnet maken</span><span class="sxs-lookup"><span data-stu-id="3d61b-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="3d61b-120">Maakt een subnet.</span><span class="sxs-lookup"><span data-stu-id="3d61b-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="3d61b-121">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="3d61b-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="3d61b-122">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="3d61b-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="3d61b-123">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="3d61b-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="3d61b-124">lijst van de regel met het nsg van netwerken AZ</span><span class="sxs-lookup"><span data-stu-id="3d61b-124">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="3d61b-125">Retourneert informatie over een groep voor de netwerkbeveiligingsregel.</span><span class="sxs-lookup"><span data-stu-id="3d61b-125">Returns information about a network security group rule.</span></span> <span data-ttu-id="3d61b-126">In dit voorbeeld wordt Hallo regelnaam opgeslagen in een variabele voor gebruik verderop in het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="3d61b-126">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="3d61b-127">AZ netwerk nsg regel update</span><span class="sxs-lookup"><span data-stu-id="3d61b-127">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="3d61b-128">Een regel voor het NSG-updates.</span><span class="sxs-lookup"><span data-stu-id="3d61b-128">Updates an NSG rule.</span></span> <span data-ttu-id="3d61b-129">In dit voorbeeld is Hallo back-end regel bijgewerkte toopass verkeer alleen via Hallo front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="3d61b-129">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="3d61b-130">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="3d61b-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3d61b-131">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="3d61b-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d61b-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d61b-132">Next steps</span></span>

<span data-ttu-id="3d61b-133">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d61b-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3d61b-134">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d61b-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
