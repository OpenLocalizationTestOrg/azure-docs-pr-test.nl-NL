---
title: Inleiding tot de volgende hop in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van de netwerk-Watcher volgende hop-functionaliteit
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="6c317-103">Inleiding tot de volgende hop in Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="6c317-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="6c317-104">Verkeer van een virtuele machine wordt verzonden naar een bestemming op basis van de effectieve routes die zijn gekoppeld aan een NIC.</span><span class="sxs-lookup"><span data-stu-id="6c317-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="6c317-105">Volgende hop opgehaald uit het volgende hoptype en IP-adres van een pakket vanuit een specifieke virtuele machine en de NIC.</span><span class="sxs-lookup"><span data-stu-id="6c317-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="6c317-106">Dit helpt te bepalen of het pakket wordt omgeleid naar de bestemming of is het verkeer wordt zwarte gaan.</span><span class="sxs-lookup"><span data-stu-id="6c317-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="6c317-107">Een onjuiste configuratie van routes door de gebruiker, waarbij een verkeer wordt omgeleid naar een on-premises locatie of een virtueel apparaat, kan leiden tot problemen met de netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="6c317-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="6c317-108">Volgende hop retourneert ook de routetabel die zijn gekoppeld aan de volgende hop.</span><span class="sxs-lookup"><span data-stu-id="6c317-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="6c317-109">Tijdens het opvragen van een volgende hop als de route is gedefinieerd als een gebruiker gedefinieerde route worden die route geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="6c317-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="6c317-110">Anders retourneert de volgende hop 'Systeemroute'.</span><span class="sxs-lookup"><span data-stu-id="6c317-110">Otherwise Next hop returns "System Route".</span></span>

![overzicht van volgende hop][1]

<span data-ttu-id="6c317-112">Hier volgt een lijst van de volgende hoptypen die kunnen worden geretourneerd bij het opvragen van de volgende hop.</span><span class="sxs-lookup"><span data-stu-id="6c317-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="6c317-113">Internet</span><span class="sxs-lookup"><span data-stu-id="6c317-113">Internet</span></span>
* <span data-ttu-id="6c317-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="6c317-114">VirtualAppliance</span></span>
* <span data-ttu-id="6c317-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="6c317-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="6c317-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="6c317-116">VnetLocal</span></span>
* <span data-ttu-id="6c317-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="6c317-117">HyperNetGateway</span></span>
* <span data-ttu-id="6c317-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="6c317-118">VnetPeering</span></span>
* <span data-ttu-id="6c317-119">Geen</span><span class="sxs-lookup"><span data-stu-id="6c317-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="6c317-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c317-120">Next steps</span></span>

<span data-ttu-id="6c317-121">Informatie over het gebruik van volgende hop vinden van problemen met de netwerkverbinding in via [controleren van de volgende hop op een virtuele machine](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6c317-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













