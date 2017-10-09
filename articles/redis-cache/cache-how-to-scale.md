---
title: aaaHow tooScale Azure Redis-Cache | Microsoft Docs
description: Meer informatie over hoe tooscale uw Azure Redis-Cache-exemplaren
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
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a><span data-ttu-id="8addf-103">Hoe tooScale Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="8addf-103">How tooScale Azure Redis Cache</span></span>
<span data-ttu-id="8addf-104">Azure Redis-Cache heeft verschillende cache aanbiedingen die flexibiliteit bij het Hallo-keuze van de cachegrootte en -functies bieden.</span><span class="sxs-lookup"><span data-stu-id="8addf-104">Azure Redis Cache has different cache offerings, which provide flexibility in hello choice of cache size and features.</span></span> <span data-ttu-id="8addf-105">Nadat een cache is gemaakt, kunt u Hallo grootte en de prijscategorie van Hallo cache als Hallo vereisten van uw toepassing veranderen Hallo schalen.</span><span class="sxs-lookup"><span data-stu-id="8addf-105">After a cache is created, you can scale hello size and hello pricing tier of hello cache if hello requirements of your application change.</span></span> <span data-ttu-id="8addf-106">Dit artikel laat zien hoe tooscale uw cache in hello Azure-portal en met behulp van hulpprogramma's zoals Azure PowerShell en Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8addf-106">This article shows you how tooscale your cache in both hello Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-tooscale"></a><span data-ttu-id="8addf-107">Wanneer tooscale</span><span class="sxs-lookup"><span data-stu-id="8addf-107">When tooscale</span></span>
<span data-ttu-id="8addf-108">U kunt Hallo [bewaking](cache-how-to-monitor.md) functies van Azure Redis-Cache toomonitor Hallo status en prestaties van uw cache en te bepalen wanneer tooscale Hallo cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-108">You can use hello [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache toomonitor hello health and performance of your cache and help determine when tooscale hello cache.</span></span> 

<span data-ttu-id="8addf-109">U kunt bewaken Hallo volgende metrische gegevens toohelp bepalen of u moet tooscale.</span><span class="sxs-lookup"><span data-stu-id="8addf-109">You can monitor hello following metrics toohelp determine if you need tooscale.</span></span>

* <span data-ttu-id="8addf-110">Redis belasting van de Server</span><span class="sxs-lookup"><span data-stu-id="8addf-110">Redis Server Load</span></span>
* <span data-ttu-id="8addf-111">Geheugengebruik</span><span class="sxs-lookup"><span data-stu-id="8addf-111">Memory Usage</span></span>
* <span data-ttu-id="8addf-112">Netwerkbandbreedte</span><span class="sxs-lookup"><span data-stu-id="8addf-112">Network Bandwidth</span></span>
* <span data-ttu-id="8addf-113">CPU-gebruik</span><span class="sxs-lookup"><span data-stu-id="8addf-113">CPU Usage</span></span>

