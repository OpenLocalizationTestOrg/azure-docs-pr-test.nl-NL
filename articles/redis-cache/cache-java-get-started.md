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
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="952b1-103">Hoe toouse Azure Redis-Cache met behulp van Java</span><span class="sxs-lookup"><span data-stu-id="952b1-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="952b1-104">.NET</span><span class="sxs-lookup"><span data-stu-id="952b1-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="952b1-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="952b1-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="952b1-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="952b1-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="952b1-107">Java</span><span class="sxs-lookup"><span data-stu-id="952b1-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="952b1-108">Python</span><span class="sxs-lookup"><span data-stu-id="952b1-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="952b1-109">Azure Redis-Cache geeft u toegang tot tooa toegewezen Redis-cache, beheerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="952b1-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="952b1-110">Uw cache is toegankelijk vanuit elke toepassing in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="952b1-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="952b1-111">Dit onderwerp leest u hoe tooget de slag met Azure Redis-Cache met behulp van Java.</span><span class="sxs-lookup"><span data-stu-id="952b1-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="952b1-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="952b1-112">Prerequisites</span></span>
<span data-ttu-id="952b1-113">[Jedis](https://github.com/xetorthio/jedis): Java-client voor Redis</span><span class="sxs-lookup"><span data-stu-id="952b1-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="952b1-114">In deze zelfstudie wordt Jedis gebruikt, maar u kunt elke andere Java-client gebruiken die wordt vermeld op [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="952b1-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="952b1-115">Een Redis-cache maken op Azure</span><span class="sxs-lookup"><span data-stu-id="952b1-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="952b1-116">Hallo-host en toegangssleutels ophalen</span><span class="sxs-lookup"><span data-stu-id="952b1-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="952b1-117">Toohello cache veilig via SSL verbinding</span><span class="sxs-lookup"><span data-stu-id="952b1-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="952b1-118">Hallo laatste builds van [jedis](https://github.com/xetorthio/jedis) ondersteuning bieden voor het verbinden van tooAzure Redis-Cache met behulp van SSL.</span><span class="sxs-lookup"><span data-stu-id="952b1-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="952b1-119">Hallo volgende voorbeeld ziet u hoe tooconnect tooAzure Redis-Cache gebruiken Hallo SSL-eindpunt van 6380.</span><span class="sxs-lookup"><span data-stu-id="952b1-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="952b1-120">Vervang `<name>` met de naam van de cache Hallo en `<key>` met ofwel de primaire of secundaire sleutel zoals beschreven in Hallo vorige [Hallo host en toegangssleutels ophalen](#retrieve-the-host-name-and-access-keys) sectie.</span><span class="sxs-lookup"><span data-stu-id="952b1-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="952b1-121">Hallo niet-SSL-poort is uitgeschakeld voor nieuwe exemplaren van Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="952b1-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="952b1-122">Als u een andere client die geen ondersteuning voor SSL gebruikt, raadpleegt u [hoe tooenable niet-SSL-poort Hallo](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="952b1-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="952b1-123">Iets toevoegen toohello in de cache en dit ophalen</span><span class="sxs-lookup"><span data-stu-id="952b1-123">Add something toohello cache and retrieve it</span></span>
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


## <a name="next-steps"></a><span data-ttu-id="952b1-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="952b1-124">Next steps</span></span>
* <span data-ttu-id="952b1-125">[Cache diagnostische gegevens inschakelen](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) zodat u kunt [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) Hallo status van de cache.</span><span class="sxs-lookup"><span data-stu-id="952b1-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="952b1-126">Lees Hallo officiële [Redis-documentatie](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="952b1-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>
