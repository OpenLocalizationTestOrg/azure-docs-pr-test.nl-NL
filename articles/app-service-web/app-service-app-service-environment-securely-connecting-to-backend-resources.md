---
title: aaaSecurely verbinding maakt met tooBackEnd bronnen van een App-serviceomgeving
description: Meer informatie over hoe toosecurely toobackend resources verbinden van een App Service-omgeving.
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="5a952-103">Veilig verbinding maakt met tooBackend bronnen van een App-serviceomgeving</span><span class="sxs-lookup"><span data-stu-id="5a952-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="5a952-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5a952-104">Overview</span></span>
<span data-ttu-id="5a952-105">Nadat een App Service-omgeving wordt altijd gemaakt **beide** een virtueel netwerk van Azure Resource Manager, **of** een klassieke implementatiemodel [virtueel netwerk] [ virtualnetwork], uitgaande verbindingen vanaf een back-endresources van App Service-omgeving tooother kunnen stromen uitsluitend via Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="5a952-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="5a952-106">Met een recente wijziging in juni 2016, worden ASEs ook geïmplementeerd in virtuele netwerken die gebruikmaken van openbare-adresbereiken of RFC1918 adresruimten (dat wil zeggen particuliere adressen).</span><span class="sxs-lookup"><span data-stu-id="5a952-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="5a952-107">Bijvoorbeeld, kan er een SQL-Server uitgevoerd op een cluster van virtuele machines met poort 1433 vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="5a952-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="5a952-108">Hallo-eindpunt is mogelijk ACLd tooonly toegang toestaan via andere bronnen op Hallo van hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="5a952-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="5a952-109">Als een ander voorbeeld gevoelige eindpunten kunnen on-premises uitgevoerd en worden verbonden tooAzure via een [Site-naar-Site] [ SiteToSite] of [Azure ExpressRoute] [ ExpressRoute] verbindingen.</span><span class="sxs-lookup"><span data-stu-id="5a952-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="5a952-110">Als gevolg hiervan alleen bronnen in virtuele netwerken verbonden toohello Site-naar-Site of ExpressRoute-tunnels kunnen tooaccess lokale eindpunten zijn.</span><span class="sxs-lookup"><span data-stu-id="5a952-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="5a952-111">Voor elk van deze scenario's, apps die worden uitgevoerd op een App Service-omgeving wordt kunnen toosecurely verbinding moeten maken toohello verschillende servers en bronnen.</span><span class="sxs-lookup"><span data-stu-id="5a952-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="5a952-112">Uitgaand verkeer van apps die worden uitgevoerd in een App Service-omgeving tooprivate-eindpunten in Hallo hetzelfde virtuele netwerk (of toohello verbonden hetzelfde virtuele netwerk), wordt alleen stroom via Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="5a952-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="5a952-113">Uitgaand verkeer tooprivate eindpunten niet worden overgebracht via openbaar Internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a952-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="5a952-114">Een voorbehoud geldt toooutbound verkeer van een App Service-omgeving tooendpoints binnen een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="5a952-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="5a952-115">App Service-omgevingen kan de eindpunten van virtuele machines zich in Hallo niet bereiken **dezelfde** subnet als het Hallo-App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5a952-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="5a952-116">Dit mag normaal gesproken geen probleem, zolang het App Service-omgevingen zijn geïmplementeerd in een subnet is gereserveerd voor exclusief gebruik door alleen Hallo App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5a952-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="5a952-117">Uitgaande verbinding en DNS-vereisten</span><span class="sxs-lookup"><span data-stu-id="5a952-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="5a952-118">Voor een App Service-omgeving toofunction juist hiervoor uitgaande toegang toovarious eindpunten.</span><span class="sxs-lookup"><span data-stu-id="5a952-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="5a952-119">Een volledige lijst met externe Hallo-eindpunten die worden gebruikt door een as-omgeving zich in de sectie 'Netwerkverbinding vereist' Hallo Hallo [netwerkconfiguratie voor ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artikel.</span><span class="sxs-lookup"><span data-stu-id="5a952-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="5a952-120">App Service-omgevingen moeten een geldige DNS-infrastructuur is geconfigureerd voor het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a952-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="5a952-121">Als voor een Hallo reden worden DNS-configuratie is gewijzigd nadat een App-serviceomgeving is gemaakt, kunnen ontwikkelaars een App Service-omgeving toopick Hallo nieuwe DNS-configuratie van afdwingen.</span><span class="sxs-lookup"><span data-stu-id="5a952-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="5a952-122">Activering rolling omgeving opgestart met behulp van Hallo 'Opnieuw starten' pictogram Hallo boven aan Hallo App Service-omgeving wordt beheerblade in Hallo-portal Hallo omgeving toopick Hallo nieuwe DNS-configuratie van.</span><span class="sxs-lookup"><span data-stu-id="5a952-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="5a952-123">Het is ook aanbevolen of aangepaste DNS-servers op Hallo vnet ingesteld voor tijd voorafgaande toocreating een App Service-omgeving worden.</span><span class="sxs-lookup"><span data-stu-id="5a952-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="5a952-124">Als een virtueel netwerk DNS-configuratie wordt gewijzigd terwijl een App Service-omgeving wordt gemaakt, wordt die leiden tot Hallo App Service-omgeving maken proces mislukken.</span><span class="sxs-lookup"><span data-stu-id="5a952-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="5a952-125">Als een aangepaste DNS-server op Hallo bestaat is andere einde van een VPN-gateway en Hallo DNS-server in een vergelijkbare vein niet bereikbaar is of niet beschikbaar is, Hallo App Service-omgeving maakproces ook mislukken.</span><span class="sxs-lookup"><span data-stu-id="5a952-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="5a952-126">Verbinding maken met SQL Server tooa</span><span class="sxs-lookup"><span data-stu-id="5a952-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="5a952-127">Een algemene configuratie van SQL Server heeft een eindpunt luisteren op poort 1433:</span><span class="sxs-lookup"><span data-stu-id="5a952-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![SQL Server-eindpunt][SqlServerEndpoint]

