---
title: aaaCache Cacheprovider voor ASP.NET
description: Meer informatie over hoe toocache ASP.NET-pagina-uitvoer met behulp van Azure Redis-Cache
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="b0e8f-103">Provider voor de uitvoercache van ASP.NET voor Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="b0e8f-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="b0e8f-104">Hallo Cacheprovider Redis is een opslagmechanisme voor out-of-process-voor de uitvoergegevens van de cache.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="b0e8f-105">Deze gegevens zijn specifiek voor volledige HTTP-antwoorden (pagina uitvoercaching).</span><span class="sxs-lookup"><span data-stu-id="b0e8f-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="b0e8f-106">Hallo-provider in Hallo nieuwe uitvoer cache provider uitbreidbaar punt die is geïntroduceerd in ASP.NET 4 wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="b0e8f-107">toouse hello Cacheprovider Redis uw cache eerst configureren en configureer vervolgens uw ASP.NET-toepassing met Hallo Redis uitvoer Cache Provider NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="b0e8f-108">In dit onderwerp bevat richtlijnen over het configureren van uw toepassing toouse hello Cacheprovider Redis.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="b0e8f-109">Zie voor meer informatie over het maken en configureren van een Azure Redis-Cache-exemplaar [een cache maken](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="b0e8f-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="b0e8f-110">ASP.NET-pagina-uitvoer opslaan in cache van de Hallo</span><span class="sxs-lookup"><span data-stu-id="b0e8f-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="b0e8f-111">tooconfigure een clienttoepassing in Visual Studio met Hallo Redis-Cache sessie status NuGet-pakket, klikt u op **NuGet Package Manager**, **Package Manager Console** van Hallo **extra** menu.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="b0e8f-112">Voer hello na de opdracht van Hallo `Package Manager Console` venster.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="b0e8f-113">Hallo Redis uitvoer Cache Provider NuGet-pakket heeft een afhankelijkheid op Hallo StackExchange.Redis.StrongName pakket.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="b0e8f-114">Als Hallo StackExchange.Redis.StrongName pakket niet aanwezig in uw project is, wordt deze geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="b0e8f-115">Zie voor meer informatie over Hallo Redis uitvoer Cache Provider NuGet-pakket Hallo [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet-pagina.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="b0e8f-116">In aanvulling toohello sterke naam StackExchange.Redis.StrongName pakket is er ook Hallo StackExchange.Redis niet-sterke naam versie.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="b0e8f-117">Als uw project Hallo niet-sterke naam StackExchange.Redis versie dat moet u deze verwijderen, ophalen anders u naamconflicten in uw project.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="b0e8f-118">Zie voor meer informatie over deze pakketten [cacheclients configureren .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="b0e8f-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="b0e8f-119">Hallo NuGet-pakket downloadt en voegt Hallo vereiste assembly verwijst naar Hallo volgende sectie in het web.config-bestand wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="b0e8f-120">Deze sectie bevat de vereiste configuratie voor uw ASP.NET-toepassing toouse hello Cacheprovider Redis Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="b0e8f-121">Hallo toegelicht sectie bevat een voorbeeld van het Hallo-kenmerken en voorbeelden van instellingen voor elk kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="b0e8f-122">Hallo-kenmerken configureren met waarden uit de cacheblade van uw in Microsoft Azure-portal Hallo Hallo en configureer andere waarden naar wens Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="b0e8f-123">Zie voor instructies over de toegang tot de eigenschappen van uw cache [configureren Redis-cache-instellingen](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="b0e8f-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="b0e8f-124">**host** – Geef uw cache-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="b0e8f-125">**poort** – uw niet-SSL-poort of uw SSL-poort, afhankelijk van het ssl-instellingen hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="b0e8f-126">**accessKey** – beide Hallo primaire of secundaire sleutel gebruiken voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="b0e8f-127">**SSL** : true als u wilt dat toosecure cache/clientcommunicatie met ssl; anders ONWAAR.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="b0e8f-128">Ervoor toospecify Hallo de juiste poort zijn.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="b0e8f-129">Hallo niet-SSL-poort is standaard uitgeschakeld voor nieuwe caches.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="b0e8f-130">Geef op waar om deze instelling toouse Hallo SSL-poort.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="b0e8f-131">Zie voor meer informatie over het inschakelen van niet-SSL-poort Hallo Hallo [toegangspoorten](cache-configure.md#access-ports) sectie in Hallo [een cache configureren](cache-configure.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="b0e8f-132">**databaseId** – opgegeven welke database toouse voor cache uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="b0e8f-133">Als niet wordt opgegeven, wordt de standaardwaarde Hallo van 0 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="b0e8f-134">**applicationName** – sleutels worden opgeslagen in redis als `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="b0e8f-135">Deze schematische kan meerdere toepassingen tooshare Hallo dezelfde sleutel.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="b0e8f-136">Deze parameter is optioneel en als u niet beschikken over een standaardwaarde wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="b0e8f-137">**connectionTimeoutInMilliseconds** – deze instelling kunt u toooverride hello connectTimeout instellen in de client StackExchange.Redis Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="b0e8f-138">Als niet wordt opgegeven, wordt de Hallo standaardinstelling connectTimeout van 5000 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="b0e8f-139">Zie voor meer informatie [configuratiemodel StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="b0e8f-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="b0e8f-140">**operationTimeoutInMilliseconds** – deze instelling kunt u toooverride hello syncTimeout instellen in de client StackExchange.Redis Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="b0e8f-141">Als niet wordt opgegeven, wordt Hallo standaardinstelling syncTimeout 1000 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="b0e8f-142">Zie voor meer informatie [configuratiemodel StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="b0e8f-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="b0e8f-143">Een OutputCache-instructie tooeach pagina waarvoor toocache Hallo uitvoer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="b0e8f-144">In het vorige voorbeeld Hallo Hallo cache pagina gegevens blijven in de cache Hallo gedurende 60 seconden en een andere versie van de pagina Hallo voor elke parametercombinatie in de cache wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="b0e8f-145">Zie voor meer informatie over de OutputCache-instructie Hallo [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="b0e8f-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="b0e8f-146">Zodra deze stappen worden uitgevoerd, is uw toepassing hello geconfigureerde toouse Cacheprovider Redis.</span><span class="sxs-lookup"><span data-stu-id="b0e8f-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0e8f-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b0e8f-147">Next steps</span></span>
<span data-ttu-id="b0e8f-148">Bekijk Hallo [ASP.NET Session State-Provider voor Azure Redis-Cache](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="b0e8f-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

