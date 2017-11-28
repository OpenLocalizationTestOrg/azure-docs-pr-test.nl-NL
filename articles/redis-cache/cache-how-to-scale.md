---
title: Schalen van Azure Redis-Cache | Microsoft Docs
description: Meer informatie over het schalen van uw Azure Redis-Cache-exemplaren
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 91b3580491a1e3504a3891b66606a9bd18c0638f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-azure-redis-cache"></a><span data-ttu-id="e24dd-103">Schalen van Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="e24dd-103">How to Scale Azure Redis Cache</span></span>
<span data-ttu-id="e24dd-104">Azure Redis-Cache heeft verschillende cache aanbiedingen die flexibiliteit bij de keuze van de cachegrootte en -functies bieden.</span><span class="sxs-lookup"><span data-stu-id="e24dd-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span></span> <span data-ttu-id="e24dd-105">Nadat een cache is gemaakt, kunt u de grootte en de prijscategorie van de cache schalen als de vereisten van uw toepassing veranderen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span></span> <span data-ttu-id="e24dd-106">In dit artikel leest u hoe schalen van uw cache in de Azure portal en gebruik van hulpprogramma's zoals Azure PowerShell en Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e24dd-106">This article shows you how to scale your cache in both the Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-to-scale"></a><span data-ttu-id="e24dd-107">Wanneer schalen</span><span class="sxs-lookup"><span data-stu-id="e24dd-107">When to scale</span></span>
<span data-ttu-id="e24dd-108">U kunt de [bewaking](cache-how-to-monitor.md) functies van Azure Redis-Cache om te controleren van de status en prestaties van de cache en te bepalen wanneer schalen van de cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span></span> 

<span data-ttu-id="e24dd-109">U kunt de volgende metrische gegevens om te bepalen wat als u wilt schalen bewaken.</span><span class="sxs-lookup"><span data-stu-id="e24dd-109">You can monitor the following metrics to help determine if you need to scale.</span></span>

* <span data-ttu-id="e24dd-110">Redis belasting van de Server</span><span class="sxs-lookup"><span data-stu-id="e24dd-110">Redis Server Load</span></span>
* <span data-ttu-id="e24dd-111">Geheugengebruik</span><span class="sxs-lookup"><span data-stu-id="e24dd-111">Memory Usage</span></span>
* <span data-ttu-id="e24dd-112">Netwerkbandbreedte</span><span class="sxs-lookup"><span data-stu-id="e24dd-112">Network Bandwidth</span></span>
* <span data-ttu-id="e24dd-113">CPU-gebruik</span><span class="sxs-lookup"><span data-stu-id="e24dd-113">CPU Usage</span></span>

