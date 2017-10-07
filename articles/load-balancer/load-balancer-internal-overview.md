---
title: aaaInternal load balancer overzicht | Microsoft Docs
description: Overzicht voor de interne load balancer en de bijbehorende functies. De werking van een load balancer voor Azure en mogelijke scenario's tooconfigure interne eindpunten
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="d2cd2-103">Interne load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="d2cd2-103">Internal load balancer overview</span></span>

<span data-ttu-id="d2cd2-104">In tegenstelling tot Hallo Internet gerichte load balancer Hallo interne load balancer (ILB) zorgt ervoor dat alleen tooresources verkeer binnen het Hallo-cloudservice of met behulp van VPN-tooaccess hello Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="d2cd2-105">Hallo infrastructuur beperkt toegang toohello taakverdeling virtuele IP-adressen (VIP's) van een Cloudservice of een virtueel netwerk, zodat ze kunnen niet rechtstreeks blootgesteld tooan Internet eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="d2cd2-106">Dit kan interne line-of-business (LOB)-toepassingen toorun in Azure en is toegankelijk vanuit binnen Hallo cloud of bronnen on-premises.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="d2cd2-107">Waarom moet u mogelijk een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="d2cd2-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="d2cd2-108">Azure interne Load Balancing (ILB) zorgt voor taakverdeling tussen virtuele machines die zich in een cloudservice of een virtueel netwerk met een regionaal bereik bevinden.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="d2cd2-109">Zie voor meer informatie over het Hallo-gebruik en de configuratie van virtuele netwerken met een regionaal bereik [regionale virtuele netwerken](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure-blog.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="d2cd2-110">Bestaande virtuele netwerken die zijn geconfigureerd voor een affiniteitsgroep kunnen ILB niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="d2cd2-111">ILB kunt Hallo typen taakverdeling te volgen:</span><span class="sxs-lookup"><span data-stu-id="d2cd2-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="d2cd2-112">Binnen een cloudservice van virtuele machines tooa set van virtuele machines die zich binnen een Hallo dezelfde cloudservice (Zie afbeelding 1).</span><span class="sxs-lookup"><span data-stu-id="d2cd2-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="d2cd2-113">Binnen een virtueel netwerk van virtuele machines in Hallo virtueel netwerk tooa set virtuele machines die zich binnen een Hallo dezelfde cloudservice Hallo virtuele netwerk (Zie afbeelding 2).</span><span class="sxs-lookup"><span data-stu-id="d2cd2-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="d2cd2-114">Voor een virtueel netwerk cross-premises van lokale computers tooa set van virtuele machines die zich binnen een Hallo dezelfde cloudservice Hallo virtuele netwerk (Zie afbeelding 3).</span><span class="sxs-lookup"><span data-stu-id="d2cd2-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="d2cd2-115">Internetgerichte toepassingen met meerdere lagen waarin Hallo back-end lagen zijn niet verbonden met Internet, maar is taakverdeling voor verkeer van Hallo internetgerichte tier.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="d2cd2-116">Taakverdeling van LOB-toepassingen die zijn gehost in Azure, zonder dat extra load balancer-hardware of software.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="d2cd2-117">Met inbegrip van lokale servers in Hallo set computers waarvan het verkeer is de belasting van taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="d2cd2-118">Internetgericht toepassingen met meerdere lagen</span><span class="sxs-lookup"><span data-stu-id="d2cd2-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="d2cd2-119">Hallo weblaag internetgerichte eindpunten voor Internet-clients heeft en deel uitmaakt van een set met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="d2cd2-120">Hallo-taakverdeling inkomend verkeer van de webserver en webclients voor TCP-poort 443 (HTTPS) toohello webservers.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="d2cd2-121">Hallo databaseservers zich achter een ILB-eindpunt dat Hallo-webservers voor de opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="d2cd2-122">Deze database-service met gelijke taakverdeling eindpunt, welk verkeer gelijkmatig verdeeld zijn over Hallo databaseservers in Hallo ILB set is.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="d2cd2-123">Hallo volgende afbeelding toont Hallo Internetgericht toepassing met meerdere lagen binnen Hallo dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![Interne load balancing één cloudservice](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="d2cd2-125">Afbeelding 1: Internetgericht toepassing met meerdere lagen</span><span class="sxs-lookup"><span data-stu-id="d2cd2-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="d2cd2-126">Ook gebruiken voor een toepassing met meerdere lagen is wanneer Hallo ILB geïmplementeerd tooa andere cloudservice dan één consumerende Hallo-service voor Hallo ILB Hallo.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="d2cd2-127">Cloud services met behulp van Hallo hetzelfde virtuele netwerk hebben toegang tot toohello ILB-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="d2cd2-128">Hallo de volgende afbeelding ziet u front-endwebservers in een andere cloudservice vanuit Hallo database back-end zijn en het gebruik van Hallo ILB-eindpunt in Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![Interne taakverdeling tussen cloudservices](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="d2cd2-130">Afbeelding 2 - front-servers in een andere cloud-service</span><span class="sxs-lookup"><span data-stu-id="d2cd2-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="d2cd2-131">Intranet line-of-business-toepassingen</span><span class="sxs-lookup"><span data-stu-id="d2cd2-131">Intranet line of business applications</span></span>

<span data-ttu-id="d2cd2-132">Verkeer van clients op Hallo on-premises netwerk ophalen taakverdeling op Hallo set van LOB-servers met behulp van VPN-verbinding tooAzure netwerk.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="d2cd2-133">Hallo-clientcomputer heeft toegang tooan IP-adres uit Azure VPN-service via de VPN-punt toosite.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="d2cd2-134">Kunt u Hallo gebruik Hallo LOB-toepassing die wordt gehost achter Hallo ILB-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![Interne load balancing via punt toosite VPN](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="d2cd2-136">Afbeelding 3 - LOB-toepassingen die worden gehost achter Hallo LB-eindpunt</span><span class="sxs-lookup"><span data-stu-id="d2cd2-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="d2cd2-137">Een ander scenario voor Hallo LOB is toohave toosite VPN-toohello virtueel netwerk met een site waarop Hallo ILB-eindpunt is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="d2cd2-138">Hiermee worden lokale netwerkverkeer gerouteerd toobe toohello ILB-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![Interne taakverdeling met behulp van site toosite VPN](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="d2cd2-140">Afbeelding 4 - On-premises netwerkverkeer gerouteerd toohello ILB-eindpunt</span><span class="sxs-lookup"><span data-stu-id="d2cd2-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="d2cd2-141">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="d2cd2-141">Limitations</span></span>

<span data-ttu-id="d2cd2-142">Interne Load Balancer-configuraties ondersteunen geen snat omzetten.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="d2cd2-143">In de context van de Hallo van dit document verwijst snat omzetten tooport onechte bron netwerkadresomzetting.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="d2cd2-144">Dit geldt tooscenarios waarin een virtuele machine in een load balancer-pool tooreach Hallo respectieve interne Load Balancer frontend-IP-adres moet.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="d2cd2-145">Dit scenario wordt niet ondersteund voor de interne Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="d2cd2-146">Verbindingsfouten uitgevoerd wanneer het Hallo-stroom taakverdeling toohello VM Hallo stroom afkomstig is.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="d2cd2-147">U moet een proxy stijl load balancer gebruiken voor dergelijke scenario's.</span><span class="sxs-lookup"><span data-stu-id="d2cd2-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2cd2-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d2cd2-148">Next Steps</span></span>

[<span data-ttu-id="d2cd2-149">Ondersteuning voor Azure Load Balancer van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d2cd2-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="d2cd2-150">De load balancer van een Internetgericht configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="d2cd2-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="d2cd2-151">Een interne load balancer configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="d2cd2-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="d2cd2-152">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="d2cd2-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d2cd2-153">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="d2cd2-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
