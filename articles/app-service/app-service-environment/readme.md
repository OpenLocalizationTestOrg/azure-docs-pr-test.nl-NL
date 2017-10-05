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
# <a name="app-service-environment-documentation"></a><span data-ttu-id="4703a-103">Documentatie voor App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="4703a-103">App Service environment documentation</span></span>
 <span data-ttu-id="4703a-104">Azure App Service-omgeving is een Azure App Service-functie een volledig geïsoleerde en toegewezen omgeving biedt voor het uitvoeren van App Service-apps veilig op grote schaal.</span><span class="sxs-lookup"><span data-stu-id="4703a-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="4703a-105">Deze mogelijkheid kan hosten uw [web-apps][webapps], [mobiele apps][mobileapps], [API-apps] [ APIApps], en [functies][Functions].</span><span class="sxs-lookup"><span data-stu-id="4703a-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="4703a-106">App Service-omgevingen (ASEs) zijn ideaal voor toepassingsworkloads die vereisen:</span><span class="sxs-lookup"><span data-stu-id="4703a-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="4703a-107">Zeer grote schaal.</span><span class="sxs-lookup"><span data-stu-id="4703a-107">Very high scale.</span></span>
* <span data-ttu-id="4703a-108">Isolatie en beveiligde netwerktoegang.</span><span class="sxs-lookup"><span data-stu-id="4703a-108">Isolation and secure network access.</span></span>

<span data-ttu-id="4703a-109">Klanten kunnen meerdere ASEs binnen één Azure-regio en tussen meerdere Azure-regio's maken.</span><span class="sxs-lookup"><span data-stu-id="4703a-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="4703a-110">Deze veelzijdigheid maakt ASEs ideaal voor stateless toepassingslagen ter ondersteuning van werklasten met hoge RPS horizontaal schalen.</span><span class="sxs-lookup"><span data-stu-id="4703a-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="4703a-111">ASEs zijn geïsoleerd, zodat slechts één klant toepassingen uitvoeren en altijd in een Azure-netwerk worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4703a-111">ASEs are isolated to running only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="4703a-112">Klanten hebben fijnmazig controle over de toepassing voor binnenkomend en uitgaand netwerkverkeer met behulp van [Netwerkbeveiligingsgroepen][NSGs].</span><span class="sxs-lookup"><span data-stu-id="4703a-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="4703a-113">Toepassingen kunnen ook tot stand brengen snelle beveiligde verbindingen via virtuele netwerken met lokale bedrijfsbronnen.</span><span class="sxs-lookup"><span data-stu-id="4703a-113">Applications can also establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="4703a-114">Apps moeten vaak toegang tot bedrijfsbronnen, zoals interne databases en -services.</span><span class="sxs-lookup"><span data-stu-id="4703a-114">Apps frequently need to access corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="4703a-115">Apps die worden uitgevoerd op ASEs toegang tot bronnen via [site-naar-site] [ SiteToSite] VPN en [Azure ExpressRoute] [ ExpressRoute] verbindingen.</span><span class="sxs-lookup"><span data-stu-id="4703a-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="4703a-116">[Wat is een App Service-omgeving?][Intro]</span><span class="sxs-lookup"><span data-stu-id="4703a-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="4703a-117">[Een App Service-omgeving maken][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="4703a-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="4703a-118">[Een interne load balancer-App Service-omgeving maken][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="4703a-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="4703a-119">[Gebruik van een App Service-omgeving][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="4703a-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="4703a-120">[Aandachtspunten voor netwerken en de App Service-omgeving][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="4703a-120">[Networking considerations and the App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="4703a-121">[Een App Service-omgeving te maken van een sjabloon][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="4703a-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="4703a-122">Video's</span><span class="sxs-lookup"><span data-stu-id="4703a-122">Videos</span></span>
<span data-ttu-id="4703a-123">Gebruik moderne PaaS voor bedrijven met Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4703a-123">Master Modern PaaS for the Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="4703a-124">Zeer schaalbare en beveiligde apps implementeren</span><span class="sxs-lookup"><span data-stu-id="4703a-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="4703a-125">Web- en mobiele apps voor bedrijven uitvoeren op Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4703a-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="4703a-126">App Service-omgeving v1</span><span class="sxs-lookup"><span data-stu-id="4703a-126">App Service Environment v1</span></span> ##
<span data-ttu-id="4703a-127">Er zijn twee versies van App Service-omgeving: ASEv1 en ASEv2.</span><span class="sxs-lookup"><span data-stu-id="4703a-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="4703a-128">Zie voor informatie over ASEv1, [App Service-omgeving v1 documentatie][ASEv1README].</span><span class="sxs-lookup"><span data-stu-id="4703a-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


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