<span data-ttu-id="e24dd-114">Als u vaststelt dat uw cache niet meer van uw toepassing vereisten voldoet, kunt u naar een grotere of kleinere cache prijscategorie die geschikt is voor uw toepassing schalen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="e24dd-115">Zie voor meer informatie over het bepalen van welke prijscategorie gebruiken cache [welke aanbieding Redis-Cache en de grootte moet ik gebruiken](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="e24dd-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="e24dd-116">Een cache schalen</span><span class="sxs-lookup"><span data-stu-id="e24dd-116">Scale a cache</span></span>
<span data-ttu-id="e24dd-117">Schalen van uw cache [Blader naar de cache](cache-configure.md#configure-redis-cache-settings) in de [Azure-portal](https://portal.azure.com) en klik op **Scale** van de **Resource menu**.</span><span class="sxs-lookup"><span data-stu-id="e24dd-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span></span>

![Schalen](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="e24dd-119">Selecteer de gewenste prijscategorie van de **Selecteer prijscategorie** blade en klik op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="e24dd-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span></span>

![Prijscategorie][redis-cache-pricing-tier-blade]


<span data-ttu-id="e24dd-121">U kunt schalen naar een andere prijscategorie met de volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="e24dd-121">You can scale to a different pricing tier with the following restrictions:</span></span>

* <span data-ttu-id="e24dd-122">U kan niet uit een hogere prijscategorie schalen naar een lagere prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="e24dd-122">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="e24dd-123">U kunt geen schalen van een **Premium** omlaag naar de cache een **standaard** of een **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="e24dd-124">U kunt geen schalen van een **standaard** omlaag naar de cache een **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="e24dd-125">U kunt opschalen van een **Basic** in de cache op een **standaard** cache, maar de grootte niet wijzigen op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="e24dd-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="e24dd-126">Als u een ander formaat nodig hebt, kunt u de volgende vergroten/verkleinen bewerking naar de gewenste grootte kunt doen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="e24dd-127">U kunt geen schalen van een **Basic** rechtstreeks naar de cache een **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="e24dd-128">Moet u de schaal van **Basic** naar **standaard** in één bewerking van de schaal en vervolgens van **standaard** naar **Premium** in een latere bewerking voor vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-128">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="e24dd-129">Kan niet worden geschaald uit een groter formaat omlaag naar de **C0 (250 MB)** grootte.</span><span class="sxs-lookup"><span data-stu-id="e24dd-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="e24dd-130">Terwijl de cache wordt geschaald naar de nieuwe prijscategorie een **schaal** status wordt weergegeven in de **Redis-Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="e24dd-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span></span>

![Schalen][redis-cache-scaling]

<span data-ttu-id="e24dd-132">Wanneer schalen voltooid is, wordt de status verandert van **schaal** naar **met**.</span><span class="sxs-lookup"><span data-stu-id="e24dd-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span></span>

## <a name="how-to-automate-a-scaling-operation"></a><span data-ttu-id="e24dd-133">Een bewerking voor vergroten/verkleinen automatiseren</span><span class="sxs-lookup"><span data-stu-id="e24dd-133">How to automate a scaling operation</span></span>
<span data-ttu-id="e24dd-134">Naast het schalen van uw cache-exemplaren in de Azure portal, kunt u de schaal met behulp van PowerShell-cmdlets, Azure CLI en met behulp van de Microsoft Azure Management-bibliotheken (MAML).</span><span class="sxs-lookup"><span data-stu-id="e24dd-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="e24dd-135">Schaal met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e24dd-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="e24dd-136">Schaal met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e24dd-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="e24dd-137">Met behulp van MAML schaal</span><span class="sxs-lookup"><span data-stu-id="e24dd-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="e24dd-138">Schaal met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e24dd-138">Scale using PowerShell</span></span>
<span data-ttu-id="e24dd-139">U kunt uw Azure Redis-Cache-exemplaren met PowerShell schalen met behulp van de [Set AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet wanneer de `Size`, `Sku`, of `ShardCount` eigenschappen zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e24dd-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="e24dd-140">Het volgende voorbeeld laat zien hoe een cache met de naam schalen `myCache` naar een cache 2,5 GB.</span><span class="sxs-lookup"><span data-stu-id="e24dd-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="e24dd-141">Zie voor meer informatie over het schalen met PowerShell [schalen van een Redis-cache met behulp van Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="e24dd-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="e24dd-142">Schaal met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e24dd-142">Scale using Azure CLI</span></span>
<span data-ttu-id="e24dd-143">Als u wilt schalen van uw Azure Redis-Cache-exemplaren die gebruikmaken van Azure CLI, roepen de `azure rediscache set` opdracht en in de gewenste configuratiewijzigingen die een nieuwe grootte, sku of clustergrootte, afhankelijk van de gewenste schaal bewerking bevatten.</span><span class="sxs-lookup"><span data-stu-id="e24dd-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span></span>

<span data-ttu-id="e24dd-144">Zie voor meer informatie over het schalen met Azure CLI [instellingen van een bestaande Redis-Cache wijzigen](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="e24dd-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="e24dd-145">Met behulp van MAML schaal</span><span class="sxs-lookup"><span data-stu-id="e24dd-145">Scale using MAML</span></span>
<span data-ttu-id="e24dd-146">Schalen van uw Azure Redis-Cache-exemplaren met de [Microsoft Azure Management-bibliotheken (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), Roep de `IRedisOperations.CreateOrUpdate` methode en geeft u de nieuwe grootte voor de `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="e24dd-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting the access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // To scale, set a new size for the redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="e24dd-147">Zie voor meer informatie de [Redis-Cache beheren met behulp van MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e24dd-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="e24dd-148">Veelgestelde vragen over het schalen</span><span class="sxs-lookup"><span data-stu-id="e24dd-148">Scaling FAQ</span></span>
<span data-ttu-id="e24dd-149">De volgende lijst bevat antwoorden op veelgestelde vragen over het schalen van Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="e24dd-150">Kan ik worden geschaald naar, uit of binnen een Premium-cache?</span><span class="sxs-lookup"><span data-stu-id="e24dd-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="e24dd-151">Na de schaal heb ik mijn cache naam of toegang tot de sleutels wijzigen?</span><span class="sxs-lookup"><span data-stu-id="e24dd-151">After scaling, do I have to change my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="e24dd-152">Hoe schalen werkt?</span><span class="sxs-lookup"><span data-stu-id="e24dd-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="e24dd-153">Ik verliest gegevens uit de cache tijdens schalen?</span><span class="sxs-lookup"><span data-stu-id="e24dd-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="e24dd-154">Mijn aangepaste databases configureert betrokken tijdens schalen?</span><span class="sxs-lookup"><span data-stu-id="e24dd-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="e24dd-155">Mijn cache is beschikbaar tijdens het schalen?</span><span class="sxs-lookup"><span data-stu-id="e24dd-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="e24dd-156">Bewerkingen die worden niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e24dd-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="e24dd-157">Hoe lang duurt schalen voordat?</span><span class="sxs-lookup"><span data-stu-id="e24dd-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="e24dd-158">Hoe weet ik wanneer de schaal is voltooid?</span><span class="sxs-lookup"><span data-stu-id="e24dd-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="e24dd-159">Kan ik worden geschaald naar, uit of binnen een Premium-cache?</span><span class="sxs-lookup"><span data-stu-id="e24dd-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="e24dd-160">U kunt geen schalen van een **Premium** omlaag naar de cache een **Basic** of **standaard** prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="e24dd-160">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="e24dd-161">U kunt opschalen van een **Premium** cache prijscategorie naar een andere.</span><span class="sxs-lookup"><span data-stu-id="e24dd-161">You can scale from one **Premium** cache pricing tier to another.</span></span>
* <span data-ttu-id="e24dd-162">U kunt geen schalen van een **Basic** rechtstreeks naar de cache een **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-162">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="e24dd-163">U moet eerst de schaal van **Basic** naar **standaard** in één bewerking van de schaal en vervolgens van **standaard** naar **Premium** in een toekomstige de bewerking is vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-163">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="e24dd-164">Als u de clustering ingeschakeld tijdens het maken van uw **Premium** cache, kunt u [wijzigen van de clustergrootte](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="e24dd-164">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="e24dd-165">Als uw cache is gemaakt zonder clustering is ingeschakeld, kunt u op een later tijdstip clustering niet configureren.</span><span class="sxs-lookup"><span data-stu-id="e24dd-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="e24dd-166">Zie [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md) (Clustering voor een Premium Azure Redis Cache configureren) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e24dd-166">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-to-change-my-cache-name-or-access-keys"></a><span data-ttu-id="e24dd-167">Na de schaal heb ik mijn cache naam of toegang tot de sleutels wijzigen?</span><span class="sxs-lookup"><span data-stu-id="e24dd-167">After scaling, do I have to change my cache name or access keys?</span></span>
<span data-ttu-id="e24dd-168">Nee, uw Cachenaam en sleutels zijn niet gewijzigd tijdens een bewerking voor vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="e24dd-169">Hoe schalen werkt?</span><span class="sxs-lookup"><span data-stu-id="e24dd-169">How does scaling work?</span></span>
* <span data-ttu-id="e24dd-170">Wanneer een **Basic** cache is geschaald naar een andere grootte, deze wordt afgesloten en een nieuwe cache is ingericht met behulp van de nieuwe grootte.</span><span class="sxs-lookup"><span data-stu-id="e24dd-170">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span></span> <span data-ttu-id="e24dd-171">Gedurende deze tijd de cache is niet beschikbaar en de gegevens in de cache worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e24dd-171">During this time, the cache is unavailable and all data in the cache is lost.</span></span>
* <span data-ttu-id="e24dd-172">Wanneer een **Basic** cache is geschaald naar een **standaard** cache, een replica-cache is ingericht en de gegevens uit de primaire cache wordt gekopieerd naar de replica-cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-172">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span></span> <span data-ttu-id="e24dd-173">De cache blijft beschikbaar tijdens het vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-173">The cache remains available during the scaling process.</span></span>
* <span data-ttu-id="e24dd-174">Wanneer een **standaard** cache wordt aangepast aan een andere grootte of aan een **Premium** cache, op een van de replica's wordt afgesloten en opnieuw wordt ingericht voor de nieuwe grootte en de overgedragen gegevens en de andere replica voert een failover voordat deze opnieuw worden ingericht, vergelijkbaar met het proces dat bij uitval van een van de cache-knooppunten plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="e24dd-174">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and re-provisioned to the new size and the data transferred over, and then the other replica performs a failover before it is re-provisioned, similar to the process that occurs during a failure of one of the cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="e24dd-175">Ik verliest gegevens uit de cache tijdens schalen?</span><span class="sxs-lookup"><span data-stu-id="e24dd-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="e24dd-176">Wanneer een **Basic** cache is geschaald naar een nieuwe grootte, alle gegevens verloren en wordt de cache is niet beschikbaar tijdens de bewerking uit te schalen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-176">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span></span>
* <span data-ttu-id="e24dd-177">Wanneer een **Basic** cache is geschaald naar een **standaard** cache, de gegevens in de cache wordt doorgaans behouden.</span><span class="sxs-lookup"><span data-stu-id="e24dd-177">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span></span>
* <span data-ttu-id="e24dd-178">Wanneer een **standaard** cache is geschaald naar een grotere grootte of laag, of een **Premium** cache is geschaald naar een groter, blijven doorgaans alle gegevens behouden.</span><span class="sxs-lookup"><span data-stu-id="e24dd-178">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span></span> <span data-ttu-id="e24dd-179">Wanneer een **standaard** of **Premium** cache naar beneden op een kleinere, gegevens zijn mogelijk verloren gegaan, afhankelijk van hoeveel gegevens zich in de cache die betrekking hebben op de nieuwe grootte wanneer deze wordt geschaald.</span><span class="sxs-lookup"><span data-stu-id="e24dd-179">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span></span> <span data-ttu-id="e24dd-180">Als gegevens verloren gaan tijdens het omlaag schalen, sleutels zijn verwijderd met behulp van de [allkeys lru](http://redis.io/topics/lru-cache) taakverwijdering beleid.</span><span class="sxs-lookup"><span data-stu-id="e24dd-180">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="e24dd-181">Mijn aangepaste databases configureert betrokken tijdens schalen?</span><span class="sxs-lookup"><span data-stu-id="e24dd-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="e24dd-182">Sommige Prijscategorieën hebben verschillende [databases limieten](cache-configure.md#databases), dus er enkele overwegingen zijn wanneer het verkleinen van als u een aangepaste waarde voor geconfigureerd de `databases` instellen tijdens het maken van de cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="e24dd-183">Tijdens het schalen naar een prijscategorie met een lagere `databases` limiet dan de huidige tier:</span><span class="sxs-lookup"><span data-stu-id="e24dd-183">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span></span>
  * <span data-ttu-id="e24dd-184">Als u het standaardaantal `databases` waarmee 16 voor alle Prijscategorieën is, gegevens niet verloren.</span><span class="sxs-lookup"><span data-stu-id="e24dd-184">If you are using the default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="e24dd-185">Als u een aangepaste aantal `databases` die valt binnen de grenzen voor de laag waarop u hebben, dit `databases` instelling blijft behouden en gegevens niet verloren.</span><span class="sxs-lookup"><span data-stu-id="e24dd-185">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="e24dd-186">Als u een aangepaste aantal `databases` die overschrijdt de grenzen van de nieuwe laag, de `databases` instelling is verlaagd tot de grenzen van de nieuwe laag en alle gegevens in de verwijderde databases wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="e24dd-186">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span></span>
* <span data-ttu-id="e24dd-187">Wanneer een de dezelfde of een hogere prijscategorie schalen `databases` limiet dan de huidige tier uw `databases` instelling blijft behouden en gegevens niet verloren.</span><span class="sxs-lookup"><span data-stu-id="e24dd-187">When scaling to a pricing tier with the same or higher `databases` limit than the current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="e24dd-188">Houd er rekening mee dat Standard en Premium-caches hebben een SLA met 99,9% voor beschikbaarheid, maar er geen SLA gegevens verloren zijn gegaan is.</span><span class="sxs-lookup"><span data-stu-id="e24dd-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="e24dd-189">Mijn cache is beschikbaar tijdens het schalen?</span><span class="sxs-lookup"><span data-stu-id="e24dd-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="e24dd-190">**Standaard** en **Premium** caches beschikbaar blijven tijdens de bewerking uit te schalen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-190">**Standard** and **Premium** caches remain available during the scaling operation.</span></span>
* <span data-ttu-id="e24dd-191">**Basic** caches zijn offline tijdens het schalen van bewerkingen die een ander formaat, maar beschikbaar blijven tijdens het schalen van **Basic** naar **standaard**.</span><span class="sxs-lookup"><span data-stu-id="e24dd-191">**Basic** caches are offline during scaling operations to a different size, but remain available when scaling from **Basic** to **Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="e24dd-192">Bewerkingen die worden niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e24dd-192">Operations that are not supported</span></span>
* <span data-ttu-id="e24dd-193">U kan niet uit een hogere prijscategorie schalen naar een lagere prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="e24dd-193">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="e24dd-194">U kunt geen schalen van een **Premium** omlaag naar de cache een **standaard** of een **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-194">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="e24dd-195">U kunt geen schalen van een **standaard** omlaag naar de cache een **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-195">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="e24dd-196">U kunt opschalen van een **Basic** in de cache op een **standaard** cache, maar de grootte niet wijzigen op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="e24dd-196">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="e24dd-197">Als u een ander formaat nodig hebt, kunt u de volgende vergroten/verkleinen bewerking naar de gewenste grootte kunt doen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-197">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="e24dd-198">U kunt geen schalen van een **Basic** rechtstreeks naar de cache een **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-198">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="e24dd-199">U moet eerst de schaal van **Basic** naar **standaard** in één bewerking van de schaal en vervolgens van **standaard** naar **Premium** in een toekomstige de bewerking is vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="e24dd-199">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="e24dd-200">Kan niet worden geschaald uit een groter formaat omlaag naar de **C0 (250 MB)** grootte.</span><span class="sxs-lookup"><span data-stu-id="e24dd-200">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>

<span data-ttu-id="e24dd-201">Als een vergroten/verkleinen mislukt, wordt geprobeerd om de bewerking terug te zetten van de service en de cache wordt teruggezet naar de oorspronkelijke grootte.</span><span class="sxs-lookup"><span data-stu-id="e24dd-201">If a scaling operation fails, the service will try to revert the operation and the cache will revert to the original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="e24dd-202">Hoe lang duurt schalen voordat?</span><span class="sxs-lookup"><span data-stu-id="e24dd-202">How long does scaling take?</span></span>
<span data-ttu-id="e24dd-203">Schalen duurt ongeveer 20 minuten, afhankelijk van hoeveel gegevens zich in de cache.</span><span class="sxs-lookup"><span data-stu-id="e24dd-203">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="e24dd-204">Hoe weet ik wanneer de schaal is voltooid?</span><span class="sxs-lookup"><span data-stu-id="e24dd-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="e24dd-205">In de Azure portal ziet u de schaal bewerking uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e24dd-205">In the Azure portal you can see the scaling operation in progress.</span></span> <span data-ttu-id="e24dd-206">Wanneer schalen voltooid is, wordt de status van de cache gewijzigd in **met**.</span><span class="sxs-lookup"><span data-stu-id="e24dd-206">When scaling is complete, the status of the cache changes to **Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



