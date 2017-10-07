---
title: aaaHow tooUse Azure Redis-Cache | Microsoft Docs
description: Meer informatie over hoe tooimprove Hallo prestaties van uw Azure-toepassingen met Azure Redis-Cache
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="ac513-103">Hoe tooUse Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="ac513-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac513-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ac513-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="ac513-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ac513-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="ac513-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="ac513-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="ac513-107">Java</span><span class="sxs-lookup"><span data-stu-id="ac513-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="ac513-108">Python</span><span class="sxs-lookup"><span data-stu-id="ac513-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="ac513-109">Deze handleiding wordt getoond hoe tooget gestart met behulp van **Azure Redis-Cache**.</span><span class="sxs-lookup"><span data-stu-id="ac513-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="ac513-110">Microsoft Azure Redis-Cache is gebaseerd op Hallo populaire open-source Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="ac513-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="ac513-111">Dit biedt u toegang tot tooa beveiligde, toegewezen Redis-cache, beheerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ac513-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="ac513-112">Een cache die u met Azure Redis-cache hebt gemaakt, is toegankelijk vanuit elke toepassing in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ac513-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="ac513-113">Microsoft Azure Redis-Cache is beschikbaar in Hallo lagen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac513-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="ac513-114">**Basic**: één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ac513-114">**Basic** – Single node.</span></span> <span data-ttu-id="ac513-115">Meerdere groottes van too53 GB.</span><span class="sxs-lookup"><span data-stu-id="ac513-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="ac513-116">**Standard**: twee knooppunten (primair/replica).</span><span class="sxs-lookup"><span data-stu-id="ac513-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="ac513-117">Meerdere groottes van too53 GB.</span><span class="sxs-lookup"><span data-stu-id="ac513-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="ac513-118">99,9% SLA.</span><span class="sxs-lookup"><span data-stu-id="ac513-118">99.9% SLA.</span></span>
* <span data-ttu-id="ac513-119">**Premium** : twee knooppunten primair/Replica met up too10 shards.</span><span class="sxs-lookup"><span data-stu-id="ac513-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="ac513-120">Meerdere groottes van 6 GB too530 GB.</span><span class="sxs-lookup"><span data-stu-id="ac513-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="ac513-121">Alle functies van de lagen Standard en Premium bieden ondersteuning voor [Redis-cluster](cache-how-to-premium-clustering.md), [Redis-persistentie](cache-how-to-premium-persistence.md) en [Azure Virtual Network](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="ac513-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="ac513-122">99,9% SLA.</span><span class="sxs-lookup"><span data-stu-id="ac513-122">99.9% SLA.</span></span>

<span data-ttu-id="ac513-123">Elke laag verschilt wat functies en prijzen betreft.</span><span class="sxs-lookup"><span data-stu-id="ac513-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="ac513-124">Zie [Prijsdetails voor caches][Cache Pricing Details] voor prijsinformatie.</span><span class="sxs-lookup"><span data-stu-id="ac513-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="ac513-125">Deze handleiding ontdekt u hoe toouse hello [StackExchange.Redis] [ StackExchange.Redis] client met C\# code.</span><span class="sxs-lookup"><span data-stu-id="ac513-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="ac513-126">Hallo scenario's worden behandeld: **maken en configureren van een cache**, **cacheclients configureren**, en **toevoegen en verwijderen van objecten uit de cache Hallo**.</span><span class="sxs-lookup"><span data-stu-id="ac513-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="ac513-127">Zie [Volgende stappen][Next Steps] voor meer informatie over het gebruik van Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="ac513-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="ac513-128">Zie voor een stapsgewijze zelfstudie over het maken van een ASP.NET MVC-web-app met Redis-Cache, [hoe toocreate een Web-App met Redis-Cache](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="ac513-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="ac513-129">Aan de slag met Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="ac513-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="ac513-130">Het is gemakkelijk om aan de slag te gaan met Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="ac513-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="ac513-131">tooget gestart, u inrichten en een cache configureren.</span><span class="sxs-lookup"><span data-stu-id="ac513-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="ac513-132">Vervolgens configureert u Hallo-cache-clients om toegang te krijgen Hallo-cache tot.</span><span class="sxs-lookup"><span data-stu-id="ac513-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="ac513-133">Nadat de cacheclients Hallo zijn geconfigureerd, kunt u beginnen met hen.</span><span class="sxs-lookup"><span data-stu-id="ac513-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="ac513-134">[Hallo-cache maken][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="ac513-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="ac513-135">[Hallo-cacheclients configureren][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="ac513-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="ac513-136">Een cache maken</span><span class="sxs-lookup"><span data-stu-id="ac513-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="ac513-137">tooaccess uw cache nadat deze gemaakt</span><span class="sxs-lookup"><span data-stu-id="ac513-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="ac513-138">Zie voor meer informatie over het configureren van uw cache [hoe tooconfigure Azure Redis-Cache](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ac513-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="ac513-139">Hallo-cacheclients configureren</span><span class="sxs-lookup"><span data-stu-id="ac513-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="ac513-140">Nadat uw clientproject is geconfigureerd voor in cache opslaan, kunt u Hallo technieken beschreven in de volgende secties voor het werken met uw cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac513-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="ac513-141">Werken met caches</span><span class="sxs-lookup"><span data-stu-id="ac513-141">Working with Caches</span></span>
<span data-ttu-id="ac513-142">Hallo stappen in deze sectie wordt beschreven hoe tooperform algemene taken met Cache.</span><span class="sxs-lookup"><span data-stu-id="ac513-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="ac513-143">[Verbinding maken met toohello cache][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="ac513-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="ac513-144">[Toevoegen aan en ophalen van objecten uit de cache Hallo][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="ac513-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="ac513-145">Werken met .NET-objecten in cache Hallo</span><span class="sxs-lookup"><span data-stu-id="ac513-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="ac513-146">Verbinding maken met toohello cache</span><span class="sxs-lookup"><span data-stu-id="ac513-146">Connect toohello cache</span></span>
<span data-ttu-id="ac513-147">tooprogrammatically werk met een cache, moet u een verwijzing toohello-cache.</span><span class="sxs-lookup"><span data-stu-id="ac513-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="ac513-148">Hallo na toohello boven aan alle bestanden waaruit u toouse hello StackExchange.Redis client tooaccess een Azure Redis-Cache wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ac513-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="ac513-149">de client StackExchange.Redis Hallo vereist .NET Framework 4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ac513-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="ac513-150">Hallo verbinding toohello Azure Redis-Cache wordt beheerd door Hallo `ConnectionMultiplexer` klasse.</span><span class="sxs-lookup"><span data-stu-id="ac513-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="ac513-151">Deze klasse mag worden gedeeld en opnieuw worden gebruikt in uw clienttoepassing en hoeft niet toobe gemaakt op basis van per bewerking.</span><span class="sxs-lookup"><span data-stu-id="ac513-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="ac513-152">tooconnect tooan Azure Redis-Cache en een exemplaar van een verbonden `ConnectionMultiplexer`, aanroep Hallo statische `Connect` methode en geeft u Hallo cache-eindpunt en -sleutel.</span><span class="sxs-lookup"><span data-stu-id="ac513-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="ac513-153">Hallo sleutel gegenereerd op basis van hello Azure-portal als wachtwoordparameter hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ac513-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="ac513-154">Waarschuwing: sla nooit referenties op in de broncode.</span><span class="sxs-lookup"><span data-stu-id="ac513-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="ac513-155">tookeep dit eenvoudige voorbeeld ik geef ze hier weer in de broncode Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac513-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="ac513-156">Zie [tekenreeksen van toepassingen en verbindingsreeksen] [ How Application Strings and Connection Strings Work] voor meer informatie over toostore referenties.</span><span class="sxs-lookup"><span data-stu-id="ac513-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="ac513-157">Als u niet dat toouse SSL wilt, ofwel ingesteld `ssl=false` of laat Hallo `ssl` parameter.</span><span class="sxs-lookup"><span data-stu-id="ac513-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="ac513-158">Hallo niet-SSL-poort is standaard uitgeschakeld voor nieuwe caches.</span><span class="sxs-lookup"><span data-stu-id="ac513-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="ac513-159">Zie voor instructies over het inschakelen van niet-SSL-poort Hallo [toegangspoorten](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="ac513-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="ac513-160">Een aanpak toosharing een `ConnectionMultiplexer` exemplaar in uw toepassing is toohave een statische eigenschap die een verbonden exemplaar retourneert, vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="ac513-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="ac513-161">Deze aanpak geeft u een thread-veilige manier tooinitialize slechts één verbonden `ConnectionMultiplexer` exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ac513-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="ac513-162">In deze voorbeelden `abortConnect` is set toofalse, wat betekent dat Hallo aanroep slaagt ook als er een verbinding toohello Azure Redis-Cache niet tot stand wordt gebracht.</span><span class="sxs-lookup"><span data-stu-id="ac513-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="ac513-163">Een belangrijke functie van `ConnectionMultiplexer` is dat deze connectiviteit toohello cache automatisch herstelt zodra Hallo netwerkprobleem of andere oorzaken opgelost zijn.</span><span class="sxs-lookup"><span data-stu-id="ac513-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="ac513-164">Zie [Configuratiemodel StackExchange.Redis][StackExchange.Redis configuration model] voor meer informatie over geavanceerde opties voor de configuratie van verbindingen.</span><span class="sxs-lookup"><span data-stu-id="ac513-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="ac513-165">Wanneer Hallo-verbinding tot stand is gebracht, het retourneren van een database met verwijzing toohello redis-cache door de aanroepende Hallo `ConnectionMultiplexer.GetDatabase` methode.</span><span class="sxs-lookup"><span data-stu-id="ac513-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="ac513-166">Hallo-object heeft geretourneerd van Hallo `GetDatabase` methode is een lichtgewicht Pass Through-object en hoeft niet toobe opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ac513-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="ac513-167">Azure Redis-caches hebben een configureerbare aantal databases (standaard van 16) die gebruikt toologically afzonderlijke Hallo gegevens binnen een Redis-cache worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="ac513-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="ac513-168">Zie [Wat zijn Redis-databases?](cache-faq.md#what-are-redis-databases) en [Standaardconfiguratie voor Redis-server](cache-configure.md#default-redis-server-configuration) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ac513-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="ac513-169">Nu dat u hoe tooconnect tooan Azure Redis-Cache-exemplaar en retourneren een verwijzing toohello database cache weet, bekijken we werken met Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="ac513-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="ac513-170">Toevoegen aan en ophalen van objecten uit de cache Hallo</span><span class="sxs-lookup"><span data-stu-id="ac513-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="ac513-171">Items kunnen worden opgeslagen in en opgehaald uit de cache met behulp van Hallo `StringSet` en `StringGet` methoden.</span><span class="sxs-lookup"><span data-stu-id="ac513-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="ac513-172">Redis slaat de meeste gegevens als Redis-tekenreeksen, maar deze tekenreeksen kunnen veel soorten gegevens, waaronder geserialiseerde binaire gegevens die kunnen worden gebruikt voor het opslaan van .NET-objecten in de cache Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="ac513-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="ac513-173">Bij het aanroepen van `StringGet`, Hallo object bestaat, wordt het geretourneerd, en als dat niet `null` wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ac513-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="ac513-174">Als `null` wordt geretourneerd, u kunt het Hallo-waarde wordt opgehaald uit de gewenste gegevensbron Hallo en opslaan in cache Hallo voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="ac513-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="ac513-175">Deze gebruikspatroon staat bekend als Hallo cache-aside '-patroon.</span><span class="sxs-lookup"><span data-stu-id="ac513-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="ac513-176">U kunt ook `RedisValue`, zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac513-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="ac513-177">`RedisValue` bevat impliciete operators voor het werken met integrale gegevenstypen en kan nuttig zijn als `null` een verwachte waarde is voor een item in de cache.</span><span class="sxs-lookup"><span data-stu-id="ac513-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="ac513-178">toospecify hello vervaldatum van een item in de cache hello, gebruik Hallo `TimeSpan` parameter van `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="ac513-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="ac513-179">Werken met .NET-objecten in cache Hallo</span><span class="sxs-lookup"><span data-stu-id="ac513-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="ac513-180">Azure Redis Cache kan zowel .NET-objecten als oudere gegevenstypen opslaan in de cache, maar voordat een .NET-object in de cache kan worden opgeslagen, moet het worden geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="ac513-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="ac513-181">Deze .NET-serialisatie-object is Hallo verantwoordelijkheid van de ontwikkelaar van de toepassing hello en hebt Hallo ontwikkelaar flexibiliteit in keuze Hallo Hallo serialisatiefunctie.</span><span class="sxs-lookup"><span data-stu-id="ac513-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="ac513-182">Een eenvoudige manier tooserialize objecten is toouse hello `JsonConvert` serialisatiemethoden in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) en tooand van JSON serialiseren.</span><span class="sxs-lookup"><span data-stu-id="ac513-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="ac513-183">Hallo volgende voorbeeld ziet u een opgehaald en ingesteld met een `Employee` exemplaar van het object.</span><span class="sxs-lookup"><span data-stu-id="ac513-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="ac513-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ac513-184">Next Steps</span></span>
<span data-ttu-id="ac513-185">Nu u Hallo basisprincipes hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="ac513-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="ac513-186">Uitchecken Hallo ASP.NET-providers voor Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="ac513-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="ac513-187">State-provider voor Azure Redis-sessies</span><span class="sxs-lookup"><span data-stu-id="ac513-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="ac513-188">Cacheprovider voor ASP.NET-uitvoer in Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="ac513-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="ac513-189">[Cache diagnostische gegevens inschakelen](cache-how-to-monitor.md#enable-cache-diagnostics) zodat u kunt [monitor](cache-how-to-monitor.md) Hallo status van de cache.</span><span class="sxs-lookup"><span data-stu-id="ac513-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="ac513-190">U kunt metrische gegevens in hello Azure-portal en u ook kunt Hallo weergeven [downloaden en bekijken](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) ze met Hallo-hulpprogramma's van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="ac513-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="ac513-191">Bekijk Hallo [documentatie over de cacheclient StackExchange.Redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="ac513-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="ac513-192">Azure Redis-cache is toegankelijk vanuit veel Redis-clients en ontwikkelingstalen.</span><span class="sxs-lookup"><span data-stu-id="ac513-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="ac513-193">Zie [http://redis.io/clients][http://redis.io/clients] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ac513-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="ac513-194">Azure Redis-cache kan ook worden gebruikt met services en hulpprogramma’s van derden, zoals Redsmin en Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="ac513-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="ac513-195">Zie voor meer informatie over Redsmin [hoe tooretrieve een verbinding met Azure Redis-tekenreeks en deze gebruiken met Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="ac513-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="ac513-196">Benader en controleer uw gegevens in Azure Redis-cache met een grafische gebruikersinterface die gebruikmaakt van [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="ac513-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="ac513-197">Zie Hallo [redis] [ redis] documentatie en lees meer over [redis-gegevenstypen] [ redis data types] en [een inleiding van vijftien minuten gegevenstypen tooRedis][a fifteen minute introduction tooRedis data types].</span><span class="sxs-lookup"><span data-stu-id="ac513-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


