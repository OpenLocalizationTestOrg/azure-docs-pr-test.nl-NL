---
title: aaaHTTP/2-ondersteuning in Azure CDN | Microsoft Docs
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
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="b8720-103">HTTP-/ 2-ondersteuning in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="b8720-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="b8720-104">HTTP/2 is een grote revisie tooHTTP/1.1\.</span><span class="sxs-lookup"><span data-stu-id="b8720-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="b8720-105">Het biedt sneller webprestaties, verminderde reactietijd, en verbeterde gebruikerservaring, terwijl Hallo bekend HTTP-methoden, statuscodes en semantiek behouden blijven.</span><span class="sxs-lookup"><span data-stu-id="b8720-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="b8720-106">Hoewel HTTP/2 ontworpen toowork met HTTP en HTTPS, ondersteunen veel client webbrowsers alleen HTTP/2 via TLS.</span><span class="sxs-lookup"><span data-stu-id="b8720-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="b8720-107">Voordelen van de HTTP-/ 2</span><span class="sxs-lookup"><span data-stu-id="b8720-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="b8720-108">Hallo voordelen van HTTP-/ 2:</span><span class="sxs-lookup"><span data-stu-id="b8720-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="b8720-109">**Multiplex en gelijktijdigheid**</span><span class="sxs-lookup"><span data-stu-id="b8720-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="b8720-110">HTTP 1.1 meerdere waardoor meerdere aanvragen van de resource is vereist voor meerdere TCP-verbindingen en elke verbinding heeft prestatieoverhead gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="b8720-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="b8720-111">HTTP/2 kunt meerdere resources toobe aangevraagd op een enkele TCP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="b8720-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="b8720-112">**Headercompressie**</span><span class="sxs-lookup"><span data-stu-id="b8720-112">**Header compression**</span></span>

    <span data-ttu-id="b8720-113">Door het comprimeren van Hallo HTTP-headers voor aangeboden bronnen tijd op de kabel Hallo aanzienlijk verminderd.</span><span class="sxs-lookup"><span data-stu-id="b8720-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="b8720-114">**Stroom-afhankelijkheden**</span><span class="sxs-lookup"><span data-stu-id="b8720-114">**Stream dependencies**</span></span>

    <span data-ttu-id="b8720-115">Afhankelijkheden van de stroom kunnen Hallo client tooindicate toohello server welke resources prioriteit hebben.</span><span class="sxs-lookup"><span data-stu-id="b8720-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="b8720-116">Ondersteuning voor HTTP/2-Browser</span><span class="sxs-lookup"><span data-stu-id="b8720-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="b8720-117">Alle belangrijke browsers Hallo hebt HTTP/2-ondersteuning in versies van hun huidige geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b8720-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="b8720-118">Niet-ondersteunde browsers wordt automatisch terugval tooHTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="b8720-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="b8720-119">Browser</span><span class="sxs-lookup"><span data-stu-id="b8720-119">Browser</span></span>|<span data-ttu-id="b8720-120">Minimale versie</span><span class="sxs-lookup"><span data-stu-id="b8720-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="b8720-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="b8720-121">Microsoft Edge</span></span>| <span data-ttu-id="b8720-122">12</span><span class="sxs-lookup"><span data-stu-id="b8720-122">12</span></span>|
|<span data-ttu-id="b8720-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="b8720-123">Google Chrome</span></span>| <span data-ttu-id="b8720-124">43</span><span class="sxs-lookup"><span data-stu-id="b8720-124">43</span></span>|
|<span data-ttu-id="b8720-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="b8720-125">Mozilla Firefox</span></span>| <span data-ttu-id="b8720-126">38</span><span class="sxs-lookup"><span data-stu-id="b8720-126">38</span></span>|
|<span data-ttu-id="b8720-127">Opera</span><span class="sxs-lookup"><span data-stu-id="b8720-127">Opera</span></span>| <span data-ttu-id="b8720-128">32</span><span class="sxs-lookup"><span data-stu-id="b8720-128">32</span></span>|
|<span data-ttu-id="b8720-129">Safari</span><span class="sxs-lookup"><span data-stu-id="b8720-129">Safari</span></span>| <span data-ttu-id="b8720-130">9</span><span class="sxs-lookup"><span data-stu-id="b8720-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="b8720-131">HTTP-/ 2-ondersteuning in Azure CDN inschakelen</span><span class="sxs-lookup"><span data-stu-id="b8720-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="b8720-132">HTTP-/ 2-ondersteuning is momenteel actief is voor **Azure CDN van Akamai** en **Azure CDN van Verizon** profielen.</span><span class="sxs-lookup"><span data-stu-id="b8720-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="b8720-133">Er is geen verdere actie vereist van klanten.</span><span class="sxs-lookup"><span data-stu-id="b8720-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="b8720-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b8720-134">Next Steps</span></span>

<span data-ttu-id="b8720-135">toosee hello voordelen van het HTTP/2 in actie, Zie [deze demo van Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="b8720-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="b8720-136">toolearn meer informatie over HTTP/2, gaat u naar Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="b8720-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="b8720-137">HTTP-/ 2-specificatie startpagina</span><span class="sxs-lookup"><span data-stu-id="b8720-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="b8720-138">Officiële HTTP/2 Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="b8720-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="b8720-139">Akamai HTTP/2-gegevens</span><span class="sxs-lookup"><span data-stu-id="b8720-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="b8720-140">toolearn meer informatie over de beschikbare functies van Azure CDN, Zie Hallo [overzicht van Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="b8720-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
