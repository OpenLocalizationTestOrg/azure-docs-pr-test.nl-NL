---
title: aaaHow tootroubleshoot Azure Redis-Cache | Microsoft Docs
description: Meer informatie over hoe tooresolve algemene problemen met een Azure Redis-Cache.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 928b9b9c-d64f-4252-884f-af7ba8309af6
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 4e736fce2b6d5200a2a8d802f3f1384b63458cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-azure-redis-cache"></a>Hoe tootroubleshoot Azure Redis-Cache
Dit artikel bevat richtlijnen voor het Hallo volgende categorieën van Azure Redis-Cache-problemen oplossen.

* [Client-side probleemoplossing](#client-side-troubleshooting) - in deze sectie bevat richtlijnen te identificeren en het oplossen van problemen veroorzaakt door Hallo toepassing verbinden tooAzure Redis-Cache.
* [Server side probleemoplossing](#server-side-troubleshooting) - in deze sectie bevat richtlijnen te identificeren en het oplossen van problemen veroorzaakt op Hallo van Azure Redis-Cache-serverzijde.
* [StackExchange.Redis time-out-uitzonderingen](#stackexchangeredis-timeout-exceptions) -in deze sectie bevat informatie over het oplossen van problemen bij het gebruik van de client StackExchange.Redis Hallo.

> [!NOTE]
> Aantal Hallo stappen in deze handleiding voor probleemoplossing bevatten instructies toorun Redis-opdrachten en verschillende maatstaven voor prestaties bewaken. Zie voor meer informatie en instructies Hallo artikelen in Hallo [aanvullende informatie](#additional-information) sectie.
> 
> 

## <a name="client-side-troubleshooting"></a>Client-side probleemoplossing
Deze sectie wordt beschreven voor het oplossen van problemen die vanwege een voorwaarde op Hallo-clienttoepassing optreden.

* [Geheugendruk op Hallo-client](#memory-pressure-on-the-client)
* [Burst van verkeer](#burst-of-traffic)
* [Hoge client CPU-gebruik](#high-client-cpu-usage)
* [Client-Side bandbreedte overschreden](#client-side-bandwidth-exceeded)
* [De grootte van veel aanvragen/reacties](#large-requestresponse-size)
* [Wat is er gebeurd toomy gegevens in Redis?](#what-happened-to-my-data-in-redis)

### <a name="memory-pressure-on-hello-client"></a>Geheugendruk op Hallo-client
#### <a name="problem"></a>Probleem
Geheugendruk op de clientcomputer Hallo leidt tooall soorten prestatieproblemen die de verwerking van gegevens die zijn verzonden door Hallo Redis exemplaar zonder enige vertraging kunnen worden vertraagd. Wanneer geheugendruk raakt, heeft Hallo system doorgaans toopage gegevens uit het fysieke geheugen toovirtual geheugen op de schijf. Dit *pagina met fout* oorzaken Hallo system tooslow omlaag aanzienlijk.

#### <a name="measurement"></a>Meting
1. Geheugengebruik op machine toomake ervoor dat het beschikbare geheugen niet overschrijdt. 
2. Monitor Hallo `Page Faults/Sec` prestatiemeteritem. De meeste systemen wordt hebben sommige wisselbestandsfouten zelfs tijdens normale werking, dus pieken in dit prestatiemeteritem voor pagina-fouten die met time-outs overeenkomen gecontroleerd.

#### <a name="resolution"></a>Oplossing
Upgrade voor de client tooa groter client VM-grootte met meer geheugen of verdiepen in uw consuption geheugen gebruikspatronen tooreduce geheugen.

### <a name="burst-of-traffic"></a>Burst van verkeer
#### <a name="problem"></a>Probleem
Bursts van verkeer, gecombineerd met slecht `ThreadPool` instellingen kunnen leiden tot vertragingen bij het verwerken van gegevens die al zijn verzonden door Hallo Redis-Server maar nog niet aan de clientzijde Hallo verbruikt.

#### <a name="measurement"></a>Meting
Monitor hoe uw `ThreadPool` statistieken wijzigen gedurende een periode met code [zoals deze](https://github.com/JonCole/SampleCode/blob/master/ThreadPoolMonitor/ThreadPoolLogger.cs). U kunt ook zoeken op Hallo `TimeoutException` bericht van StackExchange.Redis. Hier volgt een voorbeeld:

    System.TimeoutException: Timeout performing EVAL, inst: 8, mgr: Inactive, queue: 0, qu: 0, qs: 0, qc: 0, wr: 0, wq: 0, in: 64221, ar: 0, 
    IOCP: (Busy=6,Free=999,Min=2,Max=1000), WORKER: (Busy=7,Free=8184,Min=2,Max=8191)

In Hallo boven bericht zijn er verschillende problemen die interessante zijn:

1. U ziet dat in Hallo `IOCP` sectie en Hallo `WORKER` sectie die u hebt een `Busy` waarde die groter is dan Hallo `Min` waarde. Dit betekent dat uw `ThreadPool` instellingen moeten aan te passen.
2. U ziet ook `in: 64221`. Dit geeft aan dat 64211 bytes zijn ontvangen op Hallo kernel socket layer maar nog niet zijn gelezen door Hallo-toepassing (bijvoorbeeld StackExchange.Redis). Dit betekent doorgaans dat uw toepassing wordt niet lezen van gegevens vanaf het netwerk Hallo snel Hallo-server verzendt het tooyou.

#### <a name="resolution"></a>Oplossing
Configureer uw [ThreadPool instellingen](https://gist.github.com/JonCole/e65411214030f0d823cb) toomake ervoor dat de thread-groep snel onder wordt opschalen burst scenario's.

### <a name="high-client-cpu-usage"></a>Hoge client CPU-gebruik
#### <a name="problem"></a>Probleem
Hoog CPU-gebruik op Hallo-client is een indicatie dat Hallo-systeem met Hallo werk dat deze is gevraagd tooperform niet kan bijhouden. Dit betekent dat clientcomputers Hallo tooprocess een reactie van Redis op tijdige wijze kan mislukken ondanks dat Redis antwoord verzonden door Hallo zeer snel.

#### <a name="measurement"></a>Meting
Monitor Hallo System Wide CPU-gebruik via hello Azure Portal of via Hallo gekoppelde prestatiemeteritem. Wees voorzichtig niet toomonitor *proces* CPU omdat er een enkel proces lage CPU-gebruik op Hallo dezelfde tijd dat het hele systeem CPU hoge kan worden. Pieken in CPU-gebruik die met time-outs overeenkomen gecontroleerd. Als gevolg van een hoog CPU, u ziet misschien ook hoog `in: XXX` in waarden `TimeoutException` foutberichten zoals beschreven in Hallo [Burst van verkeer](#burst-of-traffic) sectie.

> [!NOTE]
> StackExchange.Redis 1.1.603 en hoger bevat Hallo `local-cpu` metrische in `TimeoutException` foutberichten. Zorg ervoor dat u de nieuwste versie Hallo Hallo [NuGet-pakket StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/). Er zijn fouten voortdurend worden gecorrigeerd in Hallo code toomake krachtiger tootimeouts zodanig dat de meest recente versie Hallo belangrijk is.
> 
> 

#### <a name="resolution"></a>Oplossing
Upgrade tooa groter VM-grootte met meer CPU-capaciteit uit of onderzoeken wat de oorzaak van CPU, pieken. 

### <a name="client-side-bandwidth-exceeded"></a>Client-side bandbreedte overschreden
#### <a name="problem"></a>Probleem
Clientcomputers van verschillende grootte hebben hun beperkingen op de hoeveelheid netwerkbandbreedte ze beschikbaar zijn. Als client Hallo overschrijdt Hallo beschikbare bandbreedte en gegevens niet snel Hallo-server verzendt deze aan de clientzijde Hallo worden verwerkt. Dit kan leiden tootimeouts.

#### <a name="measurement"></a>Meting
Controleren hoe uw bandbreedtegebruik wijzigen gedurende een periode met code [zoals deze](https://github.com/JonCole/SampleCode/blob/master/BandWidthMonitor/BandwidthLogger.cs). Houd er rekening mee dat deze code kan niet worden uitgevoerd in sommige omgevingen met beperkte machtigingen (zoals Azure websites).

#### <a name="resolution"></a>Oplossing
Client VM-grootte vergroten of verkleinen van netwerkbandbreedte.

### <a name="large-requestresponse-size"></a>De grootte van veel aanvragen/reacties
#### <a name="problem"></a>Probleem
Een veel aanvragen/reacties kan leiden tot time-outs. Stel bijvoorbeeld dat uw time-outwaarde die is geconfigureerd op de client is 1 seconde. Uw toepassing aanvragen twee sleutels (bijvoorbeeld) "A" en "B") op Hallo hetzelfde moment (met behulp van dezelfde fysieke netwerkverbinding Hallo). De meeste clients ondersteunen 'Pipelining' van aanvragen, zodat zowel aanvragen "A" en "B" worden verzonden op Hallo kabel toohello server na Hallo andere zonder te wachten Hallo-antwoorden. Hallo server stuurt Hallo-antwoorden weer Hallo dezelfde volgorde. Als antwoord "A" groot kunt is het meeste Hallo time-out voor volgende aanvragen eat. 

Hallo volgende voorbeeld laat zien in dit scenario. In dit scenario worden in aanvraag "A" en "B" verzonden snel Hallo server begint met het verzenden van antwoorden "A" en "B" snel, maar vanwege de overdrachtstijd gegevens hangen "B" achter andere aanvraag en time-out Hallo Hoewel Hallo server snel gereageerd.

    |-------- 1 Second Timeout (A)----------|
    |-Request A-|
         |-------- 1 Second Timeout (B) ----------|
         |-Request B-|
                |- Read Response A --------|
                                           |- Read Response B-| (**TIMEOUT**)



#### <a name="measurement"></a>Meting
Dit is een moeilijk één toomeasure. U hebt in feite tooinstrument uw code tootrack grote clientaanvragen en antwoorden. 

#### <a name="resolution"></a>Oplossing
1. Redis is geoptimaliseerd voor een groot aantal kleine waarden in plaats van enkele grote waarden. Hallo bij voorkeur oplossing is toobreak van uw gegevens naar gerelateerde kleinere waarden. Zie Hallo [wat Hallo ideale grootte waardebereik voor redis is? 100KB te groot is? ](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) post een bericht voor meer informatie over waarom de lagere waarden worden aanbevolen.
2. Hallo vergroten van de virtuele machine (voor client en Server voor Redis-Cache), tooget hogere bandbreedte mogelijkheden, waardoor gegevens overbrengen tijden voor grotere antwoorden. Houd er rekening mee dat meer bandbreedte ophalen op net Hallo-server of alleen op Hallo client mogelijk niet voldoende. Meet het bandbreedteverbruik en vergelijken het toohello mogelijkheden van de grootte van virtuele machine die u momenteel hebt Hallo.
3. Hallo aantal verhogen `ConnectionMultiplexer` objecten u gebruik en round robin-aanvragen via andere verbindingen.

### <a name="what-happened-toomy-data-in-redis"></a>Wat is er gebeurd toomy gegevens in Redis?
#### <a name="problem"></a>Probleem
Ik verwachtte voor bepaalde gegevens toobe in mijn Azure Redis-Cache-exemplaar, maar het toobe er niet lijkt.

#### <a name="resolution"></a>Oplossing
Zie [wat is er gebeurd toomy gegevens in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) voor mogelijke oorzaken en oplossingen.

## <a name="server-side-troubleshooting"></a>Server side problemen oplossen
Deze sectie wordt beschreven voor het oplossen van problemen die vanwege een voorwaarde op Hallo cacheserver optreden.

* [Geheugendruk op Hallo-server](#memory-pressure-on-the-server)
* [Hoog CPU-gebruik / Server laden](#high-cpu-usage-server-load)
* [Server Side bandbreedte is overschreden](#server-side-bandwidth-exceeded)

### <a name="memory-pressure-on-hello-server"></a>Geheugendruk op Hallo-server
#### <a name="problem"></a>Probleem
Geheugendruk aan serverzijde Hallo leidt tooall soorten prestatieproblemen die de verwerking van aanvragen kunnen vertragen. Wanneer geheugendruk raakt, heeft Hallo system doorgaans toopage gegevens uit het fysieke geheugen toovirtual geheugen op de schijf. Dit *pagina met fout* oorzaken Hallo system tooslow omlaag aanzienlijk. Er zijn verschillende mogelijke oorzaken van dit geheugendruk: 

1. U kunt Hallo cache toofull capaciteit hebt ingevuld met gegevens. 
2. Redis ziet hoge geheugenfragmentatie - meestal veroorzaakt door het opslaan van grote objecten (Redis is geoptimaliseerd voor een kleine objecten - Zie Hallo [wat Hallo ideale grootte waardebereik voor redis is? 100KB te groot is? ](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) post een bericht voor meer informatie). 

#### <a name="measurement"></a>Meting
Redis beschrijft de twee metrische gegevens kunt u dit probleem identificeren. Hallo wordt eerst `used_memory` en andere Hallo `used_memory_rss`. [Deze metrische gegevens](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) zijn beschikbaar in hello Azure Portal of via Hallo [Redis INFO](http://redis.io/commands/info) opdracht.

#### <a name="resolution"></a>Oplossing
Er zijn verschillende mogelijke wijzigingen die u toohelp keep-geheugengebruik in orde aanbrengen kunt:

1. [Configureer een beleid geheugen](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) en verlopen tijdstippen instellen op uw sleutels. Houd er rekening mee dat dit mogelijk niet voldoende als er fragmentatie.
2. [Een waarde maxmemory gereserveerd configureert](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) die groot genoeg toocompensate voor geheugenfragmentatie.
3. Verdeel uw grote objecten in de cache in kleinere verwante objecten.
4. [Schaal](cache-how-to-scale.md) tooa groter cachegrootte.
5. Als u een [premium cache met Redis-cluster ingeschakeld](cache-how-to-premium-clustering.md) kunt u [Verhoog het aantal shards hello](cache-how-to-premium-clustering.md#change-the-cluster-size-on-a-running-premium-cache).

### <a name="high-cpu-usage--server-load"></a>Hoog CPU-gebruik / Server laden
#### <a name="problem"></a>Probleem
Hoog CPU-gebruik kan betekenen dat de clientzijde Hallo tooprocess een reactie van Redis tijdig mislukken zelfs als Redis antwoord verzonden door Hallo zeer snel.

#### <a name="measurement"></a>Meting
Monitor Hallo System Wide CPU-gebruik via hello Azure Portal of via Hallo gekoppelde prestatiemeteritem. Wees voorzichtig niet toomonitor *proces* CPU omdat er een enkel proces lage CPU-gebruik op Hallo dezelfde tijd dat het hele systeem CPU hoge kan worden. Pieken in CPU-gebruik die met time-outs overeenkomen gecontroleerd.

#### <a name="resolution"></a>Oplossing
[Schaal](cache-how-to-scale.md) tooa grotere cache servicetier met meer CPU-capaciteit of onderzoeken wat de oorzaak van CPU, pieken. 

### <a name="server-side-bandwidth-exceeded"></a>Server Side bandbreedte is overschreden
#### <a name="problem"></a>Probleem
Exemplaren van verschillende grootte cache hebben hun beperkingen op de hoeveelheid netwerkbandbreedte ze beschikbaar zijn. Als server Hallo overschrijdt de beschikbare bandbreedte van hello, klikt u vervolgens gegevens niet verzonden toohello client zo snel. Dit kan leiden tootimeouts.

#### <a name="measurement"></a>Meting
U kunt bewaken Hallo `Cache Read` metrische gegevens Hallo hoeveelheid gegevens gelezen uit de cache Hallo in Megabytes per seconde (MB/s) tijdens Hallo opgegeven reporting interval is. Deze waarde komt overeen toohello netwerkbandbreedte gebruikt door deze cache. Als u tooset van waarschuwingen voor bandbreedtelimieten van server side netwerk wilt, u kunt ze maken gebruik van deze `Cache Read` teller. Vergelijk uw metingen met Hallo-waarden in de [deze tabel](cache-faq.md#cache-performance) voor Hallo in acht genomen ondergrenzen voor verschillende cache prijzen lagen en grootten voor de bandbreedte.

#### <a name="resolution"></a>Oplossing
Als u bijna Hallo waargenomen maximale bandbreedte voor de grootte van uw prijscategorie laag en cache consistent zijn, kunt u overwegen [schalen](cache-how-to-scale.md) tooa prijzen laag of de grootte die een groter netwerkbandbreedte heeft, met behulp van Hallo-waarden in [deze tabel](cache-faq.md#cache-performance) als richtlijn.

## <a name="stackexchangeredis-timeout-exceptions"></a>StackExchange.Redis time-out-uitzonderingen
Configuratie-instelling met de naam maakt gebruik van StackExchange.Redis `synctimeout` voor synchrone bewerkingen waarvoor een standaardwaarde van 1000 ms. Als een synchrone aanroep niet voltooit bepaald Hallo tijd, Hallo StackExchange.Redis client er wordt een time-fout vergelijkbare toohello voorbeeld te volgen.

    System.TimeoutException: Timeout performing MGET 2728cc84-58ae-406b-8ec8-3f962419f641, inst: 1,mgr: Inactive, queue: 73, qu=6, qs=67, qc=0, wr=1/1, in=0/0 IOCP: (Busy=6, Free=999, Min=2,Max=1000), WORKER (Busy=7,Free=8184,Min=2,Max=8191)


Dit foutbericht bevat metrische gegevens die kunnen helpen bij het wijst u toohello oorzaak en de mogelijke resolutie van Hallo probleem. Hallo bevat volgende tabel details over Hallo fout bericht metrische gegevens.

| Fout bericht metrische gegevens | Details |
| --- | --- |
| inst |In de afgelopen tijdsperiode Hallo: 0-opdrachten zijn uitgegeven |
| Mgr |Hallo socket manager voert `socket.select` wat het betekent dat vraagt Hallo OS tooindicate een socket met iets toodo; in feite: Hallo lezer is niet actief lezen vanaf het netwerk Hallo omdat deze niet denkt dat iets toodo |
| Wachtrij |Er zijn 73 totale voortgang-bewerkingen |
| Qu |6 van Hallo lopende bewerkingen zijn in de niet-verzonden wachtrij Hallo en zijn niet nog weggeschreven toohello uitgaande netwerk |
| Qs |67 van he lopende bewerkingen toohello server zijn verzonden, maar een antwoord is nog niet beschikbaar. antwoord Hallo kan worden `Not yet sent by hello server` of`sent by hello server but not yet processed by hello client.` |
| QC |0 van Hallo lopende bewerkingen antwoorden hebt gezien, maar zijn niet nog gemarkeerd als voltooid vanwege toowaiting op Hallo voltooiing lus |
| wR |Er is een actieve schrijver (wat betekent dat Hallo 6 unsent aanvragen worden niet genegeerd) bytes/activewriters |
| in |Er zijn geen actieve lezers en nul bytes beschikbaar toobe lezen op Hallo NIC bytes/activereaders |

### <a name="steps-tooinvestigate"></a>Stappen tooinvestigate
1. Als best practice Controleer of u Hallo tooconnect patroon volgen wanneer u de client StackExchange.Redis Hallo gebruikt.

    ```c#
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ````

    Zie voor meer informatie [toohello-cache met behulp van StackExchange.Redis verbinding](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).

1. Zorg ervoor dat uw Azure Redis-Cache en het Hallo-clienttoepassing Hallo dezelfde regio in Azure. Bijvoorbeeld, u kan zich voordoen time-outs wanneer uw cache in VS-Oost, maar Hallo client bevindt zich in VS-West en Hallo-aanvraag niet voltooid binnen de Hallo `synctimeout` interval of u kunt zich voordoen time-outs wanneer u foutopsporing van uw lokale ontwikkelcomputer. 
   
    Het is raadzaam toohave Hallo cache en Hallo in Hallo-client in dezelfde Azure-regio. Als u een scenario met aanroepen tussen regio hebt, moet u instellen Hallo `synctimeout` tooa intervalwaarde hoger is dan Hallo standaardinterval 1000 ms door een `synctimeout` eigenschap in de verbindingsreeks Hallo. Hallo volgende voorbeeld ziet u een fragment StackExchange.Redis cache verbinding tekenreeks met een `synctimeout` van 2000 ms.
   
        synctimeout=2000,cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...
2. Zorg ervoor dat u de nieuwste versie Hallo Hallo [NuGet-pakket StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/). Er zijn fouten voortdurend worden gecorrigeerd in Hallo code toomake krachtiger tootimeouts zodanig dat de meest recente versie Hallo belangrijk is.
3. Als er aanvragen die ophalen door bandbreedtebeperkingen op Hallo-server of client gebonden zijn, duurt het langer voor hen toocomplete, waardoor time-outs. toosee als de time-out is vanwege toonetwork bandbreedte op Hallo van server, raadpleegt u [bandbreedte van de Server-side overschreden](#server-side-bandwidth-exceeded). toosee als de time-out is vanwege tooclient netwerkbandbreedte, Zie [Client side bandbreedte overschreden](#client-side-bandwidth-exceeded).
4. U ophalen van de CPU of zijn gekoppeld op Hallo-server op Hallo client?
   
   * Controleer of u ophalen gebonden aan de CPU op de client waardoor Hallo aanvraag toonot kan worden verwerkt binnen Hallo `synctimeout` interval, hetgeen een time-out. Tooa groter client verplaatsen of distributie van Hallo load kunt toocontrol dit. 
   * Controleer of uw CPU gebonden op Hallo server door de bewaking van Hallo `CPU` [prestaties metrische gegevens in de cache](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Aanvragen terwijl Redis is afhankelijk van de CPU kan leiden tot de binnenkomende aanvragen tootimeout. tooaddress dit u Hallo kunt distribueren over meerdere shards in een cache premium laden of tooa groter of prijscategorie upgraden. Zie voor meer informatie [Server Side bandbreedte overschreden](#server-side-bandwidth-exceeded).
5. Zijn er opdrachten duurt lang tooprocess op Hallo server? Langlopende opdrachten die het duurt lang tooprocess op Hallo redis-server kan leiden tot time-outs. Enkele voorbeelden van langdurige opdrachten zijn `mget` met een groot aantal sleutels, `keys *` of slecht geschreven scripts lua. U kunt verbinding tooyour Azure Redis-Cache-exemplaar met behulp van Hallo redis cli client of Hallo [Redis-Console](cache-configure.md#redis-console) en Voer Hallo [SlowLog](http://redis.io/commands/slowlog) opdracht toosee als er aanvragen duurt langer dan verwacht. Redis-Server en StackExchange.Redis zijn geoptimaliseerd voor veel kleine aanvragen in plaats van minder grote aanvragen. Uw gegevens splitsen in kleinere reeksen kan dingen hier verbeteren. 
   
    Zie voor informatie over het verbinden van toohello Azure Redis-Cache SSL-eindpunt met redis cli en stunnel, Hallo [aangekondigd ASP.NET Session State-Provider voor de Preview-versie Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) blogbericht. Zie voor meer informatie [SlowLog](http://redis.io/commands/slowlog).
6. Hoge belasting van de Redis-server kan leiden tot time-outs. U kunt de serverbelasting Hallo bewaken door bewaking Hallo `Redis Server Load` [prestaties metrische gegevens in de cache](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Belasting van de server van 100 (maximumwaarde) geeft aan dat Hallo redis server actief is bezig met geen niet-actieve tijd verwerken van aanvragen. toosee als bepaalde verzoeken van alle server-functie hello, Hallo SlowLog opdracht uitvoeren, zoals beschreven in de vorige alinea Hallo. Zie voor meer informatie [hoog CPU-gebruik / Server laden](#high-cpu-usage-server-load).
7. Is er een andere gebeurtenis aan clientzijde Hallo die kan worden gelegd een blip netwerk? Controleer op Hallo-client (web, werkrol of een Iaas VM) als er een gebeurtenis als het aantal exemplaren van de client Hallo schaal omhoog of omlaag of implementeren van een nieuwe versie van de client Hallo is of automatisch schalen is ingeschakeld? Bij onze tests die hebben we gevonden voor automatisch schalen of omhoog/omlaag schalen kan veroorzaken kan uitgaande netwerkverbinding verloren zijn enkele seconden. StackExchange.Redis code robuuste toosuch gebeurtenissen is en verbinding wordt hersteld. Alle aanvragen in wachtrij voor Hallo kunnen tijdens deze periode van opnieuw verbinding een time-out.
8. Is er een grote aanvraag voorafgaand aan verschillende kleine aanvragen toohello Redis-Cache waarvoor een time-out? parameter Hallo `qs` Hallo fout bericht vertelt u hoeveel aanvragen van Hallo client toohello server zijn verzonden, maar nog niet zijn verwerkt op een antwoord. Deze waarde kan blijven groeien omdat StackExchange.Redis één TCP-verbinding gebruikt en alleen van een reactie op een tijdstip lezen kan. Hoewel er is een time-out opgetreden voor de eerste bewerking hello, stopt niet Hallo-gegevens worden verzonden vanaf de server Hallo en andere aanvragen worden geblokkeerd totdat dit proces is voltooid, waardoor een time-out. Eén oplossing is toominimize Hallo kans time-outs door ervoor te zorgen dat uw cache groot genoeg is voor uw workload is en grote waarden splitsen in kleinere reeksen. Een andere mogelijke oorzaak is toouse een groep met `ConnectionMultiplexer` in uw client-objecten en kies Hallo minste geladen `ConnectionMultiplexer` bij het verzenden van een nieuwe aanvraag. Hierdoor moet een enkel time-out veroorzaakt door andere aanvragen tooalso time-out.
9. Als u `RedisSessionStateprovider`, controleert u Hallo opnieuw time-out correct hebt ingesteld. `retrytimeoutInMilliseconds`moet hoger zijn dan `operationTimeoutinMilliseonds`, anders geen nieuwe pogingen wordt uitgevoerd. In het volgende voorbeeld Hallo `retrytimeoutInMilliseconds` too3000 is ingesteld. Zie voor meer informatie [ASP.NET Session State-Provider voor Azure Redis-Cache](cache-aspnet-session-state-provider.md) en [hoe toouse configuratieparameters van sessiestatus-Provider en de Provider voor de uitvoercache Hallo](https://github.com/Azure/aspnet-redis-providers/wiki/Configuration).

    <add
      name="AFRedisCacheSessionStateProvider"
      type="Microsoft.Web.Redis.RedisSessionStateProvider"
      host="enbwcache.redis.cache.windows.net"
      port="6380"
      accessKey="…"
      ssl="true"
      databaseId="0"
      applicationName="AFRedisCacheSessionState"
      connectionTimeoutInMilliseconds = "5000"
      operationTimeoutInMilliseconds = "1000"
      retryTimeoutInMilliseconds="3000" />


1. Controleer geheugengebruik op Hallo Azure Redis-Cache-server door [bewaking](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) `Used Memory RSS` en `Used Memory`. Als een beleid voor verwijdering gemaakt is, Redis wordt gestart wanneer onbeschikbaar maken van sleutels `Used_Memory` bereikt Hallo cachegrootte. In het ideale geval `Used Memory RSS` moet slechts iets hoger dan `Used memory`. Een grote verschil betekent dat er geheugenfragmentatie (intern of extern. Wanneer `Used Memory RSS` is minder dan `Used Memory`, betekent dit deel van het cachegeheugen Hallo heeft zijn gewisseld door Hallo-besturingssysteem. In dat geval kunt u een aantal belangrijke latenties verwachten. Omdat Redis heeft geen controle hoe de toewijzingen worden toegewezen toomemory pagina's, hoge `Used Memory RSS` is vaak Hallo resultaat van een piek in geheugengebruik. Redis maakt vrij geheugen, Hallo geheugen terug toohello toewijzer wordt gegeven als Hallo toewijzingsfunctie mogelijk of Hallo geheugen back toohello system kan niet worden geven. Er is mogelijk een discrepantie tussen Hallo `Used Memory` verbruik waarde en geheugen zoals gemeld door het Hallo-besturingssysteem. Kan worden veroorzaakt door toohello feit geheugen is gebruikt en door Redis, maar niet gegeven back toohello system uitgebracht. toohelp beperken geheugenproblemen u Hallo stappen kunt uitvoeren.
   
   * Hallo tooa groter cachegrootte bijwerken zodat u niet mogelijkheden geheugenbeperkingen op Hallo-systeem uitvoert.
   * Vervaldatum tijden op Hallo sleutels zo instellen dat oudere waarden proactief zijn verwijderd.
   * Monitor Hallo Hallo `used_memory_rss` metrische gegevens in de cache. Wanneer deze waarde Hallo grootte van de cache nadert, bent u waarschijnlijk toostart prestatieproblemen te zien. Verdelen over meerdere shards Hallo gegevens als u met behulp van een premium-cache, of een grotere cachegrootte tooa upgrade.
   
   Zie voor meer informatie [geheugendruk op Hallo server](#memory-pressure-on-the-server).

## <a name="additional-information"></a>Aanvullende informatie
* [Welk aanbod voor de Redis-cache en welke cachegrootte moet ik kiezen?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)
* [Hoe kan ik benchmark en test de prestaties van mijn cache Hallo?](cache-faq.md#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Hoe kan ik de Redis-opdrachten uitvoeren?](cache-faq.md#how-can-i-run-redis-commands)
* [Hoe toomonitor Azure Redis-Cache](cache-how-to-monitor.md)

