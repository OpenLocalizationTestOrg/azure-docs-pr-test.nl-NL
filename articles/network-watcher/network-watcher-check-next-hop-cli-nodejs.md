---
title: de volgende hop aaaFind met Azure-netwerk-Watcher volgende Hop - Azure CLI 1.0 | Microsoft Docs
description: In dit artikel wordt beschreven hoe u welke Hallo type voor het volgende hop is en het gebruik van IP-adres van volgende Hop met Azure CLI kunt vinden.
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
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="6223e-103">Ontdek welke Hallo volgend hoptype Hallo volgende Hop mogelijkheid gebruikt in Azure met Azure CLI 1.0 netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="6223e-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6223e-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6223e-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="6223e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6223e-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="6223e-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6223e-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="6223e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6223e-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="6223e-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="6223e-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="6223e-109">De volgende hop is een functie van netwerk-Watcher die de mogelijkheid Hallo biedt Hallo volgend hoptype en IP-adres op basis van een opgegeven virtuele machine ophalen.</span><span class="sxs-lookup"><span data-stu-id="6223e-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="6223e-110">Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken tooget tooits bestemming passeert.</span><span class="sxs-lookup"><span data-stu-id="6223e-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="6223e-111">Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="6223e-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6223e-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="6223e-112">Before you begin</span></span>

<span data-ttu-id="6223e-113">In dit scenario gebruikt u Azure CLI toofind Hallo volgend hoptype hello en IP-adres.</span><span class="sxs-lookup"><span data-stu-id="6223e-113">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="6223e-114">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="6223e-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="6223e-115">Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.</span><span class="sxs-lookup"><span data-stu-id="6223e-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="6223e-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="6223e-116">Scenario</span></span>

<span data-ttu-id="6223e-117">Hallo scenario beschreven in dit artikel maakt gebruik van volgende Hop, een functie van netwerk-Watcher waarmee wordt gezocht naar het volgende hoptype hello en IP-adres voor een resource.</span><span class="sxs-lookup"><span data-stu-id="6223e-117">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="6223e-118">toolearn meer informatie over het volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6223e-118">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="6223e-119">Ophalen van de volgende Hop</span><span class="sxs-lookup"><span data-stu-id="6223e-119">Get Next Hop</span></span>

<span data-ttu-id="6223e-120">tooget hello volgende hop noemen we Hallo `azure netowrk watcher next-hop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6223e-120">tooget hello next hop we call hello `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="6223e-121">We geven Hallo cmdlet Hallo netwerk-Watcher-resourcegroep, Hallo NetworkWatcher virtuele machine Id, IP-bronadres en IP-doeladres.</span><span class="sxs-lookup"><span data-stu-id="6223e-121">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="6223e-122">In dit voorbeeld is de IP-doeladres Hallo tooa VM in een ander virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="6223e-122">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="6223e-123">Er is een virtuele netwerkgateway tussen Hallo twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="6223e-123">There is a virtual network gateway between hello two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="6223e-124">Als Hallo VM meerdere NIC's en doorsturen via IP is ingeschakeld op Hallo NIC's, klikt u vervolgens Hallo NIC-parameter (-ik nic-id) moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6223e-124">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="6223e-125">Anders is optioneel.</span><span class="sxs-lookup"><span data-stu-id="6223e-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="6223e-126">Resultaten bekijken</span><span class="sxs-lookup"><span data-stu-id="6223e-126">Review results</span></span>

<span data-ttu-id="6223e-127">Als u klaar worden Hallo resultaten geleverd.</span><span class="sxs-lookup"><span data-stu-id="6223e-127">When complete, hello results are provided.</span></span> <span data-ttu-id="6223e-128">Hallo volgende hop IP-adres wordt geretourneerd en Hallo type resource is.</span><span class="sxs-lookup"><span data-stu-id="6223e-128">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="6223e-129">Hallo bevat volgende lijst de momenteel beschikbare NextHopType waarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="6223e-129">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="6223e-130">**Volgend Hoptype**</span><span class="sxs-lookup"><span data-stu-id="6223e-130">**Next Hop Type**</span></span>

* <span data-ttu-id="6223e-131">Internet</span><span class="sxs-lookup"><span data-stu-id="6223e-131">Internet</span></span>
* <span data-ttu-id="6223e-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="6223e-132">VirtualAppliance</span></span>
* <span data-ttu-id="6223e-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="6223e-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="6223e-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="6223e-134">VnetLocal</span></span>
* <span data-ttu-id="6223e-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="6223e-135">HyperNetGateway</span></span>
* <span data-ttu-id="6223e-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="6223e-136">VnetPeering</span></span>
* <span data-ttu-id="6223e-137">Geen</span><span class="sxs-lookup"><span data-stu-id="6223e-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="6223e-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6223e-138">Next steps</span></span>

<span data-ttu-id="6223e-139">Meer informatie over hoe tooreview uw netwerk groep beveiligingsinstellingen programmatisch in via [NSG controleren met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="6223e-139">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
