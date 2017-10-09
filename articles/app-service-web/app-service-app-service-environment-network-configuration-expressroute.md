---
title: aaaNetwork configuratie-informatie voor het werken met Express Route
description: Gegevens in de netwerkconfiguratie voor het uitvoeren van App Service-omgevingen in een virtuele netwerken verbonden tooan ExpressRoute-Circuit.
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: 85bbc45cfed619485957ee2a898aa0a7604173cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a>Netwerkconfiguratiedetails voor App Service-omgevingen met ExpressRoute
## <a name="overview"></a>Overzicht
Klanten kunnen verbinding maken met een [Azure ExpressRoute] [ ExpressRoute] circuit tootheir virtuele netwerkinfrastructuur, waardoor hun lokale netwerk tooAzure uitbreiden.  Een App Service-omgeving kunnen worden gemaakt in een subnet van deze [virtueel netwerk] [ virtualnetwork] infrastructuur.  Apps die worden uitgevoerd op Hallo App Service-omgeving kunnen vervolgens alleen via Hallo ExpressRoute-verbinding tot stand brengen beveiligde verbindingen tooback-end-resources die toegankelijk is.  

Een App Service-omgeving kunnen worden gemaakt in **beide** een virtueel netwerk van Azure Resource Manager, **of** classic deployment model virtueel netwerk.  Met een recente wijziging in juni 2016, worden ASEs nu ook geïmplementeerd in virtuele netwerken die gebruikmaken van openbare-adresbereiken of RFC1918 adresruimten (dat wil zeggen particuliere adressen). 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a>Vereiste netwerkverbinding
Er zijn verbindingsproblemen netwerkvereisten voor App Service-omgevingen die niet in eerste instantie kan worden voldaan in een virtueel netwerk verbonden tooan ExpressRoute.  App Service-omgevingen vereisen meer van de volgende Hallo in volgorde toofunction correct:

* Uitgaande connectiviteit tooAzure opslag netwerkeindpunten wereldwijd op beide poorten 80 en 443.  Dit omvat eindpunten zich in Hallo dezelfde regio bevinden als Hallo App Service-omgeving, evenals de storage-eindpunten zich in **andere** Azure-regio's.  Azure Storage-eindpunten omgezet onder de volgende DNS-domeinen Hallo: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net* en *file.core.windows.net*.  
* Uitgaande network connectivity toohello bestanden van de Azure-service op poort 445.
* Uitgaande connectiviteit tooSql DB netwerkeindpunten zich bevinden in Hallo dezelfde regio als Hallo App Service-omgeving.  Eindpunten van de SQL-database los onder Hallo domein te volgen: *database.windows.net*.  Hiervoor moet toegang tooports 1433, 11000 11999 en 14000 14999 openen.  Zie voor meer informatie [in dit artikel over het gebruik van Sql Database V12-poort van](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).
* Uitgaande connectiviteit toohello Azure management vlak netwerkeindpunten (ASM- en ARM-eindpunten).  Dit omvat uitgaande verbinding tooboth *management.core.windows.net* en *management.azure.com*. 
* Uitgaande netwerkverbinding te*ocsp.msocsp.com*, *mscrl.microsoft.com* en *crl.microsoft.com*.  Dit is nodig toosupport SSL-functionaliteit.
* Hallo DNS-configuratie voor het virtuele netwerk Hallo moet geschikt is voor het oplossen van alle Hallo eindpunten en domeinen die zijn vermeld in Hallo eerdere punten.  Als deze eindpunten kunnen niet worden omgezet, mislukken pogingen tot het maken van App Service-omgeving en bestaande App Service-omgevingen worden gemarkeerd als beschadigd.
* Uitgaand verkeer op poort 53 is vereist voor communicatie met de DNS-servers.
* Als u een aangepaste DNS-server bestaat op Hallo van andere einde van een VPN-gateway, Hallo DNS-server moet bereikbaar zijn vanaf Hallo subnet met Hallo App Service-omgeving. 
* Hallo uitgaande netwerkpad kan niet worden getransporteerd via interne zakelijke proxy's, die niet force tunneled tooon-premises.  Dit doet, wijzigingen Hallo effectieve NAT-adres van uitgaand netwerkverkeer van Hallo App Service-omgeving.  Hallo NAT-adres van een App Service-omgeving uitgaand netwerkverkeer wijzigt, worden connectiviteit fouten toomany Hallo-eindpunten die hierboven worden genoemd.  Dit leidt tot mislukte pogingen voor App Service-omgeving maken, evenals eerder orde App Service-omgevingen worden gemarkeerd als beschadigd.  
* Binnenkomende netwerk toegang toorequired poorten voor App Service-omgevingen moet worden toegestaan, zoals beschreven in dit [artikel][requiredports].

