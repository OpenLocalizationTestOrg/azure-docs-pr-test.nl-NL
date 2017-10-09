---
title: aaaHow toouse Azure Redis-Cache met behulp van Java | Microsoft Docs
description: Aan de slag met Azure Redis-cache met behulp van Java
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a>Hoe toouse Azure Redis-Cache met behulp van Java
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure Redis-Cache geeft u toegang tot tooa toegewezen Redis-cache, beheerd door Microsoft. Uw cache is toegankelijk vanuit elke toepassing in Microsoft Azure.

Dit onderwerp leest u hoe tooget de slag met Azure Redis-Cache met behulp van Java.

## <a name="prerequisites"></a>Vereisten
[Jedis](https://github.com/xetorthio/jedis): Java-client voor Redis

In deze zelfstudie wordt Jedis gebruikt, maar u kunt elke andere Java-client gebruiken die wordt vermeld op [http://redis.io/clients](http://redis.io/clients).

## <a name="create-a-redis-cache-on-azure"></a>Een Redis-cache maken op Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Hallo-host en toegangssleutels ophalen
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Toohello cache veilig via SSL verbinding
Hallo laatste builds van [jedis](https://github.com/xetorthio/jedis) ondersteuning bieden voor het verbinden van tooAzure Redis-Cache met behulp van SSL. Hallo volgende voorbeeld ziet u hoe tooconnect tooAzure Redis-Cache gebruiken Hallo SSL-eindpunt van 6380. Vervang `<name>` met de naam van de cache Hallo en `<key>` met ofwel de primaire of secundaire sleutel zoals beschreven in Hallo vorige [Hallo host en toegangssleutels ophalen](#retrieve-the-host-name-and-access-keys) sectie.

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> Hallo niet-SSL-poort is uitgeschakeld voor nieuwe exemplaren van Azure Redis-Cache. Als u een andere client die geen ondersteuning voor SSL gebruikt, raadpleegt u [hoe tooenable niet-SSL-poort Hallo](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Iets toevoegen toohello in de cache en dit ophalen
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a>Volgende stappen
* [Cache diagnostische gegevens inschakelen](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) zodat u kunt [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) Hallo status van de cache.
* Lees Hallo officiële [Redis-documentatie](http://redis.io/documentation).
