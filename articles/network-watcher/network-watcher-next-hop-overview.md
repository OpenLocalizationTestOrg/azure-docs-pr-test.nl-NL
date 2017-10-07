---
title: aaaIntroduction toonext hop in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van netwerk-Watcher Hallo volgende hop-functionaliteit
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
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="1f63e-103">Inleiding toonext hop in Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="1f63e-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="1f63e-104">Verkeer van een virtuele machine wordt verzonden tooa bestemming op basis van Hallo effectieve routes die zijn gekoppeld aan een NIC.</span><span class="sxs-lookup"><span data-stu-id="1f63e-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="1f63e-105">Volgende hop opgehaald Hallo volgend hoptype en IP-adres van een pakket vanuit een specifieke virtuele machine en de NIC.</span><span class="sxs-lookup"><span data-stu-id="1f63e-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="1f63e-106">Dit helpt toodetermine als hello pakket gerichte toohello bestemming wordt of het Hallo-verkeer wordt zwarte gaan is.</span><span class="sxs-lookup"><span data-stu-id="1f63e-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="1f63e-107">Een onjuiste configuratie van routes door de gebruiker hello, waarbij een verkeer gerichte tooan on-premises locatie of een virtueel apparaat is, kan leiden tooconnectivity problemen.</span><span class="sxs-lookup"><span data-stu-id="1f63e-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="1f63e-108">Ook wordt de volgende hop Hallo routetabel die zijn gekoppeld aan de volgende hop Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f63e-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="1f63e-109">Tijdens het opvragen van een volgende hop als Hallo route is gedefinieerd als een gebruiker gedefinieerde route worden die route geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="1f63e-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="1f63e-110">Anders retourneert de volgende hop 'Systeemroute'.</span><span class="sxs-lookup"><span data-stu-id="1f63e-110">Otherwise Next hop returns "System Route".</span></span>

![overzicht van volgende hop][1]

<span data-ttu-id="1f63e-112">Hallo Hieronder volgt een lijst met het volgende hoptypen hello, die kunnen worden geretourneerd bij het opvragen van de volgende hop.</span><span class="sxs-lookup"><span data-stu-id="1f63e-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="1f63e-113">Internet</span><span class="sxs-lookup"><span data-stu-id="1f63e-113">Internet</span></span>
* <span data-ttu-id="1f63e-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="1f63e-114">VirtualAppliance</span></span>
* <span data-ttu-id="1f63e-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="1f63e-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="1f63e-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="1f63e-116">VnetLocal</span></span>
* <span data-ttu-id="1f63e-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="1f63e-117">HyperNetGateway</span></span>
* <span data-ttu-id="1f63e-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="1f63e-118">VnetPeering</span></span>
* <span data-ttu-id="1f63e-119">Geen</span><span class="sxs-lookup"><span data-stu-id="1f63e-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="1f63e-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f63e-120">Next steps</span></span>

<span data-ttu-id="1f63e-121">Meer informatie over hoe de volgende hop toofind toouse problemen met de netwerkverbinding in via [selectievakje Hallo volgende hop op een virtuele machine](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1f63e-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













