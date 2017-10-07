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
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>Veilig verbinding maakt met tooBackend bronnen van een App-serviceomgeving
## <a name="overview"></a>Overzicht
Nadat een App Service-omgeving wordt altijd gemaakt **beide** een virtueel netwerk van Azure Resource Manager, **of** een klassieke implementatiemodel [virtueel netwerk] [ virtualnetwork], uitgaande verbindingen vanaf een back-endresources van App Service-omgeving tooother kunnen stromen uitsluitend via Hallo virtueel netwerk.  Met een recente wijziging in juni 2016, worden ASEs ook geïmplementeerd in virtuele netwerken die gebruikmaken van openbare-adresbereiken of RFC1918 adresruimten (dat wil zeggen particuliere adressen).  

Bijvoorbeeld, kan er een SQL-Server uitgevoerd op een cluster van virtuele machines met poort 1433 vergrendeld.  Hallo-eindpunt is mogelijk ACLd tooonly toegang toestaan via andere bronnen op Hallo van hetzelfde virtuele netwerk.  

Als een ander voorbeeld gevoelige eindpunten kunnen on-premises uitgevoerd en worden verbonden tooAzure via een [Site-naar-Site] [ SiteToSite] of [Azure ExpressRoute] [ ExpressRoute] verbindingen.  Als gevolg hiervan alleen bronnen in virtuele netwerken verbonden toohello Site-naar-Site of ExpressRoute-tunnels kunnen tooaccess lokale eindpunten zijn.

Voor elk van deze scenario's, apps die worden uitgevoerd op een App Service-omgeving wordt kunnen toosecurely verbinding moeten maken toohello verschillende servers en bronnen.  Uitgaand verkeer van apps die worden uitgevoerd in een App Service-omgeving tooprivate-eindpunten in Hallo hetzelfde virtuele netwerk (of toohello verbonden hetzelfde virtuele netwerk), wordt alleen stroom via Hallo virtueel netwerk.  Uitgaand verkeer tooprivate eindpunten niet worden overgebracht via openbaar Internet Hallo.

Een voorbehoud geldt toooutbound verkeer van een App Service-omgeving tooendpoints binnen een virtueel netwerk.  App Service-omgevingen kan de eindpunten van virtuele machines zich in Hallo niet bereiken **dezelfde** subnet als het Hallo-App Service-omgeving.  Dit mag normaal gesproken geen probleem, zolang het App Service-omgevingen zijn geïmplementeerd in een subnet is gereserveerd voor exclusief gebruik door alleen Hallo App Service-omgeving.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Uitgaande verbinding en DNS-vereisten
Voor een App Service-omgeving toofunction juist hiervoor uitgaande toegang toovarious eindpunten. Een volledige lijst met externe Hallo-eindpunten die worden gebruikt door een as-omgeving zich in de sectie 'Netwerkverbinding vereist' Hallo Hallo [netwerkconfiguratie voor ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artikel.

App Service-omgevingen moeten een geldige DNS-infrastructuur is geconfigureerd voor het virtuele netwerk Hallo.  Als voor een Hallo reden worden DNS-configuratie is gewijzigd nadat een App-serviceomgeving is gemaakt, kunnen ontwikkelaars een App Service-omgeving toopick Hallo nieuwe DNS-configuratie van afdwingen.  Activering rolling omgeving opgestart met behulp van Hallo 'Opnieuw starten' pictogram Hallo boven aan Hallo App Service-omgeving wordt beheerblade in Hallo-portal Hallo omgeving toopick Hallo nieuwe DNS-configuratie van.

Het is ook aanbevolen of aangepaste DNS-servers op Hallo vnet ingesteld voor tijd voorafgaande toocreating een App Service-omgeving worden.  Als een virtueel netwerk DNS-configuratie wordt gewijzigd terwijl een App Service-omgeving wordt gemaakt, wordt die leiden tot Hallo App Service-omgeving maken proces mislukken.  Als een aangepaste DNS-server op Hallo bestaat is andere einde van een VPN-gateway en Hallo DNS-server in een vergelijkbare vein niet bereikbaar is of niet beschikbaar is, Hallo App Service-omgeving maakproces ook mislukken.

## <a name="connecting-tooa-sql-server"></a>Verbinding maken met SQL Server tooa
Een algemene configuratie van SQL Server heeft een eindpunt luisteren op poort 1433:

![SQL Server-eindpunt][SqlServerEndpoint]

Er zijn twee benaderingen voor het beperken van verkeer toothis eindpunt:

* [Network Access Control Lists] [ NetworkAccessControlLists] (netwerk-ACL's)
* [Netwerkbeveiligingsgroepen][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>Beperken van toegang tot aan een ACL-netwerk
Poort 1433 kan worden beveiligd met behulp van een ACL (toegangsbeheerlijst) netwerk.  Hallo-voorbeeld hieronder whitelists client adressen die afkomstig zijn van binnen een virtueel netwerk en toegang blokkeert op tooall andere clients.

![Voorbeeld van een besturingselement toegang netwerk][NetworkAccessControlListExample]

Alle toepassingen die in App Service-omgeving in hetzelfde virtuele netwerk Hallo als Hallo SQL Server kunnen tooconnect toohello SQL Server-exemplaar met behulp van Hallo **VNet interne** IP-adres voor de virtuele machine van Hallo SQL Server.  

Hallo voorbeeld verbindingsreeks hieronder verwijzingen Hallo SQL Server met behulp van de privé IP-adres.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Hoewel Hallo virtuele machine een openbaar eindpunt ook heeft, wordt verbindingspogingen met Hallo openbaar IP-adres geweigerd vanwege Hallo netwerk ACL. 

## <a name="restricting-access-with-a-network-security-group"></a>Beperken van toegang met een Netwerkbeveiligingsgroep
Er is een alternatieve methode voor het beveiligen van toegang met een netwerkbeveiligingsgroep.  Netwerkbeveiligingsgroepen mag toegepaste tooindividual virtuele machines of tooa subnet met virtuele machines.

Een netwerkbeveiligingsgroep moet eerst toobe gemaakt:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Beperken van toegang tooonly interne VNet-verkeer is zeer eenvoudig met een netwerkbeveiligingsgroep.  Hallo-standaardregels in een netwerkbeveiligingsgroep alleen toegang vanaf andere netwerkclients in Hallo toestaan hetzelfde virtuele netwerk.

Als gevolg hiervan vergrendelen toegang tooSQL-Server is net zo eenvoudig als het toepassen van een netwerkbeveiligingsgroep met de standaard regels tooeither Hallo virtuele machines met SQL Server of Hallo subnet met Hallo virtuele machines.

Hallo onderstaand voorbeeld van een security group toohello met netwerksubnet toepassing:

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

Hallo eindresultaat is een set beveiligingsregels voor verbindingen die externe toegang, terwijl u VNet interne toegang blokkeren:

![Standaard-Netwerkbeveiligingsregels][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>Aan de slag
Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

tooget de slag met App Service-omgevingen, Zie [inleiding tooApp Service-omgeving][IntroToAppServiceEnvironment]

Zie voor meer informatie over beheren binnenkomend verkeer tooyour App Service-omgeving [binnenkomend verkeer tooan App Service-omgeving beheren][ControlInboundASE]

Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service][AzureAppService].

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