Hallo DNS-vereisten kan worden voldaan door te zorgen voor een geldig DNS-infrastructuur is geconfigureerd en onderhouden voor Hallo virtuele netwerk.  Als voor een Hallo reden worden DNS-configuratie is gewijzigd nadat een App-serviceomgeving is gemaakt, kunnen ontwikkelaars een App Service-omgeving toopick Hallo nieuwe DNS-configuratie van afdwingen.  Activering van rolling omgeving opgestart met behulp van Hallo pictogram "Restart" hello boven aan het Hallo-App Service-omgeving management blade in Hallo [Azure-portal] [ NewPortal] zullen Hallo omgeving toopick Hallo nieuwe DNS-configuratie.

Hallo inkomende netwerkvereisten voor toegang kunnen worden voldaan door het configureren van een [netwerkbeveiligingsgroep] [ NetworkSecurityGroups] op Hallo App Service-omgeving van subnet tooallow Hallo vereist toegang zoals is beschreven in deze [artikel][requiredports].

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a>Uitgaande netwerkverbinding inschakelen voor een App Service-omgeving
Een nieuwe ExpressRoute-circuit kondigt standaard een standaardroute waarmee uitgaande internetverbinding.  Met deze configuratie een App Service-omgeving worden kunnen tooconnect tooother Azure-eindpunten.

Maar een algemene configuratie van de klant toodefine is hun eigen standaardroute (0.0.0.0/0), waardoor uitgaande Internet tooinstead netwerkverkeer lokale.  App Service-omgevingen verbroken dit netwerkverkeer altijd omdat Hallo uitgaand verkeer geblokkeerd on-premises wordt of NAT'd tooan onherkenbare set adressen die niet langer met verschillende Azure-eindpunten werken.

