---
title: aaaNetwork architectuur overzicht van App Service-omgevingen
description: Overzicht van de architectuur van netwerk-topologie ofApp Service-omgevingen.
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 3cbc86883f5687a9ada35a3ab2f577a450a3fa0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a>Overzicht van de netwerkarchitectuur van App Service-omgevingen
## <a name="introduction"></a>Inleiding
App Service-omgevingen worden altijd gemaakt binnen een subnet van een [virtueel netwerk] [ virtualnetwork] -apps die worden uitgevoerd in een App Service-omgeving kunnen communiceren met particuliere eindpunten zich bevindt binnen Hallo dezelfde virtuele netwerktopologie.  Aangezien klanten delen van hun virtuele netwerkinfrastructuur vergrendelen kunnen, is het belangrijk toounderstand Hallo typen communicatie tenantnetwerkstromen die bij een App Service-omgeving optreden.

## <a name="general-network-flow"></a>Algemene netwerk stroom
Wanneer een as-omgeving (App Service omgeving) een openbare virtuele IP-adres (VIP) voor apps gebruikt, worden alle binnenkomend verkeer binnenkomt op die openbare VIP.  Dit omvat HTTP en HTTPS-verkeer voor apps, evenals het andere verkeer voor FTP-functionaliteit voor foutopsporing op afstand en Azure beheerbewerkingen.  Voor een volledige lijst met Hallo Zie specifieke poorten (vereiste en optionele) die beschikbaar op het openbare VIP Hallo zijn Hallo artikel op [binnenkomend verkeer te regelen] [ controllinginboundtraffic] tooan App Service-omgeving. 

App Service-omgevingen ondersteunen ook uitgevoerd apps die afhankelijk zijn van alleen tooa virtuele netwerk interne adres, ook wel aangeduid tooas een adres ILB (interne load balancer).  Op een ILB ingeschakelde as-omgeving, HTTP en HTTPS-verkeer voor apps en externe oproepen bij het opsporen van fouten op Hallo ILB adres binnenkomen.  Voor de meest voorkomende configuraties ILB-as-omgeving aankomt FTP-/ FTPS-verkeer ook op Hallo ILB adres.  Azure beheerbewerkingen wordt nog steeds tooports 454/455 op Hallo openbare VIP van een ILB ingeschakeld echter as-omgeving.

Hallo onderstaande diagram geeft een overzicht van Hallo verschillende binnenkomende en uitgaande tenantnetwerkstromen voor een App Service-omgeving waar Hallo apps gebonden tooa openbare virtuele IP-adres zijn:

![Algemene Tenantnetwerkstromen][GeneralNetworkFlows]

Een App Service-omgeving kunnen communiceren met tal van persoonlijke klant eindpunten.  Apps die worden uitgevoerd in App Service-omgeving kunnen verbinding maken toodatabase server (s) die worden uitgevoerd op IaaS virtuele machines in Hallo Hallo bijvoorbeeld dezelfde virtuele netwerktopologie.

> [!IMPORTANT]
> U bekijkt hello netwerkdiagram, Hallo 'andere Compute Resources' worden geïmplementeerd in een ander Subnet van Hallo App Service-omgeving. Implementatie van resources in Hallo blokkeren hetzelfde Subnet met Hallo as-omgeving connectiviteit van de as-omgeving toothose bronnen (met uitzondering van specifieke intra-as-omgeving routering). Implementeer tooa ander Subnet in plaats daarvan (in hetzelfde VNET Hallo). Hallo App Service-omgeving zijn vervolgens kunnen tooconnect. Er is geen aanvullende configuratie nodig.
> 
> 

App Service-omgevingen ook worden gecommuniceerd met Sql-database en Azure Storage bronnen nodig voor het beheren van en het gebruik van een App Service-omgeving.  Aantal Hallo Sql- en bronnen die een App-serviceomgeving met communiceert bevinden zich in Hallo dezelfde regio bevinden als Hallo App Service-omgeving, terwijl anderen bevinden zich in de externe Azure-regio's.  Als gevolg hiervan uitgaande verbinding toohello Internet is altijd vereist voor een App Service-omgeving toofunction goed. 

Nadat een App Service-omgeving is geïmplementeerd in een subnet, netwerkbeveiligingsgroepen gebruikte toocontrol mag binnenkomend verkeer toohello subnet.  Voor informatie over hoe toocontrol inkomend verkeer tooan App Service-omgeving, Zie de volgende Hallo [artikel][controllinginboundtraffic].

Voor meer informatie over het tooallow uitgaande internetverbinding vanaf een App Service-omgeving, zie volgende artikel over het werken met Hallo [Express Route][ExpressRoute].  Hallo dezelfde manier wordt beschreven in artikel Hallo is van toepassing wanneer het werken met Site-naar-Site-connectiviteit en met geforceerde tunneling.

## <a name="outbound-network-addresses"></a>Uitgaande netwerkadressen
Wanneer een App Service-omgeving uitgaande oproepen maakt, is een IP-adres altijd gekoppeld aan Hallo uitgaande oproepen.  Hallo specifiek IP-adres dat wordt gebruikt, is afhankelijk van of Hallo-eindpunt wordt aangeroepen zich binnen de virtuele netwerktopologie Hallo of buiten de virtuele netwerktopologie Hallo bevindt.

