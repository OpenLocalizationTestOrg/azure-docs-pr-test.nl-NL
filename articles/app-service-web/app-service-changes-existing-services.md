---
title: Azure App Service en de invloed ervan op bestaande Azure services
description: Legt uit hoe de nieuwe Azure App Service en de bijbehorende functies invloed zijn op bestaande services in Azure.
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
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="96ff1-103">Azure App Service en bestaande Azure-services</span><span class="sxs-lookup"><span data-stu-id="96ff1-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="96ff1-104">In dit artikel bevat een overzicht van de wijzigingen in bestaande Azure services als onderdeel van de verschillende Azure-services in samengebracht [Azure App Service](https://azure.microsoft.com/services/app-service/), een nieuwe geïntegreerde aanbieding.</span><span class="sxs-lookup"><span data-stu-id="96ff1-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="96ff1-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="96ff1-105">Overview</span></span>
<span data-ttu-id="96ff1-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is een nieuwe en unieke cloudservice waarmee ontwikkelaars kunnen maken van web- en mobiele apps voor elk platform en elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="96ff1-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="96ff1-107">App Service is een geïntegreerde oplossing die is ontworpen om te stroomlijnen herhaalde codering functies, integreren met enterprise- en SaaS-systemen en bedrijfsprocessen te automatiseren en te voldoen aan uw behoeften voor beveiliging, betrouwbaarheid en schaalbaarheid.</span><span class="sxs-lookup"><span data-stu-id="96ff1-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="96ff1-108">App Service verenigt de volgende bestaande Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), en [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) gecombineerd in één service, tijdens het toevoegen van krachtige nieuwe mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="96ff1-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="96ff1-109">App Service kunt u voor het hosten van de volgende typen Apps:</span><span class="sxs-lookup"><span data-stu-id="96ff1-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="96ff1-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="96ff1-110">Web Apps</span></span>
* <span data-ttu-id="96ff1-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="96ff1-111">Mobile Apps</span></span>
* <span data-ttu-id="96ff1-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="96ff1-112">API Apps</span></span>
* <span data-ttu-id="96ff1-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="96ff1-113">Logic Apps</span></span>

<span data-ttu-id="96ff1-114">De volgende tabel wordt uitgelegd hoe bestaande Azure-services zijn toegewezen aan de App Service en de beschikbaar binnen het app-typen.</span><span class="sxs-lookup"><span data-stu-id="96ff1-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="96ff1-115">Bestaande Azure-Service</span><span class="sxs-lookup"><span data-stu-id="96ff1-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="96ff1-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="96ff1-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="96ff1-117">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="96ff1-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="96ff1-118">Azure Websites</span><span class="sxs-lookup"><span data-stu-id="96ff1-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="96ff1-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="96ff1-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="96ff1-120">App Service is strikt beperkt is tot het wijzigen van de naam van de Websites in Web-Apps voor Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="96ff1-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="96ff1-121">Uw bestaande exemplaren van Websites zijn nu Web-Apps in App Service.</span><span class="sxs-lookup"><span data-stu-id="96ff1-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="96ff1-122">U kunt toegang tot uw bestaande websites via de <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, waarbij vindt u alle bestaande sites onder <em>Web-Apps</em>.</span><span class="sxs-lookup"><span data-stu-id="96ff1-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="96ff1-123"><em>Web-Hosting plannen</em> is nu <em>App Service-Plan</em>.</span><span class="sxs-lookup"><span data-stu-id="96ff1-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="96ff1-124">Een <em>App Service-Plan</em> elk type app van App Service, zoals Web-, mobiele, logische of API-apps kunnen hosten.</span><span class="sxs-lookup"><span data-stu-id="96ff1-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="96ff1-125">Azure App Service Web Apps is in het algemeen beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="96ff1-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="96ff1-126"><a href="http://azure.microsoft.com/services/app-service/web/">Meer informatie over Web-Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="96ff1-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="96ff1-127">Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="96ff1-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="96ff1-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="96ff1-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="96ff1-129">Mobile Services blijven beschikbaar als zelfstandige service en blijven volledig wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="96ff1-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="96ff1-130">Mobiele Apps is een app in App Service, die kan worden geïntegreerd in de functionaliteit van Mobile Services en meer.</span><span class="sxs-lookup"><span data-stu-id="96ff1-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="96ff1-131">Het is gemakkelijk te <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">van Mobile Services migreren naar Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="96ff1-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="96ff1-132">Als onderdeel van App Service ophalen Mobile Apps nieuwe mogelijkheden buiten Mobile Services, zoals integratie met on-premises en SaaS-systemen, sleuven, WebJobs en beter schalingsopties voor fasering.</span><span class="sxs-lookup"><span data-stu-id="96ff1-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="96ff1-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Meer informatie over Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="96ff1-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="96ff1-134">API-apps</span><span class="sxs-lookup"><span data-stu-id="96ff1-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="96ff1-135">API-Apps is een nieuw type app in App Service waarmee u gemakkelijk maken en gebruiken van API's in de cloud.</span><span class="sxs-lookup"><span data-stu-id="96ff1-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="96ff1-136"><a href="http://azure.microsoft.com/services/app-service/api/">Meer informatie over API-Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="96ff1-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="96ff1-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="96ff1-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="96ff1-138">Logic Apps is een nieuw type app in App Service waarmee u eenvoudig bedrijfsprocessen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="96ff1-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="96ff1-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Meer informatie over Logic Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="96ff1-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="96ff1-140">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="96ff1-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="96ff1-141">BizTalk API Apps</span><span class="sxs-lookup"><span data-stu-id="96ff1-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="96ff1-142">BizTalk Services kunnen blijven beschikbaar als zelfstandige service en blijven volledig wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="96ff1-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="96ff1-143">De mogelijkheden van BizTalk Services zijn geïntegreerd in App Service als zodat gebruikers voor het uitvoeren van de integratie van bedrijfstoepassingen en B2B integratiescenario's met een van de app-typen in App Service API-Apps.</span><span class="sxs-lookup"><span data-stu-id="96ff1-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="96ff1-144">Met Logic Apps kunt u nu werkstromen maken met een visuele ontwerp bedrijfsprocessen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="96ff1-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="96ff1-145">Voor meer informatie gaat u naar [App Service-documentatie](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="96ff1-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

