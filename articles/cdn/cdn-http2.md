---
title: HTTP-/ 2-ondersteuning in Azure CDN | Microsoft Docs
description: Meer informatie over ondersteuning voor HTTP/2- en CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="85dd4-103">HTTP-/ 2-ondersteuning in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="85dd4-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="85dd4-104">HTTP/2 is een grote revisie naar HTTP/1.1\.</span><span class="sxs-lookup"><span data-stu-id="85dd4-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="85dd4-105">Het biedt sneller webprestaties, verminderde reactietijd, en verbeterde gebruikerservaring, terwijl de bekende HTTP-methoden, statuscodes en semantiek behouden.</span><span class="sxs-lookup"><span data-stu-id="85dd4-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="85dd4-106">Hoewel HTTP/2 is ontworpen voor gebruik met HTTP en HTTPS, ondersteunen veel client webbrowsers alleen HTTP/2 via TLS.</span><span class="sxs-lookup"><span data-stu-id="85dd4-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="85dd4-107">Voordelen van de HTTP-/ 2</span><span class="sxs-lookup"><span data-stu-id="85dd4-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="85dd4-108">De voordelen van het HTTP/2 zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="85dd4-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="85dd4-109">**Multiplex en gelijktijdigheid**</span><span class="sxs-lookup"><span data-stu-id="85dd4-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="85dd4-110">HTTP 1.1 meerdere waardoor meerdere aanvragen van de resource is vereist voor meerdere TCP-verbindingen en elke verbinding heeft prestatieoverhead gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="85dd4-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="85dd4-111">HTTP/2 kunt meerdere resources moet worden gevraagd op een enkele TCP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="85dd4-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="85dd4-112">**Headercompressie**</span><span class="sxs-lookup"><span data-stu-id="85dd4-112">**Header compression**</span></span>

    <span data-ttu-id="85dd4-113">Door het comprimeren van de HTTP-headers voor aangeboden bronnen tijd op de kabel aanzienlijk verminderd.</span><span class="sxs-lookup"><span data-stu-id="85dd4-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="85dd4-114">**Stroom-afhankelijkheden**</span><span class="sxs-lookup"><span data-stu-id="85dd4-114">**Stream dependencies**</span></span>

    <span data-ttu-id="85dd4-115">Afhankelijkheden van de stroom kunnen de client om aan te geven met de server die bronnen prioriteit hebben.</span><span class="sxs-lookup"><span data-stu-id="85dd4-115">Stream dependencies allow the client to indicate to the server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="85dd4-116">Ondersteuning voor HTTP/2-Browser</span><span class="sxs-lookup"><span data-stu-id="85dd4-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="85dd4-117">Alle belangrijke browsers hebt HTTP/2-ondersteuning in de versies van hun huidige geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="85dd4-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="85dd4-118">Niet-ondersteunde browsers wordt automatisch fallback naar HTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="85dd4-118">Non-supported browsers will automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="85dd4-119">Browser</span><span class="sxs-lookup"><span data-stu-id="85dd4-119">Browser</span></span>|<span data-ttu-id="85dd4-120">Minimale versie</span><span class="sxs-lookup"><span data-stu-id="85dd4-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="85dd4-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="85dd4-121">Microsoft Edge</span></span>| <span data-ttu-id="85dd4-122">12</span><span class="sxs-lookup"><span data-stu-id="85dd4-122">12</span></span>|
|<span data-ttu-id="85dd4-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="85dd4-123">Google Chrome</span></span>| <span data-ttu-id="85dd4-124">43</span><span class="sxs-lookup"><span data-stu-id="85dd4-124">43</span></span>|
|<span data-ttu-id="85dd4-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="85dd4-125">Mozilla Firefox</span></span>| <span data-ttu-id="85dd4-126">38</span><span class="sxs-lookup"><span data-stu-id="85dd4-126">38</span></span>|
|<span data-ttu-id="85dd4-127">Opera</span><span class="sxs-lookup"><span data-stu-id="85dd4-127">Opera</span></span>| <span data-ttu-id="85dd4-128">32</span><span class="sxs-lookup"><span data-stu-id="85dd4-128">32</span></span>|
|<span data-ttu-id="85dd4-129">Safari</span><span class="sxs-lookup"><span data-stu-id="85dd4-129">Safari</span></span>| <span data-ttu-id="85dd4-130">9</span><span class="sxs-lookup"><span data-stu-id="85dd4-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="85dd4-131">HTTP-/ 2-ondersteuning in Azure CDN inschakelen</span><span class="sxs-lookup"><span data-stu-id="85dd4-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="85dd4-132">HTTP-/ 2-ondersteuning is momenteel actief is voor **Azure CDN van Akamai** en **Azure CDN van Verizon** profielen.</span><span class="sxs-lookup"><span data-stu-id="85dd4-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="85dd4-133">Er is geen verdere actie vereist van klanten.</span><span class="sxs-lookup"><span data-stu-id="85dd4-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="85dd4-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85dd4-134">Next Steps</span></span>

<span data-ttu-id="85dd4-135">Zie voor de voordelen van het HTTP/2 in actie [deze demo van Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="85dd4-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="85dd4-136">Voor meer informatie over HTTP/2, gaat u naar de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="85dd4-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="85dd4-137">HTTP-/ 2-specificatie startpagina</span><span class="sxs-lookup"><span data-stu-id="85dd4-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="85dd4-138">Officiële HTTP/2 Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="85dd4-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="85dd4-139">Akamai HTTP/2-gegevens</span><span class="sxs-lookup"><span data-stu-id="85dd4-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="85dd4-140">Zie voor meer informatie over de beschikbare functies van Azure CDN, de [overzicht van Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="85dd4-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>