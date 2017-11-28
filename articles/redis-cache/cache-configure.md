---
title: Het configureren van Azure Redis-Cache | Microsoft Docs
description: Inzicht in de standaardconfiguratie voor Redis voor Azure Redis-Cache en informatie over het configureren van uw Azure Redis-Cache-exemplaren
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 0274e58eb2e83202d4dbc58da0c67d0fdde22ede
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-azure-redis-cache"></a><span data-ttu-id="f925d-103">Het configureren van Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="f925d-103">How to configure Azure Redis Cache</span></span>
<span data-ttu-id="f925d-104">Dit onderwerp wordt beschreven hoe u om te controleren en bijwerken van de configuratie voor uw Azure Redis-Cache-exemplaren en bevat informatie over de configuratie standaard Redis-server voor Azure Redis-Cache-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="f925d-104">This topic describes how to review and update the configuration for your Azure Redis Cache instances, and covers the default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="f925d-105">Zie voor meer informatie over het configureren en het gebruik van Premiumfuncties cache [persistentie configureren](cache-how-to-premium-persistence.md), [clustering configureren](cache-how-to-premium-clustering.md), en [het configureren van Virtual Network-ondersteuning ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-105">For more information on configuring and using premium cache features, see [How to configure persistence](cache-how-to-premium-persistence.md), [How to configure clustering](cache-how-to-premium-clustering.md), and [How to configure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="f925d-106">Redis-cache-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="f925d-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="f925d-107">Azure Redis-Cache-instellingen worden weergegeven en geconfigureerd op de **Redis-Cache** blade met behulp van de **Resource Menu**.</span><span class="sxs-lookup"><span data-stu-id="f925d-107">Azure Redis Cache settings are viewed and configured on the **Redis Cache** blade using the **Resource Menu**.</span></span>

![Redis-Cache-instellingen](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="f925d-109">U kunt bekijken en configureren van de volgende instellingen met behulp van de **Resource Menu**.</span><span class="sxs-lookup"><span data-stu-id="f925d-109">You can view and configure the following settings using the **Resource Menu**.</span></span>

* [<span data-ttu-id="f925d-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f925d-110">Overview</span></span>](#overview)
* [<span data-ttu-id="f925d-111">Activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="f925d-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="f925d-112">Toegangsbeheer (IAM)</span><span class="sxs-lookup"><span data-stu-id="f925d-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="f925d-113">Tags</span><span class="sxs-lookup"><span data-stu-id="f925d-113">Tags</span></span>](#tags)
* [<span data-ttu-id="f925d-114">Problemen vaststellen en oplossen</span><span class="sxs-lookup"><span data-stu-id="f925d-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="f925d-115">Instellingen</span><span class="sxs-lookup"><span data-stu-id="f925d-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="f925d-116">Toegangstoetsen</span><span class="sxs-lookup"><span data-stu-id="f925d-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="f925d-117">Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="f925d-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="f925d-118">Redis-Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="f925d-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="f925d-119">Schalen</span><span class="sxs-lookup"><span data-stu-id="f925d-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="f925d-120">Clustergrootte redis</span><span class="sxs-lookup"><span data-stu-id="f925d-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="f925d-121">Redis-gegevenspersistentie</span><span class="sxs-lookup"><span data-stu-id="f925d-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="f925d-122">Updates plannen</span><span class="sxs-lookup"><span data-stu-id="f925d-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="f925d-123">Geo-replicatie</span><span class="sxs-lookup"><span data-stu-id="f925d-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="f925d-124">Virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="f925d-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="f925d-125">Firewall</span><span class="sxs-lookup"><span data-stu-id="f925d-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="f925d-126">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="f925d-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="f925d-127">Hiermee vergrendelt u</span><span class="sxs-lookup"><span data-stu-id="f925d-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="f925d-128">Automatiseringsscript</span><span class="sxs-lookup"><span data-stu-id="f925d-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="f925d-129">Beheer</span><span class="sxs-lookup"><span data-stu-id="f925d-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="f925d-130">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="f925d-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="f925d-131">Gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="f925d-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="f925d-132">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="f925d-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="f925d-133">Bewaking</span><span class="sxs-lookup"><span data-stu-id="f925d-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="f925d-134">Metrische gegevens redis</span><span class="sxs-lookup"><span data-stu-id="f925d-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="f925d-135">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="f925d-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="f925d-136">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f925d-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="f925d-137">Ondersteuning en probleemoplossing van instellingen</span><span class="sxs-lookup"><span data-stu-id="f925d-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="f925d-138">Resourcestatus</span><span class="sxs-lookup"><span data-stu-id="f925d-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="f925d-139">Nieuw ondersteuningsverzoek</span><span class="sxs-lookup"><span data-stu-id="f925d-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="f925d-140">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f925d-140">Overview</span></span>

<span data-ttu-id="f925d-141">**Overzicht** biedt u basisinformatie over uw cache, zoals naam, poort, prijscategorie, en geselecteerde cache metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="f925d-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="f925d-142">Activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="f925d-142">Activity log</span></span>

<span data-ttu-id="f925d-143">Klik op **activiteitenlogboek** om acties die worden uitgevoerd op uw cache weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f925d-143">Click **Activity log** to view actions performed on your cache.</span></span> <span data-ttu-id="f925d-144">U kunt ook filters gebruiken om uit te breiden in deze weergave zodanig dat andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="f925d-144">You can also use filtering to expand this view to include other resources.</span></span> <span data-ttu-id="f925d-145">Zie voor meer informatie over het werken met controlelogboeken [bewerkingen met Resource Manager controleren](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="f925d-146">Zie voor meer informatie over het controleren van gebeurtenissen van Azure Redis-Cache [bewerkingen en waarschuwingen](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="f925d-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="f925d-147">Toegangsbeheer (IAM)</span><span class="sxs-lookup"><span data-stu-id="f925d-147">Access control (IAM)</span></span>

<span data-ttu-id="f925d-148">De **toegangsbeheer (IAM)** sectie biedt ondersteuning voor op rollen gebaseerde toegangsbeheer (RBAC) in de Azure portal om te voldoen aan de beheervereisten toegang eenvoudig en nauwkeurig organisaties.</span><span class="sxs-lookup"><span data-stu-id="f925d-148">The **Access control (IAM)** section provides support for role-based access control (RBAC) in the Azure portal to help organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="f925d-149">Zie voor meer informatie [toegangsbeheer op basis van rollen in Azure portal](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-149">For more information, see [Role-based access control in the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="f925d-150">Tags</span><span class="sxs-lookup"><span data-stu-id="f925d-150">Tags</span></span>

<span data-ttu-id="f925d-151">De **labels** sectie helpt u bij uw resources te organiseren.</span><span class="sxs-lookup"><span data-stu-id="f925d-151">The **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="f925d-152">Zie voor meer informatie [met labels om uw Azure-resources te organiseren](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-152">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="f925d-153">Problemen vaststellen en oplossen</span><span class="sxs-lookup"><span data-stu-id="f925d-153">Diagnose and solve problems</span></span>

<span data-ttu-id="f925d-154">Klik op **diagnosticeren en oplossen van problemen** worden opgegeven met veelvoorkomende problemen en strategieën voor het oplossen ervan.</span><span class="sxs-lookup"><span data-stu-id="f925d-154">Click **Diagnose and solve problems** to be provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="f925d-155">Instellingen</span><span class="sxs-lookup"><span data-stu-id="f925d-155">Settings</span></span>
<span data-ttu-id="f925d-156">De **instellingen** sectie kunt u toegang tot en configureer de volgende instellingen voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-156">The **Settings** section allows you to access and configure the following settings for your cache.</span></span>

* [<span data-ttu-id="f925d-157">Toegangstoetsen</span><span class="sxs-lookup"><span data-stu-id="f925d-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="f925d-158">Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="f925d-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="f925d-159">Redis-Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="f925d-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="f925d-160">Schalen</span><span class="sxs-lookup"><span data-stu-id="f925d-160">Scale</span></span>](#scale)
* [<span data-ttu-id="f925d-161">Clustergrootte redis</span><span class="sxs-lookup"><span data-stu-id="f925d-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="f925d-162">Redis-gegevenspersistentie</span><span class="sxs-lookup"><span data-stu-id="f925d-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="f925d-163">Updates plannen</span><span class="sxs-lookup"><span data-stu-id="f925d-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="f925d-164">Geo-replicatie</span><span class="sxs-lookup"><span data-stu-id="f925d-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="f925d-165">Virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="f925d-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="f925d-166">Firewall</span><span class="sxs-lookup"><span data-stu-id="f925d-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="f925d-167">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="f925d-167">Properties</span></span>](#properties)
* [<span data-ttu-id="f925d-168">Hiermee vergrendelt u</span><span class="sxs-lookup"><span data-stu-id="f925d-168">Locks</span></span>](#locks)
* [<span data-ttu-id="f925d-169">Automatiseringsscript</span><span class="sxs-lookup"><span data-stu-id="f925d-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="f925d-170">Toegangssleutels</span><span class="sxs-lookup"><span data-stu-id="f925d-170">Access keys</span></span>
<span data-ttu-id="f925d-171">Klik op **toegangssleutels** weergeven of de toegangssleutels voor uw cache opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="f925d-171">Click **Access keys** to view or regenerate the access keys for your cache.</span></span> <span data-ttu-id="f925d-172">Deze sleutels worden gebruikt door de clients verbinding maken met uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-172">These keys are used by the clients connecting to your cache.</span></span>

![Redis-Cache toegangstoetsen](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="f925d-174">Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="f925d-174">Advanced settings</span></span>
<span data-ttu-id="f925d-175">De volgende instellingen zijn geconfigureerd op de **geavanceerde instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="f925d-175">The following settings are configured on the **Advanced settings** blade.</span></span>

* [<span data-ttu-id="f925d-176">-Poorten</span><span class="sxs-lookup"><span data-stu-id="f925d-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="f925d-177">Geheugen-beleid</span><span class="sxs-lookup"><span data-stu-id="f925d-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="f925d-178">Met Keyspace-kennisgevingen (geavanceerde instellingen)</span><span class="sxs-lookup"><span data-stu-id="f925d-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="f925d-179">-Poorten</span><span class="sxs-lookup"><span data-stu-id="f925d-179">Access Ports</span></span>
<span data-ttu-id="f925d-180">Voor nieuwe caches is niet-SSL-toegang standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f925d-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="f925d-181">Als de niet-SSL-poort, klikt u op **Nee** voor **toestaan alleen toegang met SSL** op de **geavanceerde instellingen** blade en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f925d-181">To enable the non-SSL port, click **No** for **Allow access only via SSL** on the **Advanced settings** blade and then click **Save**.</span></span>

![Redis-Cache-poorten](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="f925d-183">Geheugen-beleid</span><span class="sxs-lookup"><span data-stu-id="f925d-183">Memory policies</span></span>
<span data-ttu-id="f925d-184">De **Maxmemory beleid**, **maxmemory gereserveerd**, en **maxfragmentationmemory gereserveerd** instellingen op de **geavanceerde instellingen** Blade de geheugen beleidsregels configureren voor de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-184">The **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on the **Advanced settings** blade configure the memory policies for the cache.</span></span>

![Redis-Cache Maxmemory beleid](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="f925d-186">**Beleid voor Maxmemory** configureert u het beleid verwijderen voor de cache en kunt u kiezen uit de volgende beleidsregels voor verwijdering:</span><span class="sxs-lookup"><span data-stu-id="f925d-186">**Maxmemory policy** configures the eviction policy for the cache and allows you to choose from the following eviction policies:</span></span>

* <span data-ttu-id="f925d-187">`volatile-lru`-Dit is de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="f925d-187">`volatile-lru` - this is the default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="f925d-188">Voor meer informatie over `maxmemory` beleid, Zie [Taakverwijdering beleid](http://redis.io/topics/lru-cache#eviction-policies).</span><span class="sxs-lookup"><span data-stu-id="f925d-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="f925d-189">De **maxmemory gereserveerd** instelling configureert u de hoeveelheid geheugen in MB die is gereserveerd voor niet-cache-bewerkingen zoals replicatie tijdens failover.</span><span class="sxs-lookup"><span data-stu-id="f925d-189">The **maxmemory-reserved** setting configures the amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="f925d-190">Als u deze waarde instelt, kunt u een consistente gebruikerservaring voor Redis-server hebben als de belasting van uw varieert.</span><span class="sxs-lookup"><span data-stu-id="f925d-190">Setting this value allows you to have a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="f925d-191">Deze waarde moet worden ingesteld voor de werkbelastingen die zijn geschreven zware hoger.</span><span class="sxs-lookup"><span data-stu-id="f925d-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="f925d-192">Wanneer het geheugen is gereserveerd voor dergelijke bewerkingen, is het niet beschikbaar voor de opslag van gegevens in de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="f925d-193">De **maxfragmentationmemory gereserveerd** instelling configureert u de hoeveelheid geheugen in MB die is gereserveerd voor geheugenfragmentatie.</span><span class="sxs-lookup"><span data-stu-id="f925d-193">The **maxfragmentationmemory-reserved** setting configures the amount of memory in MB that is reserved to accommodate for memory fragmentation.</span></span> <span data-ttu-id="f925d-194">Als u deze waarde instelt, kunt u een consistente ervaring bieden bij de cache vol is of bijna vol is en de fragmentatie verhouding ook hoge is Redis-server hebben.</span><span class="sxs-lookup"><span data-stu-id="f925d-194">Setting this value allows you to have a more consistent Redis server experience when the cache is full or close to full and the fragmentation ratio is also high.</span></span> <span data-ttu-id="f925d-195">Wanneer het geheugen is gereserveerd voor dergelijke bewerkingen, is het niet beschikbaar voor de opslag van gegevens in de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="f925d-196">Één ding rekening moet houden bij het kiezen van een nieuwe waarde voor geheugen reservering (**maxmemory gereserveerd** of **maxfragmentationmemory gereserveerd**) is hoe deze wijziging van invloed kan zijn op een cache die al wordt uitgevoerd met grote hoeveelheden gegevens.</span><span class="sxs-lookup"><span data-stu-id="f925d-196">One thing to consider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="f925d-197">Als u een cache 53 GB met 49 GB aan gegevens, wijzig de waarde van de reservering in 8 GB, wordt dit bijvoorbeeld de maximale hoeveelheid beschikbaar geheugen voor het systeem naar beneden 45 GB verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f925d-197">For instance, if you have a 53 GB cache with 49 GB of data, then change the reservation value to 8 GB, this will drop the max available memory for the system down to 45 GB.</span></span> <span data-ttu-id="f925d-198">Als uw huidige `used_memory` of uw `used_memory_rss` waarden hoger zijn dan de nieuwe limiet van 45 GB en vervolgens het systeem heeft onbeschikbaar maken van gegevens tot beide `used_memory` en `used_memory_rss` hieronder 45 GB zijn.</span><span class="sxs-lookup"><span data-stu-id="f925d-198">If either your current `used_memory` or your `used_memory_rss` values are higher than the new limit of 45 GB, then the system will have to evict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="f925d-199">Verwijderen kan de fragmentatie van de belasting en geheugen van de server te verhogen.</span><span class="sxs-lookup"><span data-stu-id="f925d-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="f925d-200">Voor meer informatie over metrische gegevens cache zoals `used_memory` en `used_memory_rss`, Zie [beschikbare metrische gegevens en de rapportage van intervallen](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="f925d-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f925d-201">De **maxmemory gereserveerd** en **maxfragmentationmemory gereserveerd** instellingen zijn alleen beschikbaar voor Standard en Premium in cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f925d-201">The **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="f925d-202">Met Keyspace-kennisgevingen (geavanceerde instellingen)</span><span class="sxs-lookup"><span data-stu-id="f925d-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="f925d-203">Redis keyspace meldingen zijn geconfigureerd op de **geavanceerde instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="f925d-203">Redis keyspace notifications are configured on the **Advanced settings** blade.</span></span> <span data-ttu-id="f925d-204">Keyspace-kennisgevingen kunnen clients meldingen wilt ontvangen wanneer bepaalde gebeurtenissen optreden.</span><span class="sxs-lookup"><span data-stu-id="f925d-204">Keyspace notifications allow clients to receive notifications when certain events occur.</span></span>

![Redis-Cache geavanceerde instellingen](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="f925d-206">Met Keyspace-kennisgevingen en de **melden keyspace gebeurtenissen** instelling zijn alleen beschikbaar voor Standard en Premium-caches.</span><span class="sxs-lookup"><span data-stu-id="f925d-206">Keyspace notifications and the **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="f925d-207">Zie voor meer informatie [Keyspace-kennisgevingen Redis](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="f925d-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="f925d-208">Zie voor een voorbeeld van code, de [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) bestand de [Hallo wereld](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f925d-208">For sample code, see the [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in the [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="f925d-209">Redis-Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="f925d-209">Redis Cache Advisor</span></span>
<span data-ttu-id="f925d-210">De **Redis-Cache Advisor** blade geeft aanbevelingen voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-210">The **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="f925d-211">Tijdens normale bewerkingen worden geen aanbevelingen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f925d-211">During normal operations, no recommendations are displayed.</span></span> 

![Aanbevelingen](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="f925d-213">Als alle voorwaarden wordt voldaan tijdens de bewerkingen van uw cache zoals hoog geheugengebruik, netwerkbandbreedte of belasting van de server, een waarschuwing wordt weergegeven op de **Redis-Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="f925d-213">If any conditions occur during the operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on the **Redis Cache** blade.</span></span>

![Aanbevelingen](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="f925d-215">Meer informatie vindt u op de **aanbevelingen** blade.</span><span class="sxs-lookup"><span data-stu-id="f925d-215">Further information can be found on the **Recommendations** blade.</span></span>

![Aanbevelingen](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="f925d-217">U kunt deze metrische gegevens controleren op de [grafieken bewaking](cache-how-to-monitor.md#monitoring-charts) en [gebruik grafieken](cache-how-to-monitor.md#usage-charts) secties van de **Redis-Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="f925d-217">You can monitor these metrics on the [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of the **Redis Cache** blade.</span></span>

<span data-ttu-id="f925d-218">Elke prijscategorie heeft verschillende beperkingen voor clientverbindingen, geheugen en bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="f925d-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="f925d-219">Als uw cache maximale capaciteit voor deze metrische gegevens gedurende een langere periode tijd nadert, wordt een aanbeveling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f925d-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="f925d-220">Voor meer informatie over de metrische gegevens en limieten gecontroleerd door de **aanbevelingen** hulpprogramma, Zie de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="f925d-220">For more information about the metrics and limits reviewed by the **Recommendations** tool, see the following table:</span></span>

| <span data-ttu-id="f925d-221">Redis-Cache metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="f925d-221">Redis Cache metric</span></span> | <span data-ttu-id="f925d-222">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="f925d-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="f925d-223">Gebruik van netwerkbandbreedte</span><span class="sxs-lookup"><span data-stu-id="f925d-223">Network bandwidth usage</span></span> |[<span data-ttu-id="f925d-224">Prestaties van de cache - bandbreedte</span><span class="sxs-lookup"><span data-stu-id="f925d-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="f925d-225">Verbonden clients</span><span class="sxs-lookup"><span data-stu-id="f925d-225">Connected clients</span></span> |[<span data-ttu-id="f925d-226">Standaard Redis-serverconfiguratie - maxclients</span><span class="sxs-lookup"><span data-stu-id="f925d-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="f925d-227">Belasting van de server</span><span class="sxs-lookup"><span data-stu-id="f925d-227">Server load</span></span> |[<span data-ttu-id="f925d-228">Gebruik grafieken - belasting van de Redis-Server</span><span class="sxs-lookup"><span data-stu-id="f925d-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="f925d-229">Geheugengebruik</span><span class="sxs-lookup"><span data-stu-id="f925d-229">Memory usage</span></span> |[<span data-ttu-id="f925d-230">Prestaties van de cache - grootte</span><span class="sxs-lookup"><span data-stu-id="f925d-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="f925d-231">Als u wilt uw cache bijwerken, klikt u op **nu bijwerken** als de prijscategorie wilt wijzigen en [scale](#scale) uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-231">To upgrade your cache, click **Upgrade now** to change the pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="f925d-232">Zie voor meer informatie over het kiezen van een prijscategorie [welke aanbieding Redis-Cache en de grootte moet ik gebruiken?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="f925d-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="f925d-233">Schalen</span><span class="sxs-lookup"><span data-stu-id="f925d-233">Scale</span></span>
<span data-ttu-id="f925d-234">Klik op **Scale** weergeven of wijzigen van de prijscategorie voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-234">Click **Scale** to view or change the pricing tier for your cache.</span></span> <span data-ttu-id="f925d-235">Zie voor meer informatie over het schalen [How to Scale Azure Redis-Cache](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-235">For more information on scaling, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Redis-Cache prijscategorie](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="f925d-237">Clustergrootte redis</span><span class="sxs-lookup"><span data-stu-id="f925d-237">Redis Cluster Size</span></span>
<span data-ttu-id="f925d-238">Klik op **(PREVIEW) Redis clustergrootte** wijzigen van de clustergrootte voor een actieve premium-cache met clustering is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f925d-238">Click **(PREVIEW) Redis Cluster Size** to change the cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="f925d-239">Houd er rekening mee dat bij de Azure Redis-Cache Premium-laag is vrijgegeven voor algemene beschikbaarheid, de clustergrootte Redis-functie momenteel in preview is.</span><span class="sxs-lookup"><span data-stu-id="f925d-239">Note that while the Azure Redis Cache Premium tier has been released to General Availability, the Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Clustergrootte redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="f925d-241">Gebruik de schuifregelaar om de clustergrootte, of typ een getal tussen 1 en 10 in de **Shard aantal** tekstvak en klik op **OK** om op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f925d-241">To change the cluster size, use the slider or type a number between 1 and 10 in the **Shard count** text box and click **OK** to save.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f925d-242">Redis clustering is alleen beschikbaar voor Premium-caches.</span><span class="sxs-lookup"><span data-stu-id="f925d-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="f925d-243">Zie [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md) (Clustering voor een Premium Azure Redis Cache configureren) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f925d-243">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="f925d-244">Redis-gegevenspersistentie</span><span class="sxs-lookup"><span data-stu-id="f925d-244">Redis data persistence</span></span>
<span data-ttu-id="f925d-245">Klik op **Redis-gegevenspersistentie** als wilt inschakelen, uitschakelen of gegevenspersistentie configureren voor uw cache premium.</span><span class="sxs-lookup"><span data-stu-id="f925d-245">Click **Redis data persistence** to enable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="f925d-246">Azure Redis-Cache met behulp van Redis-persistentie biedt [RDB persistentie](cache-how-to-premium-persistence.md#configure-rdb-persistence) of [AOF persistentie](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="f925d-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="f925d-247">Zie voor meer informatie [persistentie voor een Premium Azure Redis-Cache configureren](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-247">For more information, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="f925d-248">Redis-gegevenspersistentie is alleen beschikbaar voor Premium-caches.</span><span class="sxs-lookup"><span data-stu-id="f925d-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="f925d-249">Updates plannen</span><span class="sxs-lookup"><span data-stu-id="f925d-249">Schedule updates</span></span>
<span data-ttu-id="f925d-250">De **updates plannen** blade kunt u een onderhoudsvenster voor Redis-serverupdates voor uw cache aanwijzen.</span><span class="sxs-lookup"><span data-stu-id="f925d-250">The **Schedule updates** blade allows you to designate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f925d-251">Het onderhoudsvenster is alleen van toepassing op Redis-serverupdates, en niet naar een Azure-updates of updates voor het besturingssysteem van de virtuele machines die als host fungeren van de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-251">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![Updates plannen](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="f925d-253">Als u een onderhoudsvenster, controleren de gewenste dagen het Beginuur van het venster Onderhoud voor elke dag opgeeft, en klik **OK**.</span><span class="sxs-lookup"><span data-stu-id="f925d-253">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="f925d-254">Houd er rekening mee dat de duur van het onderhoudsvenster is ingesteld op UTC.</span><span class="sxs-lookup"><span data-stu-id="f925d-254">Note that the maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f925d-255">De **updates plannen** functionaliteit is alleen beschikbaar voor Premium-laag caches.</span><span class="sxs-lookup"><span data-stu-id="f925d-255">The **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="f925d-256">Zie voor meer informatie en instructies [beheer van Azure Redis-Cache - updates plannen](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="f925d-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="f925d-257">Geo-replicatie</span><span class="sxs-lookup"><span data-stu-id="f925d-257">Geo-replication</span></span>

<span data-ttu-id="f925d-258">De **Geo-replicatie** blade biedt een mechanisme voor het koppelen van twee exemplaren van Premium-laag Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-258">The **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="f925d-259">Een cache is aangewezen als het primaire gekoppelde cachegeheugen en de andere als de secundaire gekoppelde cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-259">One cache is designated as the primary linked cache, and the other as the secondary linked cache.</span></span> <span data-ttu-id="f925d-260">De secundaire gekoppelde cache wordt alleen-lezen en gegevens naar de primaire cache geschreven worden gerepliceerd naar de secundaire gekoppelde cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-260">The secondary linked cache becomes read-only, and data written to the primary cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="f925d-261">Deze functionaliteit kan worden gebruikt voor het repliceren van een cache in Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="f925d-261">This functionality can be used to replicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f925d-262">**Geo-replicatie** is alleen beschikbaar voor Premium-laag caches.</span><span class="sxs-lookup"><span data-stu-id="f925d-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="f925d-263">Zie voor meer informatie en instructies [Geo-replicatie configureren voor Azure Redis-Cache](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-263">For more information and instructions, see [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="f925d-264">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="f925d-264">Virtual Network</span></span>
<span data-ttu-id="f925d-265">De **virtueel netwerk** sectie kunt u de instellingen van het virtuele netwerk voor uw cache configureren.</span><span class="sxs-lookup"><span data-stu-id="f925d-265">The **Virtual Network** section allows you to configure the virtual network settings for your cache.</span></span> <span data-ttu-id="f925d-266">Voor informatie over het maken van een premium-cache met VNET ondersteunen en bijwerken van de instellingen, Zie [ondersteuning voor virtueel netwerk configureren voor een Premium Azure Redis-Cache](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-266">For information on creating a premium cache with VNET support and updating its settings, see [How to configure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f925d-267">Instellingen voor virtuele netwerken zijn alleen beschikbaar voor premium-caches die zijn geconfigureerd met ondersteuning voor VNET tijdens het maken van de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="f925d-268">Firewall</span><span class="sxs-lookup"><span data-stu-id="f925d-268">Firewall</span></span>

<span data-ttu-id="f925d-269">Klik op **Firewall** bekijken en firewallregels configureren voor uw Premium Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-269">Click **Firewall** to view and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Firewall](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="f925d-271">U kunt firewallregels opgeven met een begin- en IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="f925d-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="f925d-272">Firewallregels zijn geconfigureerd, alleen clientverbindingen van het opgegeven IP-adresbereiken verbinding kunnen maken met de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-272">When firewall rules are configured, only client connections from the specified IP address ranges can connect to the cache.</span></span> <span data-ttu-id="f925d-273">Wanneer een firewallregel wordt opgeslagen. is er een korte vertraging optreden voordat de regel is van kracht.</span><span class="sxs-lookup"><span data-stu-id="f925d-273">When a firewall rule is saved there is a short delay before the rule is effective.</span></span> <span data-ttu-id="f925d-274">Dit uitstel is meestal minder dan een minuut.</span><span class="sxs-lookup"><span data-stu-id="f925d-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f925d-275">Verbindingen van Azure Redis-Cache bewaken altijd toegestaan, zelfs als de firewallregels zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f925d-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="f925d-276">Firewallregels zijn alleen beschikbaar voor Premium-laag caches.</span><span class="sxs-lookup"><span data-stu-id="f925d-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="f925d-277">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="f925d-277">Properties</span></span>
<span data-ttu-id="f925d-278">Klik op **eigenschappen** informatie bekijken over uw cache, met inbegrip van de cache-eindpunt en -poorten.</span><span class="sxs-lookup"><span data-stu-id="f925d-278">Click **Properties** to view information about your cache, including the cache endpoint and ports.</span></span>

![Redis-Cache-eigenschappen](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="f925d-280">Vergrendelingen</span><span class="sxs-lookup"><span data-stu-id="f925d-280">Locks</span></span>
<span data-ttu-id="f925d-281">De **vergrendelt** sectie kunt u een abonnement, resourcegroep of resource om te voorkomen dat andere gebruikers in uw organisatie per ongeluk verwijderen of wijzigen van kritieke bronnen vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="f925d-281">The **Locks** section allows you to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="f925d-282">Zie voor meer informatie [Resources vergrendelen met Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="f925d-283">Automatiseringsscript</span><span class="sxs-lookup"><span data-stu-id="f925d-283">Automation script</span></span>

<span data-ttu-id="f925d-284">Klik op **automatiseringsscript** te exporteren van een sjabloon van uw geïmplementeerde resources voor toekomstige implementaties.</span><span class="sxs-lookup"><span data-stu-id="f925d-284">Click **Automation script** to build and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="f925d-285">Zie voor meer informatie over het werken met sjablonen [implementeren van resources met Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="f925d-286">Instellingen voor beheer</span><span class="sxs-lookup"><span data-stu-id="f925d-286">Administration settings</span></span>
<span data-ttu-id="f925d-287">De instellingen in de **beheer** sectie kunt u de volgende beheertaken uitvoeren voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-287">The settings in the **Administration** section allow you to perform the following administrative tasks for your cache.</span></span> 

![Beheer](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="f925d-289">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="f925d-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="f925d-290">Gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="f925d-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="f925d-291">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="f925d-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="f925d-292">Import/Export</span><span class="sxs-lookup"><span data-stu-id="f925d-292">Import/Export</span></span>
<span data-ttu-id="f925d-293">Import/Export is een Azure Redis-Cache gegevensbewerking voor het beheer, zodat u kunt importeren en exporteren van gegevens in de cache door te importeren en exporteren van een momentopname van een Redis-Cache Database (RDB) uit de cache premium naar een paginablob in Azure Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="f925d-293">Import/Export is an Azure Redis Cache data management operation, which allows you to import and export data in the cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a page blob in an Azure Storage Account.</span></span> <span data-ttu-id="f925d-294">Voor importeren/exporteren kunt u migreren tussen verschillende exemplaren van Azure Redis-Cache of het vullen van de cache met gegevens voor het gebruik.</span><span class="sxs-lookup"><span data-stu-id="f925d-294">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="f925d-295">Invoer kan worden gebruikt om Redis compatibele RDB bestanden vanaf een willekeurige Redis-server uitgevoerd in een cloud of de omgeving, inclusief Redis uitgevoerd op Linux, Windows of elke cloudprovider zoals Amazon Web Services en andere.</span><span class="sxs-lookup"><span data-stu-id="f925d-295">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="f925d-296">Het importeren van gegevens is een eenvoudige manier voor het maken van een cache met vooraf ingestelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="f925d-296">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="f925d-297">Tijdens het importproces Azure Redis-Cache laadt de bestanden RDB uit Azure storage in het geheugen en voegt vervolgens de sleutels in de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-297">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory, and then inserts the keys into the cache.</span></span>

<span data-ttu-id="f925d-298">Exporteren kunt u de gegevens die zijn opgeslagen in Azure Redis-Cache voor Redis-compatibele RDB bestanden exporteren.</span><span class="sxs-lookup"><span data-stu-id="f925d-298">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB files.</span></span> <span data-ttu-id="f925d-299">U kunt deze functie gebruiken om gegevens te verplaatsen van een Azure Redis-Cache-exemplaar naar een andere of een andere Redis-server.</span><span class="sxs-lookup"><span data-stu-id="f925d-299">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="f925d-300">Tijdens het exportproces een tijdelijk bestand wordt gemaakt op de virtuele machine die als host fungeert voor de server-exemplaar van Azure Redis-Cache en het bestand is geüpload naar de aangewezen storage-account.</span><span class="sxs-lookup"><span data-stu-id="f925d-300">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="f925d-301">Wanneer de exportbewerking is voltooid met de status van slagen of mislukken, wordt het tijdelijke bestand verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f925d-301">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f925d-302">Import/Export is alleen beschikbaar voor Premium-laag caches.</span><span class="sxs-lookup"><span data-stu-id="f925d-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="f925d-303">Zie voor meer informatie en instructies [importeren en exporteren van gegevens in Azure Redis-Cache](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="f925d-304">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="f925d-304">Reboot</span></span>
<span data-ttu-id="f925d-305">De **opnieuw opstarten** blade kunt u opnieuw opstarten van de knooppunten van de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-305">The **Reboot** blade allows you to reboot the nodes of your cache.</span></span> <span data-ttu-id="f925d-306">Deze mogelijkheid opnieuw opstarten, kunt u de toepassing te testen voor tolerantie als er een storing van een cacheknooppunt.</span><span class="sxs-lookup"><span data-stu-id="f925d-306">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![Opnieuw opstarten](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="f925d-308">Als u een premium-cache hebt met clusteren is ingeschakeld, kunt u selecteren welke shards van de cache op te starten.</span><span class="sxs-lookup"><span data-stu-id="f925d-308">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![Opnieuw opstarten](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="f925d-310">Opnieuw opstarten van een of meer knooppunten van de cache, selecteer de gewenste knooppunten en klikt u op **opnieuw opstarten**.</span><span class="sxs-lookup"><span data-stu-id="f925d-310">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="f925d-311">Als u een premium-cache hebt met clusteren is ingeschakeld, selecteert u de shard(s) op te starten en klik vervolgens op **opnieuw opstarten**.</span><span class="sxs-lookup"><span data-stu-id="f925d-311">If you have a premium cache with clustering enabled, select the shard(s) to reboot and then click **Reboot**.</span></span> <span data-ttu-id="f925d-312">Na een paar minuten weer de geselecteerde knooppunten opnieuw worden opgestart en er wordt on line later een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="f925d-312">After a few minutes, the selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f925d-313">Opnieuw opstarten is nu beschikbaar voor alle Prijscategorieën.</span><span class="sxs-lookup"><span data-stu-id="f925d-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="f925d-314">Zie voor meer informatie en instructies [beheer van Azure Redis-Cache - opnieuw opstarten](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="f925d-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="f925d-315">Bewaking</span><span class="sxs-lookup"><span data-stu-id="f925d-315">Monitoring</span></span>

<span data-ttu-id="f925d-316">De **bewaking** sectie kunt u voor het configureren van diagnostische gegevens en de bewaking van uw Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-316">The **Monitoring** section allows you to configure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="f925d-317">Zie voor meer informatie over het controleren van Azure Redis-Cache en diagnostische gegevens [Azure Redis-Cache controleren](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How to monitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnostiek](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="f925d-319">Metrische gegevens redis</span><span class="sxs-lookup"><span data-stu-id="f925d-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="f925d-320">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="f925d-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="f925d-321">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f925d-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="f925d-322">Metrische gegevens redis</span><span class="sxs-lookup"><span data-stu-id="f925d-322">Redis metrics</span></span>
<span data-ttu-id="f925d-323">Klik op **Redis metrische gegevens** naar [metrische gegevens weergeven](cache-how-to-monitor.md#view-cache-metrics) voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-323">Click **Redis metrics** to [view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="f925d-324">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="f925d-324">Alert rules</span></span>

<span data-ttu-id="f925d-325">Klik op **waarschuwing regels** voor het configureren van waarschuwingen op basis van Redis-Cache metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="f925d-325">Click **Alert rules** to configure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="f925d-326">Zie voor meer informatie [waarschuwingen](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="f925d-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="f925d-327">Diagnostiek</span><span class="sxs-lookup"><span data-stu-id="f925d-327">Diagnostics</span></span>

<span data-ttu-id="f925d-328">Cache metrische gegevens in de Azure-Monitor zijn standaard [30 dagen bewaard](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) en vervolgens verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f925d-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="f925d-329">Om te blijven behouden de metrische gegevens van uw cache langer dan 30 dagen, klikt u op **Diagnostics** naar [configureren van het opslagaccount](cache-how-to-monitor.md#export-cache-metrics) gebruikt voor het opslaan van cache diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="f925d-329">To persist your cache metrics for longer than 30 days, click **Diagnostics** to [configure the storage account](cache-how-to-monitor.md#export-cache-metrics) used to store cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="f925d-330">Naast het archiveren van de metrische gegevens van uw cache naar de opslag, kunt u ook [ze naar een Event hub te streamen of ze verzenden naar logboekanalyse](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="f925d-330">In addition to archiving your cache metrics to storage, you can also [stream them to an Event hub or send them to Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="f925d-331">Ondersteuning en probleemoplossing van instellingen</span><span class="sxs-lookup"><span data-stu-id="f925d-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="f925d-332">De instellingen in de **ondersteuning + probleemoplossing** sectie bieden u opties voor het oplossen van problemen met uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-332">The settings in the **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Ondersteuning + probleemoplossing](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="f925d-334">Resourcestatus</span><span class="sxs-lookup"><span data-stu-id="f925d-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="f925d-335">Nieuw ondersteuningsverzoek</span><span class="sxs-lookup"><span data-stu-id="f925d-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="f925d-336">Status van resources</span><span class="sxs-lookup"><span data-stu-id="f925d-336">Resource health</span></span>
<span data-ttu-id="f925d-337">**Resourcestatus** controleert uw resource en geeft u aan als deze wordt uitgevoerd zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="f925d-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="f925d-338">Zie voor meer informatie over de health-service van Azure Resource [overzicht van Azure Resource health](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-338">For more information about the Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f925d-339">De resourcestatus is momenteel niet mogelijk om te rapporteren over de status van Azure Redis-Cache-exemplaren die worden gehost in een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="f925d-339">Resource health is currently unable to report on the health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="f925d-340">Zie voor meer informatie [alle functies van de cache werken bij het hosten van een cache in een VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="f925d-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="f925d-341">Nieuw ondersteuningsverzoek</span><span class="sxs-lookup"><span data-stu-id="f925d-341">New support request</span></span>
<span data-ttu-id="f925d-342">Klik op **nieuw ondersteuningsverzoek** om ondersteuning te vragen voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-342">Click **New support request** to open a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="f925d-343">Standaardconfiguratie van het Redis-server</span><span class="sxs-lookup"><span data-stu-id="f925d-343">Default Redis server configuration</span></span>
<span data-ttu-id="f925d-344">Nieuwe exemplaren van Azure Redis-Cache zijn geconfigureerd met de volgende Redis configuratie standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="f925d-344">New Azure Redis Cache instances are configured with the following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="f925d-345">De instellingen in deze sectie kunnen niet worden gewijzigd met de `StackExchange.Redis.IServer.ConfigSet` methode.</span><span class="sxs-lookup"><span data-stu-id="f925d-345">The settings in this section cannot be changed using the `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="f925d-346">Als deze methode wordt aangeroepen met een van de opdrachten in deze sectie, een vergelijkbaar met de volgende uitzondering:</span><span class="sxs-lookup"><span data-stu-id="f925d-346">If this method is called with one of the commands in this section, an exception similar to the following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="f925d-347">Alle waarden die kunnen worden geconfigureerd, zoals **max-geheugen-policy**, kunnen worden geconfigureerd via de Azure-portal of het opdrachtregelprogramma beheerprogramma's, zoals Azure CLI of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f925d-347">Any values that are configurable, such as **max-memory-policy**, are configurable through the Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="f925d-348">Instelling</span><span class="sxs-lookup"><span data-stu-id="f925d-348">Setting</span></span> | <span data-ttu-id="f925d-349">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="f925d-349">Default value</span></span> | <span data-ttu-id="f925d-350">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f925d-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="f925d-351">16</span><span class="sxs-lookup"><span data-stu-id="f925d-351">16</span></span> |<span data-ttu-id="f925d-352">Het aantal databases 16 is, maar u kunt een ander nummer is gebaseerd op de prijscategorie configureren. <sup>1</sup> de standaarddatabase DB 0 is, kunt u een andere naam op een afzonderlijke verbinding basis met `connection.GetDatabase(dbid)` waar `dbid` is een getal tussen `0` en `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="f925d-352">The default number of databases is 16 but you can configure a different number based on the pricing tier.<sup>1</sup> The default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="f925d-353">Afhankelijk van de prijscategorie<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="f925d-353">Depends on the pricing tier<sup>2</sup></span></span> |<span data-ttu-id="f925d-354">Dit is het maximum aantal verbonden clients tegelijk toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f925d-354">This is the maximum number of connected clients allowed at the same time.</span></span> <span data-ttu-id="f925d-355">Zodra de limiet is bereikt Redis Hiermee sluit u de nieuwe verbindingen, een 'maximum aantal clients bereikt'-fout.</span><span class="sxs-lookup"><span data-stu-id="f925d-355">Once the limit is reached Redis closes all the new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="f925d-356">Beleid voor Maxmemory is de instelling voor hoe Redis geselecteerd wat u moet verwijderen wanneer `maxmemory` (de grootte van de cache die u hebt geselecteerd bij het maken van de cache van de aanbieding) is bereikt.</span><span class="sxs-lookup"><span data-stu-id="f925d-356">Maxmemory policy is the setting for how Redis selects what to remove when `maxmemory` (the size of the cache offering you selected when you created the cache) is reached.</span></span> <span data-ttu-id="f925d-357">Met Azure Redis-Cache de standaardinstelling is `volatile-lru`, waarbij de sleutels worden verwijderd met een vervaldatum instellen met behulp van een LRU-algoritme.</span><span class="sxs-lookup"><span data-stu-id="f925d-357">With Azure Redis Cache the default setting is `volatile-lru`, which removes the keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="f925d-358">Deze instelling kan worden geconfigureerd in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f925d-358">This setting can be configured in the Azure portal.</span></span> <span data-ttu-id="f925d-359">Zie voor meer informatie [geheugen beleid](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="f925d-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="f925d-360">3</span><span class="sxs-lookup"><span data-stu-id="f925d-360">3</span></span> |<span data-ttu-id="f925d-361">Voor het opslaan van geheugen zijn LRU- en minimale TTL-algoritmes redelijk algoritmen in plaats van nauwkeurige algoritmen.</span><span class="sxs-lookup"><span data-stu-id="f925d-361">To save memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="f925d-362">Standaard Redis controles drie sleutels en aanbiedingen die minder recent is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f925d-362">By default Redis checks three keys and picks the one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="f925d-363">5,000</span><span class="sxs-lookup"><span data-stu-id="f925d-363">5,000</span></span> |<span data-ttu-id="f925d-364">Maximale uitvoeringstijd van een script Lua in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="f925d-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="f925d-365">Als de maximale uitvoeringstijd is bereikt, registreert Redis dat een script nog steeds uitgevoerd na de maximale toegestane tijd wordt en begint te reageren op query's met een fout.</span><span class="sxs-lookup"><span data-stu-id="f925d-365">If the maximum execution time is reached, Redis logs that a script is still in execution after the maximum allowed time, and starts to reply to queries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="f925d-366">500</span><span class="sxs-lookup"><span data-stu-id="f925d-366">500</span></span> |<span data-ttu-id="f925d-367">Maximale grootte van de wachtrij script.</span><span class="sxs-lookup"><span data-stu-id="f925d-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="f925d-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="f925d-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="f925d-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="f925d-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="f925d-370">De limieten van de client uitvoer buffer kunnen worden gebruikt om af te dwingen verbreken van de verbinding van clients die niet van gegevens van de server snel genoeg voor een bepaalde reden lezen zijn (een veelvoorkomende reden is dat een client Pub subitems berichten zo snel als de publisher kan ze produceren kan niet gebruiken).</span><span class="sxs-lookup"><span data-stu-id="f925d-370">The client output buffer limits can be used to force disconnection of clients that are not reading data from the server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as the publisher can produce them).</span></span> <span data-ttu-id="f925d-371">Zie voor meer informatie [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="f925d-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="f925d-372"><a name="databases"></a>
<sup>1</sup>de limiet voor `databases` verschilt voor elk Azure Redis-Cache prijscategorie en kan worden ingesteld bij het maken van de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-372"><a name="databases"></a>
<sup>1</sup>The limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="f925d-373">Als er geen `databases` instelling is opgegeven tijdens het maken van de cache, de standaardwaarde is 16.</span><span class="sxs-lookup"><span data-stu-id="f925d-373">If no `databases` setting is specified during cache creation, the default is 16.</span></span>

* <span data-ttu-id="f925d-374">Basic en Standard caches</span><span class="sxs-lookup"><span data-stu-id="f925d-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="f925d-375">C0 (250 MB)-cache - maximaal 16-databases</span><span class="sxs-lookup"><span data-stu-id="f925d-375">C0 (250 MB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="f925d-376">C1 (1 GB)-cache - maximaal 16-databases</span><span class="sxs-lookup"><span data-stu-id="f925d-376">C1 (1 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="f925d-377">C2 (2,5 GB)-cache - maximaal 16-databases</span><span class="sxs-lookup"><span data-stu-id="f925d-377">C2 (2.5 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="f925d-378">C3 (6 GB)-cache - maximaal 16-databases</span><span class="sxs-lookup"><span data-stu-id="f925d-378">C3 (6 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="f925d-379">C4 (13 GB)-cache - maximaal 32 databases</span><span class="sxs-lookup"><span data-stu-id="f925d-379">C4 (13 GB) cache - up to 32 databases</span></span>
  * <span data-ttu-id="f925d-380">C5 (26 GB)-cache - maximaal 48 databases</span><span class="sxs-lookup"><span data-stu-id="f925d-380">C5 (26 GB) cache - up to 48 databases</span></span>
  * <span data-ttu-id="f925d-381">C6 (53 GB)-cache - maximaal 64 databases</span><span class="sxs-lookup"><span data-stu-id="f925d-381">C6 (53 GB) cache - up to 64 databases</span></span>
* <span data-ttu-id="f925d-382">Premium-caches</span><span class="sxs-lookup"><span data-stu-id="f925d-382">Premium caches</span></span>
  * <span data-ttu-id="f925d-383">P1 (6 GB - 60 GB) tot maximaal 16-databases</span><span class="sxs-lookup"><span data-stu-id="f925d-383">P1 (6 GB - 60 GB) - up to 16 databases</span></span>
  * <span data-ttu-id="f925d-384">P2 (13 GB - 130 GB), maximaal 32 databases</span><span class="sxs-lookup"><span data-stu-id="f925d-384">P2 (13 GB - 130 GB) - up to 32 databases</span></span>
  * <span data-ttu-id="f925d-385">P3 (26 GB - 260 GB) tot maximaal 48 databases</span><span class="sxs-lookup"><span data-stu-id="f925d-385">P3 (26 GB - 260 GB) - up to 48 databases</span></span>
  * <span data-ttu-id="f925d-386">P4 (53 GB - 530 GB) tot maximaal 64 databases</span><span class="sxs-lookup"><span data-stu-id="f925d-386">P4 (53 GB - 530 GB) - up to 64 databases</span></span>
  * <span data-ttu-id="f925d-387">Alle premium caches met Redis-cluster ingeschakeld - Redis-cluster biedt alleen ondersteuning voor gebruik van 0-database zodat de `databases` limiet voor elke premium-cache met Redis-cluster ingeschakeld is in feite 1 en de [Selecteer](http://redis.io/commands/select) opdracht is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f925d-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so the `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and the [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="f925d-388">Zie voor meer informatie [moet ik mijn clienttoepassing clustering Breng eventuele wijzigingen?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="f925d-388">For more information, see [Do I need to make any changes to my client application to use clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="f925d-389">Zie voor meer informatie over databases [wat Redis-databases zijn?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="f925d-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="f925d-390">De `databases` instelling kan worden geconfigureerd tijdens de cache maken en alleen met behulp van PowerShell, CLI of andere clients management.</span><span class="sxs-lookup"><span data-stu-id="f925d-390">The `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="f925d-391">Voor een voorbeeld van de configuratie van `databases` tijdens het maken van de cache met behulp van PowerShell, Zie [nieuw AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="f925d-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="f925d-392"><a name="maxclients"></a>
<sup>2</sup> `maxclients` verschilt voor elk Azure Redis-Cache prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="f925d-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="f925d-393">Basic en Standard caches</span><span class="sxs-lookup"><span data-stu-id="f925d-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="f925d-394">C0 (250 MB)-cache - maximaal 256-verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-394">C0 (250 MB) cache - up to 256 connections</span></span>
  * <span data-ttu-id="f925d-395">C1 (1 GB)-cache - maximaal 1000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-395">C1 (1 GB) cache - up to 1,000 connections</span></span>
  * <span data-ttu-id="f925d-396">C2 (2,5 GB)-cache - maximaal 2.000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-396">C2 (2.5 GB) cache - up to 2,000 connections</span></span>
  * <span data-ttu-id="f925d-397">C3 (6 GB)-cache - maximaal 5000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-397">C3 (6 GB) cache - up to 5,000 connections</span></span>
  * <span data-ttu-id="f925d-398">C4 (13 GB)-cache - maximaal 10.000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-398">C4 (13 GB) cache - up to 10,000 connections</span></span>
  * <span data-ttu-id="f925d-399">C5 (26 GB)-cache - maximaal 15.000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-399">C5 (26 GB) cache - up to 15,000 connections</span></span>
  * <span data-ttu-id="f925d-400">C6 (53 GB)-cache - maximaal 20.000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-400">C6 (53 GB) cache - up to 20,000 connections</span></span>
* <span data-ttu-id="f925d-401">Premium-caches</span><span class="sxs-lookup"><span data-stu-id="f925d-401">Premium caches</span></span>
  * <span data-ttu-id="f925d-402">P1 (6 GB - 60 GB) tot 7.500 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-402">P1 (6 GB - 60 GB) - up to 7,500 connections</span></span>
  * <span data-ttu-id="f925d-403">P2 (13 GB - 130 GB) tot maximaal 15.000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-403">P2 (13 GB - 130 GB) - up to 15,000 connections</span></span>
  * <span data-ttu-id="f925d-404">P3 (26 GB - 260 GB) tot 30.000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-404">P3 (26 GB - 260 GB) - up to 30,000 connections</span></span>
  * <span data-ttu-id="f925d-405">P4 (53 GB - 530 GB) tot 40.000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="f925d-405">P4 (53 GB - 530 GB) - up to 40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="f925d-406">Kunt u elke grootte van cache *tot* een bepaald aantal verbindingen, elke verbinding met Redis heeft overhead gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f925d-406">While each size of cache allows *up to* a certain number of connections, each connection to Redis has overhead associated with it.</span></span> <span data-ttu-id="f925d-407">Een voorbeeld van een dergelijke overhead zou zijn CPU- en geheugengebruik als gevolg van TLS/SSL-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="f925d-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="f925d-408">De maximale verbindingslimiet voor een opgegeven cachegrootte wordt ervan uitgegaan dat een licht geladen cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-408">The maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="f925d-409">Als uit verbinding overhead laden *plus* laden vanaf de clientbewerkingen dan er capaciteit voor het systeem, de cache kunt capaciteitsproblemen moeten ondervinden zelfs als u hebt niet de verbindingslimiet voor de huidige cachegrootte overschreden.</span><span class="sxs-lookup"><span data-stu-id="f925d-409">If load from connection overhead *plus* load from client operations exceeds capacity for the system, the cache can experience capacity issues even if you have not exceeded the connection limit for the current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="f925d-410">Redis opdrachten niet ondersteund in Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="f925d-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f925d-411">Omdat de configuratie en beheer van exemplaren van Azure Redis-Cache wordt beheerd door Microsoft, worden de volgende opdrachten zijn uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f925d-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, the following commands are disabled.</span></span> <span data-ttu-id="f925d-412">Als u probeert aan te roepen ze, ontvangt u een foutbericht weergegeven dat vergelijkbaar is met `"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="f925d-412">If you try to invoke them, you receive an error message similar to `"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="f925d-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="f925d-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="f925d-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="f925d-414">BGSAVE</span></span>
> * <span data-ttu-id="f925d-415">CONFIGURATIE</span><span class="sxs-lookup"><span data-stu-id="f925d-415">CONFIG</span></span>
> * <span data-ttu-id="f925d-416">FOUTEN OPSPOREN</span><span class="sxs-lookup"><span data-stu-id="f925d-416">DEBUG</span></span>
> * <span data-ttu-id="f925d-417">MIGREREN</span><span class="sxs-lookup"><span data-stu-id="f925d-417">MIGRATE</span></span>
> * <span data-ttu-id="f925d-418">OPSLAAN</span><span class="sxs-lookup"><span data-stu-id="f925d-418">SAVE</span></span>
> * <span data-ttu-id="f925d-419">AFSLUITEN</span><span class="sxs-lookup"><span data-stu-id="f925d-419">SHUTDOWN</span></span>
> * <span data-ttu-id="f925d-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="f925d-420">SLAVEOF</span></span>
> * <span data-ttu-id="f925d-421">CLUSTER - schrijven zijn uitgeschakeld, maar alleen-lezen Cluster opdrachten zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f925d-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="f925d-422">Zie voor meer informatie over Redis opdrachten [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="f925d-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="f925d-423">Redis-console</span><span class="sxs-lookup"><span data-stu-id="f925d-423">Redis console</span></span>
<span data-ttu-id="f925d-424">Opdrachten kunnen veilig worden verleend aan uw Azure Redis-Cache-exemplaren die gebruikmaken van de **Redis-Console**, die beschikbaar is in de Azure-portal voor alle cachelagen.</span><span class="sxs-lookup"><span data-stu-id="f925d-424">You can securely issue commands to your Azure Redis Cache instances using the **Redis Console**, which is available in the Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="f925d-425">De Redis-Console werkt niet met [VNET](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-425">The Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="f925d-426">Wanneer uw cache deel van een VNET uitmaakt, alleen de clients in het VNET, hebben toegang tot de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-426">When your cache is part of a VNET, only clients in the VNET can access the cache.</span></span> <span data-ttu-id="f925d-427">Omdat Redis-Console wordt uitgevoerd in uw lokale browser, die zich buiten het VNET, kan het verbinden met uw cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-427">Because Redis Console runs in your local browser, which is outside the VNET, it can't connect to your cache.</span></span>
> - <span data-ttu-id="f925d-428">Niet alle Redis-opdrachten worden ondersteund in Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="f925d-429">Voor een lijst met Redis-opdrachten die zijn uitgeschakeld voor Azure Redis-Cache, Zie de vorige [Redis opdrachten niet ondersteund in Azure Redis-Cache](#redis-commands-not-supported-in-azure-redis-cache) sectie.</span><span class="sxs-lookup"><span data-stu-id="f925d-429">For a list of Redis commands that are disabled for Azure Redis Cache, see the previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="f925d-430">Zie voor meer informatie over Redis opdrachten [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="f925d-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="f925d-431">Voor toegang tot de Redis-Console, klikt u op **Console** van de **Redis-Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="f925d-431">To access the Redis Console, click **Console** from the **Redis Cache** blade.</span></span>

![Redis-console](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="f925d-433">Voor het uitgeven van opdrachten op basis van uw cache-exemplaar, typt u de gewenste opdracht in de console.</span><span class="sxs-lookup"><span data-stu-id="f925d-433">To issue commands against your cache instance, simply type the desired command into the console.</span></span>

![Redis-console](./media/cache-configure/redis-console.png)


### <a name="using-the-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="f925d-435">Gebruik de Redis-Console met een geclusterd premium-cache</span><span class="sxs-lookup"><span data-stu-id="f925d-435">Using the Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="f925d-436">Wanneer met de Redis-Console met een premium cache voor geclusterde, kunt u opdrachten uitgeven aan een enkele shard van de cache.</span><span class="sxs-lookup"><span data-stu-id="f925d-436">When using the Redis Console with a premium clustered cache, you can issue commands to a single shard of the cache.</span></span> <span data-ttu-id="f925d-437">Om een opdracht te verlenen aan een specifieke shard, eerst verbinding maken met de gewenste shard door erop te klikken op de shard-objectkiezer.</span><span class="sxs-lookup"><span data-stu-id="f925d-437">To issue a command to a specific shard, first connect to the desired shard by clicking it on the shard picker.</span></span>

![Redis-console](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="f925d-439">Als u probeert te krijgen tot een sleutel die is opgeslagen in een andere shard dan de verbonden shard, ontvangt u een foutbericht weergegeven dat vergelijkbaar is met het volgende bericht.</span><span class="sxs-lookup"><span data-stu-id="f925d-439">If you attempt to access a key that is stored in a different shard than the connected shard, you receive an error message similar to the following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="f925d-440">In het vorige voorbeeld shard 1 wordt de geselecteerde shard maar `myKey` bevindt zich in de shard 0, zoals aangegeven door de `(shard 0)` gedeelte van het foutbericht.</span><span class="sxs-lookup"><span data-stu-id="f925d-440">In the previous example, shard 1 is the selected shard, but `myKey` is located in shard 0, as indicated by the `(shard 0)` portion of the error message.</span></span> <span data-ttu-id="f925d-441">In dit voorbeeld voor toegang tot `myKey`, selecteert u shard 0 met behulp van de shard-picker en voert u de gewenste opdracht.</span><span class="sxs-lookup"><span data-stu-id="f925d-441">In this example, to access `myKey`, select shard 0 using the shard picker, and then issue the desired command.</span></span>


## <a name="move-your-cache-to-a-new-subscription"></a><span data-ttu-id="f925d-442">Uw cache verplaatsen naar een nieuw abonnement</span><span class="sxs-lookup"><span data-stu-id="f925d-442">Move your cache to a new subscription</span></span>
<span data-ttu-id="f925d-443">U kunt uw cache verplaatsen naar een nieuw abonnement door te klikken op **verplaatsen**.</span><span class="sxs-lookup"><span data-stu-id="f925d-443">You can move your cache to a new subscription by clicking **Move**.</span></span>

![Verplaatsen van Redis-Cache](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="f925d-445">Zie voor meer informatie over het verplaatsen van resources uit één resourcegroep naar een andere, en één abonnement [resources verplaatsen naar de nieuwe resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f925d-445">For information on moving resources from one resource group to another, and from one subscription to another, see [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f925d-446">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f925d-446">Next steps</span></span>
* <span data-ttu-id="f925d-447">Zie voor meer informatie over het werken met Redis-opdrachten [hoe kan ik Redis-opdrachten uitvoeren?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="f925d-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

