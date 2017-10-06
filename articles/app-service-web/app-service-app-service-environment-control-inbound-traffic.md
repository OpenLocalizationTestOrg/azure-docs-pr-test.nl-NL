---
title: aaaHow tooControl binnenkomend verkeer tooan App Service-omgeving
description: Meer informatie over hoe tooconfigure network security regels toocontrol inkomend verkeer tooan App Service-omgeving.
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>Hoe tooControl binnenkomend verkeer tooan App Service-omgeving
## <a name="overview"></a>Overzicht
Een App Service-omgeving kunnen worden gemaakt in **beide** een virtueel netwerk van Azure Resource Manager, **of** een klassieke implementatiemodel [virtueel netwerk] [ virtualnetwork].  Een nieuw virtueel netwerk en een nieuw subnet kunnen worden gedefinieerd op Hallo moment die een App Service-omgeving wordt gemaakt.  U kunt ook kunnen een App Service-omgeving worden gemaakt in een bestaand virtueel netwerk en de bestaande subnet.  Met een wijziging in juni 2016, worden ASEs ook geïmplementeerd in virtuele netwerken die gebruikmaken van openbare-adresbereiken of RFC1918 adresruimten (dat wil zeggen particuliere adressen).  Zie voor meer informatie over het maken van een App-serviceomgeving [hoe tooCreate een App-serviceomgeving][HowToCreateAnAppServiceEnvironment].

Een App-serviceomgeving moet altijd worden gemaakt binnen een subnet omdat een subnet biedt een netwerkgrens bevindt die gebruikt toolock omlaag binnenkomend verkeer achter upstream netwerkapparaten en -services worden kan zodanig dat HTTP en HTTPS-verkeer alleen wordt geaccepteerd vanuit specifieke stroomopwaarts IP-adressen.

Binnenkomende en uitgaande netwerkverkeer op een subnet wordt beheerd met behulp van een [netwerkbeveiligingsgroep][NetworkSecurityGroups]. Binnenkomend verkeer te beheren, moet netwerkbeveiligingsregels in een netwerkbeveiligingsgroep maken en vervolgens toewijzen Hallo network security groep Hallo subnet met Hallo App Service-omgeving.

Zodra een netwerkbeveiligingsgroep is tooa subnet worden toegewezen, wordt binnenkomend verkeer tooapps in App Service-omgeving toegestaan/geblokkeerd op basis van Hallo is Hallo toestaan en weigeren van regels die zijn gedefinieerd in Hallo netwerkbeveiligingsgroep.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>Inkomende netwerkpoorten worden gebruikt in een App Service-omgeving
Voordat het vergrendelen van binnenkomend netwerkverkeer koppelen aan een netwerkbeveiligingsgroep is het belangrijk tooknow Hallo reeks vereiste en optionele netwerkpoorten die wordt gebruikt door een App Service-omgeving.  Per ongeluk uit verkeer toosome poorten sluiten, kan dit leiden tot verlies aan functionaliteit in een App Service-omgeving.

Hallo Hieronder volgt een lijst met poorten die worden gebruikt door een App Service-omgeving. Alle poorten zijn **TCP**, tenzij anders wordt duidelijk vermeld:

