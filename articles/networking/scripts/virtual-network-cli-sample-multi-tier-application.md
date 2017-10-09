---
title: aaaAzure CLI script steekproef - maken van een netwerk voor toepassingen met meerdere lagen | Microsoft Docs
description: 'Azure CLI-script voorbeeld: een virtueel netwerk voor toepassingen met meerdere lagen maken.'
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="c1628-103">Een netwerk voor toepassingen met meerdere lagen maken</span><span class="sxs-lookup"><span data-stu-id="c1628-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="c1628-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="c1628-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c1628-105">Verkeer toohello front-end-subnet is beperkt tooHTTP en SSH, tijdens het verkeer toohello back-end-subnet is beperkt tooMySQL, poort 3306.</span><span class="sxs-lookup"><span data-stu-id="c1628-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="c1628-106">Na het Hallo-script wordt uitgevoerd hebt u twee virtuele machines, één in elk subnet dat u kunt webserver en MySQL-software te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c1628-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="c1628-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="c1628-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c1628-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="c1628-108">Clean up deployment</span></span> 

<span data-ttu-id="c1628-109">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1628-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="c1628-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="c1628-110">Script explanation</span></span>

<span data-ttu-id="c1628-111">Dit script maakt gebruik van Hallo opdrachten toocreate na een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="c1628-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="c1628-112">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="c1628-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="c1628-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c1628-113">Command</span></span> | <span data-ttu-id="c1628-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c1628-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c1628-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="c1628-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="c1628-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c1628-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c1628-117">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="c1628-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="c1628-118">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="c1628-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="c1628-119">AZ netwerksubnet maken</span><span class="sxs-lookup"><span data-stu-id="c1628-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="c1628-120">Maakt een back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="c1628-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="c1628-121">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="c1628-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="c1628-122">Maakt een openbare IP-adres tooaccess-Hallo VM van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="c1628-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="c1628-123">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="c1628-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="c1628-124">Virtuele netwerkinterfaces maakt en koppelt deze toohello van het virtuele netwerk front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="c1628-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c1628-125">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="c1628-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="c1628-126">Netwerkbeveiligingsgroepen (NSG) die gekoppeld toohello front-end en back-end subnetten zijn maakt.</span><span class="sxs-lookup"><span data-stu-id="c1628-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c1628-127">AZ netwerk nsg regel maken</span><span class="sxs-lookup"><span data-stu-id="c1628-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="c1628-128">NSG-regels toestaan of blokkeren van bepaalde poorten toospecific subnetten maakt.</span><span class="sxs-lookup"><span data-stu-id="c1628-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="c1628-129">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="c1628-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="c1628-130">Virtuele machines maakt en koppelt een NIC tooeach VM.</span><span class="sxs-lookup"><span data-stu-id="c1628-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="c1628-131">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toouse en beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="c1628-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="c1628-132">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="c1628-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="c1628-133">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="c1628-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1628-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1628-134">Next steps</span></span>

<span data-ttu-id="c1628-135">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c1628-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="c1628-136">Aanvullende netwerken CLI scriptvoorbeelden kunnen u vinden in Hallo [overzicht netwerken van Azure-documentatie](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="c1628-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