Hallo-oplossing is toodefine een (of meer) door de gebruiker gedefinieerde routes (udr's) op Hallo subnet met Hallo App Service-omgeving.  Een UDR definieert subnet-specifieke routes die in plaats van de standaardroute Hallo gehonoreerd.

Indien mogelijk, wordt aangeraden toouse Hallo volgende configuratie:

* Hallo ExpressRoute configuratie kondigt 0.0.0.0/0 en standaard force alle uitgaande verkeer lokale tunnels.
* Hallo UDR toegepast toohello subnet Hallo App Service-omgeving met definieert 0.0.0.0/0 met een volgend hoptype Internet (een voorbeeld hiervan is verder omlaag in dit artikel).

Hallo is gecombineerde effect van deze stappen dat Hallo subnetniveau UDR voorrang boven Hallo ExpressRoute geforceerde tunneling, zodat uitgaande toegang tot Internet vanaf Hallo App Service-omgeving.

> [!IMPORTANT]
> Hallo routes die zijn gedefinieerd in een UDR **moet** worden specifiek genoeg te hebben voorrang boven alle routes die worden geadverteerd door Hallo ExpressRoute-configuratie.  Hallo onderstaand voorbeeld Hallo brede 0.0.0.0/0-adresbereik gebruikt en als zodanig kan mogelijk worden per ongeluk genegeerd door route-advertisements met behulp van specifieke adresbereiken.
> 
> App Service-omgevingen worden niet ondersteund met ExpressRoute-configuraties die **cross adverteert routes van Hallo pad toohello persoonlijke peering pad voor openbare peering**.  ExpressRoute-configuraties waarvoor openbare peering is geconfigureerd, ontvangen route-advertisements van Microsoft voor een groot aantal Microsoft Azure-IP-adresbereiken.  Als deze adresbereiken cross aangekondigd op Hallo-pad voor persoonlijke peering, is Hallo eindresultaat dat alle uitgaande pakketten van Hallo App Service-omgeving van subnet wordt van de klant force tunneled tooa on-premises netwerkinfrastructuur.  Deze stroom netwerk wordt momenteel niet ondersteund met App Service-omgevingen.  Een oplossing toothis probleem is toostop cross-adverteert routes van Hallo pad toohello persoonlijke peering pad voor openbare peering.
> 
> 

Achtergrondinformatie over de gebruiker gedefinieerde routes zijn beschikbaar in deze [overzicht][UDROverview].  

Meer informatie over het maken en configureren van de gebruiker gedefinieerde routes zijn beschikbaar in deze [hoe tooGuide][UDRHowTo].

## <a name="example-udr-configuration-for-an-app-service-environment"></a>Voorbeeld UDR configuratie voor een App Service-omgeving
**Vereisten**

1. Azure Powershell installeren vanaf Hallo [pagina Azure Downloads] [ AzureDownloads] (met de datum juni 2015 of hoger).  Onder "Opdrachtregelprogramma's" is er een koppeling 'Install' onder 'Windows Powershell' waarop de meest recente Powershell-cmdlets hello wordt geïnstalleerd.
2. Het is raadzaam een uniek subnet wordt gemaakt voor exclusief gebruik door een App Service-omgeving.  Dit zorgt ervoor dat subnet Hallo udr's toegepast toohello uitgaand verkeer voor Hallo App Service-omgeving kan alleen worden geopend.
3. **Belangrijke**: implementeer geen App Service-omgeving tot Hallo **nadat** Hallo configuratie stappen worden gevolgd.  Dit zorgt ervoor dat de uitgaande netwerkverbinding beschikbaar is voordat u probeert een App-serviceomgeving toodeploy.

**Stap 1: Een benoemde routetabel maken**

Hallo volgende fragment een routetabel maken 'DirectInternetRouteTable' aangeroepen in Hallo West ons Azure-regio:

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

**Stap 2: Een of meer routes maakt in de routetabel Hallo**

U moet tooadd een of meer routes toohello routetabel in volgorde tooenable uitgaande toegang tot Internet.  

Hallo aanbevolen benadering voor het configureren van uitgaande toegang toohello die Internet toodefine een route voor 0.0.0.0/0 zoals hieronder weergegeven is.

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

Denk eraan dat 0.0.0.0/0 is een brede adresbereik en als zodanig wordt overschreven door meer specifieke adresbereiken die zijn aangekondigd door Hallo ExpressRoute.  toore-Hallo herhalen eerdere aanbeveling, een UDR met een 0.0.0.0/0 route moet worden gebruikt in combinatie met een configuratie voor ExressRoute die alleen ook 0.0.0.0/0 kondigt. 

Als alternatief kunt kunt u een uitgebreide en bijgewerkte lijst met CIDR-bereiken in gebruik door Azure downloaden.  Hallo Xml-bestand met alle hello Azure IP-adresbereiken is beschikbaar via Hallo [Microsoft Download Center][DownloadCenterAddressRanges].  

Let echter op dat deze bereiken op den duur veranderen, dus waardoor periodieke handmatige updates toohello door de gebruiker gedefinieerde routes tookeep synchroon.  Ook, omdat er een standaard bovenste limiet van 100 routes in een enkel UDR u nodig hebt te 'overzicht' hello Azure IP-adres toofit binnen Hallo 100 route limiet bereiken, houd in gedachten dat UDR gedefinieerde routes moeten toobe specifieker Hallo routes die worden geadverteerd door uw ExpressRoute.  

**Stap 3: Hallo route tabel toohello subnet met Hallo App Service-omgeving koppelen**

de laatste configuratiestap Hallo is tooassociate Hallo route tabel toohello subnet waar Hallo App Service-omgeving wordt geïmplementeerd.  Hallo koppelt volgende opdracht Hallo 'DirectInternetRouteTable' toohello 'ASESubnet' waarin u uiteindelijk een App Service-omgeving.

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


**Stap 4: Laatste stappen**

Zodra de routetabel Hallo is gebonden toohello subnet, wordt aanbevolen toofirst test en bevestigen Hallo bedoeld effect.  Bijvoorbeeld: een virtuele machine implementeren in Hallo subnet en Bevestig dat:

* Uitgaand verkeer tooboth Azure en niet-Azure-eindpunten vermeld eerder in dit artikel is **niet** stromende omlaag Hallo ExpressRoute-circuit.  Het is zeer belangrijk tooverify dit gedrag, aangezien als uitgaand verkeer van Hallo subnet is nog steeds gedwongen via een tunnel on-premises kunt maken van App Service-omgeving wordt altijd mislukken. 
* DNS-zoekacties voor Hallo eindpunten eerder zijn alle correct kan omzetten. 

Zodra Hallo bovenstaande stappen zijn bevestigd, moet u toodelete Hallo virtuele machine omdat Hallo-subnet moet toobe 'leeg' op Hallo tijd Hallo die App Service-omgeving wordt gemaakt.

Ga vervolgens verder met het maken van een App-serviceomgeving!

## <a name="getting-started"></a>Aan de slag
Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

tooget de slag met App Service-omgevingen, Zie [inleiding tooApp Service-omgeving][IntroToAppServiceEnvironment]

Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service][AzureAppService].

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
