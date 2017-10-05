---
title: 'Azure CLI-Script voorbeeld: twee virtuele machines maken met een interne en externe NSG | Microsoft Docs'
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
ms.openlocfilehash: 7bd8c315ab0b7b3bcbbd9ebc8f17728079611f9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="ffb1e-103">Beveiligen van netwerkverkeer tussen virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ffb1e-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="ffb1e-104">Dit script maakt twee virtuele machines en binnenkomend verkeer op beide beveiligt.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-104">This script creates two virtual machines and secures incoming traffic to both.</span></span> <span data-ttu-id="ffb1e-105">Een virtuele machine op het internet toegankelijk is en is een netwerkbeveiligingsgroep (NSG) is geconfigureerd voor verkeer op poort 22 en 80.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 22 and port 80.</span></span> <span data-ttu-id="ffb1e-106">De tweede virtuele machine is niet toegankelijk op het internet en is een NSG is geconfigureerd om alleen het verkeer van de eerste virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ffb1e-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="ffb1e-107">Sample script</span></span>

<span data-ttu-id="ffb1e-108">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "VM maken met NSG")]</span><span class="sxs-lookup"><span data-stu-id="ffb1e-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ffb1e-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="ffb1e-109">Clean up deployment</span></span> 

<span data-ttu-id="ffb1e-110">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ffb1e-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="ffb1e-111">Script explanation</span></span>

<span data-ttu-id="ffb1e-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="ffb1e-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ffb1e-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="ffb1e-114">Command</span></span> | <span data-ttu-id="ffb1e-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="ffb1e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ffb1e-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="ffb1e-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ffb1e-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ffb1e-118">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="ffb1e-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="ffb1e-119">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="ffb1e-120">AZ network vnet subnet maken</span><span class="sxs-lookup"><span data-stu-id="ffb1e-120">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="ffb1e-121">Maakt een subnet.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-121">Creates a subnet.</span></span> |
| [<span data-ttu-id="ffb1e-122">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="ffb1e-122">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ffb1e-123">De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-123">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="ffb1e-124">Met deze opdracht geeft ook de afbeelding van de virtuele machine moet worden gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-124">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="ffb1e-125">lijst van de regel met het nsg van netwerken AZ</span><span class="sxs-lookup"><span data-stu-id="ffb1e-125">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="ffb1e-126">Retourneert informatie over een groep voor de netwerkbeveiligingsregel.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-126">Returns information about a network security group rule.</span></span> <span data-ttu-id="ffb1e-127">In dit voorbeeld wordt de naam van de opgeslagen in een variabele voor gebruik verderop in het script.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-127">In this sample, the rule name is stored in a variable for use later in the script.</span></span> |
| [<span data-ttu-id="ffb1e-128">AZ netwerk nsg regel update</span><span class="sxs-lookup"><span data-stu-id="ffb1e-128">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="ffb1e-129">Een regel voor het NSG-updates.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-129">Updates an NSG rule.</span></span> <span data-ttu-id="ffb1e-130">In dit voorbeeld wordt wordt de back-end-regel bijgewerkt verkeer doorlaten alleen via het front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-130">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span></span> |
| [<span data-ttu-id="ffb1e-131">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="ffb1e-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ffb1e-132">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="ffb1e-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ffb1e-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ffb1e-133">Next steps</span></span>

<span data-ttu-id="ffb1e-134">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ffb1e-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ffb1e-135">Extra virtuele machine CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ffb1e-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
