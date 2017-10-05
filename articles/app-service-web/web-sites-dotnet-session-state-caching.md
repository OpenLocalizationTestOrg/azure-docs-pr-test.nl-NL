---
title: Sessiestatus met Azure Redis-cache in Azure App Service
description: Informatie over het gebruik van de Azure Cache Service voor de ondersteuning van ASP.NET-sessiestatus-caching.
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
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="8bdc1-103">Sessiestatus met Azure Redis Cache in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8bdc1-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="8bdc1-104">In dit onderwerp wordt uitgelegd hoe u de Azure Redis Cache Service gebruikt voor sessiestatus.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="8bdc1-105">Als uw ASP.NET-web-app sessiestatus gebruikt, moet u een externe sessiestatus-provider configureren (de Redis Cache Service of een sessiestatus-provider voor SQL Server).</span><span class="sxs-lookup"><span data-stu-id="8bdc1-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="8bdc1-106">Als u sessiestatus gebruikt maar geen externe provider, wordt uw gebruik van de web-app beperkt tot één exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="8bdc1-107">De Redis Cache Service is het snelst en eenvoudigst om in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="8bdc1-108"><a id="createcache"></a>De cache maken</span><span class="sxs-lookup"><span data-stu-id="8bdc1-108"><a id="createcache"></a>Create the Cache</span></span>
<span data-ttu-id="8bdc1-109">Volg [deze instructies](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) om de cache te maken.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <span data-ttu-id="8bdc1-110"><a id="configureproject"></a>Het NuGet-pakket van RedisSessionStateProvider toevoegen aan uw web-app</span><span class="sxs-lookup"><span data-stu-id="8bdc1-110"><a id="configureproject"></a>Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="8bdc1-111">Installeer het NuGet-pakket van `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="8bdc1-112">Gebruik de volgende opdracht om te installeren vanuit de Package Manager Console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span><span class="sxs-lookup"><span data-stu-id="8bdc1-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="8bdc1-113">Om te installeren vanuit **Tools** > **NuGet Package Manager** > **NuGet-pakketten beheren voor oplossing**, zoekt u naar `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="8bdc1-114">Zie voor meer informatie de [NuGet RedisSessionStateProvider-pagina](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) en [De cacheclient configureren](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="8bdc1-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="8bdc1-115"><a id="configurewebconfig"></a>Het bestand Web.Config wijzigen</span><span class="sxs-lookup"><span data-stu-id="8bdc1-115"><a id="configurewebconfig"></a>Modify the Web.Config File</span></span>
<span data-ttu-id="8bdc1-116">Naast het maken van assembly-verwijzingen voor Cache, voegt het NuGet-pakket stub-vermeldingen toe aan het *web.config*-bestand.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="8bdc1-117">Open de *web.config* en zoek het element **sessionState**.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="8bdc1-118">Voer de waarden in voor `host`, `accessKey`, `port` (de SSL-poort moet 6380 zijn), en stel `SSL` in op `true`.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="8bdc1-119">U vindt deze waarden op de blade [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) voor uw cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="8bdc1-120">Zie voor meer informatie [Verbinding maken met de cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="8bdc1-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="8bdc1-121">Houd er rekening mee dat de niet-SSL-poort standaard is uitgeschakeld voor nieuwe caches.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="8bdc1-122">Zie voor meer informatie over het inschakelen van de niet-SSL-poort het gedeelte [Toegangspoorten](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) in het onderwerp [Een cache configureren in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx).</span><span class="sxs-lookup"><span data-stu-id="8bdc1-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="8bdc1-123">De volgende tekst toont de wijzigingen in de *web.config* bestand, en specifiek de wijzigingen aan *poort*, *host*, accessKey * en *ssl* .</span><span class="sxs-lookup"><span data-stu-id="8bdc1-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="8bdc1-124"><a id="usesessionobject"></a>Het sessieobject in code gebruiken</span><span class="sxs-lookup"><span data-stu-id="8bdc1-124"><a id="usesessionobject"></a> Use the Session Object in Code</span></span>
<span data-ttu-id="8bdc1-125">De laatste stap is te beginnen het sessieobject te gebruiken in uw ASP.NET-code.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="8bdc1-126">U voegt objecten toe aan sessiestatus met de **Session.Add**-methode.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="8bdc1-127">Deze methode maakt gebruik van sleutelwaardeparen voor het opslaan van items in de cache van de statussessie.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="8bdc1-128">De volgende code haalt deze waarde op uit de sessiestatus.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="8bdc1-129">U kunt ook de Redis-cache gebruiken om cacheobjecten in uw web-app te cachen.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="8bdc1-130">Zie voor meer informatie [MVC film app met Azure Redis Cache in 15 minuten](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="8bdc1-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="8bdc1-131">Zie voor meer informatie over het gebruik van ASP.NET-sessiestatus [Overzicht van ASP.NET-sessiestatus][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="8bdc1-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="8bdc1-132">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8bdc1-133">U hebt geen creditcard nodig en u gaat geen verplichtingen aan.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="8bdc1-134">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="8bdc1-134">What's changed</span></span>
* <span data-ttu-id="8bdc1-135">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8bdc1-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="8bdc1-136">*Door [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="8bdc1-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

