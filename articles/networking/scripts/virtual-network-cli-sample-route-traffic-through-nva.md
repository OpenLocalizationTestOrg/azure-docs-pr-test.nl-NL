---
title: Azure CLI-voorbeeldscript - routeverkeer via een virtueel netwerkapparaat | Microsoft Docs
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
ms.openlocfilehash: 78091b515c00591a4af8d807945475b6be50188a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="b84b0-103">-Routeverkeer via een virtueel netwerkapparaat</span><span class="sxs-lookup"><span data-stu-id="b84b0-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="b84b0-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="b84b0-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="b84b0-105">Een virtuele machine wordt gemaakt met doorsturen via IP is ingeschakeld voor het routeren van netwerkverkeer tussen de twee subnetten.</span><span class="sxs-lookup"><span data-stu-id="b84b0-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="b84b0-106">U kunt na het uitvoeren van het script netwerksoftware, zoals een firewalltoepassing naar de virtuele machine implementeren.</span><span class="sxs-lookup"><span data-stu-id="b84b0-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="b84b0-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="b84b0-107">Sample script</span></span>


<span data-ttu-id="b84b0-108">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "verkeer routeren via een virtueel netwerkapparaat")]</span><span class="sxs-lookup"><span data-stu-id="b84b0-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b84b0-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="b84b0-109">Clean up deployment</span></span> 

<span data-ttu-id="b84b0-110">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b84b0-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="b84b0-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="b84b0-111">Script explanation</span></span>

<span data-ttu-id="b84b0-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="b84b0-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="b84b0-113">Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="b84b0-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="b84b0-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="b84b0-114">Command</span></span> | <span data-ttu-id="b84b0-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b84b0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b84b0-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="b84b0-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b84b0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b84b0-118">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="b84b0-119">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="b84b0-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="b84b0-120">AZ netwerksubnet maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="b84b0-121">Maakt back-end en DMZ subnetten.</span><span class="sxs-lookup"><span data-stu-id="b84b0-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="b84b0-122">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="b84b0-123">Hiermee maakt u een openbaar IP-adres voor toegang tot de virtuele machine via het Internet.</span><span class="sxs-lookup"><span data-stu-id="b84b0-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="b84b0-124">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="b84b0-125">Maakt een virtuele netwerkinterface en doorsturen via IP inschakelen voor deze.</span><span class="sxs-lookup"><span data-stu-id="b84b0-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="b84b0-126">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="b84b0-127">Maakt een netwerkbeveiligingsgroep (NSG).</span><span class="sxs-lookup"><span data-stu-id="b84b0-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="b84b0-128">AZ netwerk nsg regel maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="b84b0-129">NSG-regels waarmee HTTP en HTTPS-poorten inkomend naar de virtuele machine maakt.</span><span class="sxs-lookup"><span data-stu-id="b84b0-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="b84b0-130">AZ network vnet subnet bijwerken</span><span class="sxs-lookup"><span data-stu-id="b84b0-130">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="b84b0-131">Koppelt de nsg's en routetabellen aan subnetten.</span><span class="sxs-lookup"><span data-stu-id="b84b0-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="b84b0-132">AZ netwerk routetabel maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-132">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="b84b0-133">Een routetabel voor alle routes maken.</span><span class="sxs-lookup"><span data-stu-id="b84b0-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="b84b0-134">netwerkroute AZ-routetabel maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-134">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="b84b0-135">Routes naar verkeer leiden tussen subnetten en het Internet via de virtuele machine maakt.</span><span class="sxs-lookup"><span data-stu-id="b84b0-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="b84b0-136">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="b84b0-136">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="b84b0-137">Hiermee maakt u een virtuele machine en de NIC koppelt aan het.</span><span class="sxs-lookup"><span data-stu-id="b84b0-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="b84b0-138">Deze opdracht geeft ook aan de installatiekopie van de virtuele machine te gebruiken en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="b84b0-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="b84b0-139">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="b84b0-139">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="b84b0-140">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="b84b0-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b84b0-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b84b0-141">Next steps</span></span>

<span data-ttu-id="b84b0-142">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b84b0-142">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="b84b0-143">Aanvullende netwerken CLI scriptvoorbeelden vindt u in de [overzicht netwerken van Azure-documentatie](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="b84b0-143">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>