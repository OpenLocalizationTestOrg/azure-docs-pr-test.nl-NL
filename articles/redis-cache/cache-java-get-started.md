---
title: Azure Redis-cache gebruiken met behulp van Java | Microsoft Docs
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
ms.openlocfilehash: 3cfad3a7279b5f9bbff1e6cd9794c492e3544752
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-java"></a><span data-ttu-id="80b60-103">Azure Redis-cache gebruiken met behulp van Java</span><span class="sxs-lookup"><span data-stu-id="80b60-103">How to use Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="80b60-104">.NET</span><span class="sxs-lookup"><span data-stu-id="80b60-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="80b60-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="80b60-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="80b60-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="80b60-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="80b60-107">Java</span><span class="sxs-lookup"><span data-stu-id="80b60-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="80b60-108">Python</span><span class="sxs-lookup"><span data-stu-id="80b60-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="80b60-109">Azure Redis-cache geeft u toegang tot een toegewezen Redis-cache, beheerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="80b60-109">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="80b60-110">Uw cache is toegankelijk vanuit elke toepassing in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="80b60-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="80b60-111">In dit onderwerp wordt beschreven hoe u aan de slag kunt met Azure Redis-cache met gebruik van Java.</span><span class="sxs-lookup"><span data-stu-id="80b60-111">This topic shows you how to get started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80b60-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="80b60-112">Prerequisites</span></span>
<span data-ttu-id="80b60-113">[Jedis](https://github.com/xetorthio/jedis): Java-client voor Redis</span><span class="sxs-lookup"><span data-stu-id="80b60-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="80b60-114">In deze zelfstudie wordt Jedis gebruikt, maar u kunt elke andere Java-client gebruiken die wordt vermeld op [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="80b60-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="80b60-115">Een Redis-cache maken op Azure</span><span class="sxs-lookup"><span data-stu-id="80b60-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="80b60-116">De hostnaam en toegangssleutels ophalen</span><span class="sxs-lookup"><span data-stu-id="80b60-116">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="80b60-117">Veilig verbinding maken met de cache via SSL</span><span class="sxs-lookup"><span data-stu-id="80b60-117">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="80b60-118">De meest recente versies van [jedis](https://github.com/xetorthio/jedis) bieden ondersteuning voor een SSL-verbinding met Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="80b60-118">The latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="80b60-119">Het volgende voorbeeld laat zien hoe u via SSL-eindpunt 6380 verbinding maakt met Azure Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="80b60-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="80b60-120">Vervang `<name>` door de naam van uw cache en `<key>` door ofwel uw primaire of secundaire sleutel zoals beschreven in het vorige gedeelte genaamd [De hostnaam en toegangssleutels ophalen](#retrieve-the-host-name-and-access-keys).</span><span class="sxs-lookup"><span data-stu-id="80b60-120">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="80b60-121">De poort zonder SSL is uitgeschakeld voor nieuwe Azure Redis Cache-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="80b60-121">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="80b60-122">Gebruikt u een andere client die geen ondersteuning biedt voor SSL, raadpleeg dan [Toegang inschakelen voor poort zonder SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="80b60-122">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="80b60-123">Iets toevoegen aan de cache en dit ophalen</span><span class="sxs-lookup"><span data-stu-id="80b60-123">Add something to the cache and retrieve it</span></span>
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


## <a name="next-steps"></a><span data-ttu-id="80b60-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80b60-124">Next steps</span></span>
* <span data-ttu-id="80b60-125">[Schakel de diagnostische gegevens van de cache in](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics), zodat u de status van de cache kunt [bewaken](https://msdn.microsoft.com/library/azure/dn763945.aspx).</span><span class="sxs-lookup"><span data-stu-id="80b60-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) the health of your cache.</span></span>
* <span data-ttu-id="80b60-126">Lees de officiële [Redis-documentatie](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="80b60-126">Read the official [Redis documentation](http://redis.io/documentation).</span></span>
