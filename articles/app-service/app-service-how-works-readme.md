---
title: aaaHow Azure App Service werkt
description: Ontdek hoe App Service werkt
keywords: App Service, Azure App Service, schaal, schaalbaar, App Service-abonnement, kosten App Service
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="676d6-104">De werking van App Service</span><span class="sxs-lookup"><span data-stu-id="676d6-104">How App Service works</span></span>
<span data-ttu-id="676d6-105">Azure App Service is een cloudservice die is ontworpen toosolve Hallo praktische problemen die engineers vandaag wordt geconfronteerd.</span><span class="sxs-lookup"><span data-stu-id="676d6-105">Azure App Service is a cloud service that's designed toosolve hello practical problems that engineers face today.</span></span>
<span data-ttu-id="676d6-106">App Service richt zich op het bieden van de productiviteit van ontwikkelaars bovenliggende gevaar op Hallo nodig toodeliver toepassingen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="676d6-106">App Service focuses on providing superior developer productivity without compromising on hello need toodeliver applications at cloud scale.</span></span> 

<span data-ttu-id="676d6-107">App Service biedt ook Hallo functies en frameworks die nodig zijn voor het maken van enterprise line-of-business-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="676d6-107">App Service also provides hello features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="676d6-108">App Service kunt u het ontwikkelen van apps in de populairste ontwikkelingstalen, met inbegrip van Java, PHP, Node.js, Python en Hallo Microsoft .NET-talen.</span><span class="sxs-lookup"><span data-stu-id="676d6-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and hello Microsoft .NET languages.</span></span> <span data-ttu-id="676d6-109">Met App Service kunt u:</span><span class="sxs-lookup"><span data-stu-id="676d6-109">With App Service, you can:</span></span>

* <span data-ttu-id="676d6-110">Zeer schaalbare web-apps ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="676d6-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="676d6-111">Snel back-ends van mobiele apps maken met een set gebruiksvriendelijke mobiele mogelijkheden, zoals gegevensback-ends, gebruikersverificatie en pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="676d6-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="676d6-112">API's implementeren en publiceren met API Apps.</span><span class="sxs-lookup"><span data-stu-id="676d6-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="676d6-113">Zakelijke toepassingen met elkaar verbinden in werkstromen en gegevens transformeren met Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="676d6-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="676d6-114">Alle app-typen zijn afhankelijk van Hallo schaalbare en flexibele Web-Apps platform, waardoor ontwikkelaars toohave een geoptimaliseerde volledige levenscyclus van app-ontwerp tooapp onderhoud optreden.</span><span class="sxs-lookup"><span data-stu-id="676d6-114">All app types rely on hello scalable and flexible Web Apps platform, which enables developers toohave an optimized full lifecycle experience from app design tooapp maintenance.</span></span> <span data-ttu-id="676d6-115">Hallo levenscyclusmogelijkheden inschakelen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="676d6-115">hello lifecycle capabilities enable hello following:</span></span>

