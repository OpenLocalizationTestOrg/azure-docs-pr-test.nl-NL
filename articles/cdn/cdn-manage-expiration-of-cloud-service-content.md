---
title: Vervaldatum van webinhoud in Azure CDN beheren | Microsoft Docs
description: Informatie over het beheren van de verlooptijd van Azure Web Apps/Cloud Services, ASP.NET of IIS inhoud in Azure CDN.
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
ms.openlocfilehash: c207d780857a61d4b1fc0f39e6185cae67abc955
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="dfb84-103">Vervaldatum van Azure Web Apps/Cloud Services, ASP.NET of IIS inhoud in Azure CDN beheren</span><span class="sxs-lookup"><span data-stu-id="dfb84-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfb84-104">Azure-Web-Apps/Cloud Services, ASP.NET of IIS</span><span class="sxs-lookup"><span data-stu-id="dfb84-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="dfb84-105">Azure blob Storage-service</span><span class="sxs-lookup"><span data-stu-id="dfb84-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="dfb84-106">Kunnen bestanden van de webserver van elke openbaar toegankelijke oorsprong in cache worden opgeslagen in Azure CDN totdat de time-to-live (TTL) is verstreken.</span><span class="sxs-lookup"><span data-stu-id="dfb84-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="dfb84-107">De TTL-waarde wordt bepaald door de [ *Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in het HTTP-antwoord op de bronserver.</span><span class="sxs-lookup"><span data-stu-id="dfb84-107">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from the origin server.</span></span>  <span data-ttu-id="dfb84-108">In dit artikel wordt beschreven hoe instelt `Cache-Control` headers voor de Web-Apps van Azure, Azure Cloud Services, ASP.NET-toepassingen en Internet Information Services-sites, die allemaal op dezelfde manier zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="dfb84-108">This article describes how to set `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="dfb84-109">U kunt geen TTL ingesteld op een bestand.</span><span class="sxs-lookup"><span data-stu-id="dfb84-109">You may choose to set no TTL on a file.</span></span>  <span data-ttu-id="dfb84-110">In dit geval past Azure CDN automatisch een standaard-TTL van zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="dfb84-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="dfb84-111">Zie voor meer informatie over de werking van Azure CDN om sneller toegang tot bestanden en andere bronnen de [overzicht van Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfb84-111">For more information about how Azure CDN works to speed up access to files and other resources, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="dfb84-112">Cache-Control Headers instelling in configuratie</span><span class="sxs-lookup"><span data-stu-id="dfb84-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="dfb84-113">Voor statische inhoud, zoals afbeeldingen en opmaakmodellen, kunt u de updatefrequentie bepalen door het wijzigen van de **applicationHost.config** of **web.config** bestanden voor uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="dfb84-113">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="dfb84-114">De **system.webServer\staticContent\clientCache** element in het configuratiebestand stelt de `Cache-Control` -header voor uw inhoud.</span><span class="sxs-lookup"><span data-stu-id="dfb84-114">The **system.webServer\staticContent\clientCache** element in the configuration file will set the `Cache-Control` header for your content.</span></span> <span data-ttu-id="dfb84-115">Voor **web.config**, de configuratie-instellingen heeft gevolgen voor alles wat u in de map en alle submappen, tenzij genegeerd op het niveau van de submap.</span><span class="sxs-lookup"><span data-stu-id="dfb84-115">For **web.config**, the configuration settings will affect everything in the folder and all subfolders, unless overridden at the subfolder level.</span></span>  <span data-ttu-id="dfb84-116">U kunt bijvoorbeeld, stel een standaard time-to-live in de hoofdmap hebben alle statische inhoud in cache opgeslagen 3 dagen, maar hebben een submap die meer variabele inhoud met een cache-instelling van de 6 uur bevat.</span><span class="sxs-lookup"><span data-stu-id="dfb84-116">For example, you can set a default time-to-live at the root to have all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="dfb84-117">Voor **applicationHost.config**, alle toepassingen op de site worden beïnvloed, maar kunnen worden overschreven in **web.config** bestanden in de toepassingen.</span><span class="sxs-lookup"><span data-stu-id="dfb84-117">For **applicationHost.config**, all applications on the site will be affected, but can be overridden in **web.config** files in the applications.</span></span>

<span data-ttu-id="dfb84-118">De volgende XML-code toont een voorbeeld van de instelling **clientCache** om op te geven van een maximale leeftijd van 3 dagen:</span><span class="sxs-lookup"><span data-stu-id="dfb84-118">The following XML shows an example of setting **clientCache** to specify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="dfb84-119">Geven **UseMaxAge** voegt een `Cache-Control: max-age=<nnn>` header aan het antwoord op basis van de opgegeven waarde in de **CacheControlMaxAge** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="dfb84-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header to the response based on the value specified in the **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="dfb84-120">De indeling van de timespan is voor de **cacheControlMaxAge** kenmerk <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="dfb84-120">The format of the timespan is for the **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="dfb84-121">Voor meer informatie over de **clientCache** knooppunt, Zie [clientcache <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="dfb84-121">For more information on the **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="dfb84-122">Cache-Control van Headers instellen in Code</span><span class="sxs-lookup"><span data-stu-id="dfb84-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="dfb84-123">U kunt de CDN cachegedrag programmatisch door in te stellen instellen voor ASP.NET-toepassingen, de **HttpResponse.Cache** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="dfb84-123">For ASP.NET applications, you can set the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property.</span></span> <span data-ttu-id="dfb84-124">Voor meer informatie over de **HttpResponse.Cache** eigenschap, Zie [HttpResponse.Cache eigenschap](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) en [HttpCachePolicy klasse](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfb84-124">For more information on the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="dfb84-125">Als u maken via een programma cache toepassingsinhoud in ASP.NET wilt, zorgt u ervoor dat de inhoud is gemarkeerd als caching geschikte door HttpCacheability in te stellen op *openbare*.</span><span class="sxs-lookup"><span data-stu-id="dfb84-125">If you want to programmatically cache application content in ASP.NET, make sure that the content is marked as cacheable by setting HttpCacheability to *Public*.</span></span> <span data-ttu-id="dfb84-126">Controleer ook of er een cache-validatiefunctie is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="dfb84-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="dfb84-127">De validatie van de cache mag een laatst gewijzigd tijdstempel ingesteld door het aanroepen van SetLastModified of een etag-waarde ingesteld door het aanroepen van SetETag.</span><span class="sxs-lookup"><span data-stu-id="dfb84-127">The cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="dfb84-128">U kunt ook een cache-verlooptijd opgeven door het aanroepen van SetExpires eventueel of kunt u vertrouwen op de standaard cache methodiek die eerder in dit document worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="dfb84-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on the default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="dfb84-129">Bijvoorbeeld tot de cache inhoud gedurende één uur, Voeg het volgende toe:</span><span class="sxs-lookup"><span data-stu-id="dfb84-129">For example, to cache content for one hour, add the following:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="dfb84-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dfb84-130">Next Steps</span></span>
* [<span data-ttu-id="dfb84-131">Lees meer informatie over de **clientCache** element</span><span class="sxs-lookup"><span data-stu-id="dfb84-131">Read details about the **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="dfb84-132">Raadpleeg de documentatie van de **HttpResponse.Cache** eigenschap</span><span class="sxs-lookup"><span data-stu-id="dfb84-132">Read the documentation for the **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="dfb84-133">[Raadpleeg de documentatie van de **HttpCachePolicy klasse**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfb84-133">[Read the documentation for the **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

