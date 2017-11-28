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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="42ee0-103">Hoe toouse Azure Redis-Cache met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="42ee0-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="42ee0-104">.NET</span><span class="sxs-lookup"><span data-stu-id="42ee0-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="42ee0-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="42ee0-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="42ee0-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="42ee0-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="42ee0-107">Java</span><span class="sxs-lookup"><span data-stu-id="42ee0-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="42ee0-108">Python</span><span class="sxs-lookup"><span data-stu-id="42ee0-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="42ee0-109">Azure Redis-Cache geeft u toegang krijgen tot tooa beveiligde, toegewezen Redis-cache, beheerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="42ee0-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="42ee0-110">Uw cache is toegankelijk vanuit elke toepassing in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="42ee0-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="42ee0-111">Dit onderwerp leest u hoe tooget de slag met Azure Redis-Cache met behulp van Node.js.</span><span class="sxs-lookup"><span data-stu-id="42ee0-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="42ee0-112">Zie voor een ander voorbeeld van het gebruik van Azure Redis-Cache met behulp van Node.js [Een Node.js-chattoepassing bouwen met Socket.IO op een Azure-website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="42ee0-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42ee0-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="42ee0-113">Prerequisites</span></span>
<span data-ttu-id="42ee0-114">[node_redis](https://github.com/mranney/node_redis) installeren:</span><span class="sxs-lookup"><span data-stu-id="42ee0-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="42ee0-115">In deze zelfstudie wordt gebruikgemaakt van [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="42ee0-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="42ee0-116">Raadpleeg voor voorbeelden van het gebruik van andere clients Node.js Hallo afzonderlijke documentatie voor Hallo Node.js-clients die wordt vermeld op [Node.js Redis-clients](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="42ee0-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="42ee0-117">Een Redis-cache maken op Azure</span><span class="sxs-lookup"><span data-stu-id="42ee0-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="42ee0-118">Hallo-host en toegangssleutels ophalen</span><span class="sxs-lookup"><span data-stu-id="42ee0-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="42ee0-119">Toohello cache veilig via SSL verbinding</span><span class="sxs-lookup"><span data-stu-id="42ee0-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="42ee0-120">Hallo laatste builds van [node_redis](https://github.com/mranney/node_redis) ondersteuning bieden voor het verbinden van tooAzure Redis-Cache met behulp van SSL.</span><span class="sxs-lookup"><span data-stu-id="42ee0-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="42ee0-121">Hallo volgende voorbeeld ziet u hoe tooconnect tooAzure Redis-Cache gebruiken Hallo SSL-eindpunt van 6380.</span><span class="sxs-lookup"><span data-stu-id="42ee0-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="42ee0-122">Vervang `<name>` met de naam van de cache Hallo en `<key>` met ofwel de primaire of secundaire sleutel zoals beschreven in Hallo vorige [Hallo host en toegangssleutels ophalen](#retrieve-the-host-name-and-access-keys) sectie.</span><span class="sxs-lookup"><span data-stu-id="42ee0-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="42ee0-123">Hallo niet-SSL-poort is uitgeschakeld voor nieuwe exemplaren van Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="42ee0-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="42ee0-124">Als u een andere client die geen ondersteuning voor SSL gebruikt, raadpleegt u [hoe tooenable niet-SSL-poort Hallo](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="42ee0-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="42ee0-125">Iets toevoegen toohello in de cache en dit ophalen</span><span class="sxs-lookup"><span data-stu-id="42ee0-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="42ee0-126">Hallo volgende voorbeeld ziet u hoe tooconnect tooan van Azure Redis-Cache-exemplaar en opslaan en ophalen van een item uit Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="42ee0-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="42ee0-127">Voor meer voorbeelden van het gebruik van Redis Hello [node_redis](https://github.com/mranney/node_redis) client, Zie [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="42ee0-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="42ee0-128">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="42ee0-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="42ee0-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="42ee0-129">Next steps</span></span>
* <span data-ttu-id="42ee0-130">[Cache diagnostische gegevens inschakelen](cache-how-to-monitor.md#enable-cache-diagnostics) zodat u kunt [monitor](cache-how-to-monitor.md) Hallo status van de cache.</span><span class="sxs-lookup"><span data-stu-id="42ee0-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="42ee0-131">Lees Hallo officiële [Redis-documentatie](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="42ee0-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

