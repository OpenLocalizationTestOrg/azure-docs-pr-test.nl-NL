---
title: aaaIntroduction tooApp Service-omgeving v1
description: Meer informatie over App Service-omgeving v1 Hallo-functie met beveiligde, die lid zijn van VNet, toegewezen schaaleenheden voor het uitvoeren van uw apps.
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a>Inleiding tooApp Service-omgeving v1

> [!NOTE]
> In dit artikel gaat over het Hallo v1 App Service-omgeving.  Er is een nieuwere versie van App Service-omgeving die eenvoudiger toouse en wordt uitgevoerd op krachtiger infrastructuur Hallo. meer informatie over de nieuwe versie Hallo met Hallo beginnen toolearn [inleiding toohello App Service-omgeving](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Overzicht
Een App Service-omgeving is een [Premium] [ PremiumTier] service-plan optie van Azure App Service die een volledig geïsoleerde en toegewezen omgeving biedt voor het uitvoeren van Azure App Service-apps veilig op grote schaal, met inbegrip van [Web-Apps][WebApps], [Mobile Apps][MobileApps], en [API Apps][APIApps].  

App Service-omgevingen zijn ideaal voor toepassingsworkloads vereisen:

* Zeer grote schaal
* Isolatie en beveiligde netwerktoegang

Klanten kunnen meerdere App Service-omgevingen binnen één Azure-regio, evenals over meerdere Azure-regio's maken.  Dit maakt App Service-omgevingen ideaal voor horizontaal schalen status minder toepassingslagen ter ondersteuning van werklasten met hoge RPS.

App Service-omgevingen zijn geïsoleerd toorunning alleen één klant toepassingen en altijd in een virtueel netwerk worden geïmplementeerd.  Klanten hebben fijnmazig controle over beide-toepassing voor binnenkomend en uitgaand netwerkverkeer en toepassingen kunnen verbinding maken van snelle beveiligde verbindingen via virtuele netwerken tooon-premises bedrijfsbronnen.

Alle artikelen en hoe-aan de over App Service-omgevingen zijn beschikbaar in Hallo [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

Voor een overzicht van hoe App Service-omgevingen grote schaal inschakelen en beveiligde netwerktoegang, Zie Hallo [AzureCon diepgaand] [ AzureConDeepDive] op App Service-omgevingen.

Voor een dieper in op horizontaal schalen met meerdere App Service-omgevingen raadpleegt u Hallo artikel over het toosetup een [geografisch verspreide app footprint][GeodistributedAppFootprint].

toosee hoe Hallo-beveiligingsarchitectuur weergegeven in Hallo AzureCon diepgaand is geconfigureerd, Zie Hallo artikel over het implementeren van een [beveiligingsarchitectuur gelaagde](app-service-app-service-environment-layered-security.md) met App Service-omgevingen.

Apps die worden uitgevoerd op App Service-omgevingen kunnen de geregeld door de upstream-apparaten, zoals web application Firewall (WAF) toegang hebben.  Hallo-artikel op [een WAF configureren voor App Service-omgevingen](app-service-app-service-environment-web-application-firewall.md) bevat informatie over dit scenario. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Speciale berekenings-Resources
Alle Hallo reken-en resources in een App Service-omgeving zijn uitsluitend tooa één abonnement hebt toegewezen en een App Service-omgeving kan worden geconfigureerd met up toofifty (50) rekenresources voor exclusief gebruik door één toepassing.

Een App Service-omgeving bestaat uit een front-compute-resourcegroep, evenals een toothree worker compute resourcegroepen. 

Hallo front-groep bevat rekenresources die verantwoordelijk is voor SSL-beëindiging als ook automatische taakverdeling van app-aanvragen in een App Service-omgeving. 

Elke worker-groep bevat rekenresources te toegewezen[App Service-abonnementen][AppServicePlan], die een of meer Azure App Service-apps op hun beurt bevatten.  Aangezien er van de verschillende werknemersgroepen toothree in een App Service-omgeving zijn kunnen, hebben Hallo flexibiliteit toochoose verschillende rekenresources voor elke worker-groep.  

Bijvoorbeeld: Hiermee kunt u een werknemersgroep toocreate met minder krachtige rekenresources voor App Service-abonnementen die bestemd zijn voor ontwikkeling of tests apps.  Een tweede (of zelfs derde) werknemersgroep kan krachtiger rekenresources die bestemd zijn voor het App Service-abonnementen met productie-apps gebruiken.

Zie voor meer informatie over Hallo hoeveelheid compute resources beschikbaar toohello front-end- en werknemersgroepen [hoe tooConfigure een App-serviceomgeving][HowToConfigureanAppServiceEnvironment].  

Voor meer informatie over beschikbare Hallo resource grootten die worden ondersteund in een App Service-omgeving COMPUTE, raadpleegt u Hallo [prijzen van App Service] [ AppServicePricing] pagina en bekijk de beschikbare opties Hallo voor App Service-omgevingen in Hallo Premium prijscategorie.

## <a name="virtual-network-support"></a>Virtual Network-ondersteuning
Een App Service-omgeving kunnen worden gemaakt in **beide** een virtueel netwerk van Azure Resource Manager, **of** een virtueel netwerk voor klassieke implementatie-model ([meer informatie over virtuele netwerken][MoreInfoOnVirtualNetworks]).  Omdat een App Service-omgeving altijd in een virtueel netwerk en nauwkeuriger binnen een subnet van een virtueel netwerk bestaat, kunt u zowel binnenkomende en uitgaande netwerkcommunicatie Hallo beveiligingsfuncties van virtuele netwerken toocontrol gebruikmaken.  

Een App Service-omgeving kan worden beide Internetgericht met een openbaar IP-adres of interne geconfronteerd met alleen een adres Azure interne Load Balancer (ILB).

U kunt [netwerkbeveiligingsgroepen] [ NetworkSecurityGroups] toorestrict binnenkomende communicatie toohello netwerksubnet waarin een App Service-omgeving zich bevindt.  Hiermee kunt u apps toorun achter upstream apparaten en services, zoals web application firewalls en aanbieders van SaaS-netwerk.

Apps moeten ook regelmatig tooaccess bedrijfsbronnen zoals interne databases en webservices.  Een veelgebruikte oplossing is toomake deze eindpunten beschikbaar alleen toointernal netwerkverkeer binnen een virtuele Azure-netwerk.  Zodra een App-serviceomgeving lid toohello is hetzelfde virtuele netwerk als Hallo interne services, apps die worden uitgevoerd in de omgeving Hallo ze toegankelijk zijn, inclusief eindpunten bereikbaar is via [Site-naar-Site] [ SiteToSite]en [Azure ExpressRoute] [ ExpressRoute] verbindingen.

Voor meer informatie over de werking van App Service-omgevingen met virtuele netwerken en on-premises netwerken Raadpleeg Hallo artikelen op te volgen [netwerkarchitectuur][NetworkArchitectureOverview], [inkomende beheren Verkeer][ControllingInboundTraffic], en [veilig verbinding te maken tooBackends][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>Aan de slag
tooget de slag met App Service-omgevingen, Zie [hoe tooCreate een App Service-omgeving][HowToCreateAnAppServiceEnvironment]

Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service][AzureAppService].

Zie voor een overzicht van App Service-omgeving netwerkarchitectuur Hallo Hallo [netwerk architectuuroverzicht] [ NetworkArchitectureOverview] artikel.

Zie voor meer informatie over het gebruik van een App Service-omgeving met ExpressRoute, Hallo volgende artikel op [Express Route- en App Service-omgevingen][NetworkConfigDetailsForExpressRoute].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


