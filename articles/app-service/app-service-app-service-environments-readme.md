---
title: App Service-omgeving | Microsoft Docs
description: Wat is een Azure App Service-omgeving? Een inleiding tot de App Service-omgeving.
keywords: Azure app service-omgeving, virtueel netwerk netwerkbeveiliging
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1de3f2c513f4f5ce6fd2ab2b57514122955a9a98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-environment-documentation"></a>Documentatie voor App Service-omgeving
Een App Service-omgeving is een [Premium] [ PremiumTier] service-plan optie van Azure App Service die een volledig geïsoleerde en toegewezen omgeving biedt voor het uitvoeren van Azure App Service-apps veilig op grote schaal, met inbegrip van [Web-Apps][WebApps], [Mobile Apps][MobileApps], en [API Apps][APIApps].  

App Service-omgevingen zijn ideaal voor toepassingsworkloads vereisen:

* Zeer grote schaal
* Isolatie en beveiligde netwerktoegang

Klanten kunnen meerdere App Service-omgevingen binnen één Azure-regio, evenals over meerdere Azure-regio's maken.  Dit maakt App Service-omgevingen ideaal voor horizontaal schalen status minder toepassingslagen ter ondersteuning van werklasten met hoge RPS.

App Service-omgevingen zijn geïsoleerd, zodat slechts één klant toepassingen uitvoeren en altijd in een virtueel netwerk worden geïmplementeerd.  Klanten hebben fijnmazig controle over beide gebruikt voor het verkeer inkomend en uitgaand toepassing netwerk [netwerkbeveiligingsgroepen][NetworkSecurityGroups].  Toepassingen kunnen ook tot stand brengen snelle beveiligde verbindingen via virtuele netwerken met lokale bedrijfsbronnen.

Apps moeten vaak toegang tot bedrijfsbronnen zoals interne databases en -services.  Apps die worden uitgevoerd op App Service-omgevingen toegang tot bronnen bereikbaar is via [Site-naar-Site] [ SiteToSite] VPN en [Azure ExpressRoute] [ ExpressRoute] verbindingen.

* [Wat is een App Service-omgeving?](../app-service-web/app-service-app-service-environment-intro.md)
* [Een App Service-omgeving maken](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [Apps in een App Service-omgeving maken](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Maken en gebruiken van een interne Load Balancer met App Service-omgevingen](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [Een App Service-omgeving configureren](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [Apps schalen in een App Service-omgeving](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [Netwerkbeveiliging en architectuur](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a>Hoe van
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a>Video's
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
