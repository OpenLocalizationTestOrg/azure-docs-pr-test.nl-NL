---
title: aaaOverview van BGP met Azure VPN-Gateways | Microsoft Docs
description: Dit artikel bevat een overzicht van BGP met Azure VPN-gateways.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="49a64-103">Overzicht van BGP met Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="49a64-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="49a64-104">Dit artikel bevat een overzicht van BGP-ondersteuning (Border Gateway Protocol) in Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="49a64-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="49a64-105">BGP is Hallo standaardprotocol voor routering gebruikte in Hallo Internet tooexchange Routering en bereikbaarheid tussen twee of meer netwerken.</span><span class="sxs-lookup"><span data-stu-id="49a64-105">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="49a64-106">Wanneer gebruikt in de context Hallo van Azure Virtual Networks, maakt BGP hello Azure VPN-Gateways en uw on-premises VPN-apparaten, aangeroepen BGP-peers of neighbors, tooexchange 'routes' die wordt beide gateways informeren over Hallo beschikbaarheid en bereikbaarheid voor gebruikers voorvoegsels toogo via Hallo gateways of routers die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="49a64-106">When used in hello context of Azure Virtual Networks, BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="49a64-107">BGP ook transitroutering tussen meerdere netwerken door routes die een BGP-gateway van één BGP-peer-tooall leert andere BGP-peers.</span><span class="sxs-lookup"><span data-stu-id="49a64-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="49a64-108">Waarom BGP gebruiken?</span><span class="sxs-lookup"><span data-stu-id="49a64-108">Why use BGP?</span></span>
<span data-ttu-id="49a64-109">BGP is een optionele functie die u kunt gebruiken met op Azure-routes gebaseerde VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="49a64-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="49a64-110">Moet u zorgen dat uw on-premises VPN-apparaten BGP ondersteunen voordat u Hallo-functie inschakelen.</span><span class="sxs-lookup"><span data-stu-id="49a64-110">You should also make sure your on-premises VPN devices support BGP before you enable hello feature.</span></span> <span data-ttu-id="49a64-111">U kunt toouse Azure VPN-gateways en uw on-premises VPN-apparaten zonder BGP blijven.</span><span class="sxs-lookup"><span data-stu-id="49a64-111">You can continue toouse Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="49a64-112">Hallo equivalent van het gebruik van statische routes (zonder BGP) is *versus* gebruik van dynamische routering met BGP tussen uw netwerken en Azure.</span><span class="sxs-lookup"><span data-stu-id="49a64-112">It is hello equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="49a64-113">Het gebruik van BGP heeft een aantal voordelen en nieuwe mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="49a64-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="49a64-114">Ondersteuning van automatische en flexibele voorvoegselupdates</span><span class="sxs-lookup"><span data-stu-id="49a64-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="49a64-115">Met BGP hoeft u alleen toodeclare een minimaal voorvoegsel tooa specifieke BGP-peer via Hallo IPsec S2S VPN-tunnel.</span><span class="sxs-lookup"><span data-stu-id="49a64-115">With BGP, you only need toodeclare a minimum prefix tooa specific BGP peer over hello IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="49a64-116">Het kan ook zo klein is als een hostvoorvoegsel (/ 32) Hallo BGP-peer-IP-adres van uw on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="49a64-116">It can be as small as a host prefix (/32) of hello BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="49a64-117">U kunt bepalen welke on-premises netwerkvoorvoegsels u uw Azure Virtual Network-tooaccess tooadvertise tooAzure tooallow wilt.</span><span class="sxs-lookup"><span data-stu-id="49a64-117">You can control which on-premises network prefixes you want tooadvertise tooAzure tooallow your Azure Virtual Network tooaccess.</span></span>

<span data-ttu-id="49a64-118">U kunt ook grotere voorvoegsels met enkele van uw VNet-adresvoorvoegsels, zoals een grote privé IP-adresruimte (bijvoorbeeld 10.0.0.0/8) adverteren.</span><span class="sxs-lookup"><span data-stu-id="49a64-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="49a64-119">Houd er rekening mee dat Hallo voorvoegsels mogen niet identiek zijn met een van uw VNet-voorvoegsels.</span><span class="sxs-lookup"><span data-stu-id="49a64-119">Note though hello prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="49a64-120">Routes die identiek tooyour VNet-voorvoegsels wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="49a64-120">Those routes identical tooyour VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="49a64-121">Ondersteuning van meerdere tunnels tussen een VNet en een on-premises site met automatische failover op basis van BGP</span><span class="sxs-lookup"><span data-stu-id="49a64-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="49a64-122">U kunt meerdere verbindingen maken tussen uw Azure VNet en uw on-premises VPN-apparaten in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="49a64-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in hello same location.</span></span> <span data-ttu-id="49a64-123">Deze mogelijkheid biedt meerdere tunnels (paden) tussen de twee netwerken Hallo in een actief / actief-configuratie.</span><span class="sxs-lookup"><span data-stu-id="49a64-123">This capability provides multiple tunnels (paths) between hello two networks in an active-active configuration.</span></span> <span data-ttu-id="49a64-124">Als een van de Hallo tunnels wordt verbroken, Hallo bijbehorende routes ingetrokken via BGP en Hallo verkeer automatisch verplaatst toohello resterende tunnels.</span><span class="sxs-lookup"><span data-stu-id="49a64-124">If one of hello tunnels is disconnected, hello corresponding routes will be withdrawn via BGP and hello traffic automatically shifts toohello remaining tunnels.</span></span>

<span data-ttu-id="49a64-125">Hallo volgende diagram ziet u een eenvoudig voorbeeld van deze maximaal beschikbare installatie:</span><span class="sxs-lookup"><span data-stu-id="49a64-125">hello following diagram shows a simple example of this highly available setup:</span></span>

![Meerdere actieve paden](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="49a64-127">Ondersteuning van transitroutering tussen uw on-premises netwerken en meerdere Azure VNets</span><span class="sxs-lookup"><span data-stu-id="49a64-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="49a64-128">BGP kunnen meerdere gateways toolearn en voorvoegsels van verschillende netwerken propageren, ongeacht of ze direct of indirect verbonden bent.</span><span class="sxs-lookup"><span data-stu-id="49a64-128">BGP enables multiple gateways toolearn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="49a64-129">Op die manier is transitroutering met Azure VPN-gateways mogelijk tussen uw on-premises sites of tussen meerdere Azure Virtual Networks.</span><span class="sxs-lookup"><span data-stu-id="49a64-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="49a64-130">Hallo toont volgende diagram een voorbeeld van een Multihop-topologie met meerdere paden die verkeer tussen Hallo twee on-premises netwerken via Azure VPN-gateways binnen Hallo Microsoft Networks kan worden doorgevoerd:</span><span class="sxs-lookup"><span data-stu-id="49a64-130">hello following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between hello two on-premises networks through Azure VPN gateways within hello Microsoft Networks:</span></span>

![Multihop-transit](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="49a64-132">VEELGESTELDE VRAGEN OVER BGP</span><span class="sxs-lookup"><span data-stu-id="49a64-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="49a64-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49a64-133">Next steps</span></span>
<span data-ttu-id="49a64-134">Zie [aan de slag met BGP op Azure VPN-gateways](vpn-gateway-bgp-resource-manager-ps.md) voor stappen tooconfigure BGP voor uw cross-premises en VNet-naar-VNet-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="49a64-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps tooconfigure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