* 454: **poort vereist** gebruikt door de Azure-infrastructuur voor het beheren en onderhouden van App Service-omgevingen met SSL-beveiliging.  Verkeer toothis poort niet blokkeren.  Deze poort is altijd gebonden toohello openbare VIP van een as-omgeving.
* 455: **poort vereist** gebruikt door de Azure-infrastructuur voor het beheren en onderhouden van App Service-omgevingen met SSL-beveiliging.  Verkeer toothis poort niet blokkeren.  Deze poort is altijd gebonden toohello openbare VIP van een as-omgeving.
* 80: standaard poort voor inkomende HTTP-verkeer tooapps uitgevoerd in App Service-plannen in een App Service-omgeving.  Op een as ingeschakeld met een ILB-omgeving is deze poort gebonden toohello ILB adres Hallo as-omgeving.
* 443: standaard poort voor inkomende SSL-verkeer tooapps uitgevoerd in App Service-plannen in een App Service-omgeving.  Op een as ingeschakeld met een ILB-omgeving is deze poort gebonden toohello ILB adres Hallo as-omgeving.
* 21: besturingskanaal voor FTP.  Deze poort kan veilig worden geblokkeerd als FTP niet wordt gebruikt.  Op een as ingeschakeld met een ILB-omgeving, kan deze poort worden gebonden toohello ILB adres voor een as-omgeving.
* 990: besturingskanaal voor FTPS.  Deze poort kan veilig worden geblokkeerd als FTPS niet wordt gebruikt.  Op een as ingeschakeld met een ILB-omgeving, kan deze poort worden gebonden toohello ILB adres voor een as-omgeving.
* 10001 10020: kanalen voor FTP-gegevens.  Als met besturingskanaal hello, kunnen deze poorten worden veilig geblokkeerd als FTP niet wordt gebruikt.  Op een as ingeschakeld met een ILB-omgeving, kan deze poort gebonden toohello as-omgeving van ILB adres zijn.
* 4016: gebruikt voor foutopsporing op afstand met Visual Studio 2012.  Deze poort kan veilig worden geblokkeerd als het Hallo-functie niet wordt gebruikt.  Op een as ingeschakeld met een ILB-omgeving is deze poort gebonden toohello ILB adres Hallo as-omgeving.
* 4018: gebruikt voor foutopsporing op afstand met Visual Studio 2013.  Deze poort kan veilig worden geblokkeerd als het Hallo-functie niet wordt gebruikt.  Op een as ingeschakeld met een ILB-omgeving is deze poort gebonden toohello ILB adres Hallo as-omgeving.
* 4020: gebruikt voor foutopsporing op afstand met Visual Studio 2015.  Deze poort kan veilig worden geblokkeerd als het Hallo-functie niet wordt gebruikt.  Op een as ingeschakeld met een ILB-omgeving is deze poort gebonden toohello ILB adres Hallo as-omgeving.