<span data-ttu-id="5a952-129">Er zijn twee benaderingen voor het beperken van verkeer toothis eindpunt:</span><span class="sxs-lookup"><span data-stu-id="5a952-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="5a952-130">[Network Access Control Lists] [ NetworkAccessControlLists] (netwerk-ACL's)</span><span class="sxs-lookup"><span data-stu-id="5a952-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="5a952-131">[Netwerkbeveiligingsgroepen][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="5a952-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="5a952-132">Beperken van toegang tot aan een ACL-netwerk</span><span class="sxs-lookup"><span data-stu-id="5a952-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="5a952-133">Poort 1433 kan worden beveiligd met behulp van een ACL (toegangsbeheerlijst) netwerk.</span><span class="sxs-lookup"><span data-stu-id="5a952-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="5a952-134">Hallo-voorbeeld hieronder whitelists client adressen die afkomstig zijn van binnen een virtueel netwerk en toegang blokkeert op tooall andere clients.</span><span class="sxs-lookup"><span data-stu-id="5a952-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![Voorbeeld van een besturingselement toegang netwerk][NetworkAccessControlListExample]

<span data-ttu-id="5a952-136">Alle toepassingen die in App Service-omgeving in hetzelfde virtuele netwerk Hallo als Hallo SQL Server kunnen tooconnect toohello SQL Server-exemplaar met behulp van Hallo **VNet interne** IP-adres voor de virtuele machine van Hallo SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5a952-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="5a952-137">Hallo voorbeeld verbindingsreeks hieronder verwijzingen Hallo SQL Server met behulp van de privé IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5a952-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="5a952-138">Hoewel Hallo virtuele machine een openbaar eindpunt ook heeft, wordt verbindingspogingen met Hallo openbaar IP-adres geweigerd vanwege Hallo netwerk ACL.</span><span class="sxs-lookup"><span data-stu-id="5a952-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="5a952-139">Beperken van toegang met een Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="5a952-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="5a952-140">Er is een alternatieve methode voor het beveiligen van toegang met een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="5a952-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="5a952-141">Netwerkbeveiligingsgroepen mag toegepaste tooindividual virtuele machines of tooa subnet met virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5a952-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="5a952-142">Een netwerkbeveiligingsgroep moet eerst toobe gemaakt:</span><span class="sxs-lookup"><span data-stu-id="5a952-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="5a952-143">Beperken van toegang tooonly interne VNet-verkeer is zeer eenvoudig met een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="5a952-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="5a952-144">Hallo-standaardregels in een netwerkbeveiligingsgroep alleen toegang vanaf andere netwerkclients in Hallo toestaan hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="5a952-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="5a952-145">Als gevolg hiervan vergrendelen toegang tooSQL-Server is net zo eenvoudig als het toepassen van een netwerkbeveiligingsgroep met de standaard regels tooeither Hallo virtuele machines met SQL Server of Hallo subnet met Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5a952-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="5a952-146">Hallo onderstaand voorbeeld van een security group toohello met netwerksubnet toepassing:</span><span class="sxs-lookup"><span data-stu-id="5a952-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="5a952-147">Hallo eindresultaat is een set beveiligingsregels voor verbindingen die externe toegang, terwijl u VNet interne toegang blokkeren:</span><span class="sxs-lookup"><span data-stu-id="5a952-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Standaard-Netwerkbeveiligingsregels][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="5a952-149">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="5a952-149">Getting started</span></span>
<span data-ttu-id="5a952-150">Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="5a952-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="5a952-151">tooget de slag met App Service-omgevingen, Zie [inleiding tooApp Service-omgeving][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="5a952-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="5a952-152">Zie voor meer informatie over beheren binnenkomend verkeer tooyour App Service-omgeving [binnenkomend verkeer tooan App Service-omgeving beheren][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="5a952-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="5a952-153">Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="5a952-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
