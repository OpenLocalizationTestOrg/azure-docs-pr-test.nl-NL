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
# <a name="how-toouse-azure-redis-cache"></a>Hoe tooUse Azure Redis-Cache
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Deze handleiding wordt getoond hoe tooget gestart met behulp van **Azure Redis-Cache**. Microsoft Azure Redis-Cache is gebaseerd op Hallo populaire open-source Redis-Cache. Dit biedt u toegang tot tooa beveiligde, toegewezen Redis-cache, beheerd door Microsoft. Een cache die u met Azure Redis-cache hebt gemaakt, is toegankelijk vanuit elke toepassing in Microsoft Azure.

Microsoft Azure Redis-Cache is beschikbaar in Hallo lagen te volgen:

* **Basic**: één knooppunt. Meerdere groottes van too53 GB.
* **Standard**: twee knooppunten (primair/replica). Meerdere groottes van too53 GB. 99,9% SLA.
* **Premium** : twee knooppunten primair/Replica met up too10 shards. Meerdere groottes van 6 GB too530 GB. Alle functies van de lagen Standard en Premium bieden ondersteuning voor [Redis-cluster](cache-how-to-premium-clustering.md), [Redis-persistentie](cache-how-to-premium-persistence.md) en [Azure Virtual Network](cache-how-to-premium-vnet.md). 99,9% SLA.

Elke laag verschilt wat functies en prijzen betreft. Zie [Prijsdetails voor caches][Cache Pricing Details] voor prijsinformatie.

Deze handleiding ontdekt u hoe toouse hello [StackExchange.Redis] [ StackExchange.Redis] client met C\# code. Hallo scenario's worden behandeld: **maken en configureren van een cache**, **cacheclients configureren**, en **toevoegen en verwijderen van objecten uit de cache Hallo**. Zie [Volgende stappen][Next Steps] voor meer informatie over het gebruik van Azure Redis Cache. Zie voor een stapsgewijze zelfstudie over het maken van een ASP.NET MVC-web-app met Redis-Cache, [hoe toocreate een Web-App met Redis-Cache](cache-web-app-howto.md).

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Aan de slag met Azure Redis-cache
Het is gemakkelijk om aan de slag te gaan met Azure Redis-cache tooget gestart, u inrichten en een cache configureren. Vervolgens configureert u Hallo-cache-clients om toegang te krijgen Hallo-cache tot. Nadat de cacheclients Hallo zijn geconfigureerd, kunt u beginnen met hen.

