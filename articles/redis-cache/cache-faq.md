---
title: aaaAzure Redis Cache FAQ | Microsoft Docs
description: Meer informatie over Hallo beantwoordt toocommon vragen, patronen en aanbevolen procedures voor Azure Redis-Cache
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>Veelgestelde vragen over Azure Redis Cache
Meer informatie over Hallo beantwoordt toocommon vragen, patronen en aanbevolen procedures voor Azure Redis-Cache.

## <a name="what-if-my-question-isnt-answered-here"></a>Wat gebeurt er als mijn vraag hier niet wordt beantwoord?
Als uw vraag hier niet is vermeld, laat ons weten en wij helpen u bij een antwoord vinden.

* U kunt een vraag boeken in Hallo opmerkingen aan Hallo einde van deze Veelgestelde vragen en benaderen hello Azure Cache-team en andere communityleden over dit artikel.
* een breder publiek tooreach, kunt u een vraag plaatsen op Hallo [Azure Cache MSDN-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) en hello Azure Cache-team en andere leden van de community Hallo benaderen.
* Als u wilt dat een aanvraag van de functie toomake, kunt u indienen uw aanvragen en ideeën te[Azure Redis-Cache User Voice](https://feedback.azure.com/forums/169382-cache).
* U kunt ook een e-mail sturen toous op [externe feedback over Azure Cache](mailto:azurecache@microsoft.com).

## <a name="azure-redis-cache-basics"></a>Basisbeginselen van Azure Redis-Cache
Hallo Veelgestelde vragen in deze sectie hebben betrekking op sommige Hallo basisbeginselen van Azure Redis-Cache.

* [Wat is Azure Redis-cache?](#what-is-azure-redis-cache)
* [Hoe kan ik aan de slag met Azure Redis-Cache?](#how-can-i-get-started-with-azure-redis-cache)

Hallo volgende veelgestelde vragen hebben betrekking op basisconcepten en vragen over Azure Redis-Cache en worden beantwoord in een van Hallo andere secties Veelgestelde vragen over.

* [Welk aanbod voor de Redis-cache en welke cachegrootte moet ik kiezen?](#what-redis-cache-offering-and-size-should-i-use)
* [Welke Redis-cache-clients kan ik gebruiken?](#what-redis-cache-clients-can-i-use)
* [Is er een lokale emulator voor Azure Redis-Cache?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Hoe bewaak ik Hallo status en prestaties van mijn cache?](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>Veelgestelde vragen over plannen
* [Welk aanbod voor de Redis-cache en welke cachegrootte moet ik kiezen?](#what-redis-cache-offering-and-size-should-i-use)
* [Azure Redis-Cache-prestaties](#azure-redis-cache-performance)
* [In welke regio moet ik mijn cache vinden?](#in-what-region-should-i-locate-my-cache)
* [Hoe ben ik in rekening gebracht voor Azure Redis-Cache?](#how-am-i-billed-for-azure-redis-cache)
* [Kan ik Azure Redis-Cache gebruiken met Azure Government Cloud, Azure China Cloud of Duitse van Microsoft Azure?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>Veelgestelde vragen over ontwikkeling
* [Wat moeten Hallo StackExchange.Redis configuratieopties doen?](#what-do-the-stackexchangeredis-configuration-options-do)
* [Welke Redis-cache-clients kan ik gebruiken?](#what-redis-cache-clients-can-i-use)
* [Is er een lokale emulator voor Azure Redis-Cache?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Hoe kan ik de Redis-opdrachten uitvoeren?](#how-can-i-run-redis-commands)
* [Waarom geen Azure Redis-Cache heeft een MSDN klasse verwijzing naar de bibliotheek zoals sommige Hallo van andere Azure-services?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [Kan ik Azure Redis-Cache gebruiken als een PHP-sessie-cache?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [Wat zijn de Redis-databases?](#what-are-redis-databases)

## <a name="security-faqs"></a>Veelgestelde vragen over Security
* [Wanneer moet ik Hallo niet-SSL-poort voor het verbinden van tooRedis inschakelen?](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>Veelgestelde vragen over productie
* [Wat zijn enkele aanbevolen procedures voor productie?](#what-are-some-production-best-practices)
* [Wat zijn enkele Hallo overwegingen als u algemene Redis-opdrachten gebruikt?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [Hoe kan ik benchmark en test de prestaties van mijn cache Hallo?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Belangrijke informatie over de ThreadPool groei](#important-details-about-threadpool-growth)
* [Server GC tooget inschakelen meer doorvoer op Hallo client bij gebruik van StackExchange.Redis](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [Prestatieoverwegingen rond verbindingen](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>Bewaking en probleemoplossing Veelgestelde vragen
Veelgestelde vragen over Hello in deze sectie behandeld algemene bewaking en probleemoplossing vragen. Zie voor meer informatie over bewaking en probleemoplossing van uw Azure Redis-Cache-exemplaren [hoe toomonitor Azure Redis-Cache](cache-how-to-monitor.md) en [hoe tootroubleshoot Azure Redis-Cache](cache-how-to-troubleshoot.md).

* [Hoe bewaak ik Hallo status en prestaties van mijn cache?](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [Waarom krijg ik time-outs zien?](#why-am-i-seeing-timeouts)
* [Waarom is de client verbinding met de Hallo-cache?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>Veelgestelde vragen over eerdere Cache aanbieding
* [Welke aanbieding voor Azure-Cache is geschikt voor mij?](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>Wat is Azure Redis-cache?
Azure Redis-Cache is gebaseerd op Hallo van populaire open-source [Redis-cache](http://redis.io). Dit biedt u toegang tot tooa beveiligde, toegewezen Redis-cache, beheerd door Microsoft en toegankelijk vanuit elke toepassing in Azure. Zie voor een gedetailleerd overzicht Hallo [Azure Redis-Cache](https://azure.microsoft.com/services/cache/) productpagina op Azure.com.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>Hoe kan ik aan de slag met Azure Redis-Cache?
Er zijn verschillende manieren die u kunt aan de slag met Azure Redis-Cache.

* Raadpleeg een van onze zelfstudies beschikbaar voor [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md), en [Python](cache-python-get-started.md).
* U kunt bekijken [hoe tooBuild High-Performance Apps met behulp van Microsoft Azure Redis-Cache](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/).
* U kunt controleren Hallo client-documentatie voor Hallo-clients die overeenkomen met de programmeertaal Hallo van uw project toosee hoe toouse Redis. Er zijn veel Redis-clients die kunnen worden gebruikt met Azure Redis-Cache. Zie voor een lijst met Redis-clients, [http://redis.io/clients](http://redis.io/clients).

Als u nog een Azure-account hebt, kunt u:

* [Gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). U ontvangt tegoed dat gebruikte tootry uit betaald Azure-services worden kunnen. Zelfs nadat Hallo tegoed is gebruikt, kunt u Hallo account houden en gratis Azure-services en functies gebruikt.
* [Uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Via uw MSDN-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>Welk aanbod voor de Redis-cache en welke cachegrootte moet ik kiezen?
Elke Azure Redis-Cache biedt verschillende niveaus van **grootte**, **bandbreedte**, **hoge beschikbaarheid**, en **SLA** opties.

Hallo hieronder vindt u overwegingen voor het kiezen van een Cache-aanbieding.

* **Geheugen**: Hallo Basic en Standard lagen bieden 250 MB – 53 GB. Premium-laag Hallo biedt tot too530 GB. Zie voor meer informatie [prijzen van Azure Redis-Cache](https://azure.microsoft.com/pricing/details/cache/).
* **Netwerkprestaties**: als u een werkbelasting die hoge doorvoersnelheid nodig hebt, Hallo Premium-laag biedt meer bandbreedte vergeleken tooStandard of Basic. Binnen elke laag hebben groter formaat caches ook meer bandbreedte vanwege Hallo onderliggende virtuele machine die als host fungeert voor Hallo-cache. Zie Hallo [na tabel](#cache-performance) voor meer informatie.
* **Doorvoer**: Hallo Premium-laag biedt Hallo maximaal beschikbare doorvoer. Als bandbreedtelimieten Hallo Hallo cache-server of client bereikt, krijgt u time-outs op Hallo-client. Zie Hallo volgende tabel voor meer informatie.
* **Hoge beschikbaarheid/SLA**: Azure Redis-Cache zorgt ervoor dat een cache standaard/Premium beschikbaar minimaal 99,9% van Hallo tijd is. Zie toolearn meer over onze SLA [prijzen van Azure Redis-Cache](https://azure.microsoft.com/support/legal/sla/cache/v1_0/). Hallo SLA bevat alleen informatie over connectiviteit toohello Cache eindpunten. Hallo SLA geldt niet voor beveiliging tegen gegevensverlies. U wordt aangeraden gebruik Hallo Redis gegevens persistentie functie in Hallo Premium-laag tooincrease tolerantie tegen gegevensverlies.
* **Redis-Gegevenspersistentie**: Hallo Premium-laag kunt u toopersist Hallo cache-gegevens in een Azure Storage-account. In een cache Basic/standaard wordt alle Hallo gegevens alleen in het geheugen opgeslagen. Als er zijn onderliggende infrastructuur problemen er mogelijk gegevensverlies. U wordt aangeraden gebruik Hallo Redis gegevens persistentie functie in Hallo Premium-laag tooincrease tolerantie tegen gegevensverlies. Azure Redis-Cache biedt RDB en AOF (binnenkort) opties in Redis-persistentie. Zie voor meer informatie [hoe tooconfigure persistentie voor een Premium Azure Redis-Cache](cache-how-to-premium-persistence.md).
* **Redis-Cluster**: toocreate groter zijn dan 53 GB of tooshard gegevens caches op meerdere Redis-knooppunten, kunt u Redis clustering, die beschikbaar is in Hallo Premium-laag. Elk knooppunt bestaat uit een combinatie van de cache primair/replica voor hoge beschikbaarheid. Zie voor meer informatie [hoe tooconfigure clustering voor een Premium Azure Redis-Cache](cache-how-to-premium-clustering.md).
* **Verbeterde beveiliging en isolatie**: implementatie van Azure Virtual Network (VNET) biedt verbeterde beveiliging en isolatie voor uw Azure Redis-Cache, evenals de subnetten, toegangscontrolebeleid, en andere functies toofurther toegang beperken. Zie voor meer informatie [hoe tooconfigure Virtual Network-ondersteuning voor een Premium Azure Redis-Cache](cache-how-to-premium-vnet.md).
* **Configureren van Redis**: In Hallo Standard en Premium-categorieën, configureert u Redis voor Keyspace-kennisgevingen.
* **Maximum aantal clientverbindingen**: Hallo Premium-laag biedt Hallo kunt u het maximum aantal clients die verbinding maken met tooRedis, met een hoger aantal verbindingen voor grotere grootte caches. Zie voor meer informatie [prijzen van Azure Redis-Cache](https://azure.microsoft.com/pricing/details/cache/).
* **Speciale kern voor Redis-Server**: In Hallo Premium-laag, alle cachegrootte hebben een speciale kern voor Redis. In Hallo Basic/Standard lagen, Hallo C1 grootte en hoger hebben een speciale kern voor Redis-server.
* **Redis is één thread** zodat met meer dan twee kernen geen extra voordeel biedt ten opzichte slechts twee kernen hebben, maar grotere VM doorgaans meer bandbreedte dan kleinere hebben. Als Hallo cache-server of client hello bandbreedtelimieten is bereikt, ontvangt u time-outs op Hallo-client.
* **Verbeterde prestaties**: Caches in Hallo Premium-laag zijn geïmplementeerd op hardware met snellere processors geeft betere prestaties vergeleken toohello Basic- of Standard-laag. Premium-laag Caches hebben hogere doorvoer en lagere latenties.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Azure Redis-Cache-prestaties
Hallo volgende tabel ziet u Hallo maximale bandbreedte waarden is waargenomen tijdens het testen van verschillende grootte van de Standard en Premium in de cache opgeslagen met behulp van `redis-benchmark.exe` van een Iaas-VM voor hello Azure Redis-Cache-eindpunt. 

>[!NOTE] 
>Deze waarden niet worden gegarandeerd en er is geen SLA voor deze getallen, maar moet typische. U moet laden uw eigen toepassing toodetermine Hallo rechts cachegrootte voor uw toepassing testen.
>
>

We kunnen Hallo conclusie trekt na tekenen uit deze tabel:

* Premium-laag doorvoer voor Hallo caches die dezelfde grootte is hoger in Hallo Hallo als vergeleken toohello Standard-laag. Bijvoorbeeld, met een 6 GB-Cache is doorvoer van P1 180.000 RPS als vergeleken too49, 000 voor C3.
* Met Redis clustering, duurt doorvoer lineair omdat u het aantal shards (knooppunten) in de cluster Hallo Hallo verhogen. Als u een cluster P4 van 10 shards maakt, vervolgens Hallo beschikbaar doorvoer is bijvoorbeeld 400.000 * 10 = 4 miljoen RPS.
* Doorvoer voor grotere key sizes is hoger in de Premium-laag Hallo als vergeleken toohello Standard-laag.

| Prijscategorie | Grootte | CPU-kernen | Beschikbare bandbreedte | De grootte van 1 KB |
| --- | --- | --- | --- | --- |
| **Standaard cachegrootte** | | |**Megabits per seconde (Mb/s) / Megabytes per seconde (MB/s)** |**Aanvragen per seconde (RPS)** |
| C0 |250 MB |Gedeeld |5 / 0.625 |600 |
| C1 |1 GB |1 |100 / 12.5 |12,200 |
| C2 |2,5 GB |2 |200 / 25 |24,000 |
| C3 |6 GB |4 |400 / 50 |49,000 |
| C4 |13 GB |2 |500 / 62.5 |61,000 |
| C5 |26 GB |4 |1,000 / 125 |115,000 |
| C6 |53 GB |8 |2,000 / 250 |150,000 |
| **Premium-cachegrootte** | |**CPU-kernen per shard** | **Megabits per seconde (Mb/s) / Megabytes per seconde (MB/s)** |**Aanvragen per seconde (RPS) per shard** |
| P1 |6 GB |2 |1,500 / 187.5 |180,000 |
| P2 |13 GB |4 |3,000 / 375 |360,000 |
| P3 |26 GB |4 |3,000 / 375 |360,000 |
| P4 |53 GB |8 |6,000 / 750 |400,000 |

Voor instructies over het downloaden van Hallo Redis-hulpprogramma's zoals `redis-benchmark.exe`, Zie Hallo [hoe kan ik Redis-opdrachten uitvoeren?](#cache-commands) sectie.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>In welke regio moet ik mijn cache vinden?
Voor optimale prestaties en de laagste latentie uw Azure Redis-Cache niet vinden in Hallo dezelfde regio bevinden als de cache-clienttoepassing.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>Hoe ben ik in rekening gebracht voor Azure Redis-Cache?
Prijzen voor Azure Redis-Cache is [hier](https://azure.microsoft.com/pricing/details/cache/). pagina met prijzen Hallo bevat prijzen als uur. Caches wordt gefactureerd op basis van per minuut van Hallo hoelang Hallo-cache wordt gemaakt tot Hallo-tijd die een cache wordt verwijderd. Er is geen optie voor het stoppen of onderbreken Hallo facturering van een cache.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>Kan ik Azure Redis-Cache gebruiken met Azure Government Cloud, Azure China Cloud of Duitse van Microsoft Azure?
Ja, is Azure Redis-Cache beschikbaar in de Cloud van de overheid Azure, Azure China Cloud en Duitse van Microsoft Azure. Hallo-URL's voor toegang tot en beheer van Azure Redis-Cache zijn verschillend in deze clouds vergeleken met de openbare Azure-Cloud. 

| Cloud   | DNS-achtervoegsel voor Redis            |
|---------|---------------------------------|
| Openbaar  | *. redis.cache.windows.net       |
| Amerikaanse overheid  | *. redis.cache.usgovcloudapi.net |
| Duitsland | *. redis.cache.cloudapi.de       |
| China   | *. redis.cache.chinacloudapi.cn  |

Zie voor meer informatie over overwegingen bij het gebruik van Azure Redis-Cache met andere clouds Hallo koppelingen volgen.

- [Azure Government Databases - Azure Redis-Cache](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Azure China Cloud - Azure Redis-Cache](https://www.azure.cn/documentation/services/redis-cache/)
- [Microsoft Azure Duitsland](https://azure.microsoft.com/overview/clouds/germany/)

Zie voor meer informatie over het gebruik van Azure Redis-Cache met PowerShell in Azure Government Cloud, Azure China Cloud en Microsoft Azure Duitsland [hoe tooconnect tooother clouds - Azure Redis-Cache PowerShell](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>Wat moeten Hallo StackExchange.Redis configuratieopties doen?
StackExchange.Redis heeft een groot aantal opties. Deze sectie wordt gesproken over een aantal algemene Hallo-instellingen. Zie voor meer informatie over opties voor StackExchange.Redis gedetailleerde [StackExchange.Redis configuratie](https://stackexchange.github.io/StackExchange.Redis/Configuration).

| ConfigurationOptions | Beschrijving | Aanbeveling |
| --- | --- | --- |
| AbortOnConnectFail |Bij het instellen van tootrue, Hallo-verbinding niet verbinding wordt hersteld na een netwerkstoring op een. |Stel toofalse en laten StackExchange.Redis automatisch opnieuw verbinding maken. |
| ConnectRetry |Hallo aantal toorepeat tijdens de eerste verbindingspogingen keer verbinding maken. |Zie Hallo notities voor richtlijnen te volgen. |
| ConnectTimeout |Time-out in ms voor connect-bewerkingen. |Zie Hallo notities voor richtlijnen te volgen. |

De standaardwaarden Hallo van client Hallo zijn meestal voldoende. Hallo-opties op basis van uw werkbelasting, kunt u aanpassen.

* **Nieuwe pogingen**
  * Voor ConnectRetry en ConnectTimeout Hallo algemene richtlijnen toofail snel is en probeer het opnieuw. In deze richtlijnen is gebaseerd op uw werkbelasting en na hoeveel tijd op het duurt voor uw client-tooissue een Redis-opdracht gemiddelde en een reactie ontvangen.
  * Laat StackExchange.Redis automatisch opnieuw verbinden in plaats van de verbindingsstatus controleren en zelf opnieuw verbinding te maken. **Vermijd het gebruik van Hallo ConnectionMultiplexer.IsConnected eigenschap**.
  * Snowballing - soms u kunt uitvoeren in een probleem waarbij u opnieuw uit te proberen en Hallo snowball pogingen en nooit herstelt. Als snowballing optreedt, moet u overwegen een nieuwe poging exponentieel uitstel algoritme zoals beschreven in [Probeer algemene richtlijnen](../best-practices-retry-general.md) gepubliceerd door Hallo-groep voor Microsoft Patterns en -procedures.
* **Time-outwaarden**
  * Houd rekening met uw werkbelasting en dienovereenkomstig Hallo-waarden instellen. Als u grote waarden worden opgeslagen, Hallo tooa hogere outwaarde instellen.
  * Stel `AbortOnConnectFail` toofalse en laat StackExchange.Redis opnieuw verbinding maken voor u.
  * Gebruik één ConnectionMultiplexer exemplaar voor de toepassing hello. U kunt een LazyConnection toocreate één exemplaar dat wordt geretourneerd door de verbindingseigenschap van een, zoals wordt weergegeven in [toohello cache met behulp van Hallo ConnectionMultiplexer klasse verbinding](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).
  * Set Hallo `ConnectionMultiplexer.ClientName` tooan app-exemplaar unieke eigenschapnaam voor diagnostische doeleinden.
  * Meerdere `ConnectionMultiplexer` exemplaren voor aangepaste werkbelastingen.
      * Als u verschillende belasting in uw toepassing hebt, kunt u dit model volgen. Bijvoorbeeld:
      * U kunt een multiplexer voor het omgaan met grote sleutels hebben.
      * U kunt een multiplexer voor het omgaan met kleine sleutels hebben.
      * U kunt verschillende waarden voor time-outs voor verbindingen en Pogingslogica voor elke ConnectionMultiplexer die u gebruikt.
      * Set Hallo `ClientName` -eigenschap op elke multiplexer toohelp met diagnostische gegevens.
      * In deze richtlijnen kan leiden tot toomore gestroomlijnd latentie per `ConnectionMultiplexer`.

### <a name="what-redis-cache-clients-can-i-use"></a>Welke Redis-cache-clients kan ik gebruiken?
Een van de Hallo prettige dingen Redis is dat er veel clients ondersteunen veel verschillende ontwikkelingstalen zijn. Zie voor een huidige lijst van clients [Redis-clients](http://redis.io/clients). Zie voor zelfstudies over diverse verschillende talen en clients, [hoe toouse Azure Redis-Cache](cache-dotnet-how-to-use-azure-redis-cache.md) en van Hallo taal schakelbaar Hallo boven aan het artikel Hallo Hallo gewenste taal op.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Is er een lokale emulator voor Azure Redis-Cache?
Er is geen lokale emulator voor Azure Redis-Cache, maar u kunt Hallo MSOpenTech versie van redis-server.exe uitvoeren vanaf Hallo [Redis-opdrachtregelprogramma's](https://github.com/MSOpenTech/redis/releases/) op uw lokale machine en maak verbinding tooit tooget een vergelijkbare ervaring tooa lokale cache -emulatie, zoals wordt weergegeven in Hallo voorbeeld te volgen:

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


U kunt desgewenst configureren een [redis.conf](http://redis.io/topics/config) bestand toomore sterke overeenkomst vertonen met Hallo [cache standaardinstellingen](cache-configure.md#default-redis-server-configuration) voor uw online Azure Redis-Cache indien gewenst.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>Hoe kan ik de Redis-opdrachten uitvoeren?
U kunt Hallo opdrachten die wordt vermeld op [Redis-opdrachten](http://redis.io/commands#) , met uitzondering van opdrachten op Hallo [Redis opdrachten niet ondersteund in Azure Redis-Cache](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache). U hebt verschillende opties toorun Redis-opdrachten.

* Als u een Standard of Premium-cache hebt, kunt u de Redis-opdrachten met Hallo uitvoeren [Redis-Console](cache-configure.md#redis-console). Hallo Redis-console biedt een veilige manier toorun Redis-opdrachten in hello Azure-portal.
* U kunt ook Hallo Redis-opdrachtregelprogramma's gebruiken. toouse, voeren Hallo volgende stappen:
* Hallo downloaden [Redis-opdrachtregelprogramma's](https://github.com/MSOpenTech/redis/releases/).
* Verbinding maken met behulp van toohello cache `redis-cli.exe`. In de cache-eindpunt Hallo met Hallo -h schakeloptie en Hallo sleutel met behulp van - a zoals weergegeven in het volgende voorbeeld Hallo doorgeven:
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> Hallo Redis opdrachtregelprogramma's werken niet met SSL-poort hello, maar u kunt een hulpprogramma zoals `stunnel` toosecurely Hallo extra toohello SSL-poort verbinding door Hallo aanwijzingen in Hallo [aankondigen van ASP.NET Session State-Provider voor Preview-versie redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) blogbericht.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>Waarom geen Azure Redis-Cache heeft een MSDN klasse verwijzing naar de bibliotheek zoals sommige Hallo van andere Azure-services?
Microsoft Azure Redis-Cache is gebaseerd op Hallo populaire open-source Redis-Cache en toegankelijk zijn voor een groot aantal [Redis-clients](http://redis.io/clients) voor vele programmeertalen. Elke client heeft een eigen API dat zorgt ervoor dat aanroepen toohello Redis cache exemplaar met [Redis opdrachten](http://redis.io/commands).

Omdat elke client verschilt, is er niet één centrale klassenverwijzing op MSDN en elke client onderhoudt een eigen naslagdocumentatie. Bovendien toohello verwijzen naar documentatie, er zijn verschillende zelfstudies die laat zien hoe tooget de slag met Azure Redis-Cache met behulp van verschillende talen en cache-clients. tooaccess deze zelfstudies Zie [hoe toouse Azure Redis-Cache](cache-dotnet-how-to-use-azure-redis-cache.md) en van Hallo taal schakelbaar Hallo boven aan het artikel Hallo Hallo gewenste taal op.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>Kan ik Azure Redis-Cache gebruiken als een PHP-sessie-cache?
Ja, toouse Azure Redis-Cache als de cache van een PHP-sessie, geef Hallo verbinding tekenreeks tooyour Azure Redis-Cache-exemplaar in `session.save_path`.

> [!IMPORTANT]
> Wanneer u Azure Redis-Cache als een PHP-sessiecache, moet u URL coderen Hallo beveiliging sleutel gebruikte tooconnect toohello cache, zoals wordt weergegeven in Hallo voorbeeld te volgen:
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> Als het Hallo-sleutel is geen URL gecodeerd, ontvangt u mogelijk een uitzondering met een bericht zoals:`Failed tooparse session.save_path`
>
>

Zie voor meer informatie over het gebruik van Redis-Cache als de cache van een PHP-sessie met Hallo PhpRedis client [sessie PHP-handler](https://github.com/phpredis/phpredis#php-session-handler).

### <a name="what-are-redis-databases"></a>Wat zijn de Redis-databases?

Redis-Databases zijn alleen een logische scheiding van gegevens binnen Hallo hetzelfde Redis-exemplaar. Hallo-cachegeheugen wordt gedeeld tussen alle Hallo-databases en werkelijke geheugenverbruik van een bepaalde database, is afhankelijk van Hallo sleutels/waarden in de database opgeslagen. Zo heeft een cache C6 53 GB aan geheugen. U kunt tooput alle 53 GB in een database of u kunt het opsplitsen tussen meerdere databases. 

> [!NOTE]
> Als u een Premium Azure Redis-Cache met clusteren is ingeschakeld, wordt alleen database 0 beschikbaar is. Deze beperking is een ingebouwde Redis-beperking en is niet specifiek tooAzure Redis-Cache. Zie voor meer informatie [heb ik nodig toomake eventuele wijzigingen toomy client toepassing toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>Wanneer moet ik Hallo niet-SSL-poort voor het verbinden van tooRedis inschakelen?
Redis-server SSL geen systeemeigen ondersteuning, maar biedt Azure Redis-Cache. Als u verbinding tooAzure Redis-Cache maakt en de client SSL, zoals StackExchange.Redis ondersteunt, moet u SSL gebruiken.

>[!NOTE]
>Hallo niet-SSL-poort is standaard uitgeschakeld voor nieuwe exemplaren van Azure Redis-Cache. Als de client geen ondersteuning biedt voor SSL, dan u niet-SSL-poort Hallo inschakelen moet door Hallo aanwijzingen in Hallo [poorten openen](cache-configure.md#access-ports) sectie Hallo [een cache configureren in Azure Redis-Cache](cache-configure.md) artikel.
>
>

Hulpprogramma's zoals redis `redis-cli` werken niet met SSL-poort hello, maar u kunt een hulpprogramma zoals `stunnel` toosecurely Hallo extra toohello SSL-poort verbinding door Hallo aanwijzingen in Hallo [ASP.NET Session State-Provider aangekondigd voor de Preview-versie Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) blogbericht.

Zie voor instructies over het downloaden van Hallo Redis-hulpprogramma's, Hallo [hoe kan ik Redis-opdrachten uitvoeren?](#cache-commands) sectie.

### <a name="what-are-some-production-best-practices"></a>Wat zijn enkele aanbevolen procedures voor productie?
* [Aanbevolen procedures van StackExchange.Redis](#stackexchangeredis-best-practices)
* [Configuratie en -concepten](#configuration-and-concepts)
* [Prestaties testen](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>Aanbevolen procedures van StackExchange.Redis
* Stel `AbortConnect` toofalse, laat Hallo ConnectionMultiplexer automatisch opnieuw verbinding maken. [Hier ziet voor meer informatie](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Hallo ConnectionMultiplexer hergebruiken - Maak een nieuwe voor elke aanvraag geen. Hallo `Lazy<ConnectionMultiplexer>` patroon [hier weergegeven](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) wordt aanbevolen.
* Werkt beste redis met lagere waarden, moet deze hakken van grotere gegevens in meerdere sleutels. In [deze discussie Redis](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ), 100 kb groot wordt geacht. Lees [in dit artikel](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) voor een voorbeeld-probleem dat kan worden veroorzaakt door grote waarden.
* Configureer uw [ThreadPool instellingen](#important-details-about-threadpool-growth) tooavoid time-outs.
* Gebruik Hallo ten minste standaard connectTimeout van 5 seconden. Dit interval krijgt StackExchange.Redis voldoende tijd toore-Hallo-verbinding in geval van een blip netwerk tot stand brengen.
* Let Hallo prestaties kosten in verband met verschillende bewerkingen die u uitvoert. Bijvoorbeeld: Hallo `KEYS` opdracht is een bewerking O(n) en moeten worden vermeden. Hallo [redis.io site](http://redis.io/commands/) details rond Hallo tijd complexiteit voor elke bewerking die deze ondersteuning biedt voor heeft. Klik op elke opdracht toosee Hallo complexiteit voor elke bewerking.

#### <a name="configuration-and-concepts"></a>Configuratie en -concepten
* Standard of Premium-laag voor productiesystemen gebruiken. Hallo Basisstaffel is een systeem met één knooppunt met geen gegevensreplicatie en geen SLA. Gebruik ook ten minste een C1-cache. C0 caches worden meestal gebruikt voor scenario's eenvoudig ontwikkelen en testen.
* Houd er rekening mee dat Redis is een **In-Memory** gegevensarchief. Lees [in dit artikel](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) zodat u zich bewust bent van scenario's waarbij gegevens verloren kan gaan.
* Uw systeem ontwikkelen, zodat deze kan omgaan met verbinding blips [vanwege toopatching en failover](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md).

#### <a name="performance-testing"></a>Prestaties testen
* Start met `redis-benchmark.exe` tooget een idee voor mogelijke doorvoer voordat u uw eigen tests perf schrijft. Omdat `redis-benchmark` biedt geen ondersteuning voor SSL, moet u [Hallo niet-SSL-poort via hello Azure-portal in te schakelen](cache-configure.md#access-ports) voordat u Hallo test uitvoert. Zie voor voorbeelden [hoe kan ik benchmark en test de prestaties van mijn cache Hallo?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* Hallo client VM gebruikt voor testdoeleinden moet Hallo dezelfde regio bevinden als uw exemplaar van Redis-cache.
* U kunt het beste Dv2 VM-reeks gebruikt voor de client als ze beschikken over betere hardware en de beste resultaten Hallo geeft.
* Zorg ervoor dat uw client VM die u kiest een mogelijkheid voor ten minste net zoveel computing en bandbreedte heeft als Hallo cache die u wilt testen.
* Schakel VRSS op Hallo client-computer als u van Windows gebruikmaakt. [Hier ziet voor meer informatie](https://technet.microsoft.com/library/dn383582.aspx).
* Premium-laag Redis exemplaren hebben latentie en doorvoer beter netwerk, omdat er op betere hardware voor zowel CPU en het netwerk worden uitgevoerd.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>Wat zijn enkele Hallo overwegingen als u algemene Redis-opdrachten gebruikt?
* Sommige Redis-opdrachten die een toocomplete lang duren zonder het Hallo-impact van deze opdrachten begrijpt, moet u niet uitvoeren.
  * Bijvoorbeeld: Hallo niet uitvoeren [sleutels](http://redis.io/commands/keys) opdracht in de productieomgeving, omdat dit een tooreturn lange tijd, afhankelijk van het aantal sleutels Hallo kan duren. Redis is een server met één thread en opdrachten een tegelijk worden verwerkt. Als u andere opdrachten afgegeven na sleutels hebt, zullen ze niet worden verwerkt totdat Redis Hallo sleutels opdracht verwerkt. Hallo [redis.io site](http://redis.io/commands/) details rond Hallo tijd complexiteit voor elke bewerking die deze ondersteuning biedt voor heeft. Klik op elke opdracht toosee Hallo complexiteit voor elke bewerking.
* Sleutel grootten - moet ik gebruiken kleine sleutelwaarden of grote sleutelwaarden? In het algemeen zijn deze afhankelijk is van Hallo scenario. Als uw scenario grotere sleutels vereist, kunt u Hallo ConnectionTimeout aanpassen en probeer waarden en uw Pogingslogica aanpassen. Vanuit het oogpunt server Redis van lagere waarden in acht genomen toohave betere prestaties.
* Deze overwegingen wekken dat u een hogere waarden niet opslaan in Redis; u moet rekening houden met de Hallo overwegingen te volgen. Latenties wordt hoger zijn. Als u één set gegevens die groter is en een kleinere hebt, kunt u meerdere exemplaren van ConnectionMultiplexer, elk met een andere set waarden voor time-outs en opnieuw hebt geconfigureerd, zoals beschreven in de vorige Hallo [wat Hallo StackExchange.Redis configuratieopties doen](#cache-configuration) sectie.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>Hoe kan ik benchmark en test de prestaties van mijn cache Hallo?
* [Cache diagnostische gegevens inschakelen](cache-how-to-monitor.md#enable-cache-diagnostics) zodat u kunt [monitor](cache-how-to-monitor.md) Hallo status van de cache. U kunt metrische gegevens in hello Azure-portal en u ook kunt Hallo weergeven [downloaden en bekijken](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) ze met Hallo-hulpprogramma's van uw keuze.
* U kunt redis benchmark.exe tooload test uw Redis-server gebruiken.
* Zorg ervoor dat Hallo Hallo load test van de client en Hallo Redis-cache zijn dezelfde regio.
* Gebruik redis cli.exe en Hallo-cache met behulp van Hallo INFO opdracht bewaken.
* Als de belasting wordt veroorzaakt door hoge geheugenfragmentatie, moet u grotere cachegrootte tooa opschalen.
* Zie voor instructies over het downloaden van Hallo Redis-hulpprogramma's, Hallo [hoe kan ik Redis-opdrachten uitvoeren?](#cache-commands) sectie.

Hallo vindt volgende opdrachten u een voorbeeld van het gebruik van redis-benchmark.exe. Voor een nauwkeurige resultaten kunt u deze opdrachten uitvoeren van een virtuele machine in Hallo dezelfde regio bevinden als uw cache.

* Test gebruikt in een pijplijn SET-aanvragen met een 1 k-nettolading

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* Test gebruikt in een pijplijn ophalen aanvragen met een 1 k-nettolading.
  Opmerking: Hallo SET test bovenstaande eerste toopopulate cache uitvoeren

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>Belangrijke informatie over de ThreadPool groei
Hallo CLR ThreadPool heeft twee soorten threads - 'Worker' en 'I/o-voltooiingspoort' (aka Voltooiingspoort) threads.

* Werkthreads worden gebruikt voor de verwerking van de beheerder `Task.Run(…)` of `ThreadPool.QueueUserWorkItem(…)` methoden. Deze threads worden ook gebruikt door diverse onderdelen in Hallo CLR wanneer werk toohappen in een achtergrondthread moet.
* Voltooiingspoort threads worden gebruikt als asynchrone i/o gebeurt (bijvoorbeeld lezen van het Hallo-netwerk).

Hallo-threadgroep biedt nieuwe werkthreads of i/o-voltooiing threads op verzoek (zonder een bandbreedtebeperking) totdat het Hallo 'Minimale' instelling voor elk type thread is bereikt. Minimum aantal threads Hallo is standaard toohello aantal processors op een systeem.

Eenmaal Hallo aantal bestaande (bezet) threads treffers Hallo 'minimale' aantal threads Hallo ThreadPool wordt vertraging Hallo snelheid waarmee het nieuwe threads tooone thread per 500 milliseconden injects. Normaal gesproken als uw systeem een ' burst ' van het werk dat een thread Voltooiingspoort opgehaald, wordt verwerkt die werken zeer snel. Echter als Hallo burst van werk meer is dan Hallo 'Minimale' instelling heeft geconfigureerd, zal er een vertraging bij het verwerken van een gedeelte van Hallo werk zoals hello ThreadPool wordt gewacht op een van twee dingen toohappen.

1. Een bestaande thread wordt gratis tooprocess Hallo werk.
2. Er zijn geen bestaande thread beschikbaar voor 500ms, zodat een nieuwe thread is gemaakt.

In principe betekent dit dat als Hallo aantal threads dat bezet groter dan de Min-threads is, u waarschijnlijk een vertraging 500ms betaalt voordat netwerkverkeer wordt verwerkt door de toepassing hello. Bovendien is het belangrijk toonote dat wanneer een bestaand thread niet langer zijn dan 15 seconden (gebaseerd op wat ik onthouden) actief blijft, zal worden opgeschoond en deze cyclus van groei en inkrimping kunt herhalen.

Als we een foutbericht voorbeeld van StackExchange.Redis (1.0.450 bouwen of hoger), ziet u deze nu wordt afgedrukt ThreadPool-statistieken (Zie Voltooiingspoort- en WERKROLLEN details hieronder).

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

In het vorige voorbeeld hello ziet u dat voor Voltooiingspoort thread 6 bezet threads zijn en Hallo system minimumthreads geconfigureerde tooallow 4. In dit geval Hallo client zou hebben waarschijnlijk gezien twee 500 ms vertragingen omdat 6 > 4.

Houd er rekening mee dat time-outs in StackExchange.Redis kan worden bereikt als groei van Voltooiingspoort of WORKER threads wordt beperkt.

### <a name="recommendation"></a>Aanbeveling
Deze informatie gegeven, wordt aangeraden dat klanten Hallo minimale configuratiewaarde instellen voor Voltooiingspoort en WORKER threads toosomething groter is dan de standaardwaarde Hallo. Er kan geen standaardoplossing leidraad op deze waarde moet omdat Hallo Rechterwaarde voor een toepassing te hoge en lage voor een andere toepassing. Deze instelling kan ook invloed op Hallo prestaties van andere onderdelen van complexe toepassingen, zodat elke klant toofine-afstemmen moet, deze instelling tootheir specifieke moet. Een goed uitgangspunt gebruikt is 200 of 300, en vervolgens testen en indien nodig aanpassen.

Hoe tooconfigure deze instelling:

* Gebruik in ASP.NET, Hallo ["minIoThreads" configuratie-instelling] [ "minIoThreads" configuration setting] onder Hallo `<processModel>` configuratie-element in web.config. Als u in Azure WebSites uitvoert, wordt deze instelling niet beschikbaar via het Hallo-configuratieopties. U moet echter nog steeds kunnen tooconfigure worden deze instelling via programmacode (Zie hieronder) van uw methode Application_Start in global.asax.cs.

  > [!NOTE] 
  > Hallo waarde opgegeven in deze configuratie-element is een *core-* instelling. Bijvoorbeeld, als u een machine 4 kernen hebt en wilt dat uw minIOThreads instelling toobe 200 tijdens runtime, gebruikt u `<processModel minIoThreads="50"/>`.
  >

* Gebruik buiten de ASP.NET-, Hallo [ThreadPool.SetMinThreads(...) ](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) API.

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>Server GC tooget inschakelen meer doorvoer op Hallo client bij gebruik van StackExchange.Redis
Server GC inschakelt, kan optimaliseren Hallo-client en betere prestaties en doorvoer bieden bij het gebruik van StackExchange.Redis. Voor meer informatie over de GC-server en hoe tooenable, Zie Hallo artikelen te volgen:

* [tooenable server GC](https://msdn.microsoft.com/library/ms229357.aspx)
* [De grondbeginselen van garbagecollection](https://msdn.microsoft.com/library/ee787088.aspx)
* [Garbagecollection en prestaties](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>Prestatieoverwegingen rond verbindingen

Elke prijscategorie heeft verschillende beperkingen voor clientverbindingen, geheugen en bandbreedte. Kunt u elke grootte van cache *tot* een bepaald aantal verbindingen, elke tooRedis verbinding heeft de overhead gekoppeld. Een voorbeeld van een dergelijke overhead zou zijn CPU- en geheugengebruik als gevolg van TLS/SSL-versleuteling. Hallo maximale verbindingslimiet voor een opgegeven cachegrootte wordt ervan uitgegaan dat een licht geladen cache. Als uit verbinding overhead laden *plus* laden vanaf de clientbewerkingen dan er capaciteit voor Hallo systeem, Hallo cache kunt capaciteitsproblemen moeten ondervinden zelfs als u hebt niet de verbindingslimiet Hallo voor de huidige cachegrootte Hallo overschreden.

Zie voor meer informatie over de limieten van andere verbindingen Hallo voor elke laag [prijzen van Azure Redis-Cache](https://azure.microsoft.com/pricing/details/cache/). Zie voor meer informatie over verbindingen en andere standaardconfiguraties [serverconfiguratie standaard Redis](cache-configure.md#default-redis-server-configuration).

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>Hoe bewaak ik Hallo status en prestaties van mijn cache?
Exemplaren van Microsoft Azure Redis-Cache kunnen worden bewaakt op Hallo [Azure-portal](https://portal.azure.com). U kunt metrische gegevens weergeven, metrische gegevens grafieken toohello Startboard vastmaken Hallo datum en tijd bereik van de bewaking van grafieken aanpassen, toevoegen en metrische gegevens verwijderen uit Hallo grafieken en waarschuwingen instellen wanneer aan bepaalde voorwaarden wordt voldaan. Zie voor meer informatie [Monitor Azure Redis-Cache](cache-how-to-monitor.md).

Hallo Redis-Cache **Resource menu** bevat ook verschillende hulpprogramma's voor bewaking en probleemoplossing van uw caches.

* **Diagnosticeren en oplossen van problemen met** bevat informatie over veelvoorkomende problemen en strategieën voor het oplossen ervan.
* **Resourcestatus** controleert uw resource en geeft u aan als deze wordt uitgevoerd zoals verwacht. Zie voor meer informatie over health-service van Azure Resource Hallo [overzicht van Azure Resource health](../resource-health/resource-health-overview.md).
* **Nieuw ondersteuningsverzoek** opties tooopen een verzoek om ondersteuning biedt voor uw cache.

Deze hulpprogramma's inschakelen u toomonitor Hallo status van uw Azure Redis-Cache-exemplaren en uw cache in toepassingen te beheren. Zie voor meer informatie, Hallo 'Ondersteuning & instellingen voor het oplossen van problemen' sectie van [hoe tooconfigure Azure Redis-Cache](cache-configure.md).

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>Waarom krijg ik time-outs zien?
Time-outs optreden in Hallo client tootalk tooRedis te gebruiken. Wanneer een opdracht toohello Redis-server verzonden, Hallo-opdracht is in de wachtrij geplaatst en Redis-server uiteindelijk Hallo opdracht opgehaald en deze uitvoert. Echter Hallo-client kunt time-out tijdens dit proces en als dit het geval is een uitzondering optreedt op Hallo side aanroepen. Zie voor meer informatie over het oplossen van problemen met time-out [clientzijde probleemoplossing](cache-how-to-troubleshoot.md#client-side-troubleshooting) en [StackExchange.Redis time-out-uitzonderingen](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions).

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>Waarom is de client verbinding met de Hallo-cache?
Hallo Hier volgen enkele veelvoorkomende reden voor een cache verbinding verbreken.

* Client-side oorzaken
  * Hallo-clienttoepassing is geïmplementeerd.
  * Hallo-clienttoepassing een vergroten/verkleinen is uitgevoerd.
    * In geval van Cloud-Services of Web-Apps Hallo dit kan worden veroorzaakt tooauto schalen.
  * Hallo netwerklaag op Hallo-client is gewijzigd.
  * Tijdelijke fouten opgetreden in het Hallo-client of in Hallo netwerkknooppunten tussen Hallo-client en server Hallo.
  * Hallo bandbreedte drempelwaarde limieten zijn bereikt.
  * CPU-gebonden bewerkingen toocomplete te lang duurde.
* Serverzijde oorzaken
  * Hello Azure Redis-Cache-service gestart op Hallo standaard cache aanbieden, een failover van Hallo primaire knooppunt toohello secundair knooppunt.
  * Azure is patchen Hallo-exemplaar waarop Hallo-cache is geïmplementeerd
    * Dit kan zijn voor Redis-serverupdates of algemeen onderhoud van de virtuele machine.

### <a name="which-azure-cache-offering-is-right-for-me"></a>Welke Azure Cache-aanbieding is juist voor mij?
> [!IMPORTANT]
> Aan de hand van vorig jaar [aankondiging](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/), Azure Managed Cache Service en Azure In-Role Cache service **buiten gebruik gesteld** op 30 November 2016. Onze aanbeveling is toouse [Azure Redis-Cache](https://azure.microsoft.com/services/cache/). Zie voor meer informatie over het migreren van [migreren van Managed Cache Service tooAzure Redis-Cache](cache-migrate-to-redis.md).
>
>

### <a name="azure-redis-cache"></a>Azure Redis-cache
Azure Redis-Cache is algemeen beschikbaar op de grootten van too53 GB en heeft een beschikbaarheids-SLA van 99,9%. Hallo nieuwe [premium-laag](cache-premium-tier-intro.md) biedt grootten van too530 GB en ondersteuning voor clustering, VNET en persistentie, met een SLA met 99,9%.

Azure Redis-Cache geeft klanten Hallo mogelijkheid toouse een beveiligde, toegewezen Redis-cache, beheerd door Microsoft. Met deze aanbieding krijgt u tooleverage Hallo uitgebreide functieset en geleverd door Redis, en betrouwbare hosting en controle van Microsoft-ecosysteem.

In tegenstelling tot traditionele caches die alleen met sleutel-waardeparen te maken, is de Redis populaire voor de maximaal zodat gegevenstypen. Redis ook ondersteunt uitvoering atomische bewerkingen op deze typen, zoals voegen tooa tekenreeks; Hallo-waarde in een hash; en oplopend in stappen pushen tooa lijst. Computing set snijpunt, union en verschil; of ophalen Hallo lid met de hoogste positie in een gesorteerde set. Andere functies bieden ondersteuning voor transacties, pub subitems, Lua scripting, sleutels met een beperkte time to live en configuratie-instellingen toomake Redis werken meer, zoals een traditionele cache.

Een ander belangrijk aspect tooRedis geslaagd is in orde, heldere open-source-ecosysteem Hallo gebaseerd op het. Dit wordt doorgevoerd in diverse Hallo-set met Redis-clients in meerdere talen. Dit ecosysteem en een breed scala aan clients kunt Azure Redis-Cache toobe die wordt gebruikt door vrijwel elke werkbelasting die u in Azure maken wilt.

Zie voor meer informatie over aan de slag met Azure Redis-Cache, [hoe tooUse Azure Redis-Cache](cache-dotnet-how-to-use-azure-redis-cache.md) en [documentatie van Azure Redis-Cache](index.md).

### <a name="managed-cache-service"></a>Beheerde cacheservice
[Managed Cache service 30 November 2016 buiten gebruik werd gesteld.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview gearchiveerd documentatie, Zie [gearchiveerde Managed Cache Service documentatie](https://msdn.microsoft.com/library/azure/dn386094.aspx).

### <a name="in-role-cache"></a>In-Role Cache
[In-Role Cache 30 November 2016 buiten gebruik werd gesteld.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview gearchiveerd documentatie, Zie [gearchiveerde In-Role Cache documentatie](https://msdn.microsoft.com/library/azure/dn386103.aspx).

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
