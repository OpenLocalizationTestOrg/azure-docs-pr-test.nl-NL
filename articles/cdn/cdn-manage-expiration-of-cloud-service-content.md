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
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>Vervaldatum van Azure Web Apps/Cloud Services, ASP.NET of IIS inhoud in Azure CDN beheren
> [!div class="op_single_selector"]
> * [Azure-Web-Apps/Cloud Services, ASP.NET of IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure blob Storage-service](cdn-manage-expiration-of-blob-content.md)
> 
> 

Kunnen bestanden van de webserver van elke openbaar toegankelijke oorsprong in cache worden opgeslagen in Azure CDN totdat de time-to-live (TTL) is verstreken.  Hallo TTL, wordt bepaald door Hallo [ *Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in het Hallo-bronserver Hallo HTTP-antwoord.  Dit artikel wordt beschreven hoe tooset `Cache-Control` headers voor de Web-Apps van Azure, Azure Cloud Services, ASP.NET-toepassingen en Internet Information Services-sites, die allemaal op dezelfde manier zijn geconfigureerd.

> [!TIP]
> U kunt geen TTL voor een bestand tooset.  In dit geval past Azure CDN automatisch een standaard-TTL van zeven dagen.
> 
> Zie voor meer informatie over de werking van toospeed toofiles toegang en andere resources in Azure CDN Hallo [overzicht van Azure CDN](cdn-overview.md).
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>Cache-Control Headers instelling in configuratie
U kunt voor statische inhoud, zoals afbeeldingen en opmaakmodellen, Hallo updatefrequentie beheren doordat Hallo **applicationHost.config** of **web.config** bestanden voor uw webtoepassing.  Hallo **system.webServer\staticContent\clientCache** element in het configuratiebestand Hallo Hallo stelt `Cache-Control` -header voor uw inhoud. Voor **web.config**, Hallo configuratie-instellingen heeft gevolgen voor alles wat u in het Hallo-map en alle submappen, tenzij genegeerd op Hallo submap niveau.  Bijvoorbeeld, kunt u instellen een standaard time-to-live op Hallo hoofdmap toohave alle statische inhoud in cache opgeslagen 3 dagen, maar hebben een submap die meer variabele inhoud met een cache-instelling van de 6 uur is.  Voor **applicationHost.config**, alle toepassingen op Hallo site worden beïnvloed, maar kunnen worden overschreven in **web.config** bestanden in het Hallo-toepassingen.

Hallo volgende XML-code toont een voorbeeld van instelling **clientCache** toospecify een maximale leeftijd van 3 dagen:  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

Geven **UseMaxAge** voegt een `Cache-Control: max-age=<nnn>` toohello-header-reactie op basis van Hallo waarde die is opgegeven in Hallo **CacheControlMaxAge** kenmerk. Hallo-indeling van Hallo timespan is voor Hallo **cacheControlMaxAge** kenmerk <days>.<hours>:<min>:<sec>. Voor meer informatie over Hallo **clientCache** knooppunt, Zie [clientcache <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).  

## <a name="setting-cache-control-headers-in-code"></a>Cache-Control van Headers instellen in Code
Voor ASP.NET-toepassingen, kunt u instellen Hallo CDN cachegedrag programmatisch door Hallo instelling **HttpResponse.Cache** eigenschap. Voor meer informatie over Hallo **HttpResponse.Cache** eigenschap, Zie [HttpResponse.Cache eigenschap](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) en [HttpCachePolicy klasse](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

Als u wilt dat tooprogrammatically cache toepassingsinhoud in ASP.NET, zorgt u ervoor dat Hallo inhoud is gemarkeerd als caching geschikte door in te stellen HttpCacheability te*openbare*. Controleer ook of er een cache-validatiefunctie is ingesteld. Hallo cache validator mag een laatst gewijzigd tijdstempel ingesteld door het aanroepen van SetLastModified of een etag-waarde ingesteld door het aanroepen van SetETag. U kunt ook een cache-verlooptijd opgeven door het aanroepen van SetExpires eventueel of kunt u vertrouwen op Hallo standaard cache methodiek die eerder in dit document worden beschreven.  

Bijvoorbeeld toocache inhoud gedurende één uur Hallo volgende toevoegen:  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>Volgende stappen
* [Lees meer informatie over Hallo **clientCache** element](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [Lees Hallo-documentatie voor Hallo **HttpResponse.Cache** eigenschap](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [Lees Hallo-documentatie voor Hallo **HttpCachePolicy klasse**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

