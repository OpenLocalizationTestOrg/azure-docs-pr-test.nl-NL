---
title: aaaAzure CLI voorbeeldscript - Filter VM-netwerkverkeer | Microsoft Docs
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="55d32-103">Filteren van binnenkomende en uitgaande netwerkverkeer voor VM</span><span class="sxs-lookup"><span data-stu-id="55d32-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="55d32-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="55d32-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="55d32-105">Binnenkomend netwerkverkeer toohello front-end-subnet is beperkt tooHTTP, HTTPS en SSH, terwijl het uitgaande verkeer toohello Internet van Hallo back-end-subnet is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="55d32-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="55d32-106">Na het uitvoeren van script hello, hebt u één virtuele machine met twee NIC's.</span><span class="sxs-lookup"><span data-stu-id="55d32-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="55d32-107">Elke NIC is verbonden tooa ander subnet.</span><span class="sxs-lookup"><span data-stu-id="55d32-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="55d32-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="55d32-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="55d32-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="55d32-109">Clean up deployment</span></span> 

<span data-ttu-id="55d32-110">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="55d32-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="55d32-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="55d32-111">Script explanation</span></span>

<span data-ttu-id="55d32-112">Dit script maakt gebruik van Hallo opdrachten toocreate na een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="55d32-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="55d32-113">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="55d32-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="55d32-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="55d32-114">Command</span></span> | <span data-ttu-id="55d32-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="55d32-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="55d32-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="55d32-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="55d32-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="55d32-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="55d32-118">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="55d32-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="55d32-119">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="55d32-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="55d32-120">AZ netwerksubnet maken</span><span class="sxs-lookup"><span data-stu-id="55d32-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="55d32-121">Maakt een back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="55d32-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="55d32-122">AZ network vnet subnet bijwerken</span><span class="sxs-lookup"><span data-stu-id="55d32-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="55d32-123">Nsg's toosubnets koppelt.</span><span class="sxs-lookup"><span data-stu-id="55d32-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="55d32-124">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="55d32-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="55d32-125">Maakt een openbare IP-adres tooaccess-Hallo VM van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="55d32-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="55d32-126">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="55d32-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="55d32-127">Virtuele netwerkinterfaces maakt en koppelt deze toohello van het virtuele netwerk front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="55d32-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="55d32-128">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="55d32-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="55d32-129">Netwerkbeveiligingsgroepen (NSG) die gekoppeld toohello front-end en back-end subnetten zijn maakt.</span><span class="sxs-lookup"><span data-stu-id="55d32-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="55d32-130">AZ netwerk nsg regel maken</span><span class="sxs-lookup"><span data-stu-id="55d32-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="55d32-131">NSG-regels toestaan of blokkeren van bepaalde poorten toospecific subnetten maakt.</span><span class="sxs-lookup"><span data-stu-id="55d32-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="55d32-132">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="55d32-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="55d32-133">Virtuele machines maakt en koppelt een NIC tooeach VM.</span><span class="sxs-lookup"><span data-stu-id="55d32-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="55d32-134">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toouse en beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="55d32-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="55d32-135">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="55d32-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="55d32-136">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="55d32-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="55d32-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55d32-137">Next steps</span></span>

<span data-ttu-id="55d32-138">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55d32-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="55d32-139">Aanvullende netwerken CLI scriptvoorbeelden kunnen u vinden in Hallo [overzicht netwerken van Azure-documentatie](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="55d32-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
