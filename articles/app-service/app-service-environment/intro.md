---
title: aaaIntroduction tooAzure App Service-omgevingen
description: Beknopt overzicht van Azure App Service-omgevingen
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 9261041333cf59374974a039edf89c4983c45cdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environments"></a>Inleiding tooApp Service-omgevingen #
 
## <a name="overview"></a>Overzicht ##

Azure App Service-omgeving is een Azure App Service-functie een volledig geïsoleerde en toegewezen omgeving biedt voor het uitvoeren van App Service-apps veilig op grote schaal. Deze mogelijkheid kan hosten uw [web-apps][webapps], [mobiele apps][mobileapps], [API-apps] [ APIapps], en [functies][Functions].

App Service-omgevingen (ASEs) zijn geschikt is voor de toepassing werklast die nodig:

- Zeer grote schaal.
- Isolatie en beveiligde netwerktoegang.
- Hoog geheugengebruik.

Klanten kunnen meerdere ASEs binnen één Azure-regio of op meerdere Azure-regio's maken. Deze flexibiliteit maakt ASEs ideaal voor stateless toepassingslagen ter ondersteuning van werklasten met hoge RPS horizontaal schalen.

ASEs zijn geïsoleerd toorunning alleen één klant toepassingen en altijd in een virtueel netwerk worden geïmplementeerd. Klanten hebben fijnmazig controle over de toepassing voor binnenkomend en uitgaand netwerkverkeer. Toepassingen kunnen tot stand brengen van snelle beveiligde verbindingen via een VPN-verbindingen tooon-premises bedrijfsbronnen.

Alle artikelen en hoe-tooinstructions over ASEs zijn beschikbaar in Hallo [Leesmij-bestand voor App Service-omgevingen][ASEReadme]:

* ASEs inschakelen hoge schaalbaarheid app hosten met beveiligde netwerktoegang. Zie voor meer informatie, Hallo [AzureCon diepgaand](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) op ASEs.
* Meerdere ASEs kunnen gebruikte tooscale horizontaal zijn. Zie voor meer informatie [hoe tooset geografisch verspreide app inneemt](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).
* ASEs mag gebruikte tooconfigure beveiligingsarchitectuur, zoals wordt weergegeven in Hallo AzureCon diepgaand. toosee hoe Hallo-beveiligingsarchitectuur weergegeven in Hallo AzureCon diepgaand is geconfigureerd, Zie Hallo [artikel over het tooimplement een gelaagd beveiligingsarchitectuur](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) met App Service-omgevingen.
* Apps die worden uitgevoerd op ASEs kunnen de geregeld door de upstream-apparaten, zoals web application firewalls (WAFs) toegang hebben. Zie voor meer informatie [configureren van een WAF voor App Service-omgevingen](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).

## <a name="dedicated-environment"></a>Specifieke omgeving ##

Een as-omgeving is uitsluitend tooa één abonnement specifiek en 100 exemplaren kan hosten. Hallo bereik kan 100 exemplaren in een enkele App Service plan too100 single instance App Service-abonnementen en alles in tussen omspannen.

Een as-omgeving bestaat uit een front-ends en werknemers. Front-ends zijn verantwoordelijk voor het HTTP/HTTPS-beëindiging en automatische taakverdeling van app-aanvragen in een as-omgeving. Front-ends worden automatisch toegevoegd als Hallo App Service-abonnementen in Hallo as-omgeving zijn uitgebreid.

Werknemers zijn functies die klant-apps host. Werknemers zijn beschikbaar in drie vaste grootten:

* Een core/3.5 GB RAM-geheugen
* Twee core/7 GB RAM-geheugen
* Vier core/14 GB RAM-geheugen

Klanten hoeven niet toomanage-front-ends en werknemers. Alle infrastructuur wordt automatisch toegevoegd als klanten scale-out hun App Service-abonnementen. App service abonnementen zijn gemaakt of geschaald in een as-omgeving vereist Hallo infrastructuur wordt toegevoegd of verwijderd naar gelang van toepassing.

Er is een plat maandelijks percentage voor een as-omgeving die betaalt voor Hallo-infrastructuur en verandert niet met een grootte Hallo Hallo as-omgeving. Er is bovendien een kosten per core van App Service-plan. Alle apps die worden gehost in een as-omgeving zich in Hallo geïsoleerd SKU prijzen. Zie voor informatie over prijzen voor een as-omgeving Hallo [App Service-prijzen] [ Pricing] pagina en bekijk de beschikbare opties Hallo voor ASEs.

## <a name="virtual-network-support"></a>Virtual network-ondersteuning ##

Een as-omgeving kan alleen in een virtueel netwerk van Azure Resource Manager worden gemaakt. toolearn meer informatie over virtuele netwerken in Azure, Zie Hallo [Azure virtuele netwerken Veelgestelde vragen over](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). Een as-omgeving bestaat altijd in een virtueel netwerk en nauwkeuriger, binnen een subnet van een virtueel netwerk. U kunt Hallo beveiligingsfuncties van virtuele netwerken toocontrol binnenkomende en uitgaande communicatie voor apps in uw netwerk.

Een as-omgeving kan worden internetgerichte met een openbaar IP-adres of interne bedrijfstoepassingen met alleen een adres voor Azure interne load balancer (ILB).

[Netwerkbeveiligingsgroepen] [ NSGs] beperken van binnenkomende communicatie toohello netwerksubnet waarin een as-omgeving zich bevindt. U kunt nsg's toorun apps achter upstream apparaten en services, zoals WAFs en aanbieders van SaaS-netwerk.

Apps moeten ook regelmatig tooaccess bedrijfsbronnen zoals interne databases en webservices. Als u Hallo as-omgeving in een virtueel netwerk met een VPN-verbinding toohello on-premises netwerk implementeert, Hallo-apps in Hallo as-omgeving, hebben toegang tot Hallo lokale bronnen. Deze mogelijkheid geldt ongeacht Hallo VPN wordt aangegeven of een [site-naar-site](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) of [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.

Zie voor meer informatie over de werking van ASEs met virtuele netwerken en on-premises netwerken [overwegingen met betrekking tot het netwerk van het App Service-omgeving][ASENetwork].

## <a name="app-service-environment-v1"></a>App Service-omgeving v1 ##

App Service-omgeving zijn er twee versies: ASEv1 en ASEv2. Hallo voorgaande informatie is gebaseerd op ASEv2. Deze sectie ziet u verschillen tussen ASEv1 en ASEv2 Hallo. 

In de ASEv1, moet u toomanage alle bronnen handmatig Hallo. Dat betekent onder meer Hallo-front-ends, werknemers en IP-adressen gebruikt voor SSL op basis van IP. Voordat u uw App Service-abonnement uitbreiden kunt, moet u toofirst uitbreiden Hallo werknemersgroep waar u toohost deze.

ASEv1 maakt gebruik van een andere prijscategorie model uit ASEv2. In ASEv1 betaalt u voor elke core toegewezen. Dat betekent onder meer kernen gebruikt voor de front-ends of workers die werkbelastingen worden niet als host. Hallo standaardgrootte maximale schaal van een as-omgeving is in ASEv1, 55 totale hosts. Die bevat werknemers en -front-ends. Een voordeel tooASEv1 is dat deze kan worden geïmplementeerd in een klassiek virtueel netwerk en een virtueel netwerk van Resource Manager. toolearn meer informatie over ASEv1, Zie [App Service-omgeving v1 inleiding][ASEv1Intro].

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
