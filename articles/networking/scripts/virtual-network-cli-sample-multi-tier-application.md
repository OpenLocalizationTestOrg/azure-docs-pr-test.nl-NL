---
title: Azure CLI-script steekproef - maken van een netwerk voor toepassingen met meerdere lagen | Microsoft Docs
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
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="c67fc-103">Een netwerk voor toepassingen met meerdere lagen maken</span><span class="sxs-lookup"><span data-stu-id="c67fc-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="c67fc-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="c67fc-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c67fc-105">Het verkeer naar de front-end-subnet is beperkt tot HTTP- en SSH, terwijl het verkeer naar de back-end-subnet wordt beperkt tot MySQL, poort 3306.</span><span class="sxs-lookup"><span data-stu-id="c67fc-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="c67fc-106">Nadat het script is uitgevoerd, hebt u twee virtuele machines, één in elk subnet dat u kunt webserver en MySQL-software te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c67fc-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="c67fc-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="c67fc-107">Sample script</span></span>


<span data-ttu-id="c67fc-108">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "virtuele netwerk voor de toepassing met meerdere lagen")]</span><span class="sxs-lookup"><span data-stu-id="c67fc-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c67fc-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="c67fc-109">Clean up deployment</span></span> 

<span data-ttu-id="c67fc-110">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c67fc-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="c67fc-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="c67fc-111">Script explanation</span></span>

<span data-ttu-id="c67fc-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="c67fc-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="c67fc-113">Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="c67fc-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="c67fc-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c67fc-114">Command</span></span> | <span data-ttu-id="c67fc-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c67fc-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c67fc-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="c67fc-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="c67fc-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c67fc-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c67fc-118">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="c67fc-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="c67fc-119">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="c67fc-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="c67fc-120">AZ netwerksubnet maken</span><span class="sxs-lookup"><span data-stu-id="c67fc-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="c67fc-121">Maakt een back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="c67fc-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="c67fc-122">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="c67fc-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="c67fc-123">Hiermee maakt u een openbaar IP-adres voor toegang tot de virtuele machine via het Internet.</span><span class="sxs-lookup"><span data-stu-id="c67fc-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="c67fc-124">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="c67fc-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="c67fc-125">Virtuele netwerkinterfaces maakt en gekoppeld aan het virtuele netwerk front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="c67fc-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c67fc-126">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="c67fc-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="c67fc-127">Netwerk maakt beveiligingsgroepen (NSG) die gekoppeld aan de front-end en back-end subnetten zijn.</span><span class="sxs-lookup"><span data-stu-id="c67fc-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c67fc-128">AZ netwerk nsg regel maken</span><span class="sxs-lookup"><span data-stu-id="c67fc-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="c67fc-129">Maakt NSG-regels die bepaalde poorten tot specifieke subnetten blokkeren of toestaan.</span><span class="sxs-lookup"><span data-stu-id="c67fc-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="c67fc-130">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="c67fc-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="c67fc-131">Hiermee maakt u virtuele machines en een NIC koppelt aan elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c67fc-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="c67fc-132">Deze opdracht geeft ook aan de installatiekopie van de virtuele machine te gebruiken en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="c67fc-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="c67fc-133">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="c67fc-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="c67fc-134">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="c67fc-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c67fc-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c67fc-135">Next steps</span></span>

<span data-ttu-id="c67fc-136">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c67fc-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="c67fc-137">Aanvullende netwerken CLI scriptvoorbeelden vindt u in de [overzicht netwerken van Azure-documentatie](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="c67fc-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>