## <a name="outbound-connectivity-and-dns-requirements"></a>Uitgaande verbinding en DNS-vereisten
Voor een App Service-omgeving toofunction correct, het is ook vereist uitgaande toegang toovarious eindpunten. Een volledige lijst met externe Hallo-eindpunten die worden gebruikt door een as-omgeving zich in de sectie 'Netwerkverbinding vereist' Hallo Hallo [netwerkconfiguratie voor ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artikel.

App Service-omgevingen moeten een geldige DNS-infrastructuur is geconfigureerd voor het virtuele netwerk Hallo.  Als voor een Hallo reden worden DNS-configuratie is gewijzigd nadat een App-serviceomgeving is gemaakt, kunnen ontwikkelaars een App Service-omgeving toopick Hallo nieuwe DNS-configuratie van afdwingen.  Activering van rolling omgeving opgestart met behulp van Hallo pictogram "Restart" hello boven aan het Hallo-App Service-omgeving management blade in Hallo [Azure-portal] [ NewPortal] zullen Hallo omgeving toopick Hallo nieuwe DNS-configuratie.

Het is ook aanbevolen of aangepaste DNS-servers op Hallo vnet ingesteld voor tijd voorafgaande toocreating een App Service-omgeving worden.  Als een virtueel netwerk DNS-configuratie wordt gewijzigd terwijl een App Service-omgeving wordt gemaakt, wordt die leiden tot Hallo App Service-omgeving maken proces mislukken.  Als een aangepaste DNS-server op Hallo bestaat is andere einde van een VPN-gateway en Hallo DNS-server in een vergelijkbare vein niet bereikbaar is of niet beschikbaar is, Hallo App Service-omgeving maakproces ook mislukken.

## <a name="creating-a-network-security-group"></a>Een Netwerkbeveiligingsgroep maken
Volledige Raadpleeg voor informatie over hoe netwerk werk beveiligingsgroepen Hallo volgende [informatie][NetworkSecurityGroups].  onderstaande verbeterd op Hallo Azure Service Management-voorbeeld illustreert van netwerkbeveiligingsgroepen en een focus over het configureren en toepassen van een security group tooa netwerksubnet waarin een App Service-omgeving.

**Opmerking:** netwerkbeveiligingsgroepen worden geconfigureerd met grafisch Hallo [Azure Portal](https://portal.azure.com) of via Azure PowerShell.

Netwerkbeveiligingsgroepen worden eerst gemaakt als een zelfstandige entiteit die is gekoppeld aan een abonnement. Aangezien netwerkbeveiligingsgroepen in een Azure-regio worden gemaakt, zorg ervoor dat die beveiligingsgroep Hallo-netwerk wordt gemaakt in Hallo dezelfde regio als Hallo App Service-omgeving.

Hallo hieronder ziet u een netwerkbeveiligingsgroep maken:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Zodra een netwerkbeveiligingsgroep is gemaakt, worden een of meer netwerkbeveiligingsregels tooit toegevoegd.  Aangezien Hallo reeks regels kan worden gewijzigd na verloop van tijd, wordt u aangeraden toospace uit Hallo nummering schema gebruikt voor regel prioriteiten toomake eenvoudig tooinsert extra regels gedurende een bepaalde periode.

Hallo in het volgende voorbeeld ziet u een regel die expliciet verleent toegang toohello management poorten die nodig is voor hello Azure-infrastructuur toomanage en onderhouden van een App Service-omgeving.  Houd er rekening mee dat alle beheerverkeer via SSL loopt en wordt beveiligd door clientcertificaten, dus Hoewel Hallo poorten zijn geopend niet toegankelijk door een andere entiteit dan Azure beheerinfrastructuur zijn.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


Wanneer vergrendelen toegang tooport 80 en 443 te 'verbergen' een App-serviceomgeving achter upstream apparaten of services, moet u tooknow Hallo upstream IP-adres.  Bijvoorbeeld, als u een web application firewall (WAF) gebruikt, Hallo WAF heeft een eigen IP-adres (of adressen) die worden gebruikt bij via een proxy verkeer tooa downstream-App Service-omgeving.  U moet toouse dit IP-adres in Hallo *SourceAddressPrefix* parameter van een netwerkbeveiligingsregel.

In onderstaande Hallo voorbeeld, is inkomend verkeer van een specifiek IP-adres upstream expliciet toegestaan.  Hallo adres *1.2.3.4* wordt gebruikt als een tijdelijke aanduiding voor Hallo IP-adres van een upstream WAF.  Hallo waarde toomatch Hallo adres dat wordt gebruikt door een upstream-apparaat of de service wijzigen.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Als u FTP-ondersteuning, kan Hallo volgens de regels worden gebruikt als een sjabloon toogrant toohello FTP-besturingselement toegangspoort en gegevens channel-poorten.  Omdat FTP een stateful protocol, mogelijk niet kunnen tooroute FTP-verkeer via een traditionele HTTP/HTTPS-firewall of proxyserver apparaat.  In dit geval moet u tooset hello *SourceAddressPrefix* tooa andere waarde - bijvoorbeeld Hallo IP-adresbereik van ontwikkelaars of implementatie machines op waarmee FTP-clients worden uitgevoerd. 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**Opmerking:** hello gegevenskanaalpoortbereik kan worden gewijzigd tijdens de evaluatieperiode Hallo.)

Als u foutopsporing op afstand met Visual Studio gebruikt, Hallo volgens de regels voor laten zien hoe toogrant toegang tot.  Er is een afzonderlijke regel voor elke ondersteunde versie van Visual Studio aangezien elke versie een andere poort voor foutopsporing op afstand gebruikt.  Net zoals bij FTP-toegang mogelijk niet correct externe foutopsporing verkeer stromen via een traditionele WAF of de proxyapparaat.  Hallo *SourceAddressPrefix* kan in plaats daarvan toohello IP-adresbereik van Visual Studio developer machines worden ingesteld.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>Een Netwerkbeveiligingsgroep tooa Subnet toewijzen
Een netwerkbeveiligingsgroep heeft een standaardbeveiligingsregel waarmee externe toegang tooall-verkeer.  resultaat van het combineren van Hallo netwerkbeveiligingsregels hierboven beschreven, Hallo en Hallo standaardbeveiligingsregel inkomend verkeer blokkeert, wordt alleen verkeer van de bron-adresbereiken die zijn gekoppeld aan een *toestaan* actie kan worden toosend verkeer tooapps uitvoert in een App Service-omgeving.

Nadat een netwerkbeveiligingsgroep is gevuld met beveiligingsregels, moet deze toobe toegewezen toohello subnet met Hallo App Service-omgeving.  Hallo toewijzing opdracht verwijst naar de naam van beide Hallo Hallo virtuele netwerk waarin Hallo App Service-omgeving zich bevindt, evenals de naam Hallo van Hallo subnet waar Hallo App Service-omgeving is gemaakt.  

Hallo in het volgende voorbeeld ziet u een netwerkbeveiligingsgroep tooa subnet en virtueel netwerk worden toegewezen:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

Zodra het Hallo network security groepstoewijzing is gelukt (Hallo-toewijzing is een langlopende bewerkingen en kan een paar minuten toocomplete), alleen inkomend verkeer die overeenkomt met *toestaan* regels wordt apps in App Hallo is bereikt Service-omgeving.

Voor de volledigheid Hallo ziet volgende voorbeeld u hoe tooremove en dus DIS koppelen Hallo netwerkbeveiliging groep uit Hallo subnet:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>Speciale overwegingen voor expliciete IP-SSL
Als een app is geconfigureerd met een expliciete SSL IP-adres (toepasselijke *alleen* tooASEs waarvoor een openbare VIP), in plaats van Hallo standaard IP-adres van Hallo App Service-omgeving, HTTP en HTTPS-verkeer stroomt in Hallo subnet via een andere set van poorten dan de poorten 80 en 443.

Hallo afzonderlijke set van poorten gebruikt door elk IP-SSL-adres vindt u in de portal gebruikersinterface Hallo Hallo App Service-omgeving van details UX-blade.  Selecteer 'alle instellingen'--> 'IP-adressen'.  Hallo 'IP-adressen' blade ziet u een tabel met alle expliciet geconfigureerd IP-SSL-adressen voor Hallo App Service-omgeving, samen met de Hallo speciale poort paar dat wordt gebruikt tooroute HTTP en HTTPS-verkeer met de bijbehorende IP-SSL.  Deze poort paar die toobe voor Hallo DestinationPortRange parameters worden gebruikt bij het configureren van regels in een netwerkbeveiligingsgroep nodig is.

Wanneer een app op een as-omgeving geconfigureerde toouse IP-SSL is, is externe klanten niet zien en hoeft niet tooworry over speciale poorttoewijzing paar Hallo.  Verkeer toohello apps stromen normaal toohello geconfigureerd SSL IP-adres.  Hallo vertaling toohello speciale poort paar automatisch uitgevoerd intern tijdens de laatste fase van het routeren van verkeer Hallo in Hallo subnet met Hallo as-omgeving. 

## <a name="getting-started"></a>Aan de slag
tooget de slag met App Service-omgevingen, Zie [inleiding tooApp Service-omgeving][IntroToAppServiceEnvironment]

Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

Zie voor meer informatie over apps die gebruikmaken van veilig toobackend resource van een App-serviceomgeving [tooBackend resources veilig verbinding te maken van een App-serviceomgeving][SecurelyConnecttoBackend]

Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

