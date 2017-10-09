---
title: de volgende hop aaaFind met Azure-netwerk-Watcher volgende Hop - Azure-portal | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt zoeken welke Hallo type voor het volgende hop is en het IP-adres met behulp van volgende Hop hello Azure-portal
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
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="862cc-103">Ontdek welke Hallo volgend hoptype Hallo volgende Hop mogelijkheid gebruikt in Azure met behulp van de portal Hallo netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="862cc-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="862cc-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="862cc-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="862cc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="862cc-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="862cc-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="862cc-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="862cc-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="862cc-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="862cc-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="862cc-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="862cc-109">De volgende hop is een functie van netwerk-Watcher die de mogelijkheid Hallo biedt Hallo volgend hoptype en IP-adres op basis van een opgegeven virtuele machine ophalen.</span><span class="sxs-lookup"><span data-stu-id="862cc-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="862cc-110">Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken tooget tooits bestemming passeert.</span><span class="sxs-lookup"><span data-stu-id="862cc-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="862cc-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="862cc-111">Before you begin</span></span>

<span data-ttu-id="862cc-112">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="862cc-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="862cc-113">Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.</span><span class="sxs-lookup"><span data-stu-id="862cc-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="862cc-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="862cc-114">Scenario</span></span>

<span data-ttu-id="862cc-115">Hallo scenario beschreven in dit artikel maakt gebruik van volgende hop toofind uit het volgende hoptype hello en IP-adres voor een resource.</span><span class="sxs-lookup"><span data-stu-id="862cc-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="862cc-116">toolearn meer informatie over het volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="862cc-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="862cc-117">U wordt in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="862cc-117">In this scenario, you will:</span></span>

* <span data-ttu-id="862cc-118">De volgende hop Hallo ophalen van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="862cc-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="862cc-119">Ophalen van de volgende Hop</span><span class="sxs-lookup"><span data-stu-id="862cc-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="862cc-120">Stap 1</span><span class="sxs-lookup"><span data-stu-id="862cc-120">Step 1</span></span>

<span data-ttu-id="862cc-121">Navigeer tooyour netwerk-Watcher-bron in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="862cc-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="862cc-122">Stap 2</span><span class="sxs-lookup"><span data-stu-id="862cc-122">Step 2</span></span>

<span data-ttu-id="862cc-123">Klik op **volgende hop** invullen in het navigatiedeelvenster Hallo, selecteer Hallo virtuele machine en netwerkinterface, de Hallo bron en doel-IP en klikt u op Hallo **volgende hop** knop.</span><span class="sxs-lookup"><span data-stu-id="862cc-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="862cc-124">Volgende hop is vereist dat de VM-resource Hallo toorun wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="862cc-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![volgende hop-overzicht][1]

### <a name="step-3"></a><span data-ttu-id="862cc-126">Stap 3</span><span class="sxs-lookup"><span data-stu-id="862cc-126">Step 3</span></span>

<span data-ttu-id="862cc-127">Zodra het Hallo-taak is voltooid, worden Hallo resultaten verstrekt.</span><span class="sxs-lookup"><span data-stu-id="862cc-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="862cc-128">Hallo IP-adres en het type apparaat Hallo volgende hop is, wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="862cc-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="862cc-129">Hallo volgende tabel toont Hallo beschikbare geretourneerde waarden in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="862cc-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="862cc-130">**Volgend Hoptype**</span><span class="sxs-lookup"><span data-stu-id="862cc-130">**Next Hop Type**</span></span>

* <span data-ttu-id="862cc-131">Internet</span><span class="sxs-lookup"><span data-stu-id="862cc-131">Internet</span></span>
* <span data-ttu-id="862cc-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="862cc-132">VirtualAppliance</span></span>
* <span data-ttu-id="862cc-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="862cc-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="862cc-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="862cc-134">VnetLocal</span></span>
* <span data-ttu-id="862cc-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="862cc-135">HyperNetGateway</span></span>
* <span data-ttu-id="862cc-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="862cc-136">VnetPeering</span></span>
* <span data-ttu-id="862cc-137">Geen</span><span class="sxs-lookup"><span data-stu-id="862cc-137">None</span></span>

<span data-ttu-id="862cc-138">Als een aangepaste route gebruikte tooroute is wordt dit verkeer, Hallo gebruiker opgegeven routes (UDR) ook met Hallo resultaten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="862cc-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![ophalen van de volgende hop-resultaten][2]

## <a name="next-steps"></a><span data-ttu-id="862cc-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="862cc-140">Next steps</span></span>

<span data-ttu-id="862cc-141">Meer informatie over hoe tooreview uw netwerk groep beveiligingsinstellingen programmatisch in via [NSG controleren met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="862cc-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














