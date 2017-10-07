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
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Provider voor de uitvoercache van ASP.NET voor Azure Redis-Cache
Hallo Cacheprovider Redis is een opslagmechanisme voor out-of-process-voor de uitvoergegevens van de cache. Deze gegevens zijn specifiek voor volledige HTTP-antwoorden (pagina uitvoercaching). Hallo-provider in Hallo nieuwe uitvoer cache provider uitbreidbaar punt die is geïntroduceerd in ASP.NET 4 wordt geplaatst.

toouse hello Cacheprovider Redis uw cache eerst configureren en configureer vervolgens uw ASP.NET-toepassing met Hallo Redis uitvoer Cache Provider NuGet-pakket. In dit onderwerp bevat richtlijnen over het configureren van uw toepassing toouse hello Cacheprovider Redis. Zie voor meer informatie over het maken en configureren van een Azure Redis-Cache-exemplaar [een cache maken](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

## <a name="store-aspnet-page-output-in-hello-cache"></a>ASP.NET-pagina-uitvoer opslaan in cache van de Hallo
tooconfigure een clienttoepassing in Visual Studio met Hallo Redis-Cache sessie status NuGet-pakket, klikt u op **NuGet Package Manager**, **Package Manager Console** van Hallo **extra** menu.

Voer hello na de opdracht van Hallo `Package Manager Console` venster.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

Hallo Redis uitvoer Cache Provider NuGet-pakket heeft een afhankelijkheid op Hallo StackExchange.Redis.StrongName pakket. Als Hallo StackExchange.Redis.StrongName pakket niet aanwezig in uw project is, wordt deze geïnstalleerd. Zie voor meer informatie over Hallo Redis uitvoer Cache Provider NuGet-pakket Hallo [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet-pagina.

>[!NOTE]
>In aanvulling toohello sterke naam StackExchange.Redis.StrongName pakket is er ook Hallo StackExchange.Redis niet-sterke naam versie. Als uw project Hallo niet-sterke naam StackExchange.Redis versie dat moet u deze verwijderen, ophalen anders u naamconflicten in uw project. Zie voor meer informatie over deze pakketten [cacheclients configureren .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hallo NuGet-pakket downloadt en voegt Hallo vereiste assembly verwijst naar Hallo volgende sectie in het web.config-bestand wordt toegevoegd. Deze sectie bevat de vereiste configuratie voor uw ASP.NET-toepassing toouse hello Cacheprovider Redis Hallo.

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

Hallo toegelicht sectie bevat een voorbeeld van het Hallo-kenmerken en voorbeelden van instellingen voor elk kenmerk.

Hallo-kenmerken configureren met waarden uit de cacheblade van uw in Microsoft Azure-portal Hallo Hallo en configureer andere waarden naar wens Hallo. Zie voor instructies over de toegang tot de eigenschappen van uw cache [configureren Redis-cache-instellingen](cache-configure.md#configure-redis-cache-settings).

* **host** – Geef uw cache-eindpunt.
* **poort** – uw niet-SSL-poort of uw SSL-poort, afhankelijk van het ssl-instellingen hello gebruiken.
* **accessKey** – beide Hallo primaire of secundaire sleutel gebruiken voor uw cache.
* **SSL** : true als u wilt dat toosecure cache/clientcommunicatie met ssl; anders ONWAAR. Ervoor toospecify Hallo de juiste poort zijn.
  * Hallo niet-SSL-poort is standaard uitgeschakeld voor nieuwe caches. Geef op waar om deze instelling toouse Hallo SSL-poort. Zie voor meer informatie over het inschakelen van niet-SSL-poort Hallo Hallo [toegangspoorten](cache-configure.md#access-ports) sectie in Hallo [een cache configureren](cache-configure.md) onderwerp.
* **databaseId** – opgegeven welke database toouse voor cache uitvoergegevens. Als niet wordt opgegeven, wordt de standaardwaarde Hallo van 0 gebruikt.
* **applicationName** – sleutels worden opgeslagen in redis als `<AppName>_<SessionId>_Data`. Deze schematische kan meerdere toepassingen tooshare Hallo dezelfde sleutel. Deze parameter is optioneel en als u niet beschikken over een standaardwaarde wordt gebruikt.
* **connectionTimeoutInMilliseconds** – deze instelling kunt u toooverride hello connectTimeout instellen in de client StackExchange.Redis Hallo. Als niet wordt opgegeven, wordt de Hallo standaardinstelling connectTimeout van 5000 gebruikt. Zie voor meer informatie [configuratiemodel StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** – deze instelling kunt u toooverride hello syncTimeout instellen in de client StackExchange.Redis Hallo. Als niet wordt opgegeven, wordt Hallo standaardinstelling syncTimeout 1000 gebruikt. Zie voor meer informatie [configuratiemodel StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Een OutputCache-instructie tooeach pagina waarvoor toocache Hallo uitvoer toevoegen.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

In het vorige voorbeeld Hallo Hallo cache pagina gegevens blijven in de cache Hallo gedurende 60 seconden en een andere versie van de pagina Hallo voor elke parametercombinatie in de cache wordt opgeslagen. Zie voor meer informatie over de OutputCache-instructie Hallo [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).

Zodra deze stappen worden uitgevoerd, is uw toepassing hello geconfigureerde toouse Cacheprovider Redis.

## <a name="next-steps"></a>Volgende stappen
Bekijk Hallo [ASP.NET Session State-Provider voor Azure Redis-Cache](cache-aspnet-session-state-provider.md).

