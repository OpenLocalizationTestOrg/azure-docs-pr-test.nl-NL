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
# <a name="how-tooscale-azure-redis-cache"></a>Hoe tooScale Azure Redis-Cache
Azure Redis-Cache heeft verschillende cache aanbiedingen die flexibiliteit bij het Hallo-keuze van de cachegrootte en -functies bieden. Nadat een cache is gemaakt, kunt u Hallo grootte en de prijscategorie van Hallo cache als Hallo vereisten van uw toepassing veranderen Hallo schalen. Dit artikel laat zien hoe tooscale uw cache in hello Azure-portal en met behulp van hulpprogramma's zoals Azure PowerShell en Azure CLI.

## <a name="when-tooscale"></a>Wanneer tooscale
U kunt Hallo [bewaking](cache-how-to-monitor.md) functies van Azure Redis-Cache toomonitor Hallo status en prestaties van uw cache en te bepalen wanneer tooscale Hallo cache. 

U kunt bewaken Hallo volgende metrische gegevens toohelp bepalen of u moet tooscale.

* Redis belasting van de Server
* Geheugengebruik
* Netwerkbandbreedte
* CPU-gebruik

Als u vaststelt dat uw cache niet meer van uw toepassing vereisten voldoet, kunt u tooa groter of kleiner cache prijscategorie die geschikt is voor uw toepassing schalen. Zie voor meer informatie over het bepalen van die in de cache prijscategorie laag toouse [welke aanbieding Redis-Cache en de grootte moet ik gebruiken](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="scale-a-cache"></a>Een cache schalen
tooscale uw cache [toohello cache Bladeren](cache-configure.md#configure-redis-cache-settings) in Hallo [Azure-portal](https://portal.azure.com) en klik op **Scale** van Hallo **Resource menu**.

![Schalen](./media/cache-how-to-scale/redis-cache-scale-menu.png)

Selecteer Hallo gewenste prijscategorie uit Hallo **Selecteer prijscategorie** blade en klik op **Selecteer**.

![Prijscategorie][redis-cache-pricing-tier-blade]


U kunt andere prijscategorie Hello volgen beperkingen tooa schalen:

* U kan niet uit een hogere prijscategorie laag tooa lagere prijscategorie schalen.
  * U kunt geen schalen van een **Premium** cache omlaag tooa **standaard** of een **Basic** cache.
  * U kunt geen schalen van een **standaard** cache omlaag tooa **Basic** cache.
* U kunt opschalen van een **Basic** cache tooa **standaard** cache, maar niet wijzigen Hallo grootte op Hallo hetzelfde moment. Als u een ander formaat nodig hebt, kunt u een daaropvolgende vergroten/verkleinen bewerking toohello gewenst grootte kunt doen.
* U kunt geen schalen van een **Basic** cache rechtstreeks tooa **Premium** cache. U moet de schaal van **Basic** te**standaard** in één bewerking van de schaal en vervolgens van **standaard** te**Premium** bij een volgende schaal de bewerking.
* Kan niet worden geschaald uit een groter formaat omlaag toohello **C0 (250 MB)** grootte.
 
Tijdens het Hallo-cache wordt geschaald toohello nieuwe prijscategorie, een **schaal** status wordt weergegeven op Hallo **Redis-Cache** blade.

![Schalen][redis-cache-scaling]

Wanneer schalen voltooid is, Hallo status verandert van **schaal** te**met**.

## <a name="how-tooautomate-a-scaling-operation"></a>Hoe tooautomate een bewerking voor vergroten/verkleinen
In toevoeging tooscaling Hallo uw cache-exemplaren in Azure-portal, kunt u met behulp van PowerShell-cmdlets, Azure CLI schalen en Hallo met behulp van Microsoft Azure Management-bibliotheken (MAML). 

* [Schaal met behulp van PowerShell](#scale-using-powershell)
* [Schaal met Azure CLI](#scale-using-azure-cli)
* [Met behulp van MAML schaal](#scale-using-maml)

### <a name="scale-using-powershell"></a>Schaal met behulp van PowerShell
U kunt uw Azure Redis-Cache-exemplaren met PowerShell schalen met behulp van Hallo [Set AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet wanneer hello `Size`, `Sku`, of `ShardCount` eigenschappen zijn gewijzigd. Hallo volgende voorbeeld laat zien hoe tooscale een cache met de naam `myCache` tooa 2,5 GB cache. 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Zie voor meer informatie over het schalen met PowerShell [tooscale een Redis-cache met behulp van Powershell](cache-howto-manage-redis-cache-powershell.md#scale).

### <a name="scale-using-azure-cli"></a>Schaal met Azure CLI
tooscale uw Azure Redis-Cache-exemplaren die gebruikmaken van Azure CLI aanroepen Hallo `azure rediscache set` opdracht en geeft u Hallo gewenst configuratiewijzigingen die een nieuwe grootte, sku of clustergrootte, afhankelijk van Hallo gewenst vergroten/verkleinen bewerking.

Zie voor meer informatie over het schalen met Azure CLI [instellingen van een bestaande Redis-Cache wijzigen](cache-manage-cli.md#scale).

### <a name="scale-using-maml"></a>Met behulp van MAML schaal
tooscale uw Azure Redis-Cache-exemplaren die gebruikmaken van Hallo [Microsoft Azure Management-bibliotheken (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), aanroep Hallo `IRedisOperations.CreateOrUpdate` methode en geeft u nieuwe grootte voor Hallo Hallo `RedisProperties.SKU.Capacity`.

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

Zie voor meer informatie, Hallo [Redis-Cache beheren met behulp van MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) voorbeeld.

## <a name="scaling-faq"></a>Veelgestelde vragen over het schalen
Hallo bevat volgende lijst toocommonly van antwoorden op veelgestelde vragen over het schalen van Azure Redis-Cache.

* [Kan ik worden geschaald naar, uit of binnen een Premium-cache?](#can-i-scale-to-from-or-within-a-premium-cache)
* [Na de schaal heb ik toochange mijn cache naam of toegang tot de sleutels?](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [Hoe schalen werkt?](#how-does-scaling-work)
* [Ik verliest gegevens uit de cache tijdens schalen?](#will-i-lose-data-from-my-cache-during-scaling)
* [Mijn aangepaste databases configureert betrokken tijdens schalen?](#is-my-custom-databases-setting-affected-during-scaling)
* [Mijn cache is beschikbaar tijdens het schalen?](#will-my-cache-be-available-during-scaling)
* [Bewerkingen die worden niet ondersteund](#operations-that-are-not-supported)
* [Hoe lang duurt schalen voordat?](#how-long-does-scaling-take)
* [Hoe weet ik wanneer de schaal is voltooid?](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a>Kan ik worden geschaald naar, uit of binnen een Premium-cache?
* U kunt geen schalen van een **Premium** cache omlaag tooa **Basic** of **standaard** prijscategorie.
* U kunt opschalen van een **Premium** cache laag tooanother prijzen.
* U kunt geen schalen van een **Basic** cache rechtstreeks tooa **Premium** cache. U moet eerst de schaal van **Basic** te**standaard** in één bewerking van de schaal en vervolgens van **standaard** te**Premium** in een toekomstige de bewerking is vergroten/verkleinen.
* Als u de clustering ingeschakeld tijdens het maken van uw **Premium** cache, kunt u [Hallo clustergrootte wijzigen](cache-how-to-premium-clustering.md#cluster-size). Als uw cache is gemaakt zonder clustering is ingeschakeld, kunt u op een later tijdstip clustering niet configureren.
  
  Zie voor meer informatie [hoe tooconfigure clustering voor een Premium Azure Redis-Cache](cache-how-to-premium-clustering.md).

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a>Na de schaal heb ik toochange mijn cache naam of toegang tot de sleutels?
Nee, uw Cachenaam en sleutels zijn niet gewijzigd tijdens een bewerking voor vergroten/verkleinen.

### <a name="how-does-scaling-work"></a>Hoe schalen werkt?
* Wanneer een **Basic** cache wordt geschaald tooa verschillende grootte, deze wordt afgesloten en een nieuwe cache met behulp van de nieuwe grootte Hallo is ingericht. Gedurende deze tijd Hallo-cache is niet beschikbaar en alle gegevens in cache Hallo verloren.
* Wanneer een **Basic** -cache is geschaald tooa **standaard** cache, een replica-cache is ingericht en Hallo gegevens van Hallo primaire cache toohello replica cache is gekopieerd. Hallo-cache blijft tijdens Hallo proces schalen beschikbaar.
* Wanneer een **standaard** -cache is geschaald tooa andere grootte of tooa **Premium** cache, op een van de Hallo replica's wordt afgesloten en opnieuw ingericht toohello nieuwe grootte en Hallo gegevens overgedragen en andere Hallo replica voert een failover voordat deze opnieuw wordt ingericht, een soortgelijk proces uit toohello vindt wel plaats tijdens een storing van een cache-knooppunten Hallo.

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a>Ik verliest gegevens uit de cache tijdens schalen?
* Wanneer een **Basic** cache is geschaald tooa nieuwe grootte, alle gegevens verloren en Hallo-cache is niet beschikbaar tijdens het Hallo bewerking schalen.
* Wanneer een **Basic** -cache is geschaald tooa **standaard** in de cache, hello gegevens in cache Hallo is doorgaans behouden.
* Wanneer een **standaard** cache is geschaald tooa groter of laag, of een **Premium** cache wordt geschaald tooa groter formaat, alle gegevens doorgaans blijft behouden. Wanneer een **standaard** of **Premium** cache omlaag tooa kleinere, gegevens zijn mogelijk verloren gegaan, afhankelijk van hoeveel gegevens zich in de cache Hallo toohello nieuwe grootte gerelateerde wanneer deze wordt geschaald. Als gegevens verloren gaan tijdens het omlaag schalen, sleutels zijn verwijderd met behulp van Hallo [allkeys lru](http://redis.io/topics/lru-cache) taakverwijdering beleid. 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a>Mijn aangepaste databases configureert betrokken tijdens schalen?
Sommige Prijscategorieën hebben verschillende [databases limieten](cache-configure.md#databases), dus er enkele overwegingen zijn bij het verkleinen van als u een aangepaste waarde voor Hallo geconfigureerd `databases` instellen tijdens het maken van de cache.

* Wanneer schalen tooa prijscategorie met een lagere `databases` limiet dan de huidige tier Hallo:
  * Als u van Hallo standaardaantal gebruikmaakt `databases` waarmee 16 voor alle Prijscategorieën is, gegevens niet verloren.
  * Als u een aangepaste aantal `databases` die voor Hallo laag toowhich u schaling valt binnen de grenzen Hallo dit `databases` instelling blijft behouden en gegevens niet verloren.
  * Als u een aangepaste aantal `databases` die groter is dan Hallo grenzen van de nieuwe laag hello, hello `databases` verlaagde toohello grenzen van Hallo nieuwe laag is en alle gegevens in Hallo verwijderd databases wordt verbroken.
* Wanneer schalen tooa prijscategorie Hello dezelfde of een hogere `databases` limiet dan de huidige tier Hallo uw `databases` instelling blijft behouden en gegevens niet verloren.

Houd er rekening mee dat Standard en Premium-caches hebben een SLA met 99,9% voor beschikbaarheid, maar er geen SLA gegevens verloren zijn gegaan is.

### <a name="will-my-cache-be-available-during-scaling"></a>Mijn cache is beschikbaar tijdens het schalen?
* **Standaard** en **Premium** caches beschikbaar blijven tijdens Hallo bewerking schalen.
* **Basic** caches zijn offline tijdens het schalen van andere bewerkingen tooa-grootte, maar beschikbaar blijven tijdens het schalen van **Basic** te**standaard**.

### <a name="operations-that-are-not-supported"></a>Bewerkingen die worden niet ondersteund
* U kan niet uit een hogere prijscategorie laag tooa lagere prijscategorie schalen.
  * U kunt geen schalen van een **Premium** cache omlaag tooa **standaard** of een **Basic** cache.
  * U kunt geen schalen van een **standaard** cache omlaag tooa **Basic** cache.
* U kunt opschalen van een **Basic** cache tooa **standaard** cache, maar niet wijzigen Hallo grootte op Hallo hetzelfde moment. Als u een ander formaat nodig hebt, kunt u een daaropvolgende vergroten/verkleinen bewerking toohello gewenst grootte kunt doen.
* U kunt geen schalen van een **Basic** cache rechtstreeks tooa **Premium** cache. U moet eerst de schaal van **Basic** te**standaard** in één bewerking van de schaal en vervolgens van **standaard** te**Premium** in een toekomstige de bewerking is vergroten/verkleinen.
* Kan niet worden geschaald uit een groter formaat omlaag toohello **C0 (250 MB)** grootte.

Als een vergroten/verkleinen mislukt Hallo-service probeert toorevert Hallo bewerking en Hallo cache toohello oorspronkelijke grootte wordt teruggezet.

### <a name="how-long-does-scaling-take"></a>Hoe lang duurt schalen voordat?
Duurt ongeveer 20 minuten, afhankelijk van hoeveel gegevens zich in de cache Hallo schalen.

### <a name="how-can-i-tell-when-scaling-is-complete"></a>Hoe weet ik wanneer de schaal is voltooid?
Hello Azure-portal ziet u Hallo schalen bewerking uitgevoerd. Wanneer schalen voltooid is, Hallo u status van de wijzigingen in cache hello te**met**.

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



