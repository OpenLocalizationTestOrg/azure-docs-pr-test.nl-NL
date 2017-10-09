---
title: Voorbeelden van aaaAzure Redis-Cache | Microsoft Docs
description: Meer informatie over hoe toouse Azure Redis-Cache
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a>Azure Redis-Cache-voorbeelden
Dit onderwerp bevat een lijst met voorbeelden van Azure Redis-Cache, die betrekking hebben op scenario's zoals tooa cache verbinding te maken, lezen en schrijven van gegevens tooand uit de cache en Hallo-providers voor ASP.NET Redis-Cache. Aantal steekproeven Hallo downloadbare projecten zijn en sommige bieden stapsgewijze instructies en codefragmenten bevatten, maar niet tooa downloadbare project koppelen.

## <a name="hello-world-samples"></a>Hallo wereld-voorbeelden
Hallo-voorbeelden in deze sectie laten zien Hallo basisbeginselen van Azure Redis-Cache-exemplaar tooan verbinding te maken en lezen en schrijven van gegevens toohello cache met behulp van verschillende talen en Redis-clients.

Hallo [Hallo wereld](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) voorbeeld toont hoe tooperform verschillende bewerkingen met behulp van Hallo cache [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET-client.

In dit voorbeeld laat zien hoe:

* Gebruik verschillende verbindingsopties
* Lezen en schrijven van objecten tooand op Hallo-cache met behulp van synchrone en asynchrone bewerkingen
* Gebruik Redis MGET/MSET opdrachten tooreturn waarden van de opgegeven sleutels
* Redis transactionele bewerkingen uitvoeren
* Werken met Redis-lijsten en gesorteerde sets
* .NET-objecten met behulp van JsonConvert objectserializers opslaan
* Gebruik Redis ingesteld tooimplement tagging
* Werken met Redis-Cluster

Zie voor meer informatie, Hallo [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) documentatie op github, en voor meer informatie over het gebruik van scenario's Zie Hallo [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) eenheidstests.

[Hoe toouse Azure Redis-Cache met behulp van Python](cache-python-get-started.md) ziet u hoe tooget de slag met Azure Redis-Cache met behulp van Python en Hallo [redis-py](https://github.com/andymccurdy/redis-py) client.

[Werken met .NET-objecten in cache Hallo](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) ziet u enkele tooserialize .NET-objecten zodat u ze, kunt u tooand schrijven kunt lezen van een Azure Redis-Cache-exemplaar. 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>Redis-Cache gebruiken als een Scale-out Backplane voor ASP.NET-SignalR
Hallo [Redis-Cache gebruiken als een Scale-out Backplane voor ASP.NET-SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) voorbeeld laat zien hoe u Azure Redis-Cache kunt gebruiken als een SignalR backplane. Zie voor meer informatie over backplane [SignalR Scaleout met Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).

## <a name="redis-cache-customer-query-sample"></a>Voorbeeld van een Cache klant query redis
Dit voorbeeld demonstreert vergelijkt prestaties tussen toegang tot gegevens uit de cache en toegang tot gegevens uit de opslag voor persistentie. Dit voorbeeld heeft twee projecten.

* [Demo hoe Redis-Cache kunt de prestaties verbeteren door gegevens opslaan in cache](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [Seed hello Database en de Cache voor Hallo-demo](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>ASP.NET-sessiestatus en uitvoercaching
Hallo [gebruik Azure Redis-Cache toostore ASP.NET SessionState en OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) voorbeeld laat zien hoe u toouse Azure Redis-Cache toostore ASP.NET-sessie en het gebruik van de uitvoercache Hallo SessionState en OutputCache providers voor Redis.

## <a name="manage-azure-redis-cache-with-maml"></a>Azure Redis-Cache met MAML beheren
Hallo [beheren van Azure Redis-Cache met behulp van Azure Management-bibliotheken](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) voorbeeld laat zien hoe kunt u Azure Management-bibliotheken toomanage - (maken / bijwerken / verwijderen) uw Cache. 

## <a name="custom-monitoring-sample"></a>Aangepaste bewaking voorbeeld
Hallo [gegevens voor het bewaken van toegang tot Redis-Cache](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) voorbeeld laat zien hoe u toegang hebt tot bewakingsgegevens voor uw Azure Redis-Cache buiten hello Azure-Portal.

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>Een Twitter-stijl-kloon geschreven met behulp van PHP en Redis
Hallo [Retwis](https://github.com/SyntaxC4-MSFT/retwis) voorbeeld Redis Hallo wereld Hallo is. Het is een minimale Twitter-stijl sociale netwerken kloon geschreven met behulp van Redis en PHP met Hallo [Predis](https://github.com/nrk/predis) client. Hallo broncode is ontworpen toobe zeer eenvoudig en op Hallo dezelfde tooshow verschillende Redis gegevensstructuren tijdstip.

## <a name="bandwidth-monitor"></a>Bandbreedte-monitor
Hallo [bandbreedte monitor](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) voorbeeld kunt u toomonitor Hallo bandbreedte op Hallo-client gebruikt. toomeasure Hallo bandbreedte, Hallo-voorbeeld uitvoeren op Hallo cache-clientcomputer aanroepen toohello cache maken en Hallo-bandbreedte die zijn gerapporteerd door Hallo bandbreedte monitor voorbeeld zien.

