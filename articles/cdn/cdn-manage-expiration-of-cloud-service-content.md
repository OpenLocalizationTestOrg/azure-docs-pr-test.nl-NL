---
title: aaaManage vervaldatum van webinhoud in Azure CDN | Microsoft Docs
description: Meer informatie over hoe toomanage verlooptijd van Azure Web Apps/Cloud Services, ASP.NET of IIS inhoud in Azure CDN.
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="9e6a6-103">Vervaldatum van Azure Web Apps/Cloud Services, ASP.NET of IIS inhoud in Azure CDN beheren</span><span class="sxs-lookup"><span data-stu-id="9e6a6-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e6a6-104">Azure-Web-Apps/Cloud Services, ASP.NET of IIS</span><span class="sxs-lookup"><span data-stu-id="9e6a6-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="9e6a6-105">Azure blob Storage-service</span><span class="sxs-lookup"><span data-stu-id="9e6a6-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="9e6a6-106">Kunnen bestanden van de webserver van elke openbaar toegankelijke oorsprong in cache worden opgeslagen in Azure CDN totdat de time-to-live (TTL) is verstreken.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="9e6a6-107">Hallo TTL, wordt bepaald door Hallo [ *Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in het Hallo-bronserver Hallo HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-107">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from hello origin server.</span></span>  <span data-ttu-id="9e6a6-108">Dit artikel wordt beschreven hoe tooset `Cache-Control` headers voor de Web-Apps van Azure, Azure Cloud Services, ASP.NET-toepassingen en Internet Information Services-sites, die allemaal op dezelfde manier zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-108">This article describes how tooset `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="9e6a6-109">U kunt geen TTL voor een bestand tooset.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-109">You may choose tooset no TTL on a file.</span></span>  <span data-ttu-id="9e6a6-110">In dit geval past Azure CDN automatisch een standaard-TTL van zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="9e6a6-111">Zie voor meer informatie over de werking van toospeed toofiles toegang en andere resources in Azure CDN Hallo [overzicht van Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e6a6-111">For more information about how Azure CDN works toospeed up access toofiles and other resources, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="9e6a6-112">Cache-Control Headers instelling in configuratie</span><span class="sxs-lookup"><span data-stu-id="9e6a6-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="9e6a6-113">U kunt voor statische inhoud, zoals afbeeldingen en opmaakmodellen, Hallo updatefrequentie beheren doordat Hallo **applicationHost.config** of **web.config** bestanden voor uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-113">For static content, such as images and style sheets, you can control hello update frequency by modifying hello **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="9e6a6-114">Hallo **system.webServer\staticContent\clientCache** element in het configuratiebestand Hallo Hallo stelt `Cache-Control` -header voor uw inhoud.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-114">hello **system.webServer\staticContent\clientCache** element in hello configuration file will set hello `Cache-Control` header for your content.</span></span> <span data-ttu-id="9e6a6-115">Voor **web.config**, Hallo configuratie-instellingen heeft gevolgen voor alles wat u in het Hallo-map en alle submappen, tenzij genegeerd op Hallo submap niveau.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-115">For **web.config**, hello configuration settings will affect everything in hello folder and all subfolders, unless overridden at hello subfolder level.</span></span>  <span data-ttu-id="9e6a6-116">Bijvoorbeeld, kunt u instellen een standaard time-to-live op Hallo hoofdmap toohave alle statische inhoud in cache opgeslagen 3 dagen, maar hebben een submap die meer variabele inhoud met een cache-instelling van de 6 uur is.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-116">For example, you can set a default time-to-live at hello root toohave all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="9e6a6-117">Voor **applicationHost.config**, alle toepassingen op Hallo site worden beïnvloed, maar kunnen worden overschreven in **web.config** bestanden in het Hallo-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-117">For **applicationHost.config**, all applications on hello site will be affected, but can be overridden in **web.config** files in hello applications.</span></span>

<span data-ttu-id="9e6a6-118">Hallo volgende XML-code toont een voorbeeld van instelling **clientCache** toospecify een maximale leeftijd van 3 dagen:</span><span class="sxs-lookup"><span data-stu-id="9e6a6-118">hello following XML shows an example of setting **clientCache** toospecify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="9e6a6-119">Geven **UseMaxAge** voegt een `Cache-Control: max-age=<nnn>` toohello-header-reactie op basis van Hallo waarde die is opgegeven in Hallo **CacheControlMaxAge** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header toohello response based on hello value specified in hello **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="9e6a6-120">Hallo-indeling van Hallo timespan is voor Hallo **cacheControlMaxAge** kenmerk <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-120">hello format of hello timespan is for hello **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="9e6a6-121">Voor meer informatie over Hallo **clientCache** knooppunt, Zie [clientcache <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="9e6a6-121">For more information on hello **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="9e6a6-122">Cache-Control van Headers instellen in Code</span><span class="sxs-lookup"><span data-stu-id="9e6a6-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="9e6a6-123">Voor ASP.NET-toepassingen, kunt u instellen Hallo CDN cachegedrag programmatisch door Hallo instelling **HttpResponse.Cache** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-123">For ASP.NET applications, you can set hello CDN caching behavior programmatically by setting hello **HttpResponse.Cache** property.</span></span> <span data-ttu-id="9e6a6-124">Voor meer informatie over Hallo **HttpResponse.Cache** eigenschap, Zie [HttpResponse.Cache eigenschap](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) en [HttpCachePolicy klasse](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e6a6-124">For more information on hello **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="9e6a6-125">Als u wilt dat tooprogrammatically cache toepassingsinhoud in ASP.NET, zorgt u ervoor dat Hallo inhoud is gemarkeerd als caching geschikte door in te stellen HttpCacheability te*openbare*.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-125">If you want tooprogrammatically cache application content in ASP.NET, make sure that hello content is marked as cacheable by setting HttpCacheability too*Public*.</span></span> <span data-ttu-id="9e6a6-126">Controleer ook of er een cache-validatiefunctie is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="9e6a6-127">Hallo cache validator mag een laatst gewijzigd tijdstempel ingesteld door het aanroepen van SetLastModified of een etag-waarde ingesteld door het aanroepen van SetETag.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-127">hello cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="9e6a6-128">U kunt ook een cache-verlooptijd opgeven door het aanroepen van SetExpires eventueel of kunt u vertrouwen op Hallo standaard cache methodiek die eerder in dit document worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="9e6a6-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on hello default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="9e6a6-129">Bijvoorbeeld toocache inhoud gedurende één uur Hallo volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="9e6a6-129">For example, toocache content for one hour, add hello following:</span></span>  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="9e6a6-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e6a6-130">Next Steps</span></span>
* [<span data-ttu-id="9e6a6-131">Lees meer informatie over Hallo **clientCache** element</span><span class="sxs-lookup"><span data-stu-id="9e6a6-131">Read details about hello **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="9e6a6-132">Lees Hallo-documentatie voor Hallo **HttpResponse.Cache** eigenschap</span><span class="sxs-lookup"><span data-stu-id="9e6a6-132">Read hello documentation for hello **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="9e6a6-133">[Lees Hallo-documentatie voor Hallo **HttpCachePolicy klasse**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e6a6-133">[Read hello documentation for hello **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