* [Hallo-cache maken][Create hello cache]
* [Hallo-cacheclients configureren][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>Een cache maken
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess uw cache nadat deze gemaakt
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Zie voor meer informatie over het configureren van uw cache [hoe tooconfigure Azure Redis-Cache](cache-configure.md).

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Hallo-cacheclients configureren
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

Nadat uw clientproject is geconfigureerd voor in cache opslaan, kunt u Hallo technieken beschreven in de volgende secties voor het werken met uw cache Hallo.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>Werken met caches
Hallo stappen in deze sectie wordt beschreven hoe tooperform algemene taken met Cache.

* [Verbinding maken met toohello cache][Connect toohello cache]
* [Toevoegen aan en ophalen van objecten uit de cache Hallo][Add and retrieve objects from hello cache]
* [Werken met .NET-objecten in cache Hallo](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>Verbinding maken met toohello cache
tooprogrammatically werk met een cache, moet u een verwijzing toohello-cache. Hallo na toohello boven aan alle bestanden waaruit u toouse hello StackExchange.Redis client tooaccess een Azure Redis-Cache wilt toevoegen.

    using StackExchange.Redis;

> [!NOTE]
> de client StackExchange.Redis Hallo vereist .NET Framework 4 of hoger.
> 
> 

Hallo verbinding toohello Azure Redis-Cache wordt beheerd door Hallo `ConnectionMultiplexer` klasse. Deze klasse mag worden gedeeld en opnieuw worden gebruikt in uw clienttoepassing en hoeft niet toobe gemaakt op basis van per bewerking. 

tooconnect tooan Azure Redis-Cache en een exemplaar van een verbonden `ConnectionMultiplexer`, aanroep Hallo statische `Connect` methode en geeft u Hallo cache-eindpunt en -sleutel. Hallo sleutel gegenereerd op basis van hello Azure-portal als wachtwoordparameter hello worden gebruikt.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Waarschuwing: sla nooit referenties op in de broncode. tookeep dit eenvoudige voorbeeld ik geef ze hier weer in de broncode Hallo. Zie [tekenreeksen van toepassingen en verbindingsreeksen] [ How Application Strings and Connection Strings Work] voor meer informatie over toostore referenties.
> 
> 

Als u niet dat toouse SSL wilt, ofwel ingesteld `ssl=false` of laat Hallo `ssl` parameter.

> [!NOTE]
> Hallo niet-SSL-poort is standaard uitgeschakeld voor nieuwe caches. Zie voor instructies over het inschakelen van niet-SSL-poort Hallo [toegangspoorten](cache-configure.md#access-ports).
> 
> 

Een aanpak toosharing een `ConnectionMultiplexer` exemplaar in uw toepassing is toohave een statische eigenschap die een verbonden exemplaar retourneert, vergelijkbare toohello voorbeeld te volgen. Deze aanpak geeft u een thread-veilige manier tooinitialize slechts één verbonden `ConnectionMultiplexer` exemplaar. In deze voorbeelden `abortConnect` is set toofalse, wat betekent dat Hallo aanroep slaagt ook als er een verbinding toohello Azure Redis-Cache niet tot stand wordt gebracht. Een belangrijke functie van `ConnectionMultiplexer` is dat deze connectiviteit toohello cache automatisch herstelt zodra Hallo netwerkprobleem of andere oorzaken opgelost zijn.

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

Zie [Configuratiemodel StackExchange.Redis][StackExchange.Redis configuration model] voor meer informatie over geavanceerde opties voor de configuratie van verbindingen.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

Wanneer Hallo-verbinding tot stand is gebracht, het retourneren van een database met verwijzing toohello redis-cache door de aanroepende Hallo `ConnectionMultiplexer.GetDatabase` methode. Hallo-object heeft geretourneerd van Hallo `GetDatabase` methode is een lichtgewicht Pass Through-object en hoeft niet toobe opgeslagen.

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

Azure Redis-caches hebben een configureerbare aantal databases (standaard van 16) die gebruikt toologically afzonderlijke Hallo gegevens binnen een Redis-cache worden kunnen. Zie [Wat zijn Redis-databases?](cache-faq.md#what-are-redis-databases) en [Standaardconfiguratie voor Redis-server](cache-configure.md#default-redis-server-configuration) voor meer informatie.

Nu dat u hoe tooconnect tooan Azure Redis-Cache-exemplaar en retourneren een verwijzing toohello database cache weet, bekijken we werken met Hallo-cache.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>Toevoegen aan en ophalen van objecten uit de cache Hallo
Items kunnen worden opgeslagen in en opgehaald uit de cache met behulp van Hallo `StringSet` en `StringGet` methoden.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

Redis slaat de meeste gegevens als Redis-tekenreeksen, maar deze tekenreeksen kunnen veel soorten gegevens, waaronder geserialiseerde binaire gegevens die kunnen worden gebruikt voor het opslaan van .NET-objecten in de cache Hallo bevatten.

Bij het aanroepen van `StringGet`, Hallo object bestaat, wordt het geretourneerd, en als dat niet `null` wordt geretourneerd. Als `null` wordt geretourneerd, u kunt het Hallo-waarde wordt opgehaald uit de gewenste gegevensbron Hallo en opslaan in cache Hallo voor later gebruik. Deze gebruikspatroon staat bekend als Hallo cache-aside '-patroon.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

U kunt ook `RedisValue`, zoals weergegeven in het volgende voorbeeld Hallo. `RedisValue` bevat impliciete operators voor het werken met integrale gegevenstypen en kan nuttig zijn als `null` een verwachte waarde is voor een item in de cache.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


toospecify hello vervaldatum van een item in de cache hello, gebruik Hallo `TimeSpan` parameter van `StringSet`.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Werken met .NET-objecten in cache Hallo
Azure Redis Cache kan zowel .NET-objecten als oudere gegevenstypen opslaan in de cache, maar voordat een .NET-object in de cache kan worden opgeslagen, moet het worden geserialiseerd. Deze .NET-serialisatie-object is Hallo verantwoordelijkheid van de ontwikkelaar van de toepassing hello en hebt Hallo ontwikkelaar flexibiliteit in keuze Hallo Hallo serialisatiefunctie.

Een eenvoudige manier tooserialize objecten is toouse hello `JsonConvert` serialisatiemethoden in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) en tooand van JSON serialiseren. Hallo volgende voorbeeld ziet u een opgehaald en ingesteld met een `Employee` exemplaar van het object.

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

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Redis-Cache.

* Uitchecken Hallo ASP.NET-providers voor Azure Redis-Cache.
  * [State-provider voor Azure Redis-sessies](cache-aspnet-session-state-provider.md)
  * [Cacheprovider voor ASP.NET-uitvoer in Azure Redis-cache](cache-aspnet-output-cache-provider.md)
* [Cache diagnostische gegevens inschakelen](cache-how-to-monitor.md#enable-cache-diagnostics) zodat u kunt [monitor](cache-how-to-monitor.md) Hallo status van de cache. U kunt metrische gegevens in hello Azure-portal en u ook kunt Hallo weergeven [downloaden en bekijken](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) ze met Hallo-hulpprogramma's van uw keuze.
* Bekijk Hallo [documentatie over de cacheclient StackExchange.Redis][StackExchange.Redis cache client documentation].
  * Azure Redis-cache is toegankelijk vanuit veel Redis-clients en ontwikkelingstalen. Zie [http://redis.io/clients][http://redis.io/clients] voor meer informatie.
* Azure Redis-cache kan ook worden gebruikt met services en hulpprogramma’s van derden, zoals Redsmin en Redis Desktop Manager.
  * Zie voor meer informatie over Redsmin [hoe tooretrieve een verbinding met Azure Redis-tekenreeks en deze gebruiken met Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].
  * Benader en controleer uw gegevens in Azure Redis-cache met een grafische gebruikersinterface die gebruikmaakt van [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).
* Zie Hallo [redis] [ redis] documentatie en lees meer over [redis-gegevenstypen] [ redis data types] en [een inleiding van vijftien minuten gegevenstypen tooRedis][a fifteen minute introduction tooRedis data types].

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


