---
title: Interne load balancer overzicht | Microsoft Docs
description: Overzicht voor de interne load balancer en de bijbehorende functies. De werking van een load balancer voor Azure en mogelijke scenario's voor het configureren van interne eindpunten
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
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="743c3-103">Interne load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="743c3-103">Internal load balancer overview</span></span>

<span data-ttu-id="743c3-104">In tegenstelling tot het Internet gerichte load balancer, stuurt de interne load balancer (ILB) verkeer alleen bronnen in de cloudservice of via VPN voor toegang tot de Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="743c3-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="743c3-105">De infrastructuur de toegang beperkt tot de taakverdeling virtuele IP-adressen (VIP's) van een Cloudservice of een virtueel netwerk, zodat ze wordt nooit worden rechtstreeks blootgesteld aan een Internet-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="743c3-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="743c3-106">Dit kan interne line-of-business (LOB)-toepassingen voor uitvoeren in Azure en is toegankelijk vanuit de cloud of via lokale.</span><span class="sxs-lookup"><span data-stu-id="743c3-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="743c3-107">Waarom moet u mogelijk een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="743c3-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="743c3-108">Azure interne Load Balancing (ILB) zorgt voor taakverdeling tussen virtuele machines die zich in een cloudservice of een virtueel netwerk met een regionaal bereik bevinden.</span><span class="sxs-lookup"><span data-stu-id="743c3-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="743c3-109">Zie voor meer informatie over het gebruik en de configuratie van virtuele netwerken met een regionaal bereik [regionale virtuele netwerken](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in de Azure-blog.</span><span class="sxs-lookup"><span data-stu-id="743c3-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="743c3-110">Bestaande virtuele netwerken die zijn geconfigureerd voor een affiniteitsgroep kunnen ILB niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="743c3-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="743c3-111">ILB maakt gebruik van de volgende soorten taakverdeling:</span><span class="sxs-lookup"><span data-stu-id="743c3-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="743c3-112">Binnen een cloudservice van virtuele machines naar een set van virtuele machines die zich in dezelfde cloudservice bevinden (Zie afbeelding 1).</span><span class="sxs-lookup"><span data-stu-id="743c3-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="743c3-113">Binnen een virtueel netwerk van virtuele machines in het virtuele netwerk naar een set van virtuele machines die zich in dezelfde cloudservice van het virtuele bevinden netwerk (Zie afbeelding 2).</span><span class="sxs-lookup"><span data-stu-id="743c3-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="743c3-114">Voor een virtueel netwerk cross-premises van lokale computers naar een set van virtuele machines die zich in dezelfde cloudservice van het virtuele bevinden netwerk (Zie afbeelding 3).</span><span class="sxs-lookup"><span data-stu-id="743c3-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="743c3-115">Internetgerichte toepassingen met meerdere lagen waarin de back-end-lagen zijn niet verbonden met Internet, maar is taakverdeling voor verkeer van de internetgerichte tier.</span><span class="sxs-lookup"><span data-stu-id="743c3-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="743c3-116">Taakverdeling van LOB-toepassingen die zijn gehost in Azure, zonder dat extra load balancer-hardware of software.</span><span class="sxs-lookup"><span data-stu-id="743c3-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="743c3-117">Met inbegrip van lokale servers in de set van computers waarvan het verkeer is de belasting van taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="743c3-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="743c3-118">Internetgericht toepassingen met meerdere lagen</span><span class="sxs-lookup"><span data-stu-id="743c3-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="743c3-119">De weblaag internetgerichte eindpunten voor Internet-clients heeft en deel uitmaakt van een set met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="743c3-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="743c3-120">De load balancer wordt binnenkomende verkeer van de webserver en webclients voor TCP-poort 443 (HTTPS) met de webservers.</span><span class="sxs-lookup"><span data-stu-id="743c3-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="743c3-121">De database-servers zich achter een ILB-eindpunt waarvan de webservers voor de opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="743c3-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="743c3-122">Deze database-service met gelijke taakverdeling eindpunt, welk verkeer gelijkmatig verdeeld over de databaseservers in de set ILB wordt.</span><span class="sxs-lookup"><span data-stu-id="743c3-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="743c3-123">De volgende afbeelding toont de Internetgericht toepassing met meerdere lagen in dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="743c3-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![Interne load balancing één cloudservice](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="743c3-125">Afbeelding 1: Internetgericht toepassing met meerdere lagen</span><span class="sxs-lookup"><span data-stu-id="743c3-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="743c3-126">Ook gebruiken voor een toepassing met meerdere lagen is wanneer de ILB geïmplementeerd op een andere cloudservice dan het gebruiken van de service voor de ILB.</span><span class="sxs-lookup"><span data-stu-id="743c3-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="743c3-127">Cloudservices met hetzelfde virtuele netwerk hebben toegang tot de ILB-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="743c3-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="743c3-128">De volgende afbeelding toont de front-end web servers bevinden zich in een andere cloud-service van de back-end van de database en het gebruik van het ILB-eindpunt in hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="743c3-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![Interne taakverdeling tussen cloudservices](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="743c3-130">Afbeelding 2 - front-servers in een andere cloud-service</span><span class="sxs-lookup"><span data-stu-id="743c3-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="743c3-131">Intranet line-of-business-toepassingen</span><span class="sxs-lookup"><span data-stu-id="743c3-131">Intranet line of business applications</span></span>

<span data-ttu-id="743c3-132">Verkeer van clients op de on-premises netwerk ophalen taakverdeling op de set van LOB-servers met behulp van VPN-verbinding met Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="743c3-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="743c3-133">De clientcomputer hebben toegang tot een IP-adres van de Azure VPN-service gebruikt naar-site VPN.</span><span class="sxs-lookup"><span data-stu-id="743c3-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="743c3-134">Kunt u het gebruik LOB-toepassing die wordt gehost achter de ILB-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="743c3-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![Interne taakverdeling met behulp van de punt naar-site VPN](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="743c3-136">Afbeelding 3 - LOB-toepassingen die worden gehost achter de Load Balancer-eindpunt</span><span class="sxs-lookup"><span data-stu-id="743c3-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="743c3-137">Een ander scenario voor het LOB is om een site naar site VPN met het virtuele netwerk waarin de ILB-eindpunt is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="743c3-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="743c3-138">Hiermee worden lokale netwerkverkeer worden doorgestuurd naar de ILB-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="743c3-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![Interne taakverdeling met behulp van site naar site VPN](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="743c3-140">Afbeelding 4: On-premises netwerkverkeer doorgestuurd naar de ILB-eindpunt</span><span class="sxs-lookup"><span data-stu-id="743c3-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="743c3-141">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="743c3-141">Limitations</span></span>

<span data-ttu-id="743c3-142">Interne Load Balancer-configuraties ondersteunen geen snat omzetten.</span><span class="sxs-lookup"><span data-stu-id="743c3-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="743c3-143">In de context van dit document verwijst snat omzetten naar poort onechte bron netwerkadresomzetting.</span><span class="sxs-lookup"><span data-stu-id="743c3-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="743c3-144">Dit geldt voor scenario's waarbij een virtuele machine in een load balancer-groep nodig heeft om de respectieve interne Load Balancer frontend-IP-adres.</span><span class="sxs-lookup"><span data-stu-id="743c3-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="743c3-145">Dit scenario wordt niet ondersteund voor de interne Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="743c3-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="743c3-146">Verbindingsfouten uitgevoerd wanneer de stroom wordt verdeeld op de virtuele machine die afkomstig is van de stroom.</span><span class="sxs-lookup"><span data-stu-id="743c3-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="743c3-147">U moet een proxy stijl load balancer gebruiken voor dergelijke scenario's.</span><span class="sxs-lookup"><span data-stu-id="743c3-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="743c3-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="743c3-148">Next Steps</span></span>

[<span data-ttu-id="743c3-149">Ondersteuning voor Azure Load Balancer van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="743c3-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="743c3-150">De load balancer van een Internetgericht configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="743c3-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="743c3-151">Een interne load balancer configureren aan de slag</span><span class="sxs-lookup"><span data-stu-id="743c3-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="743c3-152">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="743c3-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="743c3-153">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="743c3-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
