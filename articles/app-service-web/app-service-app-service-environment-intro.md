---
title: Inleiding tot de App Service-omgeving v1
description: Meer informatie over de App Service-omgeving v1-functie met beveiligde, die lid zijn van VNet, toegewezen schaaleenheden voor het uitvoeren van uw apps.
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
ms.openlocfilehash: 38cb79eb32bd61cdbfb6da91d50e6713d71a2b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environment-v1"></a><span data-ttu-id="193bd-103">Inleiding tot de App Service-omgeving v1</span><span class="sxs-lookup"><span data-stu-id="193bd-103">Introduction to App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="193bd-104">In dit artikel gaat over de v1 App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="193bd-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="193bd-105">Er is een nieuwere versie van de App Service-omgeving die eenvoudiger te gebruiken en wordt uitgevoerd op krachtiger infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="193bd-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="193bd-106">Voor meer informatie over de nieuwe versie begin met het [Inleiding tot de App-serviceomgeving](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="193bd-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="193bd-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="193bd-107">Overview</span></span>
<span data-ttu-id="193bd-108">Een App Service-omgeving is een [Premium] [ PremiumTier] service-plan optie van Azure App Service die een volledig geïsoleerde en toegewezen omgeving biedt voor het uitvoeren van Azure App Service-apps veilig op grote schaal, met inbegrip van [Web-Apps][WebApps], [Mobile Apps][MobileApps], en [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="193bd-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="193bd-109">App Service-omgevingen zijn ideaal voor toepassingsworkloads vereisen:</span><span class="sxs-lookup"><span data-stu-id="193bd-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="193bd-110">Zeer grote schaal</span><span class="sxs-lookup"><span data-stu-id="193bd-110">Very high scale</span></span>
* <span data-ttu-id="193bd-111">Isolatie en beveiligde netwerktoegang</span><span class="sxs-lookup"><span data-stu-id="193bd-111">Isolation and secure network access</span></span>

<span data-ttu-id="193bd-112">Klanten kunnen meerdere App Service-omgevingen binnen één Azure-regio, evenals over meerdere Azure-regio's maken.</span><span class="sxs-lookup"><span data-stu-id="193bd-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="193bd-113">Dit maakt App Service-omgevingen ideaal voor horizontaal schalen status minder toepassingslagen ter ondersteuning van werklasten met hoge RPS.</span><span class="sxs-lookup"><span data-stu-id="193bd-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="193bd-114">App Service-omgevingen zijn geïsoleerd, zodat slechts één klant toepassingen uitvoeren en altijd in een virtueel netwerk worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="193bd-114">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="193bd-115">Klanten hebben fijnmazig controle over beide-toepassing voor binnenkomend en uitgaand netwerkverkeer en toepassingen kunnen verbinding maken snelle beveiligde verbindingen via virtuele netwerken met lokale bedrijfsbronnen.</span><span class="sxs-lookup"><span data-stu-id="193bd-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="193bd-116">Alle artikelen en hoe-aan de over App Service-omgevingen zijn beschikbaar in de [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="193bd-116">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="193bd-117">Voor een overzicht van hoe App Service-omgevingen grote schaal inschakelen en beveiligde netwerktoegang, Zie de [AzureCon diepgaand] [ AzureConDeepDive] op App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="193bd-117">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="193bd-118">Voor een dieper in op horizontaal schalen met meerdere App Service-omgevingen Zie het artikel over de installatie een [geografisch verspreide app footprint][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="193bd-118">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="193bd-119">Hoe de beveiligingsarchitectuur weergegeven in de diepgaand AzureCon is geconfigureerd, Zie het artikel over het implementeren van een [beveiligingsarchitectuur gelaagde](app-service-app-service-environment-layered-security.md) met App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="193bd-119">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="193bd-120">Apps die worden uitgevoerd op App Service-omgevingen kunnen de geregeld door de upstream-apparaten, zoals web application Firewall (WAF) toegang hebben.</span><span class="sxs-lookup"><span data-stu-id="193bd-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="193bd-121">Het artikel over [een WAF configureren voor App Service-omgevingen](app-service-app-service-environment-web-application-firewall.md) bevat informatie over dit scenario.</span><span class="sxs-lookup"><span data-stu-id="193bd-121">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="193bd-122">Speciale berekenings-Resources</span><span class="sxs-lookup"><span data-stu-id="193bd-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="193bd-123">Alle resources in een App-serviceomgeving compute zijn toegewezen aan één abonnement en een App Service-omgeving kan worden geconfigureerd met maximaal vijftig (50) rekenresources voor exclusief gebruik door één toepassing.</span><span class="sxs-lookup"><span data-stu-id="193bd-123">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="193bd-124">Een App Service-omgeving bestaat uit een front-compute-resourcegroep, evenals één tot drie worker compute resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="193bd-124">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span></span> 

<span data-ttu-id="193bd-125">De front-groep bevat de rekenresources die verantwoordelijk is voor SSL-beëindiging als ook automatische taakverdeling van app-aanvragen in een App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="193bd-125">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="193bd-126">Elke worker-groep bevat rekenresources die zijn toegewezen aan [App Service-abonnementen][AppServicePlan], die een of meer Azure App Service-apps op hun beurt bevatten.</span><span class="sxs-lookup"><span data-stu-id="193bd-126">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="193bd-127">Omdat er kunnen maximaal drie verschillende werknemersgroepen in een App Service-omgeving, kunt u hebt de flexibiliteit om te kiezen verschillende rekenresources voor elke worker-groep.</span><span class="sxs-lookup"><span data-stu-id="193bd-127">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="193bd-128">Bijvoorbeeld: Hiermee kunt u één worker-groep maken met minder krachtige rekenresources voor App Service-abonnementen die bestemd zijn voor ontwikkeling of tests apps.</span><span class="sxs-lookup"><span data-stu-id="193bd-128">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="193bd-129">Een tweede (of zelfs derde) werknemersgroep kan krachtiger rekenresources die bestemd zijn voor het App Service-abonnementen met productie-apps gebruiken.</span><span class="sxs-lookup"><span data-stu-id="193bd-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="193bd-130">Zie voor meer informatie over de hoeveelheid beschikbaar is op de front- en werkrollen opslaggroepen rekenresources [het configureren van een App-serviceomgeving][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="193bd-130">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="193bd-131">Voor meer informatie over de beschikbare compute resource grootten die worden ondersteund in een App Service-omgeving, Raadpleeg de [prijzen van App Service] [ AppServicePricing] pagina en bekijk de beschikbare opties voor App Service-omgevingen in de prijscategorie Premium.</span><span class="sxs-lookup"><span data-stu-id="193bd-131">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="193bd-132">Virtual Network-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="193bd-132">Virtual Network Support</span></span>
<span data-ttu-id="193bd-133">Een App Service-omgeving kunnen worden gemaakt in **beide** een virtueel netwerk van Azure Resource Manager, **of** een virtueel netwerk voor klassieke implementatie-model ([meer informatie over virtuele netwerken][MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="193bd-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="193bd-134">Omdat een App Service-omgeving altijd in een virtueel netwerk en nauwkeuriger binnen een subnet van een virtueel netwerk bestaat, kunt u gebruikmaken van de beveiligingsfuncties van virtuele netwerken om te beheren, zowel binnenkomend en uitgaand netwerkcommunicatie.</span><span class="sxs-lookup"><span data-stu-id="193bd-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span></span>  

<span data-ttu-id="193bd-135">Een App Service-omgeving kan worden beide Internetgericht met een openbaar IP-adres of interne geconfronteerd met alleen een adres Azure interne Load Balancer (ILB).</span><span class="sxs-lookup"><span data-stu-id="193bd-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="193bd-136">U kunt [netwerkbeveiligingsgroepen] [ NetworkSecurityGroups] te beperken van binnenkomende netwerkcommunicatie met het subnet waarin een App Service-omgeving zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="193bd-136">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="193bd-137">Hiermee kunt u apps achter upstream apparaten en services, zoals web application firewalls en aanbieders van SaaS-netwerk uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="193bd-137">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="193bd-138">Apps moeten ook vaak toegang tot bedrijfsbronnen zoals interne databases en -services.</span><span class="sxs-lookup"><span data-stu-id="193bd-138">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="193bd-139">Vaak wordt deze eindpunten om beschikbaar te maken alleen voor interne netwerkverkeer dat binnen een virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="193bd-139">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="193bd-140">Zodra een App-serviceomgeving is toegevoegd aan hetzelfde virtuele netwerk als de interne services, apps die worden uitgevoerd in de omgeving ze toegankelijk zijn, inclusief eindpunten bereikbaar is via [Site-naar-Site] [ SiteToSite] en [Azure ExpressRoute] [ ExpressRoute] verbindingen.</span><span class="sxs-lookup"><span data-stu-id="193bd-140">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="193bd-141">Voor meer informatie over de werking van App Service-omgevingen met virtuele netwerken en on-premises netwerken raadpleegt u de volgende artikelen op [netwerkarchitectuur][NetworkArchitectureOverview], [binnenkomend verkeer beheren][ControllingInboundTraffic], en [veilig verbinding te maken met back-ends][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="193bd-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="193bd-142">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="193bd-142">Getting started</span></span>
<span data-ttu-id="193bd-143">Om aan de slag met App Service-omgevingen, Zie [hoe te maken van een App Service-omgeving][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="193bd-143">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="193bd-144">Alle artikelen en hoe-aan de voor App Service-omgevingen zijn beschikbaar in de [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="193bd-144">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="193bd-145">Zie voor meer informatie over het Azure App Service-platform [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="193bd-145">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="193bd-146">Zie voor een overzicht van de App Service-omgeving netwerkarchitectuur de [netwerk architectuuroverzicht] [ NetworkArchitectureOverview] artikel.</span><span class="sxs-lookup"><span data-stu-id="193bd-146">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="193bd-147">Zie voor meer informatie over het gebruik van een App Service-omgeving met ExpressRoute, het volgende artikel op [Express Route- en App Service-omgevingen][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="193bd-147">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