<span data-ttu-id="8addf-114">Als u vaststelt dat uw cache niet meer van uw toepassing vereisten voldoet, kunt u tooa groter of kleiner cache prijscategorie die geschikt is voor uw toepassing schalen.</span><span class="sxs-lookup"><span data-stu-id="8addf-114">If you determine that your cache is no longer meeting your application's requirements, you can scale tooa larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="8addf-115">Zie voor meer informatie over het bepalen van die in de cache prijscategorie laag toouse [welke aanbieding Redis-Cache en de grootte moet ik gebruiken](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="8addf-115">For more information on determining which cache pricing tier toouse, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="8addf-116">Een cache schalen</span><span class="sxs-lookup"><span data-stu-id="8addf-116">Scale a cache</span></span>
<span data-ttu-id="8addf-117">tooscale uw cache [toohello cache Bladeren](cache-configure.md#configure-redis-cache-settings) in Hallo [Azure-portal](https://portal.azure.com) en klik op **Scale** van Hallo **Resource menu**.</span><span class="sxs-lookup"><span data-stu-id="8addf-117">tooscale your cache, [browse toohello cache](cache-configure.md#configure-redis-cache-settings) in hello [Azure portal](https://portal.azure.com) and click **Scale** from hello **Resource menu**.</span></span>

![Schalen](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="8addf-119">Selecteer Hallo gewenste prijscategorie uit Hallo **Selecteer prijscategorie** blade en klik op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="8addf-119">Select hello desired pricing tier from hello **Select pricing tier** blade and click **Select**.</span></span>

![Prijscategorie][redis-cache-pricing-tier-blade]


<span data-ttu-id="8addf-121">U kunt andere prijscategorie Hello volgen beperkingen tooa schalen:</span><span class="sxs-lookup"><span data-stu-id="8addf-121">You can scale tooa different pricing tier with hello following restrictions:</span></span>

* <span data-ttu-id="8addf-122">U kan niet uit een hogere prijscategorie laag tooa lagere prijscategorie schalen.</span><span class="sxs-lookup"><span data-stu-id="8addf-122">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="8addf-123">U kunt geen schalen van een **Premium** cache omlaag tooa **standaard** of een **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-123">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="8addf-124">U kunt geen schalen van een **standaard** cache omlaag tooa **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-124">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="8addf-125">U kunt opschalen van een **Basic** cache tooa **standaard** cache, maar niet wijzigen Hallo grootte op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="8addf-125">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="8addf-126">Als u een ander formaat nodig hebt, kunt u een daaropvolgende vergroten/verkleinen bewerking toohello gewenst grootte kunt doen.</span><span class="sxs-lookup"><span data-stu-id="8addf-126">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="8addf-127">U kunt geen schalen van een **Basic** cache rechtstreeks tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-127">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="8addf-128">U moet de schaal van **Basic** te**standaard** in één bewerking van de schaal en vervolgens van **standaard** te**Premium** bij een volgende schaal de bewerking.</span><span class="sxs-lookup"><span data-stu-id="8addf-128">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="8addf-129">Kan niet worden geschaald uit een groter formaat omlaag toohello **C0 (250 MB)** grootte.</span><span class="sxs-lookup"><span data-stu-id="8addf-129">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="8addf-130">Tijdens het Hallo-cache wordt geschaald toohello nieuwe prijscategorie, een **schaal** status wordt weergegeven op Hallo **Redis-Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="8addf-130">While hello cache is scaling toohello new pricing tier, a **Scaling** status is displayed in hello **Redis Cache** blade.</span></span>

![Schalen][redis-cache-scaling]

<span data-ttu-id="8addf-132">Wanneer schalen voltooid is, Hallo status verandert van **schaal** te**met**.</span><span class="sxs-lookup"><span data-stu-id="8addf-132">When scaling is complete, hello status changes from **Scaling** too**Running**.</span></span>

## <a name="how-tooautomate-a-scaling-operation"></a><span data-ttu-id="8addf-133">Hoe tooautomate een bewerking voor vergroten/verkleinen</span><span class="sxs-lookup"><span data-stu-id="8addf-133">How tooautomate a scaling operation</span></span>
<span data-ttu-id="8addf-134">In toevoeging tooscaling Hallo uw cache-exemplaren in Azure-portal, kunt u met behulp van PowerShell-cmdlets, Azure CLI schalen en Hallo met behulp van Microsoft Azure Management-bibliotheken (MAML).</span><span class="sxs-lookup"><span data-stu-id="8addf-134">In addition tooscaling your cache instances in hello Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using hello Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="8addf-135">Schaal met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="8addf-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="8addf-136">Schaal met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8addf-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="8addf-137">Met behulp van MAML schaal</span><span class="sxs-lookup"><span data-stu-id="8addf-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="8addf-138">Schaal met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="8addf-138">Scale using PowerShell</span></span>
<span data-ttu-id="8addf-139">U kunt uw Azure Redis-Cache-exemplaren met PowerShell schalen met behulp van Hallo [Set AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet wanneer hello `Size`, `Sku`, of `ShardCount` eigenschappen zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8addf-139">You can scale your Azure Redis Cache instances with PowerShell by using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="8addf-140">Hallo volgende voorbeeld laat zien hoe tooscale een cache met de naam `myCache` tooa 2,5 GB cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-140">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="8addf-141">Zie voor meer informatie over het schalen met PowerShell [tooscale een Redis-cache met behulp van Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="8addf-141">For more information on scaling with PowerShell, see [tooscale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="8addf-142">Schaal met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8addf-142">Scale using Azure CLI</span></span>
<span data-ttu-id="8addf-143">tooscale uw Azure Redis-Cache-exemplaren die gebruikmaken van Azure CLI aanroepen Hallo `azure rediscache set` opdracht en geeft u Hallo gewenst configuratiewijzigingen die een nieuwe grootte, sku of clustergrootte, afhankelijk van Hallo gewenst vergroten/verkleinen bewerking.</span><span class="sxs-lookup"><span data-stu-id="8addf-143">tooscale your Azure Redis Cache instances using Azure CLI, call hello `azure rediscache set` command and pass in hello desired configuration changes that include a new size, sku, or cluster size, depending on hello desired scaling operation.</span></span>

<span data-ttu-id="8addf-144">Zie voor meer informatie over het schalen met Azure CLI [instellingen van een bestaande Redis-Cache wijzigen](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="8addf-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="8addf-145">Met behulp van MAML schaal</span><span class="sxs-lookup"><span data-stu-id="8addf-145">Scale using MAML</span></span>
<span data-ttu-id="8addf-146">tooscale uw Azure Redis-Cache-exemplaren die gebruikmaken van Hallo [Microsoft Azure Management-bibliotheken (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), aanroep Hallo `IRedisOperations.CreateOrUpdate` methode en geeft u nieuwe grootte voor Hallo Hallo `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="8addf-146">tooscale your Azure Redis Cache instances using hello [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call hello `IRedisOperations.CreateOrUpdate` method and pass in hello new size for hello `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="8addf-147">Zie voor meer informatie, Hallo [Redis-Cache beheren met behulp van MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8addf-147">For more information, see hello [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="8addf-148">Veelgestelde vragen over het schalen</span><span class="sxs-lookup"><span data-stu-id="8addf-148">Scaling FAQ</span></span>
<span data-ttu-id="8addf-149">Hallo bevat volgende lijst toocommonly van antwoorden op veelgestelde vragen over het schalen van Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-149">hello following list contains answers toocommonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="8addf-150">Kan ik worden geschaald naar, uit of binnen een Premium-cache?</span><span class="sxs-lookup"><span data-stu-id="8addf-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="8addf-151">Na de schaal heb ik toochange mijn cache naam of toegang tot de sleutels?</span><span class="sxs-lookup"><span data-stu-id="8addf-151">After scaling, do I have toochange my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="8addf-152">Hoe schalen werkt?</span><span class="sxs-lookup"><span data-stu-id="8addf-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="8addf-153">Ik verliest gegevens uit de cache tijdens schalen?</span><span class="sxs-lookup"><span data-stu-id="8addf-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="8addf-154">Mijn aangepaste databases configureert betrokken tijdens schalen?</span><span class="sxs-lookup"><span data-stu-id="8addf-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="8addf-155">Mijn cache is beschikbaar tijdens het schalen?</span><span class="sxs-lookup"><span data-stu-id="8addf-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="8addf-156">Bewerkingen die worden niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="8addf-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="8addf-157">Hoe lang duurt schalen voordat?</span><span class="sxs-lookup"><span data-stu-id="8addf-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="8addf-158">Hoe weet ik wanneer de schaal is voltooid?</span><span class="sxs-lookup"><span data-stu-id="8addf-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="8addf-159">Kan ik worden geschaald naar, uit of binnen een Premium-cache?</span><span class="sxs-lookup"><span data-stu-id="8addf-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="8addf-160">U kunt geen schalen van een **Premium** cache omlaag tooa **Basic** of **standaard** prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="8addf-160">You can't scale from a **Premium** cache down tooa **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="8addf-161">U kunt opschalen van een **Premium** cache laag tooanother prijzen.</span><span class="sxs-lookup"><span data-stu-id="8addf-161">You can scale from one **Premium** cache pricing tier tooanother.</span></span>
* <span data-ttu-id="8addf-162">U kunt geen schalen van een **Basic** cache rechtstreeks tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-162">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="8addf-163">U moet eerst de schaal van **Basic** te**standaard** in één bewerking van de schaal en vervolgens van **standaard** te**Premium** in een toekomstige de bewerking is vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="8addf-163">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="8addf-164">Als u de clustering ingeschakeld tijdens het maken van uw **Premium** cache, kunt u [Hallo clustergrootte wijzigen](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="8addf-164">If you enabled clustering when you created your **Premium** cache, you can [change hello cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="8addf-165">Als uw cache is gemaakt zonder clustering is ingeschakeld, kunt u op een later tijdstip clustering niet configureren.</span><span class="sxs-lookup"><span data-stu-id="8addf-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="8addf-166">Zie voor meer informatie [hoe tooconfigure clustering voor een Premium Azure Redis-Cache](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="8addf-166">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a><span data-ttu-id="8addf-167">Na de schaal heb ik toochange mijn cache naam of toegang tot de sleutels?</span><span class="sxs-lookup"><span data-stu-id="8addf-167">After scaling, do I have toochange my cache name or access keys?</span></span>
<span data-ttu-id="8addf-168">Nee, uw Cachenaam en sleutels zijn niet gewijzigd tijdens een bewerking voor vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="8addf-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="8addf-169">Hoe schalen werkt?</span><span class="sxs-lookup"><span data-stu-id="8addf-169">How does scaling work?</span></span>
* <span data-ttu-id="8addf-170">Wanneer een **Basic** cache wordt geschaald tooa verschillende grootte, deze wordt afgesloten en een nieuwe cache met behulp van de nieuwe grootte Hallo is ingericht.</span><span class="sxs-lookup"><span data-stu-id="8addf-170">When a **Basic** cache is scaled tooa different size, it is shut down and a new cache is provisioned using hello new size.</span></span> <span data-ttu-id="8addf-171">Gedurende deze tijd Hallo-cache is niet beschikbaar en alle gegevens in cache Hallo verloren.</span><span class="sxs-lookup"><span data-stu-id="8addf-171">During this time, hello cache is unavailable and all data in hello cache is lost.</span></span>
* <span data-ttu-id="8addf-172">Wanneer een **Basic** -cache is geschaald tooa **standaard** cache, een replica-cache is ingericht en Hallo gegevens van Hallo primaire cache toohello replica cache is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="8addf-172">When a **Basic** cache is scaled tooa **Standard** cache, a replica cache is provisioned and hello data is copied from hello primary cache toohello replica cache.</span></span> <span data-ttu-id="8addf-173">Hallo-cache blijft tijdens Hallo proces schalen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8addf-173">hello cache remains available during hello scaling process.</span></span>
* <span data-ttu-id="8addf-174">Wanneer een **standaard** -cache is geschaald tooa andere grootte of tooa **Premium** cache, op een van de Hallo replica's wordt afgesloten en opnieuw ingericht toohello nieuwe grootte en Hallo gegevens overgedragen en andere Hallo replica voert een failover voordat deze opnieuw wordt ingericht, een soortgelijk proces uit toohello vindt wel plaats tijdens een storing van een cache-knooppunten Hallo.</span><span class="sxs-lookup"><span data-stu-id="8addf-174">When a **Standard** cache is scaled tooa different size or tooa **Premium** cache, one of hello replicas is shut down and re-provisioned toohello new size and hello data transferred over, and then hello other replica performs a failover before it is re-provisioned, similar toohello process that occurs during a failure of one of hello cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="8addf-175">Ik verliest gegevens uit de cache tijdens schalen?</span><span class="sxs-lookup"><span data-stu-id="8addf-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="8addf-176">Wanneer een **Basic** cache is geschaald tooa nieuwe grootte, alle gegevens verloren en Hallo-cache is niet beschikbaar tijdens het Hallo bewerking schalen.</span><span class="sxs-lookup"><span data-stu-id="8addf-176">When a **Basic** cache is scaled tooa new size, all data is lost and hello cache is unavailable during hello scaling operation.</span></span>
* <span data-ttu-id="8addf-177">Wanneer een **Basic** -cache is geschaald tooa **standaard** in de cache, hello gegevens in cache Hallo is doorgaans behouden.</span><span class="sxs-lookup"><span data-stu-id="8addf-177">When a **Basic** cache is scaled tooa **Standard** cache, hello data in hello cache is typically preserved.</span></span>
* <span data-ttu-id="8addf-178">Wanneer een **standaard** cache is geschaald tooa groter of laag, of een **Premium** cache wordt geschaald tooa groter formaat, alle gegevens doorgaans blijft behouden.</span><span class="sxs-lookup"><span data-stu-id="8addf-178">When a **Standard** cache is scaled tooa larger size or tier, or a **Premium** cache is scaled tooa larger size, all data is typically preserved.</span></span> <span data-ttu-id="8addf-179">Wanneer een **standaard** of **Premium** cache omlaag tooa kleinere, gegevens zijn mogelijk verloren gegaan, afhankelijk van hoeveel gegevens zich in de cache Hallo toohello nieuwe grootte gerelateerde wanneer deze wordt geschaald.</span><span class="sxs-lookup"><span data-stu-id="8addf-179">When scaling a **Standard** or **Premium** cache down tooa smaller size, data may be lost depending on how much data is in hello cache related toohello new size when it is scaled.</span></span> <span data-ttu-id="8addf-180">Als gegevens verloren gaan tijdens het omlaag schalen, sleutels zijn verwijderd met behulp van Hallo [allkeys lru](http://redis.io/topics/lru-cache) taakverwijdering beleid.</span><span class="sxs-lookup"><span data-stu-id="8addf-180">If data is lost when scaling down, keys are evicted using hello [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="8addf-181">Mijn aangepaste databases configureert betrokken tijdens schalen?</span><span class="sxs-lookup"><span data-stu-id="8addf-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="8addf-182">Sommige Prijscategorieën hebben verschillende [databases limieten](cache-configure.md#databases), dus er enkele overwegingen zijn bij het verkleinen van als u een aangepaste waarde voor Hallo geconfigureerd `databases` instellen tijdens het maken van de cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="8addf-183">Wanneer schalen tooa prijscategorie met een lagere `databases` limiet dan de huidige tier Hallo:</span><span class="sxs-lookup"><span data-stu-id="8addf-183">When scaling tooa pricing tier with a lower `databases` limit than hello current tier:</span></span>
  * <span data-ttu-id="8addf-184">Als u van Hallo standaardaantal gebruikmaakt `databases` waarmee 16 voor alle Prijscategorieën is, gegevens niet verloren.</span><span class="sxs-lookup"><span data-stu-id="8addf-184">If you are using hello default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="8addf-185">Als u een aangepaste aantal `databases` die voor Hallo laag toowhich u schaling valt binnen de grenzen Hallo dit `databases` instelling blijft behouden en gegevens niet verloren.</span><span class="sxs-lookup"><span data-stu-id="8addf-185">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="8addf-186">Als u een aangepaste aantal `databases` die groter is dan Hallo grenzen van de nieuwe laag hello, hello `databases` verlaagde toohello grenzen van Hallo nieuwe laag is en alle gegevens in Hallo verwijderd databases wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="8addf-186">If you are using a custom number of `databases` that exceeds hello limits of hello new tier, hello `databases` setting is lowered toohello limits of hello new tier and all data in hello removed databases is lost.</span></span>
* <span data-ttu-id="8addf-187">Wanneer schalen tooa prijscategorie Hello dezelfde of een hogere `databases` limiet dan de huidige tier Hallo uw `databases` instelling blijft behouden en gegevens niet verloren.</span><span class="sxs-lookup"><span data-stu-id="8addf-187">When scaling tooa pricing tier with hello same or higher `databases` limit than hello current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="8addf-188">Houd er rekening mee dat Standard en Premium-caches hebben een SLA met 99,9% voor beschikbaarheid, maar er geen SLA gegevens verloren zijn gegaan is.</span><span class="sxs-lookup"><span data-stu-id="8addf-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="8addf-189">Mijn cache is beschikbaar tijdens het schalen?</span><span class="sxs-lookup"><span data-stu-id="8addf-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="8addf-190">**Standaard** en **Premium** caches beschikbaar blijven tijdens Hallo bewerking schalen.</span><span class="sxs-lookup"><span data-stu-id="8addf-190">**Standard** and **Premium** caches remain available during hello scaling operation.</span></span>
* <span data-ttu-id="8addf-191">**Basic** caches zijn offline tijdens het schalen van andere bewerkingen tooa-grootte, maar beschikbaar blijven tijdens het schalen van **Basic** te**standaard**.</span><span class="sxs-lookup"><span data-stu-id="8addf-191">**Basic** caches are offline during scaling operations tooa different size, but remain available when scaling from **Basic** too**Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="8addf-192">Bewerkingen die worden niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="8addf-192">Operations that are not supported</span></span>
* <span data-ttu-id="8addf-193">U kan niet uit een hogere prijscategorie laag tooa lagere prijscategorie schalen.</span><span class="sxs-lookup"><span data-stu-id="8addf-193">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="8addf-194">U kunt geen schalen van een **Premium** cache omlaag tooa **standaard** of een **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-194">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="8addf-195">U kunt geen schalen van een **standaard** cache omlaag tooa **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-195">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="8addf-196">U kunt opschalen van een **Basic** cache tooa **standaard** cache, maar niet wijzigen Hallo grootte op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="8addf-196">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="8addf-197">Als u een ander formaat nodig hebt, kunt u een daaropvolgende vergroten/verkleinen bewerking toohello gewenst grootte kunt doen.</span><span class="sxs-lookup"><span data-stu-id="8addf-197">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="8addf-198">U kunt geen schalen van een **Basic** cache rechtstreeks tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="8addf-198">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="8addf-199">U moet eerst de schaal van **Basic** te**standaard** in één bewerking van de schaal en vervolgens van **standaard** te**Premium** in een toekomstige de bewerking is vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="8addf-199">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="8addf-200">Kan niet worden geschaald uit een groter formaat omlaag toohello **C0 (250 MB)** grootte.</span><span class="sxs-lookup"><span data-stu-id="8addf-200">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>

<span data-ttu-id="8addf-201">Als een vergroten/verkleinen mislukt Hallo-service probeert toorevert Hallo bewerking en Hallo cache toohello oorspronkelijke grootte wordt teruggezet.</span><span class="sxs-lookup"><span data-stu-id="8addf-201">If a scaling operation fails, hello service will try toorevert hello operation and hello cache will revert toohello original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="8addf-202">Hoe lang duurt schalen voordat?</span><span class="sxs-lookup"><span data-stu-id="8addf-202">How long does scaling take?</span></span>
<span data-ttu-id="8addf-203">Duurt ongeveer 20 minuten, afhankelijk van hoeveel gegevens zich in de cache Hallo schalen.</span><span class="sxs-lookup"><span data-stu-id="8addf-203">Scaling takes approximately 20 minutes, depending on how much data is in hello cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="8addf-204">Hoe weet ik wanneer de schaal is voltooid?</span><span class="sxs-lookup"><span data-stu-id="8addf-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="8addf-205">Hello Azure-portal ziet u Hallo schalen bewerking uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8addf-205">In hello Azure portal you can see hello scaling operation in progress.</span></span> <span data-ttu-id="8addf-206">Wanneer schalen voltooid is, Hallo u status van de wijzigingen in cache hello te**met**.</span><span class="sxs-lookup"><span data-stu-id="8addf-206">When scaling is complete, hello status of hello cache changes too**Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



