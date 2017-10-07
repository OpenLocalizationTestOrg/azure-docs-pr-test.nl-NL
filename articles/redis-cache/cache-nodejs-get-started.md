---
title: aaaHow toouse Azure Redis-Cache met behulp van Node.js | Microsoft Docs
description: Aan de slag met Azure Redis-cache met behulp van Node.js en node_redis.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Hoe toouse Azure Redis-Cache met behulp van Node.js
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure Redis-Cache geeft u toegang krijgen tot tooa beveiligde, toegewezen Redis-cache, beheerd door Microsoft. Uw cache is toegankelijk vanuit elke toepassing in Microsoft Azure.

Dit onderwerp leest u hoe tooget de slag met Azure Redis-Cache met behulp van Node.js. Zie voor een ander voorbeeld van het gebruik van Azure Redis-Cache met behulp van Node.js [Een Node.js-chattoepassing bouwen met Socket.IO op een Azure-website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).

## <a name="prerequisites"></a>Vereisten
[node_redis](https://github.com/mranney/node_redis) installeren:

    npm install redis

In deze zelfstudie wordt gebruikgemaakt van [node_redis](https://github.com/mranney/node_redis). Raadpleeg voor voorbeelden van het gebruik van andere clients Node.js Hallo afzonderlijke documentatie voor Hallo Node.js-clients die wordt vermeld op [Node.js Redis-clients](http://redis.io/clients#nodejs).

## <a name="create-a-redis-cache-on-azure"></a>Een Redis-cache maken op Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Hallo-host en toegangssleutels ophalen
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Toohello cache veilig via SSL verbinding
Hallo laatste builds van [node_redis](https://github.com/mranney/node_redis) ondersteuning bieden voor het verbinden van tooAzure Redis-Cache met behulp van SSL. Hallo volgende voorbeeld ziet u hoe tooconnect tooAzure Redis-Cache gebruiken Hallo SSL-eindpunt van 6380. Vervang `<name>` met de naam van de cache Hallo en `<key>` met ofwel de primaire of secundaire sleutel zoals beschreven in Hallo vorige [Hallo host en toegangssleutels ophalen](#retrieve-the-host-name-and-access-keys) sectie.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> Hallo niet-SSL-poort is uitgeschakeld voor nieuwe exemplaren van Azure Redis-Cache. Als u een andere client die geen ondersteuning voor SSL gebruikt, raadpleegt u [hoe tooenable niet-SSL-poort Hallo](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Iets toevoegen toohello in de cache en dit ophalen
Hallo volgende voorbeeld ziet u hoe tooconnect tooan van Azure Redis-Cache-exemplaar en opslaan en ophalen van een item uit Hallo-cache. Voor meer voorbeelden van het gebruik van Redis Hello [node_redis](https://github.com/mranney/node_redis) client, Zie [http://redis.js.org/](http://redis.js.org/).

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

Uitvoer:

    OK
    value


## <a name="next-steps"></a>Volgende stappen
* [Cache diagnostische gegevens inschakelen](cache-how-to-monitor.md#enable-cache-diagnostics) zodat u kunt [monitor](cache-how-to-monitor.md) Hallo status van de cache.
* Lees Hallo officiële [Redis-documentatie](http://redis.io/documentation).