* <span data-ttu-id="676d6-116">**Snel apps maken**.</span><span class="sxs-lookup"><span data-stu-id="676d6-116">**Quick app creation**.</span></span> <span data-ttu-id="676d6-117">Start vanaf het begin of kies een pakket operationele ondersteuningssysteem (besturingssystemen) van hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="676d6-117">Start from scratch or pick an operational support system (OSS) package from hello Azure Marketplace.</span></span>
* <span data-ttu-id="676d6-118">**Doorlopende implementatie**.</span><span class="sxs-lookup"><span data-stu-id="676d6-118">**Continuous deployment**.</span></span> <span data-ttu-id="676d6-119">Implementeer nieuwe code automatisch uit populaire broncodebeheeroplossingen zoals TFS, GitHub en BitBucket en synchroniseer inhoud van onlineopslagservices zoals OneDrive en DropBox.</span><span class="sxs-lookup"><span data-stu-id="676d6-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="676d6-120">**Testen tijdens productie**.</span><span class="sxs-lookup"><span data-stu-id="676d6-120">**Test in production**.</span></span> <span data-ttu-id="676d6-121">Soepel pre-productieomgevingen maken en beheren van Hallo hoeveelheid verkeer dat toothem wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="676d6-121">Smoothly create pre-production environments and manage hello amount of traffic that's going toothem.</span></span> <span data-ttu-id="676d6-122">Fouten opsporen in Hallo cloud wanneer nodig en rol weer wanneer er problemen zijn gevonden.</span><span class="sxs-lookup"><span data-stu-id="676d6-122">Debug in hello cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="676d6-123">**Asynchrone taken en batchopdrachten uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="676d6-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="676d6-124">Voer code uit in een achtergrondproces of activeer uw code op basis van gebeurtenissen (zoals berichten die terechtkomen in een Azure Storage-wachtrij) en geplande tijden (CRON).</span><span class="sxs-lookup"><span data-stu-id="676d6-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="676d6-125">**Schalen Hallo app**.</span><span class="sxs-lookup"><span data-stu-id="676d6-125">**Scaling hello app**.</span></span> <span data-ttu-id="676d6-126">Gebruik een van de vele opties tooautomatically schaal uw service horizontaal en verticaal op basis van verkeer en resourceverbruik gebruik.</span><span class="sxs-lookup"><span data-stu-id="676d6-126">Use one of many options tooautomatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="676d6-127">Persoonlijke omgevingen die toegewezen tooyour apps zijn configureren.</span><span class="sxs-lookup"><span data-stu-id="676d6-127">Configure private environments that are dedicated tooyour apps.</span></span>   
* <span data-ttu-id="676d6-128">**Beheren van Hallo app**.</span><span class="sxs-lookup"><span data-stu-id="676d6-128">**Maintaining hello app**.</span></span> <span data-ttu-id="676d6-129">Gebruikmaken van vele Hallo foutopsporing en diagnostische gegevens functies toostay tevoren problemen en tooefficiently in realtime (met functies zoals automatisch herstel en live foutopsporing) omzetten of na Hallo feit door te analyseren in Logboeken en dumpbestanden.</span><span class="sxs-lookup"><span data-stu-id="676d6-129">Use many of hello debugging and diagnostics features toostay ahead of problems and tooefficiently resolve them either in real time (with features such as auto-healing and live debugging) or after hello fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="676d6-130">Als een geheel mogelijkheden van App Service inschakelen ontwikkelaars toofocus op hun code en snel een stabiele en zeer schaalbare productiestatus bereiken.</span><span class="sxs-lookup"><span data-stu-id="676d6-130">As a whole, App Service capabilities enable developers toofocus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="676d6-131">Hallo API-Apps en Logic Apps-functies, kunnen ontwikkelaars zakelijke toepassingen die barrières tussen bedrijfsoplossingen en on-premises toocloud integratie overbruggen.</span><span class="sxs-lookup"><span data-stu-id="676d6-131">With hello API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises toocloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="676d6-132">Video's</span><span class="sxs-lookup"><span data-stu-id="676d6-132">Videos</span></span>
* [<span data-ttu-id="676d6-133">Azure App Service-architectuur</span><span class="sxs-lookup"><span data-stu-id="676d6-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="676d6-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="676d6-134">Next steps</span></span>

<span data-ttu-id="676d6-135">Meer informatie over App Service in een van de volgende onderwerpen Hallo:</span><span class="sxs-lookup"><span data-stu-id="676d6-135">Learn more about App Service in one of hello following topics:</span></span>

* [<span data-ttu-id="676d6-136">Wat is Azure App Service?</span><span class="sxs-lookup"><span data-stu-id="676d6-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="676d6-137">Web-app</span><span class="sxs-lookup"><span data-stu-id="676d6-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="676d6-138">Mobiele app</span><span class="sxs-lookup"><span data-stu-id="676d6-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="676d6-139">API-app</span><span class="sxs-lookup"><span data-stu-id="676d6-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="676d6-140">Azure App Service-architectuur (presentatie)</span><span class="sxs-lookup"><span data-stu-id="676d6-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="676d6-141">Vergelijking van Azure App Service, Cloud Services en Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="676d6-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="676d6-142">App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="676d6-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="676d6-143">Inleiding tooApp Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="676d6-143">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="676d6-144">Oefening: een App Service-omgeving maken</span><span class="sxs-lookup"><span data-stu-id="676d6-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="676d6-145">Ondersteuning voor Azure App Service-ontwikkelingsstacks</span><span class="sxs-lookup"><span data-stu-id="676d6-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