Als Hallo-eindpunt wordt aangeroepen **buiten** van de virtuele netwerktopologie Hallo vervolgens Hallo uitgaande adres (aka Hallo uitgaande NAT-adres) dat wordt gebruikt is openbare VIP Hallo Hallo App Service-omgeving.  Dit adres vindt u in de portal gebruikersinterface Hallo voor Hallo App Service-omgeving in eigenschappenblade.

![Uitgaande IP-adres][OutboundIPAddress]

Dit adres kan ook worden bepaald voor ASEs waarvoor alleen openbare VIP door het maken van een app in App Service-omgeving Hallo en vervolgens uit te voeren een *nslookup* op Hallo-app-adres. Hallo resulterende IP-adres is zowel openbare VIP hello, evenals Hallo App Service-omgeving van uitgaande NAT-adres.

Als Hallo-eindpunt wordt aangeroepen **binnen** uitgaande adres Hallo van Hallo aanroepen app is van de virtuele netwerktopologie hello, Hallo interne IP-adres van afzonderlijke berekeningsresource Hallo Hallo app uitvoert.  Er is echter geen permanente toewijzing van virtueel netwerk interne IP-adressen tooapps.  Apps kunnen verplaatsen tussen verschillende rekenresources en Hallo-groep met beschikbare compute-resources in een App Service-omgeving vanwege tooscaling bewerkingen kan wijzigen.

Echter, omdat er nog steeds een App Service-omgeving zich in een subnet, wordt gegarandeerd dat Hallo interne IP-adres van een berekeningsresource uitvoeren van een app altijd binnen Hallo CIDR-bereik van subnet hello wordt liggen.  Als gevolg hiervan wanneer fijnmazig ACL's of netwerkbeveiligingsgroepen worden gebruikt toosecure toegang tot tooother eindpunten in het virtuele netwerk hello, Hallo subnetbereik met Hallo App Service-omgeving behoeften toobe toegang verleend.

Hallo volgende diagram ziet u deze concepten in meer detail:

![Uitgaande netwerkadressen][OutboundNetworkAddresses]

In de Hallo hierboven diagram:

* Omdat de openbare VIP Hallo Hallo App Service-omgeving 192.23.1.2, die is Hallo uitgaande IP-adres is gebruikt bij het aanroepen te 'Internet' eindpunten.
* Hallo CIDR-bereik van subnet voor Hallo App Service-omgeving met Hallo is 10.0.1.0/26.  Andere eindpunten binnen Hallo dezelfde virtuele netwerkinfrastructuur aanroepen vanuit apps zien als zijnde afkomstig van ergens binnen dit adresbereik.

## <a name="calls-between-app-service-environments"></a>Aanroepen tussen App Service-omgevingen
Een complexere kan gebeuren als u meerdere App Service-omgevingen implementeert in hetzelfde virtuele netwerk Hallo en uitgaande aanroepen vanuit een App Service-omgeving tooanother App Service-omgeving.  Deze typen cross-App Service-omgeving aanroepen, ook worden behandeld als 'Internet' aanroepen.

Hallo volgende diagram toont een voorbeeld van een gelaagde architectuur met apps op één App Service-omgeving (bijvoorbeeld) 'Voordeur' web-apps) voor het aanroepen van apps op een tweede App Service-omgeving (bijvoorbeeld interne back-end-API-apps niet de bedoeling dat toegankelijk is vanaf Internet Hallo toobe). 

![Aanroepen tussen App Service-omgevingen][CallsBetweenAppServiceEnvironments] 

In Hallo heeft voorbeeld hierboven Hallo 'As-omgeving een' App Service-omgeving een uitgaande IP-adres van 192.23.1.2.  Als een app uitgevoerd op App Service-omgeving een uitgaande aanroep tooan app uitgevoerd op een tweede App Service-omgeving ('as-omgeving twee' maakt) zich in hetzelfde virtuele netwerk, Hallo Hallo uitgaande aanroep beschouwd als een aanroep van 'Internet'.  Als gevolg hiervan Hallo netwerkverkeer dat binnenkomt op Hallo tweede App Service-omgeving wordt weergegeven als zijnde afkomstig van 192.23.1.2 (d.w.z. niet Hallo subnet adresbereik van eerste App Service-omgeving Hallo).

Hoewel aanroepen tussen verschillende App Service-omgevingen worden behandeld als 'Internet'-aanroepen wanneer beide App Service-omgevingen bevinden zich in Hallo dezelfde Azure-regio Hallo-netwerkverkeer blijft op Hallo regionale Azure-netwerk en niet fysiek stromen via openbaar Internet Hallo.  Als gevolg hiervan kunt u een netwerkbeveiligingsgroep op Hallo subnet Hallo tweede App Service-omgeving tooonly toestaan binnenkomende oproepen van eerste App Service-omgeving (192.23.1.2 waarvan uitgaande IP-adres is), zodat een veilige communicatie tussen Hallo Hallo App Service-omgevingen.

## <a name="additional-links-and-information"></a>Aanvullende koppelingen en informatie
Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

Meer informatie over binnenkomende poorten gebruikt door App Service-omgevingen en met behulp van network security groepen toocontrol binnenkomend verkeer beschikbaar [hier][controllinginboundtraffic].

Informatie over het gebruik van de gebruiker gedefinieerde routes toogrant uitgaande Internet access tooApp Service-omgevingen zijn beschikbaar in deze [artikel][ExpressRoute]. 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

