---
title: Vinden van de volgende hop met Azure-netwerk-Watcher volgende Hop - Azure-portal | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt vinden wat het volgende hoptype is en IP-adres met de volgende Hop met de Azure portal
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5434b7972346821985c459fc4620805adb88676b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="4e987-103">Uitzoeken wat het volgende hoptype gebruikt de mogelijkheid van de volgende Hop in Azure met behulp van de portal netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="4e987-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4e987-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4e987-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="4e987-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e987-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="4e987-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4e987-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="4e987-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4e987-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="4e987-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="4e987-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="4e987-109">De volgende hop is een functie van netwerk-Watcher die de mogelijkheid get biedt de volgende hoptype en IP-adres op basis van een opgegeven virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4e987-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="4e987-110">Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken om te gaan naar de bestemming passeert.</span><span class="sxs-lookup"><span data-stu-id="4e987-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4e987-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="4e987-111">Before you begin</span></span>

<span data-ttu-id="4e987-112">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="4e987-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="4e987-113">Het scenario wordt ervan uitgegaan dat er een resourcegroep met een geldige virtuele machine bestaat om te worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4e987-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="4e987-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="4e987-114">Scenario</span></span>

<span data-ttu-id="4e987-115">Het scenario beschreven in dit artikel maakt gebruik van volgende hop voor informatie over het volgende hoptype en IP-adres voor een resource.</span><span class="sxs-lookup"><span data-stu-id="4e987-115">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="4e987-116">Voor meer informatie over de volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e987-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="4e987-117">U wordt in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="4e987-117">In this scenario, you will:</span></span>

* <span data-ttu-id="4e987-118">De volgende hop ophalen van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4e987-118">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="4e987-119">Ophalen van de volgende Hop</span><span class="sxs-lookup"><span data-stu-id="4e987-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="4e987-120">Stap 1</span><span class="sxs-lookup"><span data-stu-id="4e987-120">Step 1</span></span>

<span data-ttu-id="4e987-121">Navigeer naar uw netwerk-Watcher-resource in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4e987-121">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="4e987-122">Stap 2</span><span class="sxs-lookup"><span data-stu-id="4e987-122">Step 2</span></span>

<span data-ttu-id="4e987-123">Klik op **volgende hop** in het navigatiedeelvenster, selecteer de virtuele machine en de netwerkinterface, invullen van de bron en doel-IP en op de **volgende hop** knop.</span><span class="sxs-lookup"><span data-stu-id="4e987-123">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="4e987-124">Volgende hop is vereist dat de VM-resource wordt toegewezen om te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4e987-124">Next hop requires that the VM resource is allocated to run.</span></span>

![volgende hop-overzicht][1]

### <a name="step-3"></a><span data-ttu-id="4e987-126">Stap 3</span><span class="sxs-lookup"><span data-stu-id="4e987-126">Step 3</span></span>

<span data-ttu-id="4e987-127">Zodra de taak voltooid is, worden de resultaten worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="4e987-127">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="4e987-128">Het IP-adres en het type apparaat dat de volgende hop is, worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4e987-128">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="4e987-129">De volgende tabel bevat de beschikbare geretourneerde waarden in de portal.</span><span class="sxs-lookup"><span data-stu-id="4e987-129">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="4e987-130">**Volgend Hoptype**</span><span class="sxs-lookup"><span data-stu-id="4e987-130">**Next Hop Type**</span></span>

* <span data-ttu-id="4e987-131">Internet</span><span class="sxs-lookup"><span data-stu-id="4e987-131">Internet</span></span>
* <span data-ttu-id="4e987-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="4e987-132">VirtualAppliance</span></span>
* <span data-ttu-id="4e987-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="4e987-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="4e987-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="4e987-134">VnetLocal</span></span>
* <span data-ttu-id="4e987-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="4e987-135">HyperNetGateway</span></span>
* <span data-ttu-id="4e987-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="4e987-136">VnetPeering</span></span>
* <span data-ttu-id="4e987-137">Geen</span><span class="sxs-lookup"><span data-stu-id="4e987-137">None</span></span>

<span data-ttu-id="4e987-138">Als een aangepaste route is gebruikt voor dit verkeer routeren, wordt de gebruiker gedefinieerde route (UDR) ook met de resultaten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4e987-138">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![ophalen van de volgende hop-resultaten][2]

## <a name="next-steps"></a><span data-ttu-id="4e987-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4e987-140">Next steps</span></span>

<span data-ttu-id="4e987-141">Meer informatie over het bekijken van de groep beveiligingsinstellingen van uw netwerk via een programma te bezoeken [NSG controleren met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="4e987-141">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














