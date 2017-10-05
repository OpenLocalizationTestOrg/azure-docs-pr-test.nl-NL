---
title: Vinden van de volgende hop met Azure-netwerk-Watcher volgende Hop - Azure CLI 1.0 | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt vinden wat het volgende hoptype is en IP-adres met de volgende Hop met Azure CLI.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: ff88e945060ae033717ceb29db1352e112f05a3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="8d5d1-103">Uitzoeken wat het volgende hoptype gebruikt de mogelijkheid van de volgende Hop in Azure met Azure CLI 1.0 netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="8d5d1-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8d5d1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8d5d1-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="8d5d1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d5d1-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="8d5d1-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8d5d1-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="8d5d1-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8d5d1-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="8d5d1-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="8d5d1-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="8d5d1-109">De volgende hop is een functie van netwerk-Watcher die de mogelijkheid get biedt de volgende hoptype en IP-adres op basis van een opgegeven virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="8d5d1-110">Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken om te gaan naar de bestemming passeert.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="8d5d1-111">Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8d5d1-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="8d5d1-112">Before you begin</span></span>

<span data-ttu-id="8d5d1-113">In dit scenario gebruikt u de Azure CLI het volgende hoptype en IP-adres vinden.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-113">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="8d5d1-114">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="8d5d1-115">Het scenario wordt ervan uitgegaan dat er een resourcegroep met een geldige virtuele machine bestaat om te worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="8d5d1-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="8d5d1-116">Scenario</span></span>

<span data-ttu-id="8d5d1-117">Het scenario beschreven in dit artikel maakt gebruik van volgende Hop, een functie van netwerk-Watcher waarmee wordt gezocht naar de volgende hoptype en IP-adres voor een resource.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-117">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="8d5d1-118">Voor meer informatie over de volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8d5d1-118">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="8d5d1-119">Ophalen van de volgende Hop</span><span class="sxs-lookup"><span data-stu-id="8d5d1-119">Get Next Hop</span></span>

<span data-ttu-id="8d5d1-120">Ophalen van de volgende hop we noemen de `azure netowrk watcher next-hop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-120">To get the next hop we call the `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="8d5d1-121">De cmdlet geven we de resourcegroep voor netwerk-Watcher, de NetworkWatcher virtuele machine Id, IP-bronadres en IP-doeladres.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-121">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="8d5d1-122">In dit voorbeeld is het IP-doeladres voor een virtuele machine in een ander virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-122">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="8d5d1-123">Er is een virtuele netwerkgateway tussen de twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-123">There is a virtual network gateway between the two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="8d5d1-124">Als de virtuele machine meerdere NIC's heeft en doorsturen via IP is ingeschakeld op een van de NIC's en vervolgens de NIC-parameter (-ik nic-id) moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-124">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="8d5d1-125">Anders is optioneel.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="8d5d1-126">Resultaten bekijken</span><span class="sxs-lookup"><span data-stu-id="8d5d1-126">Review results</span></span>

<span data-ttu-id="8d5d1-127">Na voltooiing wordt worden de resultaten geleverd.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-127">When complete, the results are provided.</span></span> <span data-ttu-id="8d5d1-128">De volgende hop-IP-adres en het type resource dat is geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8d5d1-128">The next hop IP address is returned as well as the type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="8d5d1-129">De volgende lijst bevat de momenteel beschikbare NextHopType waarden:</span><span class="sxs-lookup"><span data-stu-id="8d5d1-129">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="8d5d1-130">**Volgend Hoptype**</span><span class="sxs-lookup"><span data-stu-id="8d5d1-130">**Next Hop Type**</span></span>

* <span data-ttu-id="8d5d1-131">Internet</span><span class="sxs-lookup"><span data-stu-id="8d5d1-131">Internet</span></span>
* <span data-ttu-id="8d5d1-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="8d5d1-132">VirtualAppliance</span></span>
* <span data-ttu-id="8d5d1-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="8d5d1-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="8d5d1-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="8d5d1-134">VnetLocal</span></span>
* <span data-ttu-id="8d5d1-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="8d5d1-135">HyperNetGateway</span></span>
* <span data-ttu-id="8d5d1-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="8d5d1-136">VnetPeering</span></span>
* <span data-ttu-id="8d5d1-137">Geen</span><span class="sxs-lookup"><span data-stu-id="8d5d1-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d5d1-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d5d1-138">Next steps</span></span>

<span data-ttu-id="8d5d1-139">Meer informatie over het bekijken van de groep beveiligingsinstellingen van uw netwerk via een programma te bezoeken [NSG controleren met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8d5d1-139">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
