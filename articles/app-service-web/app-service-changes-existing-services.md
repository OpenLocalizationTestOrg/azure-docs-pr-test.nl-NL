---
title: aaaAzure App Service en de invloed ervan op bestaande Azure services
description: Legt uit hoe Hallo nieuwe Azure App Service en de functies gevolgen voor bestaande services in Azure.
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="98d8b-103">Azure App Service en bestaande Azure-services</span><span class="sxs-lookup"><span data-stu-id="98d8b-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="98d8b-104">In dit artikel bevat een overzicht van Hallo wijzigingen tooexisting Azure-services als onderdeel van Hallo wijziging toobring samen verschillende Azure-services in [Azure App Service](https://azure.microsoft.com/services/app-service/), een nieuwe geïntegreerde aanbieding.</span><span class="sxs-lookup"><span data-stu-id="98d8b-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="98d8b-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="98d8b-105">Overview</span></span>
<span data-ttu-id="98d8b-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is een nieuwe en unieke cloudservice waarmee ontwikkelaars toocreate web- en mobiele apps voor elk platform en elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="98d8b-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="98d8b-107">App Service is dat een geïntegreerde oplossing ontworpen toostreamline herhaald codering functies, integreren met enterprise- en SaaS-systemen en bedrijfsprocessen te automatiseren en te voldoen aan uw behoeften voor beveiliging, betrouwbaarheid en schaalbaarheid.</span><span class="sxs-lookup"><span data-stu-id="98d8b-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="98d8b-108">App Service samenbrengt Hallo volgende op bestaande Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), en [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) gecombineerd in één service, terwijl krachtige nieuwe mogelijkheden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="98d8b-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="98d8b-109">App Service kunt u toohost Hallo volgende app-typen:</span><span class="sxs-lookup"><span data-stu-id="98d8b-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="98d8b-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="98d8b-110">Web Apps</span></span>
* <span data-ttu-id="98d8b-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="98d8b-111">Mobile Apps</span></span>
* <span data-ttu-id="98d8b-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="98d8b-112">API Apps</span></span>
* <span data-ttu-id="98d8b-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="98d8b-113">Logic Apps</span></span>

<span data-ttu-id="98d8b-114">Hallo volgende tabel wordt uitgelegd hoe bestaande Azure services tooApp-Service en Hallo typen Apps die beschikbaar zijn binnen deze worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="98d8b-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="98d8b-115">Bestaande Azure-Service</span><span class="sxs-lookup"><span data-stu-id="98d8b-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="98d8b-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="98d8b-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="98d8b-117">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="98d8b-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="98d8b-118">Azure Websites</span><span class="sxs-lookup"><span data-stu-id="98d8b-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="98d8b-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="98d8b-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="98d8b-120">App Service is voor Azure Websites strikt beperkt toochanging Hallo naam Websites tooWeb Apps.</span><span class="sxs-lookup"><span data-stu-id="98d8b-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="98d8b-121">Uw bestaande exemplaren van Websites zijn nu Web-Apps in App Service.</span><span class="sxs-lookup"><span data-stu-id="98d8b-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="98d8b-122">U kunt toegang tot uw bestaande websites via Hallo <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, waarbij vindt u alle bestaande sites onder <em>Web-Apps</em>.</span><span class="sxs-lookup"><span data-stu-id="98d8b-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="98d8b-123"><em>Web-Hosting plannen</em> is nu <em>App Service-Plan</em>.</span><span class="sxs-lookup"><span data-stu-id="98d8b-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="98d8b-124">Een <em>App Service-Plan</em> elk type app van App Service, zoals Web-, mobiele, logische of API-apps kunnen hosten.</span><span class="sxs-lookup"><span data-stu-id="98d8b-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="98d8b-125">Azure App Service Web Apps is in het algemeen beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="98d8b-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="98d8b-126"><a href="http://azure.microsoft.com/services/app-service/web/">Meer informatie over Web-Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="98d8b-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="98d8b-127">Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="98d8b-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="98d8b-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="98d8b-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="98d8b-129">Mobile Services toobe beschikbaar als zelfstandige service blijven en blijven volledig wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="98d8b-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="98d8b-130">Mobiele Apps is een app in App Service, die kan worden geïntegreerd Hallo-functionaliteit van Mobile Services en meer.</span><span class="sxs-lookup"><span data-stu-id="98d8b-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="98d8b-131">Het is te eenvoudig<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migreren van Mobile Services tooMobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="98d8b-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="98d8b-132">Als onderdeel van App Service ophalen Mobile Apps nieuwe mogelijkheden buiten Mobile Services, zoals integratie met on-premises en SaaS-systemen, sleuven, WebJobs en beter schalingsopties voor fasering.</span><span class="sxs-lookup"><span data-stu-id="98d8b-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="98d8b-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Meer informatie over Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="98d8b-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="98d8b-134">API-apps</span><span class="sxs-lookup"><span data-stu-id="98d8b-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="98d8b-135">API-Apps is een nieuw type app in App Service waarmee u eenvoudig bouwen en API's in de cloud hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="98d8b-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="98d8b-136"><a href="http://azure.microsoft.com/services/app-service/api/">Meer informatie over API-Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="98d8b-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="98d8b-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="98d8b-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="98d8b-138">Logic Apps is een nieuw type app in App Service waarmee u eenvoudig bedrijfsprocessen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="98d8b-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="98d8b-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Meer informatie over Logic Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="98d8b-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="98d8b-140">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="98d8b-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="98d8b-141">BizTalk API Apps</span><span class="sxs-lookup"><span data-stu-id="98d8b-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="98d8b-142">BizTalk Services toobe beschikbaar als zelfstandige service blijven en blijven volledig wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="98d8b-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="98d8b-143">Alle Hallo-mogelijkheden van BizTalk Services zijn geïntegreerd in App Service API-Apps inschakelen gebruikers tooperform integratie van bedrijfstoepassingen en B2B integratiescenario's met een van de app-typen Hallo in App Service.</span><span class="sxs-lookup"><span data-stu-id="98d8b-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="98d8b-144">Met Logic Apps kunt u nu gebruik van een visuele ontwerp ervaring toocreate werkstromen bedrijfsprocessen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="98d8b-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="98d8b-145">toolearn meer, gaat u naar [App Service-documentatie](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="98d8b-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

