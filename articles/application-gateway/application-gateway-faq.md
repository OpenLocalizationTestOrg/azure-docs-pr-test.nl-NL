---
title: Veelgestelde vragen voor Azure Application Gateway aaaFrequently | Microsoft Docs
description: Deze pagina vindt u antwoorden op veelgestelde vragen over Azure Application Gateway toofrequently
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="6f15e-103">Veelgestelde vragen voor Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6f15e-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="6f15e-104">Algemeen</span><span class="sxs-lookup"><span data-stu-id="6f15e-104">General</span></span>

<span data-ttu-id="6f15e-105">**Q. Wat is Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="6f15e-106">Azure Application Gateway is een toepassing levering Controller (ADC) als een service biedt u verschillende laag 7 taakverdeling mogelijkheden voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6f15e-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="6f15e-107">Maximaal beschikbare en schaalbare service, die volledig worden beheerd door Azure biedt.</span><span class="sxs-lookup"><span data-stu-id="6f15e-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="6f15e-108">**Q. Welke functies biedt ondersteuning voor Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="6f15e-109">Toepassingsgateway ondersteunt SSL-offloading- en einddatum tooend SSL, Web Application Firewall, sessie cookies gebaseerde affiniteit, url op basis van het pad routering, hosting van multi-site en anderen.</span><span class="sxs-lookup"><span data-stu-id="6f15e-109">Application Gateway supports SSL offloading and end tooend SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="6f15e-110">Voor een volledige lijst van ondersteunde functies, gaat u naar [inleiding tooApplication Gateway](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6f15e-110">For a full list of supported features, visit [Introduction tooApplication Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="6f15e-111">**Q. Wat is Hallo verschil tussen een Application Gateway en Azure Load Balancer?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-111">**Q. What is hello difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="6f15e-112">Application Gateway is een load balancer van laag 7, wat betekent dat dit proces werkt met alleen webverkeer (HTTP/HTTPS/WebSocket).</span><span class="sxs-lookup"><span data-stu-id="6f15e-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="6f15e-113">Mogelijkheden, zoals SSL-beëindiging sessie cookies gebaseerde affiniteit en round-robin worden ondersteund voor load balancing-verkeer.</span><span class="sxs-lookup"><span data-stu-id="6f15e-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="6f15e-114">De Load Balancer, laadt het saldo's verkeer op laag 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="6f15e-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="6f15e-115">**Q. Welke protocollen biedt ondersteuning voor Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="6f15e-116">Application Gateway biedt ondersteuning voor HTTP, HTTPS en WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6f15e-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="6f15e-117">**Q. Welke bronnen worden nu ondersteund als onderdeel van de back-endpool?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="6f15e-118">Back-endpools kunnen bestaan uit NIC's, virtuele-machineschaalsets, openbare IP-adressen, de namen van interne IP-adressen, de volledig gekwalificeerde domeinnaam (FQDN) en back-ends van meerdere tenants zoals Azure Webapps.</span><span class="sxs-lookup"><span data-stu-id="6f15e-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="6f15e-119">Toepassingsgateway back-end-groepsleden niet zijn gekoppeld tooan beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="6f15e-119">Application Gateway backend pool members are not tied tooan availability set.</span></span> <span data-ttu-id="6f15e-120">Leden van de back-endpools mag tussen verschillende clusters, datacenters, of buiten Azure zolang ze beschikken over IP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="6f15e-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="6f15e-121">**Q. Welke regio's is het Hallo-service beschikbaar is in?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-121">**Q. What regions is hello service available in?**</span></span>

<span data-ttu-id="6f15e-122">Application Gateway is beschikbaar in alle regio's van globale Azure.</span><span class="sxs-lookup"><span data-stu-id="6f15e-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="6f15e-123">Het is ook beschikbaar in [Azure China](https://www.azure.cn/) en [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="6f15e-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="6f15e-124">**Q. Is dit een specifieke implementatie voor mijn abonnement of is het voor klanten is gedeeld?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="6f15e-125">Application Gateway is een specifieke implementatie in uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="6f15e-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="6f15e-126">**Q. HTTP-is > omleiding van HTTPS ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="6f15e-127">Omleiding wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6f15e-127">Redirection is supported.</span></span> <span data-ttu-id="6f15e-128">Ga naar [Application Gateway omleiding overzicht](application-gateway-redirect-overview.md) toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="6f15e-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn more.</span></span>

<span data-ttu-id="6f15e-129">**Q. In welke volgorde listeners verwerkt?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="6f15e-130">Listeners worden verwerkt in Hallo volgorde waarin die ze worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6f15e-130">Listeners are processed in hello order they are shown.</span></span> <span data-ttu-id="6f15e-131">Daarom als een eenvoudige listener overeenkomt met een inkomende aanvraag verwerkt eerst.</span><span class="sxs-lookup"><span data-stu-id="6f15e-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="6f15e-132">Multi-site-listeners moeten worden geconfigureerd voordat een basic-listener tooensure-verkeer gerouteerd toohello juiste back-end wordt.</span><span class="sxs-lookup"><span data-stu-id="6f15e-132">Multi-site listeners should be configured before a basic listener tooensure traffic is routed toohello correct back-end.</span></span>

<span data-ttu-id="6f15e-133">**Q. Waar vind ik de IP- en DNS van de Gateway van de toepassing?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="6f15e-134">Wanneer u een openbaar IP-adres gebruikt als een eindpunt, kunt deze informatie vinden op Hallo openbare IP-adres resource of op de pagina overzicht Hallo voor Hallo Application Gateway in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="6f15e-134">When using a public IP address as an endpoint, this information can be found on hello public IP address resource or on hello Overview page for hello Application Gateway in hello portal.</span></span> <span data-ttu-id="6f15e-135">Voor interne IP-adressen, kan dit worden gevonden op de pagina overzicht Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f15e-135">For internal IP addresses, this can be found on hello Overview page.</span></span>

<span data-ttu-id="6f15e-136">**Q. Hallo IP- of DNS-verandert gedurende de levensduur Hallo Hallo Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-136">**Q. Does hello IP or DNS change over hello lifetime of hello Application Gateway?**</span></span>

<span data-ttu-id="6f15e-137">Hallo VIP kunt wijzigen als Hallo gateway wordt gestopt en door de klant Hallo gestart.</span><span class="sxs-lookup"><span data-stu-id="6f15e-137">hello VIP can change if hello gateway is stopped and started by hello customer.</span></span> <span data-ttu-id="6f15e-138">Hallo DNS die zijn gekoppeld aan de toepassingsgateway wordt niet gewijzigd gedurende de levenscyclus Hallo van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="6f15e-138">hello DNS associated with Application Gateway does not change over hello lifecycle of hello gateway.</span></span> <span data-ttu-id="6f15e-139">Daarom is het aanbevolen toouse een CNAME-alias en wijs het DNS-serveradres toohello Hallo Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f15e-139">For this reason, it is recommended toouse a CNAME alias and point it toohello DNS address of hello Application Gateway.</span></span>

<span data-ttu-id="6f15e-140">**Q. Application Gateway biedt ondersteuning voor statische IP-adres?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="6f15e-141">Nee, Application Gateway biedt geen ondersteuning voor statische openbare IP-adressen, maar biedt ondersteuning voor statische interne IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="6f15e-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="6f15e-142">**Q. Ondersteunt Application Gateway meerdere openbare IP-adressen op Hallo gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-142">**Q. Does Application Gateway support multiple public IPs on hello gateway?**</span></span>

<span data-ttu-id="6f15e-143">Slechts één openbaar IP-adres wordt ondersteund op een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6f15e-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="6f15e-144">**Q. Application Gateway biedt ondersteuning voor x doorgestuurd voor headers?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="6f15e-145">Ja, Application Gateway wordt ingevoegd x doorgestuurd voor, x-doorgestuurd-protocol en headers van de x-doorgestuurd-poort in Hallo aanvraag doorgestuurd toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="6f15e-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into hello request forwarded toohello backend.</span></span> <span data-ttu-id="6f15e-146">Hallo-indeling voor x doorgestuurd voor header is een door komma's gescheiden lijst met IP: poort.</span><span class="sxs-lookup"><span data-stu-id="6f15e-146">hello format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="6f15e-147">geldige waarden voor de x-doorgestuurd protocol Hallo zijn http of https.</span><span class="sxs-lookup"><span data-stu-id="6f15e-147">hello valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="6f15e-148">X-doorgestuurd poort geeft Hallo-poort op welke Hallo verzoek op Hallo Application Gateway is bereikt.</span><span class="sxs-lookup"><span data-stu-id="6f15e-148">X-forwarded-port specifies hello port at which hello request reached at hello Application Gateway.</span></span>

<span data-ttu-id="6f15e-149">**Q. Hoe lang duurt toodeploy een Application Gateway? Mijn Application Gateway nog steeds werkt als wordt bijgewerkt?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-149">**Q. How long does it take toodeploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="6f15e-150">Nieuwe Application Gateway-implementaties kunnen tooprovision van too20 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="6f15e-150">New Application Gateway deployments can take up too20 minutes tooprovision.</span></span> <span data-ttu-id="6f15e-151">Wijzigingen tooinstance grootte/count zijn niet verstoren en Hallo gateway blijft actief gedurende deze tijd.</span><span class="sxs-lookup"><span data-stu-id="6f15e-151">Changes tooinstance size/count are not disruptive, and hello gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="6f15e-152">Configuratie</span><span class="sxs-lookup"><span data-stu-id="6f15e-152">Configuration</span></span>

<span data-ttu-id="6f15e-153">**Q. Toepassingsgateway altijd geïmplementeerd in een virtueel netwerk?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="6f15e-154">Ja, Application Gateway altijd in een virtueel netwerksubnet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6f15e-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="6f15e-155">Dit subnet kan alleen Toepassingsgateways bevatten.</span><span class="sxs-lookup"><span data-stu-id="6f15e-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="6f15e-156">**Q. Kan de toepassingsgateway communiceren tooinstances buiten het virtuele netwerk?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-156">**Q. Can Application Gateway talk tooinstances outside its virtual network?**</span></span>

<span data-ttu-id="6f15e-157">Toepassingsgateway kunt contact opnemen tooinstances buiten Hallo virtuele netwerk dat het, zolang er een IP-verbinding is.</span><span class="sxs-lookup"><span data-stu-id="6f15e-157">Application Gateway can talk tooinstances outside of hello virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="6f15e-158">Interne IP-adressen als back-end-groepsleden, dan is vereist als u van plan toouse bent [VNET-Peering](../virtual-network/virtual-network-peering-overview.md) of [VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="6f15e-158">If you plan toouse internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="6f15e-159">**Q. Kan ik iets anders in Hallo-subnet voor Application Gateway implementeren?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-159">**Q. Can I deploy anything else in hello Application Gateway subnet?**</span></span>

<span data-ttu-id="6f15e-160">Nee, maar u kunt andere Toepassingsgateways in Hallo subnet implementeren.</span><span class="sxs-lookup"><span data-stu-id="6f15e-160">No, but you can deploy other application gateways in hello subnet.</span></span>

<span data-ttu-id="6f15e-161">**Q. Worden Netwerkbeveiligingsgroepen op Hallo Application Gateway subnet ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-161">**Q. Are Network Security Groups supported on hello Application Gateway subnet?**</span></span>

<span data-ttu-id="6f15e-162">Netwerkbeveiligingsgroepen worden ondersteund op Hallo Application Gateway-subnet met Hallo volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="6f15e-162">Network Security Groups are supported on hello Application Gateway subnet with hello following restrictions:</span></span>

* <span data-ttu-id="6f15e-163">Uitzonderingen moeten in worden geplaatst voor binnenkomend verkeer op poort 65503 65534 voor back-end health toowork correct.</span><span class="sxs-lookup"><span data-stu-id="6f15e-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health toowork correctly.</span></span>

* <span data-ttu-id="6f15e-164">Uitgaande verbinding met internet kan niet worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="6f15e-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="6f15e-165">Verkeer van Hallo AzureLoadBalancer-tag moet worden toegestaan.</span><span class="sxs-lookup"><span data-stu-id="6f15e-165">Traffic from hello AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="6f15e-166">**Q. Wat zijn Hallo beperkingen op Application Gateway? Kan ik deze limieten verhogen?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-166">**Q. What are hello limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="6f15e-167">Ga naar [Application Gateway limieten](../azure-subscription-service-limits.md#application-gateway-limits) tooview Hallo limieten.</span><span class="sxs-lookup"><span data-stu-id="6f15e-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limits.</span></span>

<span data-ttu-id="6f15e-168">**Q. Kan ik tegelijkertijd Application Gateway voor externe en interne verkeer gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="6f15e-169">Ja, Application Gateway ondersteunt het gebruik van een intern IP-adres en één extern IP-adres per Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f15e-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="6f15e-170">**Q. Wordt VNet-peering ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="6f15e-171">Ja, VNet-peering wordt ondersteund en is handig voor taakverdeling verkeer in andere virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="6f15e-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="6f15e-172">**Q. Kan ik tooon lokale servers praten wanneer ze zijn verbonden via ExpressRoute- of VPN-tunnels?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-172">**Q. Can I talk tooon-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="6f15e-173">Ja, zolang er verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="6f15e-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="6f15e-174">**Q. Kan ik een back-endpool voor veel toepassingen op verschillende poorten hebben?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="6f15e-175">Architectuur micro service wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6f15e-175">Micro service architecture is supported.</span></span> <span data-ttu-id="6f15e-176">U moet meerdere tooprobe van HTTP-instellingen die zijn geconfigureerd op verschillende poorten.</span><span class="sxs-lookup"><span data-stu-id="6f15e-176">You would need multiple http settings configured tooprobe on different ports.</span></span>

<span data-ttu-id="6f15e-177">**Q. Ondersteunen aangepaste tests jokertekens/regex op antwoordgegevens?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="6f15e-178">Aangepaste tests ondersteunen geen jokertekens of reguliere expressie op antwoordgegevens.</span><span class="sxs-lookup"><span data-stu-id="6f15e-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="6f15e-179">**Q. Hoe kan ik regels verwerkt?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="6f15e-180">Regels worden verwerkt in Hallo volgorde waarin die ze zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6f15e-180">Rules are processed in hello order they are configured.</span></span> <span data-ttu-id="6f15e-181">Het wordt aanbevolen dat de regels voor meerdere sites zijn geconfigureerd voordat basisregels tooreduce Hallo kans dat verkeer wordt doorgestuurd toohello ongeschikte back-end omdat Hallo basic regel zou overeenkomt met het verkeer op basis van eerdere toohello multi-site poortregel wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="6f15e-181">It is recommended that multi-site rules are configured before basic rules tooreduce hello chance that traffic is routed toohello inappropriate backend as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="6f15e-182">**Q. Hoe kan ik regels verwerkt?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="6f15e-183">Regels worden verwerkt op Hallo volgorde die ze zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6f15e-183">Rules are processed in hello order they are created.</span></span> <span data-ttu-id="6f15e-184">Het wordt aanbevolen dat de regels voor meerdere locaties zijn geconfigureerd voor het basisregels.</span><span class="sxs-lookup"><span data-stu-id="6f15e-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="6f15e-185">Deze configuratie vermindert multi-site-listeners eerst configureert, Hallo kans dat verkeer gerouteerd toohello ongeschikte back-end wordt.</span><span class="sxs-lookup"><span data-stu-id="6f15e-185">By configuring multi-site listeners first, this configuration reduces hello chance that traffic is routed toohello inappropriate backend.</span></span> <span data-ttu-id="6f15e-186">Deze routering probleem kan optreden omdat Hallo basic regel zou overeenkomt met het verkeer op basis van eerdere toohello multi-site poortregel wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="6f15e-186">This routing issue can occur as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="6f15e-187">**Q. Wat Hallo Host veld voor aangepaste tests geven?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-187">**Q. What does hello Host field for custom probes signify?**</span></span>

<span data-ttu-id="6f15e-188">Veld host geeft Hallo naam toosend Hallo test op.</span><span class="sxs-lookup"><span data-stu-id="6f15e-188">Host field specifies hello name toosend hello probe to.</span></span> <span data-ttu-id="6f15e-189">Van toepassing alleen als er meerdere locaties is geconfigureerd op Application Gateway, of gebruik anders '127.0.0.1'.</span><span class="sxs-lookup"><span data-stu-id="6f15e-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="6f15e-190">Deze waarde verschilt van de VM-hostnaam en indeling \<protocol\>://\<host\>:\<poort\>\<pad\>.</span><span class="sxs-lookup"><span data-stu-id="6f15e-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="6f15e-191">**Q. Kan ik geaccepteerde Application Gateway toegang tooa enkele bron-IP-adressen?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-191">**Q. Can I whitelist Application Gateway access tooa few source IPs?**</span></span>

<span data-ttu-id="6f15e-192">Dit scenario kan worden gedaan met nsg's op Application Gateway-subnet.</span><span class="sxs-lookup"><span data-stu-id="6f15e-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="6f15e-193">Hallo volgen beperkingen moet worden geplaatst op Hallo subnet in volgorde van prioriteit Hallo vermeld:</span><span class="sxs-lookup"><span data-stu-id="6f15e-193">hello following restrictions should be put on hello subnet in hello listed order of priority:</span></span>

* <span data-ttu-id="6f15e-194">Toestaan dat binnenkomend verkeer van de bron-IP-of het IP-bereik.</span><span class="sxs-lookup"><span data-stu-id="6f15e-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="6f15e-195">Toestaan van binnenkomende aanvragen van alle bronnen tooports 65503 65534 voor [back-end health communicatie](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6f15e-195">Allow incoming requests from all sources tooports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="6f15e-196">Toestaan van binnenkomende Azure Load Balancer-tests (AzureLoadBalancer-tag) en binnenkomende virtueel netwerkverkeer (VirtualNetwork-tag) op Hallo [NSG](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="6f15e-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on hello [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="6f15e-197">Alle andere binnenkomende verkeer met een weigeren alle regel blokkeren.</span><span class="sxs-lookup"><span data-stu-id="6f15e-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="6f15e-198">Toestaan dat het uitgaande verkeer toohello internet voor alle bestemmingen.</span><span class="sxs-lookup"><span data-stu-id="6f15e-198">Allow outbound traffic toohello internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="6f15e-199">Prestaties</span><span class="sxs-lookup"><span data-stu-id="6f15e-199">Performance</span></span>

<span data-ttu-id="6f15e-200">**Q. Hoe ondersteunt Application Gateway hoge beschikbaarheid en schaalbaarheid?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="6f15e-201">Toepassingsgateway ondersteunt scenario's voor hoge beschikbaarheid als er twee of meer instanties zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6f15e-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="6f15e-202">Azure distributie van deze exemplaren over de update en fouttolerantie domeinen tooensure die alle exemplaren niet op Hallo mislukken hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="6f15e-202">Azure distributes these instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="6f15e-203">Toepassingsgateway schaalbaarheid door meerdere exemplaren van Hallo toe te voegen ondersteunt dezelfde gateway tooshare Hallo laden.</span><span class="sxs-lookup"><span data-stu-id="6f15e-203">Application Gateway supports scalability by adding multiple instances of hello same gateway tooshare hello load.</span></span>

<span data-ttu-id="6f15e-204">**Q. Hoe ik herstel na noodgevallen bereikt via datacenters met Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="6f15e-205">Klanten kunnen Traffic Manager toodistribute verkeer over meerdere Toepassingsgateways in verschillende datacenters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f15e-205">Customers can use Traffic Manager toodistribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="6f15e-206">**Q. Wordt automatische schaling ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="6f15e-207">Nee, maar Application Gateway heeft een doorvoer metrische gegevens die gebruikt tooalert worden kan u wanneer een drempelwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="6f15e-207">No, but Application Gateway has a throughput metric that can be used tooalert you when a threshold is reached.</span></span> <span data-ttu-id="6f15e-208">Handmatig exemplaren toevoegen of wijzigen van grootte Hallo gateway niet opnieuw wordt opgestart en heeft geen gevolgen voor bestaande-verkeer.</span><span class="sxs-lookup"><span data-stu-id="6f15e-208">Manually adding instances or changing size does not restart hello gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="6f15e-209">**Q. Ondersteunt handmatige schaal omhoog/omlaag oorzaak uitvaltijd?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="6f15e-210">Er is geen downtime, exemplaren zijn verdeeld over upgradedomeinen en domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="6f15e-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="6f15e-211">**Q. Kan ik exemplaargrootte wijzigen van gemiddeld toolarge zonder onderbreking?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-211">**Q. Can I change instance size from medium toolarge without disruption?**</span></span>

<span data-ttu-id="6f15e-212">Ja, Azure exemplaren distributie over de update en fouttolerantie domeinen tooensure die alle exemplaren niet op Hallo mislukken hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="6f15e-212">Yes, Azure distributes instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="6f15e-213">Een toepassing Gateway ondersteunt schalen door toevoeging van meerdere exemplaren van dezelfde gateway tooshare Hallo load Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f15e-213">Application Gateway supports scaling by adding multiple instances of hello same gateway tooshare hello load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="6f15e-214">SSL-configuratie</span><span class="sxs-lookup"><span data-stu-id="6f15e-214">SSL Configuration</span></span>

<span data-ttu-id="6f15e-215">**Q. Welke certificaten op Application Gateway worden ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="6f15e-216">Zelf-ondertekende certificaten, CA-certificaten, en certificaten voor het jokerteken worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6f15e-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="6f15e-217">EV certificaten worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6f15e-217">EV certs are not supported.</span></span>

<span data-ttu-id="6f15e-218">**Q. Wat zijn Hallo huidige versleutelingssuites die door Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-218">**Q. What are hello current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="6f15e-219">Hallo volgen Hallo huidige coderingssuites wordt ondersteund door de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6f15e-219">hello following are hello current cipher suites supported by application gateway.</span></span> <span data-ttu-id="6f15e-220">Ga naar: [configureren SSL beleid versies en coderingssuites in toepassingsgateway](application-gateway-configure-ssl-policy-powershell.md) toolearn hoe toocustomize SSL-opties.</span><span class="sxs-lookup"><span data-stu-id="6f15e-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn how toocustomize SSL options.</span></span>

- <span data-ttu-id="6f15e-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="6f15e-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="6f15e-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="6f15e-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="6f15e-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="6f15e-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="6f15e-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="6f15e-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="6f15e-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="6f15e-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="6f15e-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="6f15e-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="6f15e-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="6f15e-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="6f15e-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="6f15e-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="6f15e-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="6f15e-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="6f15e-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="6f15e-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="6f15e-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6f15e-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="6f15e-247">**Q. Ondersteunt Application Gateway ook opnieuw versleutelen van back-end van verkeer toohello?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-247">**Q. Does Application Gateway also support re-encryption of traffic toohello backend?**</span></span>

<span data-ttu-id="6f15e-248">Ja, Application Gateway ondersteunt het SSL-offload en end tooend SSL, dit opnieuw Hallo verkeer toohello back-end versleutelt.</span><span class="sxs-lookup"><span data-stu-id="6f15e-248">Yes, Application Gateway supports SSL offload, and end tooend SSL, which re-encrypts hello traffic toohello backend.</span></span>

<span data-ttu-id="6f15e-249">**Q. Kan ik een SSL-beleid toocontrol SSL-Protocol versie configureren?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-249">**Q. Can I configure SSL policy toocontrol SSL Protocol versions?**</span></span>

<span data-ttu-id="6f15e-250">Ja, kunt u Application Gateway toodeny TLS1.0 TLS1.1 en TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="6f15e-250">Yes, you can configure Application Gateway toodeny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="6f15e-251">SSL 2.0 en 3.0 zijn standaard al uitgeschakeld en zijn niet configureerbaar.</span><span class="sxs-lookup"><span data-stu-id="6f15e-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="6f15e-252">**Q. Kan ik coderingssuites en beleid volgorde configureren?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="6f15e-253">Ja, [configuratie van coderingssuites](application-gateway-ssl-policy-overview.md) wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6f15e-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="6f15e-254">Bij het definiëren van een aangepast beleid moet ten minste één van de volgende coderingssuites Hallo zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6f15e-254">When defining a custom policy, at least one of hello following cipher suites must be enabled.</span></span> <span data-ttu-id="6f15e-255">Toepassingsgateway gebruikt SHA256 toofor back-end-management.</span><span class="sxs-lookup"><span data-stu-id="6f15e-255">Application gateway uses SHA256 toofor backend management.</span></span>

* <span data-ttu-id="6f15e-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="6f15e-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="6f15e-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="6f15e-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="6f15e-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="6f15e-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6f15e-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="6f15e-262">**Q. Hoeveel SSL-certificaten worden ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="6f15e-263">Up too20 SSL zijn certificaten worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6f15e-263">Up too20 SSL certificates are supported.</span></span>

<span data-ttu-id="6f15e-264">**Q. Hoeveel verificatiecertificaten voor opnieuw versleutelen van back-end worden ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="6f15e-265">Certificaten voor clientverificatie worden up too10 ondersteund met een standaardwaarde van 5.</span><span class="sxs-lookup"><span data-stu-id="6f15e-265">Up too10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="6f15e-266">**Q. Kan Application Gateway integreren met Azure Key Vault systeemeigen?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="6f15e-267">Nee, dit niet is geïntegreerd met Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="6f15e-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="6f15e-268">Web Application Firewall (WAF)-configuratie</span><span class="sxs-lookup"><span data-stu-id="6f15e-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="6f15e-269">**Q. Biedt Hallo WAF SKU alle Hallo functies die beschikbaar zijn met de Hallo standaard SKU?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-269">**Q. Does hello WAF SKU offer all hello features available with hello Standard SKU?**</span></span>

<span data-ttu-id="6f15e-270">Ja, ondersteunt WAF alle Hallo-functies in Hallo standaard SKU.</span><span class="sxs-lookup"><span data-stu-id="6f15e-270">Yes, WAF supports all hello features in hello Standard SKU.</span></span>

<span data-ttu-id="6f15e-271">**Q. Wat is Hallo CRS versie die biedt ondersteuning voor Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-271">**Q. What is hello CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="6f15e-272">Toepassingsgateway ondersteunt CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) en CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="6f15e-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="6f15e-273">**Q. Hoe bewaak ik WAF?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="6f15e-274">WAF via Diagnostische logboekregistratie wordt bewaakt, meer informatie over het vastleggen van diagnostische gegevens kan worden gevonden op [logboekregistratie van diagnostische gegevens en metrische gegevens voor de toepassingsgateway](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="6f15e-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="6f15e-275">**Q. Blokkeert modus detectie verkeer?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="6f15e-276">Nee, registreert detectie-modus alleen-verkeer, wat een regel WAF geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="6f15e-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="6f15e-277">**Q. Hoe ik WAF regels aanpassen?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="6f15e-278">Ja, WAF regels kunnen worden aangepast, voor meer informatie over hoe toocustomize die ze bezoeken [regelgroepen WAF aanpassen en regels](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6f15e-278">Yes, WAF rules are customizable, for more information on how toocustomize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="6f15e-279">**Q. Welke regels zijn momenteel beschikbaar?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="6f15e-280">Op dit moment ondersteunt CRS WAF [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) en [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), die een basislijn beveiliging tegen de meeste Hallo top 10 zwakke plekken die zijn geïdentificeerd door Hallo Open Web Application Security Project (OWASP) dat u hier vindt [OWASP top 10 beveiligingsproblemen](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="6f15e-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of hello top 10 vulnerabilities identified by hello Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="6f15e-281">Beveiliging tegen SQL-injecties</span><span class="sxs-lookup"><span data-stu-id="6f15e-281">SQL injection protection</span></span>

* <span data-ttu-id="6f15e-282">Beveiliging tegen scripting op meerdere sites</span><span class="sxs-lookup"><span data-stu-id="6f15e-282">Cross site scripting protection</span></span>

* <span data-ttu-id="6f15e-283">Beveiliging tegen veelvoorkomende aanvallen via internet, zoals opdrachtinjectie, het smokkelen van HTTP-aanvragen, het uitsplitsen van HTTP-antwoorden en aanvallen waarbij een extern bestand wordt ingesloten</span><span class="sxs-lookup"><span data-stu-id="6f15e-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="6f15e-284">Beveiliging tegen schendingen van het HTTP-protocol</span><span class="sxs-lookup"><span data-stu-id="6f15e-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="6f15e-285">Beveiliging tegen afwijkingen van het HTTP-protocol, zoals een gebruikersagent voor de host en Accept-headers die ontbreken</span><span class="sxs-lookup"><span data-stu-id="6f15e-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="6f15e-286">Beveiliging tegen bots, crawlers en scanners</span><span class="sxs-lookup"><span data-stu-id="6f15e-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="6f15e-287">Detectie van veelvoorkomende onvolkomenheden in toepassing (dat wil zeggen, Apache, IIS, enz.)</span><span class="sxs-lookup"><span data-stu-id="6f15e-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="6f15e-288">**Q. Ondersteunt WAF ook DDoS voorkomen?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="6f15e-289">Nee, WAF biedt geen DDoS te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="6f15e-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="6f15e-290">Diagnostische gegevens en logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="6f15e-290">Diagnostics and Logging</span></span>

<span data-ttu-id="6f15e-291">**Q. Welke typen logboeken beschikbaar zijn met Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="6f15e-292">Er zijn drie logboeken beschikbaar zijn voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6f15e-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="6f15e-293">Voor meer informatie over deze logboeken en andere diagnostische mogelijkheden, gaat u naar [back-end status, diagnostische logboeken en metrische gegevens voor Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6f15e-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="6f15e-294">**ApplicationGatewayAccessLog** -toegangslogboek Hallo bevat elke aanvraag is verzonden toohello Application Gateway frontend.</span><span class="sxs-lookup"><span data-stu-id="6f15e-294">**ApplicationGatewayAccessLog** - hello access log contains each request submitted toohello Application Gateway frontend.</span></span> <span data-ttu-id="6f15e-295">Hallo gegevens omvatten Hallo aanroeper IP-adres aangevraagd, URL antwoord latentie, retourcode, bytes in en uit. Toegangslogboek verzameld om de 300 seconden.</span><span class="sxs-lookup"><span data-stu-id="6f15e-295">hello data includes hello caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="6f15e-296">Dit logboek bevat één record per exemplaar van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="6f15e-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="6f15e-297">**ApplicationGatewayPerformanceLog** -Hallo prestatielogboek bevat informatie over de prestaties op per exemplaar basis totale aanvraag geleverd, inclusief doorvoer in bytes, het totaal aantal aanvragen dat is geleverd, mislukte aanvraag count, orde is en niet in orde back-end-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="6f15e-297">**ApplicationGatewayPerformanceLog** - hello performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="6f15e-298">**ApplicationGatewayFirewallLog** -Hallo firewall logboek bevat aanvragen die zijn geregistreerd via de modus voor detectie of ter voorkoming van een toepassingsgateway die is geconfigureerd met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="6f15e-298">**ApplicationGatewayFirewallLog** - hello firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="6f15e-299">**Q. Hoe weet ik of Mijn back-end-groepsleden in orde zijn?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="6f15e-300">U kunt de PowerShell-cmdlet Hallo `Get-AzureRmApplicationGatewayBackendHealth` of status via Hallo portal controleren door bezoeken [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="6f15e-300">You can use hello PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through hello portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="6f15e-301">**Q. Wat is het bewaarbeleid Hallo op Hallo diagnostische logboeken?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-301">**Q. What is hello retention policy on hello diagnostics logs?**</span></span>

<span data-ttu-id="6f15e-302">Diagnostische logboeken stroom toohello klanten storage-account en klanten Hallo bewaarbeleid op basis van hun voorkeur kunnen instellen.</span><span class="sxs-lookup"><span data-stu-id="6f15e-302">Diagnostic logs flow toohello customers storage account and customers can set hello retention policy based on their preference.</span></span> <span data-ttu-id="6f15e-303">Logboeken met diagnostische gegevens kunnen ook tooan Event Hub of Log Analytics worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="6f15e-303">Diagnostic logs can also be sent tooan Event Hub or Log Analytics.</span></span> <span data-ttu-id="6f15e-304">Ga naar [Application Gateway Diagnostics](application-gateway-diagnostics.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6f15e-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="6f15e-305">**Q. Hoe krijg controlelogboeken voor Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="6f15e-306">Controlelogboeken zijn beschikbaar voor Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f15e-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="6f15e-307">Klik in de portal Hallo op **activiteitenlogboek** op Hallo menu blade van een toepassingsgateway tooaccess Hallo-controlelogboek.</span><span class="sxs-lookup"><span data-stu-id="6f15e-307">In hello portal, click **Activity Log** in hello menu blade of an Application Gateway tooaccess hello audit log.</span></span> 

<span data-ttu-id="6f15e-308">**Q. Kan ik waarschuwingen met Application Gateway instellen?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="6f15e-309">Ja, Application Gateway biedt ondersteuning voor waarschuwingen, waarschuwingen uitschakelen metrische gegevens zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6f15e-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="6f15e-310">Toepassingsgateway heeft momenteel metric 'doorvoer', mag de geconfigureerde tooalert.</span><span class="sxs-lookup"><span data-stu-id="6f15e-310">Application Gateway currently has a metric of "throughput", which can be configured tooalert.</span></span> <span data-ttu-id="6f15e-311">toolearn meer informatie over waarschuwingen, gaat u naar [meldingen van waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="6f15e-311">toolearn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="6f15e-312">**Q. Back-end health status onbekend, wat kan worden veroorzaakt door deze status retourneert?**</span><span class="sxs-lookup"><span data-stu-id="6f15e-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="6f15e-313">Hallo meest voorkomende reden is toegang toohello backend wordt geblokkeerd door een NSG of aangepaste DNS.</span><span class="sxs-lookup"><span data-stu-id="6f15e-313">hello most common reason is access toohello backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="6f15e-314">Ga naar [back-end health logboekregistratie van diagnostische gegevens en metrische gegevens voor Application Gateway](application-gateway-diagnostics.md) toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="6f15e-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f15e-315">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f15e-315">Next Steps</span></span>

<span data-ttu-id="6f15e-316">meer informatie over Application Gateway bezoeken toolearn [inleiding tooApplication Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f15e-316">toolearn more about Application Gateway visit [Introduction tooApplication Gateway](application-gateway-introduction.md).</span></span>
