---
title: Azure CLI-voorbeeldscript - Filter VM-netwerkverkeer | Microsoft Docs
description: Azure CLI-script steekproef - binnenkomend en uitgaand netwerkverkeer voor VM filteren.
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="24d66-103">Filteren van binnenkomende en uitgaande netwerkverkeer voor VM</span><span class="sxs-lookup"><span data-stu-id="24d66-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="24d66-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="24d66-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="24d66-105">Binnenkomend netwerkverkeer naar de front-end-subnet is beperkt tot HTTP, HTTPS en SSH, terwijl uitgaand verkeer naar Internet van de back-end-subnet is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="24d66-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="24d66-106">Nadat het script is uitgevoerd, hebt u één virtuele machine met twee NIC's.</span><span class="sxs-lookup"><span data-stu-id="24d66-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="24d66-107">Elke NIC is verbonden met een ander subnet.</span><span class="sxs-lookup"><span data-stu-id="24d66-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="24d66-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="24d66-108">Sample script</span></span>


<span data-ttu-id="24d66-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM-netwerkverkeer")]</span><span class="sxs-lookup"><span data-stu-id="24d66-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="24d66-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="24d66-110">Clean up deployment</span></span> 

<span data-ttu-id="24d66-111">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="24d66-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="24d66-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="24d66-112">Script explanation</span></span>

<span data-ttu-id="24d66-113">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="24d66-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="24d66-114">Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="24d66-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="24d66-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="24d66-115">Command</span></span> | <span data-ttu-id="24d66-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="24d66-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="24d66-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="24d66-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="24d66-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="24d66-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="24d66-119">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="24d66-119">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="24d66-120">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="24d66-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="24d66-121">AZ netwerksubnet maken</span><span class="sxs-lookup"><span data-stu-id="24d66-121">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="24d66-122">Maakt een back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="24d66-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="24d66-123">AZ network vnet subnet bijwerken</span><span class="sxs-lookup"><span data-stu-id="24d66-123">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="24d66-124">Nsg's koppelt aan subnetten.</span><span class="sxs-lookup"><span data-stu-id="24d66-124">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="24d66-125">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="24d66-125">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="24d66-126">Hiermee maakt u een openbaar IP-adres voor toegang tot de virtuele machine via het Internet.</span><span class="sxs-lookup"><span data-stu-id="24d66-126">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="24d66-127">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="24d66-127">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="24d66-128">Virtuele netwerkinterfaces maakt en gekoppeld aan het virtuele netwerk front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="24d66-128">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="24d66-129">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="24d66-129">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="24d66-130">Netwerk maakt beveiligingsgroepen (NSG) die gekoppeld aan de front-end en back-end subnetten zijn.</span><span class="sxs-lookup"><span data-stu-id="24d66-130">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="24d66-131">AZ netwerk nsg regel maken</span><span class="sxs-lookup"><span data-stu-id="24d66-131">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="24d66-132">Maakt NSG-regels die bepaalde poorten tot specifieke subnetten blokkeren of toestaan.</span><span class="sxs-lookup"><span data-stu-id="24d66-132">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="24d66-133">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="24d66-133">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="24d66-134">Hiermee maakt u virtuele machines en een NIC koppelt aan elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="24d66-134">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="24d66-135">Deze opdracht geeft ook aan de installatiekopie van de virtuele machine te gebruiken en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="24d66-135">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="24d66-136">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="24d66-136">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="24d66-137">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="24d66-137">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="24d66-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24d66-138">Next steps</span></span>

<span data-ttu-id="24d66-139">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="24d66-139">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="24d66-140">Aanvullende netwerken CLI scriptvoorbeelden vindt u in de [overzicht netwerken van Azure-documentatie](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="24d66-140">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>