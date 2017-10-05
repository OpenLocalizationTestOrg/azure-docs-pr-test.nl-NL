---
title: Azure App Service-omgeving Leesmij-bestand
description: Geeft een lijst van de documentatie die Azure App Service-omgeving beschrijft
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 5b1362854dbc3b0098718bd2ea3cffb06366000c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="app-service-environment-documentation"></a>Documentatie voor App Service-omgeving
 Azure App Service-omgeving is een Azure App Service-functie een volledig geïsoleerde en toegewezen omgeving biedt voor het uitvoeren van App Service-apps veilig op grote schaal. Deze mogelijkheid kan hosten uw [web-apps][webapps], [mobiele apps][mobileapps], [API-apps] [ APIApps], en [functies][Functions].

App Service-omgevingen (ASEs) zijn ideaal voor toepassingsworkloads die vereisen:

* Zeer grote schaal.
* Isolatie en beveiligde netwerktoegang.

Klanten kunnen meerdere ASEs binnen één Azure-regio en tussen meerdere Azure-regio's maken. Deze veelzijdigheid maakt ASEs ideaal voor stateless toepassingslagen ter ondersteuning van werklasten met hoge RPS horizontaal schalen.

ASEs zijn geïsoleerd, zodat slechts één klant toepassingen uitvoeren en altijd in een Azure-netwerk worden geïmplementeerd. Klanten hebben fijnmazig controle over de toepassing voor binnenkomend en uitgaand netwerkverkeer met behulp van [Netwerkbeveiligingsgroepen][NSGs]. Toepassingen kunnen ook tot stand brengen snelle beveiligde verbindingen via virtuele netwerken met lokale bedrijfsbronnen.

Apps moeten vaak toegang tot bedrijfsbronnen, zoals interne databases en -services. Apps die worden uitgevoerd op ASEs toegang tot bronnen via [site-naar-site] [ SiteToSite] VPN en [Azure ExpressRoute] [ ExpressRoute] verbindingen.

* [Wat is een App Service-omgeving?][Intro]
* [Een App Service-omgeving maken][MakeExternalASE]
* [Een interne load balancer-App Service-omgeving maken][MakeILBASE]
* [Gebruik van een App Service-omgeving][UsingASE]
* [Aandachtspunten voor netwerken en de App Service-omgeving][ASENetwork]
* [Een App Service-omgeving te maken van een sjabloon][MakeASEfromTemplate]


## <a name="videos"></a>Video's
Gebruik moderne PaaS voor bedrijven met Azure App Service
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

Zeer schaalbare en beveiligde apps implementeren
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

Web- en mobiele apps voor bedrijven uitvoeren op Azure App Service
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a>App Service-omgeving v1 ##
Er zijn twee versies van App Service-omgeving: ASEv1 en ASEv2. Zie voor informatie over ASEv1, [App Service-omgeving v1 documentatie][ASEv1README].


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
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
