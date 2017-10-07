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
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="2208b-103">Sessiestatus met Azure Redis Cache in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="2208b-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="2208b-104">Dit onderwerp wordt uitgelegd hoe toouse Azure Redis Cache Service Hallo voor sessiestatus.</span><span class="sxs-lookup"><span data-stu-id="2208b-104">This topic explains how toouse hello Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="2208b-105">Als uw ASP.NET-web-app sessiestatus gebruikt, moet u tooconfigure een externe sessiestatus-provider (Hallo Redis Cache Service of een sessiestatus-provider voor SQL Server).</span><span class="sxs-lookup"><span data-stu-id="2208b-105">If your ASP.NET web app uses session state, you will need tooconfigure an external session state provider (either hello Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="2208b-106">Als u sessiestatus gebruikt en een externe provider niet gebruikt, kunt u zich beperkt tooone exemplaar van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="2208b-106">If you use session state, and don't use an external provider, you will be limited tooone instance of your web app.</span></span> <span data-ttu-id="2208b-107">Hallo Redis Cache Service is het snelst en eenvoudigst tooenable Hallo.</span><span class="sxs-lookup"><span data-stu-id="2208b-107">hello Redis Cache Service is hello fastest and simplest tooenable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="2208b-108"><a id="createcache"></a>Hallo Cache maken</span><span class="sxs-lookup"><span data-stu-id="2208b-108"><a id="createcache"></a>Create hello Cache</span></span>
<span data-ttu-id="2208b-109">Ga als volgt [deze richtingen](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate Hallo cache.</span><span class="sxs-lookup"><span data-stu-id="2208b-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello cache.</span></span>

## <span data-ttu-id="2208b-110"><a id="configureproject"></a>Hallo RedisSessionStateProvider NuGet-pakket tooyour web-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="2208b-110"><a id="configureproject"></a>Add hello RedisSessionStateProvider NuGet package tooyour web app</span></span>
<span data-ttu-id="2208b-111">Hallo NuGet installeren `RedisSessionStateProvider` pakket.</span><span class="sxs-lookup"><span data-stu-id="2208b-111">Install hello NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="2208b-112">Gebruik Hallo volgende opdracht tooinstall vanuit Hallo package manager console (**extra** > **NuGet Package Manager** > **Package Manager Console**):</span><span class="sxs-lookup"><span data-stu-id="2208b-112">Use hello following command tooinstall from hello package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="2208b-113">tooinstall van **extra** > **NuGet Package Manager** > **Nuget-pakketten beheren voor oplossing**, zoekt u `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="2208b-113">tooinstall from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="2208b-114">Zie voor meer informatie Hallo [NuGet RedisSessionStateProvider-pagina](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) en [configureren Hallo-cacheclient](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="2208b-114">For more information see hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure hello cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="2208b-115"><a id="configurewebconfig"></a>Hallo bestand Web.Config wijzigen</span><span class="sxs-lookup"><span data-stu-id="2208b-115"><a id="configurewebconfig"></a>Modify hello Web.Config File</span></span>
<span data-ttu-id="2208b-116">Bovendien toomaking assembly verwijst naar voor Cache, Hallo NuGet-pakket stub-vermeldingen toegevoegd in Hallo *web.config* bestand.</span><span class="sxs-lookup"><span data-stu-id="2208b-116">In addition toomaking assembly references for Cache, hello NuGet package adds stub entries in hello *web.config* file.</span></span> 

1. <span data-ttu-id="2208b-117">Open Hallo *web.config* en Hallo Hallo zoeken **sessionState** element.</span><span class="sxs-lookup"><span data-stu-id="2208b-117">Open hello *web.config* and find hello hello **sessionState** element.</span></span>
2. <span data-ttu-id="2208b-118">Voer waarden in Hallo voor `host`, `accessKey`, `port` (Hallo SSL-poort moet 6380 zijn), en stel `SSL` te`true`.</span><span class="sxs-lookup"><span data-stu-id="2208b-118">Enter hello values for `host`, `accessKey`, `port` (hello SSL port should be 6380), and set `SSL` too`true`.</span></span> <span data-ttu-id="2208b-119">Deze waarden kunnen worden verkregen van Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade voor uw cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="2208b-119">These values can be obtained from hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="2208b-120">Zie voor meer informatie [toohello cache verbinding](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="2208b-120">For more information, see [Connect toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="2208b-121">Houd er rekening mee dat Hallo niet-SSL-poort is standaard uitgeschakeld voor nieuwe caches.</span><span class="sxs-lookup"><span data-stu-id="2208b-121">Note that hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="2208b-122">Zie voor meer informatie over het inschakelen van niet-SSL-poort Hallo Hallo [toegangspoorten](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) sectie in Hallo [een cache configureren in Azure Redis-Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="2208b-122">For more information about enabling hello non-SSL port, see hello [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in hello [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="2208b-123">Hallo volgende tekst toont Hallo wijzigingen toohello *web.config* bestand, specifiek Hallo wijzigingen te*poort*, *host*, accessKey * en *ssl*.</span><span class="sxs-lookup"><span data-stu-id="2208b-123">hello following markup shows hello changes toohello *web.config* file, specifically hello changes too*port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="2208b-124"><a id="usesessionobject"></a>Hallo sessieobject in Code gebruiken</span><span class="sxs-lookup"><span data-stu-id="2208b-124"><a id="usesessionobject"></a> Use hello Session Object in Code</span></span>
<span data-ttu-id="2208b-125">de laatste stap Hallo is toobegin Hallo sessie-object gebruiken in uw ASP.NET-code.</span><span class="sxs-lookup"><span data-stu-id="2208b-125">hello final step is toobegin using hello Session object in your ASP.NET code.</span></span> <span data-ttu-id="2208b-126">U objecten toosession status toevoegen met behulp van Hallo **Session.Add** methode.</span><span class="sxs-lookup"><span data-stu-id="2208b-126">You add objects toosession state by using hello **Session.Add** method.</span></span> <span data-ttu-id="2208b-127">Deze methode maakt gebruik van sleutel-waardeparen toostore items in de sessiecache status Hallo.</span><span class="sxs-lookup"><span data-stu-id="2208b-127">This method uses key-value pairs toostore items in hello session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="2208b-128">Hallo volgende code haalt deze waarde van de sessiestatus.</span><span class="sxs-lookup"><span data-stu-id="2208b-128">hello following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="2208b-129">U kunt ook Hallo Redis-Cache toocache objecten in uw web-app.</span><span class="sxs-lookup"><span data-stu-id="2208b-129">You can also use hello Redis Cache toocache objects in your web app.</span></span> <span data-ttu-id="2208b-130">Zie voor meer informatie [MVC film app met Azure Redis Cache in 15 minuten](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="2208b-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="2208b-131">Voor meer informatie over het toouse ASP.NET-sessiestatus, Zie [overzicht van ASP.NET-sessiestatus][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="2208b-131">For more details about how toouse ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="2208b-132">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="2208b-132">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2208b-133">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="2208b-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="2208b-134">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="2208b-134">What's changed</span></span>
* <span data-ttu-id="2208b-135">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="2208b-135">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="2208b-136">*Door [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="2208b-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

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

