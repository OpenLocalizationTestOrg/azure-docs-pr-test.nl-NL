---
title: aaaAzure CLI voorbeeldscript - routeverkeer via een virtueel netwerkapparaat | Microsoft Docs
description: 'Azure CLI - voorbeeldscript: de Route-verkeer via een firewall netwerk virtueel apparaat.'
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="7ac1a-103">-Routeverkeer via een virtueel netwerkapparaat</span><span class="sxs-lookup"><span data-stu-id="7ac1a-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="7ac1a-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="7ac1a-105">Een virtuele machine wordt gemaakt met ingeschakelde tooroute verkeer tussen de twee subnetten Hallo doorsturen via IP.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="7ac1a-106">U kunt na het uitvoeren van script Hallo netwerksoftware, zoals een firewalltoepassing toohello VM implementeren.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="7ac1a-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="7ac1a-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7ac1a-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="7ac1a-108">Clean up deployment</span></span> 

<span data-ttu-id="7ac1a-109">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="7ac1a-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="7ac1a-110">Script explanation</span></span>

<span data-ttu-id="7ac1a-111">Dit script maakt gebruik van Hallo opdrachten toocreate na een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="7ac1a-112">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="7ac1a-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="7ac1a-113">Command</span></span> | <span data-ttu-id="7ac1a-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7ac1a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7ac1a-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="7ac1a-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7ac1a-117">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="7ac1a-118">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="7ac1a-119">AZ netwerksubnet maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="7ac1a-120">Maakt back-end en DMZ subnetten.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="7ac1a-121">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="7ac1a-122">Maakt een openbare IP-adres tooaccess-Hallo VM van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="7ac1a-123">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="7ac1a-124">Maakt een virtuele netwerkinterface en doorsturen via IP inschakelen voor deze.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="7ac1a-125">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="7ac1a-126">Maakt een netwerkbeveiligingsgroep (NSG).</span><span class="sxs-lookup"><span data-stu-id="7ac1a-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="7ac1a-127">AZ netwerk nsg regel maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="7ac1a-128">NSG-regels waarmee HTTP en HTTPS-poorten inkomend toohello VM maakt.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-128">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="7ac1a-129">AZ network vnet subnet bijwerken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="7ac1a-130">Gekoppeld Hallo nsg's en route toosubnets tabellen.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-130">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="7ac1a-131">AZ netwerk routetabel maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-131">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="7ac1a-132">Een routetabel voor alle routes maken.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="7ac1a-133">netwerkroute AZ-routetabel maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="7ac1a-134">Routes maakt tooroute verkeer tussen subnetten en Hallo Internet via VM Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-134">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="7ac1a-135">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="7ac1a-135">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="7ac1a-136">Een virtuele machine maakt en koppelt Hallo NIC tooit.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-136">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="7ac1a-137">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toouse en beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-137">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="7ac1a-138">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="7ac1a-138">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="7ac1a-139">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="7ac1a-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7ac1a-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7ac1a-140">Next steps</span></span>

<span data-ttu-id="7ac1a-141">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ac1a-141">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="7ac1a-142">Aanvullende netwerken CLI scriptvoorbeelden kunnen u vinden in Hallo [overzicht netwerken van Azure-documentatie](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="7ac1a-142">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
