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
# <a name="app-service-environment-documentation"></a><span data-ttu-id="e1d01-105">Documentatie voor App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="e1d01-105">App Service Environment Documentation</span></span>
<span data-ttu-id="e1d01-106">Een App Service-omgeving is een [Premium] [ PremiumTier] service-plan optie van Azure App Service die een volledig geïsoleerde en toegewezen omgeving biedt voor het uitvoeren van Azure App Service-apps veilig op grote schaal, met inbegrip van [Web-Apps][WebApps], [Mobile Apps][MobileApps], en [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="e1d01-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="e1d01-107">App Service-omgevingen zijn ideaal voor toepassingsworkloads vereisen:</span><span class="sxs-lookup"><span data-stu-id="e1d01-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="e1d01-108">Zeer grote schaal</span><span class="sxs-lookup"><span data-stu-id="e1d01-108">Very high scale</span></span>
* <span data-ttu-id="e1d01-109">Isolatie en beveiligde netwerktoegang</span><span class="sxs-lookup"><span data-stu-id="e1d01-109">Isolation and secure network access</span></span>

<span data-ttu-id="e1d01-110">Klanten kunnen meerdere App Service-omgevingen binnen één Azure-regio, evenals over meerdere Azure-regio's maken.</span><span class="sxs-lookup"><span data-stu-id="e1d01-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="e1d01-111">Dit maakt App Service-omgevingen ideaal voor horizontaal schalen status minder toepassingslagen ter ondersteuning van werklasten met hoge RPS.</span><span class="sxs-lookup"><span data-stu-id="e1d01-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="e1d01-112">App Service-omgevingen zijn geïsoleerd, zodat slechts één klant toepassingen uitvoeren en altijd in een virtueel netwerk worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e1d01-112">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="e1d01-113">Klanten hebben fijnmazig controle over beide gebruikt voor het verkeer inkomend en uitgaand toepassing netwerk [netwerkbeveiligingsgroepen][NetworkSecurityGroups].</span><span class="sxs-lookup"><span data-stu-id="e1d01-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="e1d01-114">Toepassingen kunnen ook tot stand brengen snelle beveiligde verbindingen via virtuele netwerken met lokale bedrijfsbronnen.</span><span class="sxs-lookup"><span data-stu-id="e1d01-114">Applications can also establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="e1d01-115">Apps moeten vaak toegang tot bedrijfsbronnen zoals interne databases en -services.</span><span class="sxs-lookup"><span data-stu-id="e1d01-115">Apps frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="e1d01-116">Apps die worden uitgevoerd op App Service-omgevingen toegang tot bronnen bereikbaar is via [Site-naar-Site] [ SiteToSite] VPN en [Azure ExpressRoute] [ ExpressRoute] verbindingen.</span><span class="sxs-lookup"><span data-stu-id="e1d01-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="e1d01-117">Wat is een App Service-omgeving?</span><span class="sxs-lookup"><span data-stu-id="e1d01-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="e1d01-118">Een App Service-omgeving maken</span><span class="sxs-lookup"><span data-stu-id="e1d01-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="e1d01-119">Apps in een App Service-omgeving maken</span><span class="sxs-lookup"><span data-stu-id="e1d01-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="e1d01-120">Maken en gebruiken van een interne Load Balancer met App Service-omgevingen</span><span class="sxs-lookup"><span data-stu-id="e1d01-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="e1d01-121">Een App Service-omgeving configureren</span><span class="sxs-lookup"><span data-stu-id="e1d01-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="e1d01-122">Apps schalen in een App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="e1d01-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="e1d01-123">Netwerkbeveiliging en architectuur</span><span class="sxs-lookup"><span data-stu-id="e1d01-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="e1d01-124">Hoe van</span><span class="sxs-lookup"><span data-stu-id="e1d01-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="e1d01-125">Video's</span><span class="sxs-lookup"><span data-stu-id="e1d01-125">Videos</span></span>
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
