---
title: status aaaSession met Azure Redis-cache in Azure App Service
description: Meer informatie over hoe toouse hello Azure Cache Service toosupport ASP.NET-sessiestatus-caching.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a>Sessiestatus met Azure Redis Cache in Azure App Service
Dit onderwerp wordt uitgelegd hoe toouse Azure Redis Cache Service Hallo voor sessiestatus.

Als uw ASP.NET-web-app sessiestatus gebruikt, moet u tooconfigure een externe sessiestatus-provider (Hallo Redis Cache Service of een sessiestatus-provider voor SQL Server). Als u sessiestatus gebruikt en een externe provider niet gebruikt, kunt u zich beperkt tooone exemplaar van uw web-app. Hallo Redis Cache Service is het snelst en eenvoudigst tooenable Hallo.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a>Hallo Cache maken
Ga als volgt [deze richtingen](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate Hallo cache.

## <a id="configureproject"></a>Hallo RedisSessionStateProvider NuGet-pakket tooyour web-app toevoegen
Hallo NuGet installeren `RedisSessionStateProvider` pakket.  Gebruik Hallo volgende opdracht tooinstall vanuit Hallo package manager console (**extra** > **NuGet Package Manager** > **Package Manager Console**):

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

tooinstall van **extra** > **NuGet Package Manager** > **Nuget-pakketten beheren voor oplossing**, zoekt u `RedisSessionStateProvider`.

Zie voor meer informatie Hallo [NuGet RedisSessionStateProvider-pagina](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) en [configureren Hallo-cacheclient](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).

## <a id="configurewebconfig"></a>Hallo bestand Web.Config wijzigen
Bovendien toomaking assembly verwijst naar voor Cache, Hallo NuGet-pakket stub-vermeldingen toegevoegd in Hallo *web.config* bestand. 

1. Open Hallo *web.config* en Hallo Hallo zoeken **sessionState** element.
2. Voer waarden in Hallo voor `host`, `accessKey`, `port` (Hallo SSL-poort moet 6380 zijn), en stel `SSL` te`true`. Deze waarden kunnen worden verkregen van Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade voor uw cache-exemplaar. Zie voor meer informatie [toohello cache verbinding](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache). Houd er rekening mee dat Hallo niet-SSL-poort is standaard uitgeschakeld voor nieuwe caches. Zie voor meer informatie over het inschakelen van niet-SSL-poort Hallo Hallo [toegangspoorten](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) sectie in Hallo [een cache configureren in Azure Redis-Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) onderwerp. Hallo volgende tekst toont Hallo wijzigingen toohello *web.config* bestand, specifiek Hallo wijzigingen te*poort*, *host*, accessKey * en *ssl*.
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <a id="usesessionobject"></a>Hallo sessieobject in Code gebruiken
de laatste stap Hallo is toobegin Hallo sessie-object gebruiken in uw ASP.NET-code. U objecten toosession status toevoegen met behulp van Hallo **Session.Add** methode. Deze methode maakt gebruik van sleutel-waardeparen toostore items in de sessiecache status Hallo.

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

Hallo volgende code haalt deze waarde van de sessiestatus.

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

U kunt ook Hallo Redis-Cache toocache objecten in uw web-app. Zie voor meer informatie [MVC film app met Azure Redis Cache in 15 minuten](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).
Voor meer informatie over het toouse ASP.NET-sessiestatus, Zie [overzicht van ASP.NET-sessiestatus][ASP.NET Session State Overview].

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)
  
  *Door [Rick Anderson](https://twitter.com/RickAndMSFT)*

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

