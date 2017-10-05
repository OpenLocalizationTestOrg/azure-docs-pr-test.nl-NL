---
title: Veilig verbinding te maken met back-Endresources van een App-serviceomgeving
description: Meer informatie over veilige manier verbinding maken met back-endresources van een App Service-omgeving.
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
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="2960e-103">Veilig verbinding te maken met back-Endresources van een App-serviceomgeving</span><span class="sxs-lookup"><span data-stu-id="2960e-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="2960e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2960e-104">Overview</span></span>
<span data-ttu-id="2960e-105">Nadat een App Service-omgeving wordt altijd gemaakt **beide** een virtueel netwerk van Azure Resource Manager, **of** een klassieke implementatiemodel [virtueel netwerk] [ virtualnetwork], uitgaande verbindingen van een App Service-omgeving naar andere bronnen van de back-end kunnen stromen uitsluitend via het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2960e-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="2960e-106">Met een recente wijziging in juni 2016, kan ASEs ook worden geïmplementeerd in virtuele netwerken die gebruikmaken van openbare-adresbereiken of RFC1918 adresruimten (dat wil zeggen</span><span class="sxs-lookup"><span data-stu-id="2960e-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="2960e-107">particuliere adressen).</span><span class="sxs-lookup"><span data-stu-id="2960e-107">private addresses).</span></span>  

<span data-ttu-id="2960e-108">Bijvoorbeeld, kan er een SQL-Server uitgevoerd op een cluster van virtuele machines met poort 1433 vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="2960e-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="2960e-109">Het eindpunt mogelijk ACLd alleen toegang toestaan via andere bronnen in hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2960e-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="2960e-110">Als een ander voorbeeld gevoelige eindpunten on-premises kan worden uitgevoerd en naar Azure worden verbonden via een [Site-naar-Site] [ SiteToSite] of [Azure ExpressRoute] [ ExpressRoute] verbindingen.</span><span class="sxs-lookup"><span data-stu-id="2960e-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="2960e-111">Als gevolg hiervan zich worden alleen de resources in virtuele netwerken die zijn verbonden met de Site-naar-Site of een ExpressRoute-tunnels voor toegang tot lokale eindpunten.</span><span class="sxs-lookup"><span data-stu-id="2960e-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="2960e-112">Voor elk van deze scenario's, apps die worden uitgevoerd op een App Service-omgeving kan worden veilig verbinding kunnen maken met de verschillende servers en -bronnen.</span><span class="sxs-lookup"><span data-stu-id="2960e-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="2960e-113">Uitgaand verkeer van apps die worden uitgevoerd in een App Service-omgeving naar persoonlijke eindpunten in hetzelfde virtuele netwerk (of verbonden met hetzelfde virtuele netwerk), wordt alleen overdracht via het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2960e-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="2960e-114">Uitgaand verkeer naar persoonlijke eindpunten worden niet overgebracht via het openbare Internet.</span><span class="sxs-lookup"><span data-stu-id="2960e-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="2960e-115">Een voorbehoud geldt voor uitgaand verkeer van een App Service-omgeving naar eindpunten binnen een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2960e-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="2960e-116">App Service-omgevingen niet bereiken eindpunten van virtuele machines zich in de **dezelfde** subnet als de App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="2960e-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="2960e-117">Dit mag normaal gesproken geen probleem, zolang het App Service-omgevingen zijn geïmplementeerd in een subnet is gereserveerd voor exclusief gebruik door alleen de App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="2960e-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="2960e-118">Uitgaande verbinding en DNS-vereisten</span><span class="sxs-lookup"><span data-stu-id="2960e-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="2960e-119">Voor een App Service-omgeving te laten functioneren, vereist deze uitgaande toegang tot verschillende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="2960e-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="2960e-120">Een volledige lijst met de externe eindpunten die worden gebruikt door een as-omgeving is in de sectie 'Netwerkverbinding vereist' van de [netwerkconfiguratie voor ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artikel.</span><span class="sxs-lookup"><span data-stu-id="2960e-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="2960e-121">App Service-omgevingen moeten een geldige DNS-infrastructuur is geconfigureerd voor het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2960e-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="2960e-122">Als voor een bepaalde reden worden de DNS-configuratie is gewijzigd nadat een App-serviceomgeving is gemaakt, kunnen ontwikkelaars een App Service-omgeving naar de nieuwe DNS-configuratie worden opgepikt afdwingen.</span><span class="sxs-lookup"><span data-stu-id="2960e-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="2960e-123">Activering van rolling omgeving opgestart met het pictogram 'Opnieuw starten' boven aan de blade voor het beheer van App Service-omgeving in de portal zal de omgeving voor de nieuwe DNS-configuratie worden opgepikt.</span><span class="sxs-lookup"><span data-stu-id="2960e-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="2960e-124">Het is ook raadzaam dat alle aangepaste DNS-servers op het vnet ingesteld worden voordat u een App-serviceomgeving tevoren.</span><span class="sxs-lookup"><span data-stu-id="2960e-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="2960e-125">Als een virtueel netwerk DNS-configuratie wordt gewijzigd terwijl een App Service-omgeving wordt gemaakt, wordt die leiden tot het mislukken van de App Service-omgeving maken van het proces.</span><span class="sxs-lookup"><span data-stu-id="2960e-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="2960e-126">In een vergelijkbare vein als een aangepaste DNS-server op het andere einde van een VPN-gateway bestaat en de DNS-server onbereikbaar is of niet beschikbaar is, is mislukt het proces voor het maken van App Service-omgeving ook.</span><span class="sxs-lookup"><span data-stu-id="2960e-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="2960e-127">Verbinding maken met een SQL-Server</span><span class="sxs-lookup"><span data-stu-id="2960e-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="2960e-128">Een algemene configuratie van SQL Server heeft een eindpunt luisteren op poort 1433:</span><span class="sxs-lookup"><span data-stu-id="2960e-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![SQL Server-eindpunt][SqlServerEndpoint]

<span data-ttu-id="2960e-130">Er zijn twee methoden voor het beperken van verkeer naar dit eindpunt:</span><span class="sxs-lookup"><span data-stu-id="2960e-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="2960e-131">[Network Access Control Lists] [ NetworkAccessControlLists] (netwerk-ACL's)</span><span class="sxs-lookup"><span data-stu-id="2960e-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="2960e-132">[Netwerkbeveiligingsgroepen][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="2960e-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="2960e-133">Beperken van toegang tot aan een ACL-netwerk</span><span class="sxs-lookup"><span data-stu-id="2960e-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="2960e-134">Poort 1433 kan worden beveiligd met behulp van een ACL (toegangsbeheerlijst) netwerk.</span><span class="sxs-lookup"><span data-stu-id="2960e-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="2960e-135">In het voorbeeld hieronder whitelists client adressen die afkomstig zijn van binnen een virtueel netwerk en toegang tot alle andere clients worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="2960e-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Voorbeeld van een besturingselement toegang netwerk][NetworkAccessControlListExample]

<span data-ttu-id="2960e-137">Alle toepassingen die in App Service-omgeving in hetzelfde virtuele netwerk als de SQL-Server verbinding kunnen maken met de SQL Server-exemplaar op met de **VNet interne** IP-adres voor de virtuele machine van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2960e-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="2960e-138">De verbindingsreeks voorbeeld verwijst naar de SQL-Server de privé IP-adres.</span><span class="sxs-lookup"><span data-stu-id="2960e-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="2960e-139">Hoewel de virtuele machine een openbaar eindpunt ook heeft, wordt verbindingspogingen met het openbare IP-adres wordt geweigerd vanwege de ACL van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="2960e-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="2960e-140">Beperken van toegang met een Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="2960e-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="2960e-141">Er is een alternatieve methode voor het beveiligen van toegang met een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="2960e-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="2960e-142">Netwerkbeveiligingsgroepen kunnen worden toegepast op afzonderlijke virtuele machines, of op een subnet met virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2960e-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="2960e-143">Een netwerkbeveiligingsgroep moet eerst worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="2960e-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="2960e-144">Toegang beperken tot alleen VNet interne verkeer is zeer eenvoudig met een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="2960e-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="2960e-145">De standaardregels in een netwerkbeveiligingsgroep alleen toestaan toegang van andere netwerkclients in hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2960e-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="2960e-146">Als gevolg hiervan vergrendelen toegang tot SQL Server is net zo eenvoudig als het toepassen van een netwerkbeveiligingsgroep met de standaardregels op beide virtuele machines met SQL Server of het subnet met de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2960e-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="2960e-147">Het onderstaande voorbeeld geldt een netwerkbeveiligingsgroep voor het subnet met:</span><span class="sxs-lookup"><span data-stu-id="2960e-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="2960e-148">Het eindresultaat is een set beveiligingsregels voor verbindingen die externe toegang, terwijl u VNet interne toegang blokkeren:</span><span class="sxs-lookup"><span data-stu-id="2960e-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Standaard-Netwerkbeveiligingsregels][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="2960e-150">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="2960e-150">Getting started</span></span>
<span data-ttu-id="2960e-151">Alle artikelen en hoe-aan de voor App Service-omgevingen zijn beschikbaar in de [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="2960e-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="2960e-152">Om aan de slag met App Service-omgevingen, Zie [Inleiding tot de App Service-omgeving][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="2960e-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="2960e-153">Zie voor meer informatie om binnenkomend verkeer naar uw App Service-omgeving beheren [binnenkomend verkeer naar een App-serviceomgeving beheren][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="2960e-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="2960e-154">Zie voor meer informatie over het Azure App Service-platform [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="2960e-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
