---
title: aaaHow tooconfigure Azure Redis-Cache | Microsoft Docs
description: Hallo standaard Redis-configuratie voor Azure Redis-Cache begrijpen en meer informatie over hoe tooconfigure uw Azure Redis-Cache-exemplaren
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
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="b869e-103">Hoe tooconfigure Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="b869e-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="b869e-104">Dit onderwerp wordt beschreven hoe tooreview en update Hallo configuratie voor uw Azure Redis-Cache-exemplaren en dekt Hallo Redis server standaardconfiguratie voor Azure Redis-Cache-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="b869e-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="b869e-105">Zie voor meer informatie over het configureren en het gebruik van Premiumfuncties cache [hoe tooconfigure persistentie](cache-how-to-premium-persistence.md), [hoe tooconfigure clustering](cache-how-to-premium-clustering.md), en [hoe tooconfigure virtueel netwerk ondersteunen ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="b869e-106">Redis-cache-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="b869e-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="b869e-107">Azure Redis-Cache-instellingen worden weergegeven en geconfigureerd op Hallo **Redis-Cache** blade via Hallo **Resource Menu**.</span><span class="sxs-lookup"><span data-stu-id="b869e-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Redis-Cache-instellingen](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="b869e-109">U kunt bekijken en configureren van Hallo-instellingen met Hallo na **Resource Menu**.</span><span class="sxs-lookup"><span data-stu-id="b869e-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="b869e-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b869e-110">Overview</span></span>](#overview)
* [<span data-ttu-id="b869e-111">Activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="b869e-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="b869e-112">Toegangsbeheer (IAM)</span><span class="sxs-lookup"><span data-stu-id="b869e-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="b869e-113">Tags</span><span class="sxs-lookup"><span data-stu-id="b869e-113">Tags</span></span>](#tags)
* [<span data-ttu-id="b869e-114">Problemen vaststellen en oplossen</span><span class="sxs-lookup"><span data-stu-id="b869e-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="b869e-115">Instellingen</span><span class="sxs-lookup"><span data-stu-id="b869e-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="b869e-116">Toegangstoetsen</span><span class="sxs-lookup"><span data-stu-id="b869e-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="b869e-117">Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="b869e-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="b869e-118">Redis-Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="b869e-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="b869e-119">Schalen</span><span class="sxs-lookup"><span data-stu-id="b869e-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="b869e-120">Clustergrootte redis</span><span class="sxs-lookup"><span data-stu-id="b869e-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="b869e-121">Redis-gegevenspersistentie</span><span class="sxs-lookup"><span data-stu-id="b869e-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="b869e-122">Updates plannen</span><span class="sxs-lookup"><span data-stu-id="b869e-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="b869e-123">Geo-replicatie</span><span class="sxs-lookup"><span data-stu-id="b869e-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="b869e-124">Virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="b869e-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="b869e-125">Firewall</span><span class="sxs-lookup"><span data-stu-id="b869e-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="b869e-126">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b869e-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="b869e-127">Hiermee vergrendelt u</span><span class="sxs-lookup"><span data-stu-id="b869e-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="b869e-128">Automatiseringsscript</span><span class="sxs-lookup"><span data-stu-id="b869e-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="b869e-129">Beheer</span><span class="sxs-lookup"><span data-stu-id="b869e-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="b869e-130">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="b869e-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="b869e-131">Gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="b869e-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="b869e-132">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="b869e-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="b869e-133">Bewaking</span><span class="sxs-lookup"><span data-stu-id="b869e-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="b869e-134">Metrische gegevens redis</span><span class="sxs-lookup"><span data-stu-id="b869e-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="b869e-135">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="b869e-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="b869e-136">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="b869e-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="b869e-137">Ondersteuning en probleemoplossing van instellingen</span><span class="sxs-lookup"><span data-stu-id="b869e-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="b869e-138">Resourcestatus</span><span class="sxs-lookup"><span data-stu-id="b869e-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="b869e-139">Nieuw ondersteuningsverzoek</span><span class="sxs-lookup"><span data-stu-id="b869e-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="b869e-140">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b869e-140">Overview</span></span>

<span data-ttu-id="b869e-141">**Overzicht** biedt u basisinformatie over uw cache, zoals naam, poort, prijscategorie, en geselecteerde cache metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="b869e-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="b869e-142">Activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="b869e-142">Activity log</span></span>

<span data-ttu-id="b869e-143">Klik op **activiteitenlogboek** tooview acties uitgevoerd op uw cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="b869e-144">U kunt ook filteren tooexpand deze weergave tooinclude andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="b869e-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="b869e-145">Zie voor meer informatie over het werken met controlelogboeken [bewerkingen met Resource Manager controleren](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="b869e-146">Zie voor meer informatie over het controleren van gebeurtenissen van Azure Redis-Cache [bewerkingen en waarschuwingen](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="b869e-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="b869e-147">Toegangsbeheer (IAM)</span><span class="sxs-lookup"><span data-stu-id="b869e-147">Access control (IAM)</span></span>

<span data-ttu-id="b869e-148">Hallo **toegangsbeheer (IAM)** sectie biedt ondersteuning voor op rollen gebaseerde toegangsbeheer (RBAC) in hello Azure portal toohelp organisaties voldoen aan de beheervereisten toegang eenvoudig en nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="b869e-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="b869e-149">Zie voor meer informatie [toegangsbeheer op basis van rollen in hello Azure-portal](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="b869e-150">Tags</span><span class="sxs-lookup"><span data-stu-id="b869e-150">Tags</span></span>

<span data-ttu-id="b869e-151">Hallo **labels** sectie helpt u bij uw resources te organiseren.</span><span class="sxs-lookup"><span data-stu-id="b869e-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="b869e-152">Zie voor meer informatie [Using tags tooorganize uw Azure-resources](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="b869e-153">Problemen vaststellen en oplossen</span><span class="sxs-lookup"><span data-stu-id="b869e-153">Diagnose and solve problems</span></span>

<span data-ttu-id="b869e-154">Klik op **diagnosticeren en oplossen van problemen** toobe veelvoorkomende problemen en strategieën voor het oplossen van deze voorzien.</span><span class="sxs-lookup"><span data-stu-id="b869e-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="b869e-155">Instellingen</span><span class="sxs-lookup"><span data-stu-id="b869e-155">Settings</span></span>
<span data-ttu-id="b869e-156">Hallo **instellingen** sectie kunt u tooaccess en configureren van instellingen voor uw cache te volgen Hallo.</span><span class="sxs-lookup"><span data-stu-id="b869e-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="b869e-157">Toegangstoetsen</span><span class="sxs-lookup"><span data-stu-id="b869e-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="b869e-158">Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="b869e-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="b869e-159">Redis-Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="b869e-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="b869e-160">Schalen</span><span class="sxs-lookup"><span data-stu-id="b869e-160">Scale</span></span>](#scale)
* [<span data-ttu-id="b869e-161">Clustergrootte redis</span><span class="sxs-lookup"><span data-stu-id="b869e-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="b869e-162">Redis-gegevenspersistentie</span><span class="sxs-lookup"><span data-stu-id="b869e-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="b869e-163">Updates plannen</span><span class="sxs-lookup"><span data-stu-id="b869e-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="b869e-164">Geo-replicatie</span><span class="sxs-lookup"><span data-stu-id="b869e-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="b869e-165">Virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="b869e-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="b869e-166">Firewall</span><span class="sxs-lookup"><span data-stu-id="b869e-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="b869e-167">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b869e-167">Properties</span></span>](#properties)
* [<span data-ttu-id="b869e-168">Hiermee vergrendelt u</span><span class="sxs-lookup"><span data-stu-id="b869e-168">Locks</span></span>](#locks)
* [<span data-ttu-id="b869e-169">Automatiseringsscript</span><span class="sxs-lookup"><span data-stu-id="b869e-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="b869e-170">Toegangssleutels</span><span class="sxs-lookup"><span data-stu-id="b869e-170">Access keys</span></span>
<span data-ttu-id="b869e-171">Klik op **toegangssleutels** tooview of opnieuw genereren Hallo toegangssleutels voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="b869e-172">Deze sleutels worden gebruikt door het Hallo-clients verbinding maken met tooyour cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Redis-Cache toegangstoetsen](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="b869e-174">Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="b869e-174">Advanced settings</span></span>
<span data-ttu-id="b869e-175">Hallo volgende instellingen zijn geconfigureerd op Hallo **geavanceerde instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="b869e-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="b869e-176">-Poorten</span><span class="sxs-lookup"><span data-stu-id="b869e-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="b869e-177">Geheugen-beleid</span><span class="sxs-lookup"><span data-stu-id="b869e-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="b869e-178">Met Keyspace-kennisgevingen (geavanceerde instellingen)</span><span class="sxs-lookup"><span data-stu-id="b869e-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="b869e-179">-Poorten</span><span class="sxs-lookup"><span data-stu-id="b869e-179">Access Ports</span></span>
<span data-ttu-id="b869e-180">Voor nieuwe caches is niet-SSL-toegang standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b869e-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="b869e-181">tooenable Hallo niet-SSL-poort, klikt u op **Nee** voor **toestaan alleen toegang met SSL** op Hallo **geavanceerde instellingen** blade en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b869e-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Redis-Cache-poorten](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="b869e-183">Geheugen-beleid</span><span class="sxs-lookup"><span data-stu-id="b869e-183">Memory policies</span></span>
<span data-ttu-id="b869e-184">Hallo **Maxmemory beleid**, **maxmemory gereserveerd**, en **maxfragmentationmemory gereserveerd** instellingen op Hallo **geavanceerde instellingen**blade Hallo geheugen beleid voor Hallo-cache configureren.</span><span class="sxs-lookup"><span data-stu-id="b869e-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Redis-Cache Maxmemory beleid](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="b869e-186">**Beleid voor Maxmemory** hello taakverwijdering beleid voor Hallo cache configureert en kunt u toochoose van Hallo na verwijdering beleid:</span><span class="sxs-lookup"><span data-stu-id="b869e-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="b869e-187">`volatile-lru`-Dit is de standaardinstelling Hallo.</span><span class="sxs-lookup"><span data-stu-id="b869e-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="b869e-188">Voor meer informatie over `maxmemory` beleid, Zie [Taakverwijdering beleid](http://redis.io/topics/lru-cache#eviction-policies).</span><span class="sxs-lookup"><span data-stu-id="b869e-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="b869e-189">Hallo **maxmemory gereserveerd** instelling configureert u het Hallo hoeveelheid geheugen in MB die is gereserveerd voor niet-cache-bewerkingen zoals replicatie tijdens failover.</span><span class="sxs-lookup"><span data-stu-id="b869e-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="b869e-190">Als u deze waarde kunt u toohave een consistente gebruikerservaring voor Redis-server als de belasting van uw varieert.</span><span class="sxs-lookup"><span data-stu-id="b869e-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="b869e-191">Deze waarde moet worden ingesteld voor de werkbelastingen die zijn geschreven zware hoger.</span><span class="sxs-lookup"><span data-stu-id="b869e-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="b869e-192">Wanneer het geheugen is gereserveerd voor dergelijke bewerkingen, is het niet beschikbaar voor de opslag van gegevens in de cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="b869e-193">Hallo **maxfragmentationmemory gereserveerd** instelling Hallo hoeveelheid geheugen in MB die is gereserveerd tooaccommodate voor geheugenfragmentatie configureert.</span><span class="sxs-lookup"><span data-stu-id="b869e-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="b869e-194">Als u deze waarde kunt u toohave een consistente gebruikerservaring voor Redis-server wanneer Hallo cache vol is of sluiten toofull en Hallo fragmentatie verhouding ook hoog is.</span><span class="sxs-lookup"><span data-stu-id="b869e-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="b869e-195">Wanneer het geheugen is gereserveerd voor dergelijke bewerkingen, is het niet beschikbaar voor de opslag van gegevens in de cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="b869e-196">Één ding tooconsider bij het kiezen van een nieuwe waarde voor geheugen reservering (**maxmemory gereserveerd** of **maxfragmentationmemory gereserveerd**) is hoe deze wijziging van invloed kan zijn op een cache die al wordt uitgevoerd met grote hoeveelheden gegevens.</span><span class="sxs-lookup"><span data-stu-id="b869e-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="b869e-197">Als u een cache 53 GB met 49 GB aan gegevens vervolgens Hallo reservering waarde too8 GB wijzigen, wordt dit voor het exemplaar Hallo maximale geheugen beschikbaar voor Hallo system omlaag too45 GB verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b869e-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="b869e-198">Als uw huidige `used_memory` of uw `used_memory_rss` waarden hoger zijn dan de nieuwe limiet Hallo van 45 GB en vervolgens system Hallo tooevict gegevens hebben tot beide `used_memory` en `used_memory_rss` hieronder 45 GB zijn.</span><span class="sxs-lookup"><span data-stu-id="b869e-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="b869e-199">Verwijderen kan de fragmentatie van de belasting en geheugen van de server te verhogen.</span><span class="sxs-lookup"><span data-stu-id="b869e-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="b869e-200">Voor meer informatie over metrische gegevens cache zoals `used_memory` en `used_memory_rss`, Zie [beschikbare metrische gegevens en de rapportage van intervallen](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="b869e-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b869e-201">Hallo **maxmemory gereserveerd** en **maxfragmentationmemory gereserveerd** instellingen zijn alleen beschikbaar voor Standard en Premium in cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b869e-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="b869e-202">Met Keyspace-kennisgevingen (geavanceerde instellingen)</span><span class="sxs-lookup"><span data-stu-id="b869e-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="b869e-203">Meldingen zijn geconfigureerd op Hallo keyspace redis **geavanceerde instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="b869e-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="b869e-204">Keyspace-kennisgevingen kunnen clients meldingen tooreceive wanneer bepaalde gebeurtenissen optreden.</span><span class="sxs-lookup"><span data-stu-id="b869e-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Redis-Cache geavanceerde instellingen](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="b869e-206">Met Keyspace meldingen en Hallo **melden keyspace gebeurtenissen** instelling zijn alleen beschikbaar voor Standard en Premium-caches.</span><span class="sxs-lookup"><span data-stu-id="b869e-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="b869e-207">Zie voor meer informatie [Keyspace-kennisgevingen Redis](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="b869e-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="b869e-208">Zie voor voorbeeldcode Hallo [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) bestand in Hallo [Hallo wereld](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b869e-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="b869e-209">Redis-Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="b869e-209">Redis Cache Advisor</span></span>
<span data-ttu-id="b869e-210">Hallo **Redis-Cache Advisor** blade geeft aanbevelingen voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="b869e-211">Tijdens normale bewerkingen worden geen aanbevelingen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b869e-211">During normal operations, no recommendations are displayed.</span></span> 

![Aanbevelingen](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="b869e-213">Als alle voorwaarden wordt voldaan tijdens het Hallo-bewerkingen van uw cache zoals hoog geheugengebruik, netwerkbandbreedte of belasting van de server, een waarschuwing wordt weergegeven op Hallo **Redis-Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="b869e-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![Aanbevelingen](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="b869e-215">Meer informatie vindt u op Hallo **aanbevelingen** blade.</span><span class="sxs-lookup"><span data-stu-id="b869e-215">Further information can be found on hello **Recommendations** blade.</span></span>

![Aanbevelingen](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="b869e-217">Kunt u deze metrische gegevens op Hallo bewaken [grafieken bewaking](cache-how-to-monitor.md#monitoring-charts) en [gebruik grafieken](cache-how-to-monitor.md#usage-charts) secties Hallo **Redis-Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="b869e-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="b869e-218">Elke prijscategorie heeft verschillende beperkingen voor clientverbindingen, geheugen en bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="b869e-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="b869e-219">Als uw cache maximale capaciteit voor deze metrische gegevens gedurende een langere periode tijd nadert, wordt een aanbeveling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b869e-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="b869e-220">Voor meer informatie over Hallo metrische gegevens en limieten beoordeeld door Hallo **aanbevelingen** hulpprogramma, raadpleegt u Hallo volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="b869e-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="b869e-221">Redis-Cache metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="b869e-221">Redis Cache metric</span></span> | <span data-ttu-id="b869e-222">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="b869e-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="b869e-223">Gebruik van netwerkbandbreedte</span><span class="sxs-lookup"><span data-stu-id="b869e-223">Network bandwidth usage</span></span> |[<span data-ttu-id="b869e-224">Prestaties van de cache - bandbreedte</span><span class="sxs-lookup"><span data-stu-id="b869e-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="b869e-225">Verbonden clients</span><span class="sxs-lookup"><span data-stu-id="b869e-225">Connected clients</span></span> |[<span data-ttu-id="b869e-226">Standaard Redis-serverconfiguratie - maxclients</span><span class="sxs-lookup"><span data-stu-id="b869e-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="b869e-227">Belasting van de server</span><span class="sxs-lookup"><span data-stu-id="b869e-227">Server load</span></span> |[<span data-ttu-id="b869e-228">Gebruik grafieken - belasting van de Redis-Server</span><span class="sxs-lookup"><span data-stu-id="b869e-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="b869e-229">Geheugengebruik</span><span class="sxs-lookup"><span data-stu-id="b869e-229">Memory usage</span></span> |[<span data-ttu-id="b869e-230">Prestaties van de cache - grootte</span><span class="sxs-lookup"><span data-stu-id="b869e-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="b869e-231">tooupgrade uw cache, klikt u op **nu bijwerken** toochange Hallo prijscategorie en [scale](#scale) uw cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="b869e-232">Zie voor meer informatie over het kiezen van een prijscategorie [welke aanbieding Redis-Cache en de grootte moet ik gebruiken?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="b869e-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="b869e-233">Schalen</span><span class="sxs-lookup"><span data-stu-id="b869e-233">Scale</span></span>
<span data-ttu-id="b869e-234">Klik op **Scale** tooview of wijzig Hallo prijscategorie voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="b869e-235">Zie voor meer informatie over het schalen [hoe tooScale Azure Redis-Cache](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Redis-Cache prijscategorie](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="b869e-237">Clustergrootte redis</span><span class="sxs-lookup"><span data-stu-id="b869e-237">Redis Cluster Size</span></span>
<span data-ttu-id="b869e-238">Klik op **(PREVIEW) Redis clustergrootte** toochange Hallo clustergrootte voor een actieve premium in de cache met clustering is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b869e-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="b869e-239">Denk eraan dat bij hello Azure Redis-Cache Premium laag is vrijgegeven tooGeneral beschikbaarheid, Hallo clustergrootte Redis-functie is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="b869e-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Clustergrootte redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="b869e-241">Hallo clustergrootte toochange gebruik Hallo schuifregelaar of typ een getal tussen 1 en 10 in Hallo **Shard aantal** tekstvak en klik op **OK** toosave.</span><span class="sxs-lookup"><span data-stu-id="b869e-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b869e-242">Redis clustering is alleen beschikbaar voor Premium-caches.</span><span class="sxs-lookup"><span data-stu-id="b869e-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="b869e-243">Zie voor meer informatie [hoe tooconfigure clustering voor een Premium Azure Redis-Cache](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="b869e-244">Redis-gegevenspersistentie</span><span class="sxs-lookup"><span data-stu-id="b869e-244">Redis data persistence</span></span>
<span data-ttu-id="b869e-245">Klik op **Redis-gegevenspersistentie** tooenable, uitschakelen of gegevenspersistentie configureren voor uw cache premium.</span><span class="sxs-lookup"><span data-stu-id="b869e-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="b869e-246">Azure Redis-Cache met behulp van Redis-persistentie biedt [RDB persistentie](cache-how-to-premium-persistence.md#configure-rdb-persistence) of [AOF persistentie](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="b869e-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="b869e-247">Zie voor meer informatie [hoe tooconfigure persistentie voor een Premium Azure Redis-Cache](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="b869e-248">Redis-gegevenspersistentie is alleen beschikbaar voor Premium-caches.</span><span class="sxs-lookup"><span data-stu-id="b869e-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="b869e-249">Updates plannen</span><span class="sxs-lookup"><span data-stu-id="b869e-249">Schedule updates</span></span>
<span data-ttu-id="b869e-250">Hallo **updates plannen** blade kunt u een onderhoudsvenster voor Redis-serverupdates voor uw cache toodesignate.</span><span class="sxs-lookup"><span data-stu-id="b869e-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b869e-251">Hallo-onderhoudsvenster van toepassing is alleen tooRedis serverupdates en niet tooany Azure-updates of updates toohello besturingssysteem Hallo VM's die als host Hallo-cache fungeren.</span><span class="sxs-lookup"><span data-stu-id="b869e-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![Updates plannen](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="b869e-253">een onderhoudsvenster toospecify controleren Hallo gewenst dagen Hallo onderhoud-venster Beginuur voor elke dag opgeven, en klik **OK**.</span><span class="sxs-lookup"><span data-stu-id="b869e-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="b869e-254">Houd er rekening mee dat de duur van het onderhoudsvenster Hallo ingesteld op UTC is.</span><span class="sxs-lookup"><span data-stu-id="b869e-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b869e-255">Hallo **updates plannen** functionaliteit is alleen beschikbaar voor Premium-laag caches.</span><span class="sxs-lookup"><span data-stu-id="b869e-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="b869e-256">Zie voor meer informatie en instructies [beheer van Azure Redis-Cache - updates plannen](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="b869e-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="b869e-257">Geo-replicatie</span><span class="sxs-lookup"><span data-stu-id="b869e-257">Geo-replication</span></span>

<span data-ttu-id="b869e-258">Hallo **Geo-replicatie** blade biedt een mechanisme voor het koppelen van twee exemplaren van Premium-laag Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="b869e-259">Een cache is aangewezen als Hallo primaire gekoppelde cache en andere als secundaire gekoppelde cache Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b869e-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="b869e-260">Hallo secundaire gekoppelde cache wordt alleen-lezen en gegevens die zijn geschreven toohello primaire-cache is gerepliceerd toohello secundaire gekoppelde cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="b869e-261">Deze functionaliteit kan gebruikte tooreplicate een cache in Azure-regio's zijn.</span><span class="sxs-lookup"><span data-stu-id="b869e-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b869e-262">**Geo-replicatie** is alleen beschikbaar voor Premium-laag caches.</span><span class="sxs-lookup"><span data-stu-id="b869e-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="b869e-263">Zie voor meer informatie en instructies [hoe tooconfigure Geo-replicatie voor Azure Redis-Cache](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="b869e-264">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="b869e-264">Virtual Network</span></span>
<span data-ttu-id="b869e-265">Hallo **virtueel netwerk** sectie kunt u tooconfigure Hallo virtuele-netwerkinstellingen voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="b869e-266">Voor informatie over het maken van een premium-cache met VNET ondersteunen en bijwerken van de instellingen, Zie [hoe tooconfigure Virtual Network-ondersteuning voor een Premium Azure Redis-Cache](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b869e-267">Instellingen voor virtuele netwerken zijn alleen beschikbaar voor premium-caches die zijn geconfigureerd met ondersteuning voor VNET tijdens het maken van de cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="b869e-268">Firewall</span><span class="sxs-lookup"><span data-stu-id="b869e-268">Firewall</span></span>

<span data-ttu-id="b869e-269">Klik op **Firewall** tooview en firewallregels configureren voor uw Premium Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Firewall](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="b869e-271">U kunt firewallregels opgeven met een begin- en IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="b869e-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="b869e-272">Wanneer de firewallregels zijn geconfigureerd, wordt alleen clientverbindingen van Hallo opgegeven IP-adresbereiken verbinding kunnen maken van toohello cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="b869e-273">Wanneer een firewallregel wordt opgeslagen is er een korte vertraging optreden voordat het Hallo-regel is van kracht.</span><span class="sxs-lookup"><span data-stu-id="b869e-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="b869e-274">Dit uitstel is meestal minder dan een minuut.</span><span class="sxs-lookup"><span data-stu-id="b869e-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b869e-275">Verbindingen van Azure Redis-Cache bewaken altijd toegestaan, zelfs als de firewallregels zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b869e-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="b869e-276">Firewallregels zijn alleen beschikbaar voor Premium-laag caches.</span><span class="sxs-lookup"><span data-stu-id="b869e-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="b869e-277">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b869e-277">Properties</span></span>
<span data-ttu-id="b869e-278">Klik op **eigenschappen** tooview informatie over uw cache, waaronder Hallo cache-eindpunt en poorten.</span><span class="sxs-lookup"><span data-stu-id="b869e-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Redis-Cache-eigenschappen](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="b869e-280">Vergrendelingen</span><span class="sxs-lookup"><span data-stu-id="b869e-280">Locks</span></span>
<span data-ttu-id="b869e-281">Hallo **vergrendelt** sectie kunt u toolock een abonnement, resourcegroep of resource tooprevent andere gebruikers in uw organisatie per ongeluk worden kritieke bronnen wijzigen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b869e-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="b869e-282">Zie voor meer informatie [Resources vergrendelen met Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="b869e-283">Automatiseringsscript</span><span class="sxs-lookup"><span data-stu-id="b869e-283">Automation script</span></span>

<span data-ttu-id="b869e-284">Klik op **automatiseringsscript** toobuild en exporteren van een sjabloon van uw geïmplementeerde resources voor toekomstige implementaties.</span><span class="sxs-lookup"><span data-stu-id="b869e-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="b869e-285">Zie voor meer informatie over het werken met sjablonen [implementeren van resources met Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="b869e-286">Instellingen voor beheer</span><span class="sxs-lookup"><span data-stu-id="b869e-286">Administration settings</span></span>
<span data-ttu-id="b869e-287">Hallo-instellingen in Hallo **beheer** sectie kunt u tooperform Hallo beheertaken voor uw cache te volgen.</span><span class="sxs-lookup"><span data-stu-id="b869e-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![Beheer](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="b869e-289">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="b869e-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="b869e-290">Gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="b869e-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="b869e-291">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="b869e-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="b869e-292">Import/Export</span><span class="sxs-lookup"><span data-stu-id="b869e-292">Import/Export</span></span>
<span data-ttu-id="b869e-293">Import/Export is een Azure Redis-Cache gegevensbewerking voor het beheer, zodat u tooimport en exporteren van gegevens in cache van Hallo door te importeren en exporteren van een momentopname van een Redis-Cache Database (RDB) van een premium cache tooa pagina-blob in Azure Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="b869e-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="b869e-294">Voor importeren/exporteren kunt u toomigrate tussen verschillende exemplaren van Azure Redis-Cache of vullen Hallo cache met gegevens voor het gebruik.</span><span class="sxs-lookup"><span data-stu-id="b869e-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="b869e-295">Importeren kan gebruikte toobring Redis compatibele RDB bestanden vanaf een willekeurige Redis-server uitgevoerd in een cloud of de omgeving, inclusief Redis uitgevoerd op Linux, Windows of elke cloudprovider zoals Amazon Web Services en andere zijn.</span><span class="sxs-lookup"><span data-stu-id="b869e-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="b869e-296">Het importeren van gegevens is een eenvoudige manier toocreate een cache met vooraf ingestelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="b869e-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="b869e-297">Tijdens het importproces hello, Azure Redis-Cache Hallo RDB bestanden uit Azure storage in het geheugen geladen en Hallo sleutels wordt ingevoegd in de cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="b869e-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="b869e-298">Exporteren kunt u tooexport Hallo opgeslagen gegevens in Azure Redis-Cache tooRedis compatibele RDB bestanden.</span><span class="sxs-lookup"><span data-stu-id="b869e-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="b869e-299">U kunt deze functie toomove op gegevens uit een Azure Redis-Cache-exemplaar tooanother of tooanother Redis-server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b869e-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="b869e-300">Tijdens het exportproces hello, wordt een tijdelijk bestand op Hallo VM dat hosts Hallo server-exemplaar van Azure Redis-Cache en Hallo bestand geüploade toohello aangewezen storage-account is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b869e-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="b869e-301">Wanneer de exportbewerking Hallo is voltooid met de status van slagen of mislukken, wordt Hallo tijdelijk bestand verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b869e-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b869e-302">Import/Export is alleen beschikbaar voor Premium-laag caches.</span><span class="sxs-lookup"><span data-stu-id="b869e-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="b869e-303">Zie voor meer informatie en instructies [importeren en exporteren van gegevens in Azure Redis-Cache](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="b869e-304">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="b869e-304">Reboot</span></span>
<span data-ttu-id="b869e-305">Hallo **opnieuw opstarten** blade kunt u tooreboot Hallo knooppunten van de cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="b869e-306">Deze mogelijkheid opnieuw opstarten kan tootest u uw toepassing voor tolerantie als er een storing van een cacheknooppunt.</span><span class="sxs-lookup"><span data-stu-id="b869e-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Opnieuw opstarten](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="b869e-308">Als u een premium-cache hebt met clusteren is ingeschakeld, kunt u selecteren welke shards van Hallo cache tooreboot.</span><span class="sxs-lookup"><span data-stu-id="b869e-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Opnieuw opstarten](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="b869e-310">tooreboot een of meer knooppunten van de cache Hallo gewenst knooppunten te selecteren en klik op **opnieuw opstarten**.</span><span class="sxs-lookup"><span data-stu-id="b869e-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="b869e-311">Als u een premium-cache hebt met clustering is ingeschakeld, Hallo shard(s) tooreboot selecteren en klik vervolgens op **opnieuw opstarten**.</span><span class="sxs-lookup"><span data-stu-id="b869e-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="b869e-312">Hallo geselecteerde knooppunt opnieuw opstarten na een paar minuten en weer online zijn een paar minuten later.</span><span class="sxs-lookup"><span data-stu-id="b869e-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b869e-313">Opnieuw opstarten is nu beschikbaar voor alle Prijscategorieën.</span><span class="sxs-lookup"><span data-stu-id="b869e-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="b869e-314">Zie voor meer informatie en instructies [beheer van Azure Redis-Cache - opnieuw opstarten](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="b869e-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="b869e-315">Bewaking</span><span class="sxs-lookup"><span data-stu-id="b869e-315">Monitoring</span></span>

<span data-ttu-id="b869e-316">Hallo **bewaking** sectie kunt u tooconfigure diagnostische gegevens en de bewaking van uw Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="b869e-317">Zie voor meer informatie over het controleren van Azure Redis-Cache en diagnostische gegevens [hoe toomonitor Azure Redis-Cache](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnostiek](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="b869e-319">Metrische gegevens redis</span><span class="sxs-lookup"><span data-stu-id="b869e-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="b869e-320">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="b869e-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="b869e-321">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="b869e-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="b869e-322">Metrische gegevens redis</span><span class="sxs-lookup"><span data-stu-id="b869e-322">Redis metrics</span></span>
<span data-ttu-id="b869e-323">Klik op **Redis metrische gegevens** te[metrische gegevens weergeven](cache-how-to-monitor.md#view-cache-metrics) voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="b869e-324">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="b869e-324">Alert rules</span></span>

<span data-ttu-id="b869e-325">Klik op **waarschuwing regels** tooconfigure waarschuwingen op basis van Redis-Cache metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="b869e-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="b869e-326">Zie voor meer informatie [waarschuwingen](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="b869e-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="b869e-327">Diagnostiek</span><span class="sxs-lookup"><span data-stu-id="b869e-327">Diagnostics</span></span>

<span data-ttu-id="b869e-328">Cache metrische gegevens in de Azure-Monitor zijn standaard [30 dagen bewaard](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) en vervolgens verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b869e-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="b869e-329">toopersist metrische gegevens van uw cache langer dan 30 dagen, klikt u op **Diagnostics** te[opslagaccount Hallo configureren](cache-how-to-monitor.md#export-cache-metrics) toostore cache diagnostische gegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b869e-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="b869e-330">In aanvulling tooarchiving uw cache metrische gegevens toostorage, kunt u ook [stream ze tooan Event hub of verzend deze tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="b869e-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="b869e-331">Ondersteuning en probleemoplossing van instellingen</span><span class="sxs-lookup"><span data-stu-id="b869e-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="b869e-332">Hallo-instellingen in Hallo **ondersteuning + probleemoplossing** sectie bieden u opties voor het oplossen van problemen met uw cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Ondersteuning + probleemoplossing](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="b869e-334">Resourcestatus</span><span class="sxs-lookup"><span data-stu-id="b869e-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="b869e-335">Nieuw ondersteuningsverzoek</span><span class="sxs-lookup"><span data-stu-id="b869e-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="b869e-336">Status van resources</span><span class="sxs-lookup"><span data-stu-id="b869e-336">Resource health</span></span>
<span data-ttu-id="b869e-337">**Resourcestatus** controleert uw resource en geeft u aan als deze wordt uitgevoerd zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="b869e-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="b869e-338">Zie voor meer informatie over health-service van Azure Resource Hallo [overzicht van Azure Resource health](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b869e-339">De resourcestatus is momenteel niet mogelijk tooreport Hallo gezondheid van Azure Redis-Cache-exemplaren die worden gehost in een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="b869e-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="b869e-340">Zie voor meer informatie [alle functies van de cache werken bij het hosten van een cache in een VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="b869e-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="b869e-341">Nieuw ondersteuningsverzoek</span><span class="sxs-lookup"><span data-stu-id="b869e-341">New support request</span></span>
<span data-ttu-id="b869e-342">Klik op **nieuw ondersteuningsverzoek** tooopen ondersteuning aan te vragen voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="b869e-343">Standaardconfiguratie van het Redis-server</span><span class="sxs-lookup"><span data-stu-id="b869e-343">Default Redis server configuration</span></span>
<span data-ttu-id="b869e-344">Nieuwe exemplaren van Azure Redis-Cache zijn geconfigureerd met Hallo standaardwaarden van het Redis-configuratie te volgen.</span><span class="sxs-lookup"><span data-stu-id="b869e-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="b869e-345">Hallo-instellingen in deze sectie kunnen niet worden gewijzigd met Hallo `StackExchange.Redis.IServer.ConfigSet` methode.</span><span class="sxs-lookup"><span data-stu-id="b869e-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="b869e-346">Als deze methode is aangeroepen met een van de opdrachten in deze sectie hello, wordt een uitzondering vergelijkbare toohello volgende gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="b869e-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="b869e-347">Alle waarden die kunnen worden geconfigureerd, zoals **max-geheugen-policy**, kunnen worden geconfigureerd via hello Azure-portal of beheer via de opdrachtregel-hulpprogramma's zoals Azure CLI of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b869e-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="b869e-348">Instelling</span><span class="sxs-lookup"><span data-stu-id="b869e-348">Setting</span></span> | <span data-ttu-id="b869e-349">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="b869e-349">Default value</span></span> | <span data-ttu-id="b869e-350">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b869e-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="b869e-351">16</span><span class="sxs-lookup"><span data-stu-id="b869e-351">16</span></span> |<span data-ttu-id="b869e-352">Hallo standaardaantal databases dat is 16 maar u kunt een ander nummer op basis van Hallo prijscategorie configureren. <sup>1</sup> Hallo standaarddatabase DB 0 is, kunt u een andere naam op een afzonderlijke verbinding basis met `connection.GetDatabase(dbid)` waar `dbid` is een getal tussen `0` en `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="b869e-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="b869e-353">Afhankelijk van Hallo prijscategorie<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="b869e-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="b869e-354">Dit is Hallo kunt u het maximum aantal verbonden clients toegestaan op Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="b869e-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="b869e-355">Zodra Hallo limiet is bereikt Redis Hiermee sluit u alle Hallo nieuwe verbindingen, een 'max. aantal clients bereikt'-fout.</span><span class="sxs-lookup"><span data-stu-id="b869e-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="b869e-356">Maxmemory beleid is Hallo-instelling voor hoe Redis welke tooremove geselecteerd wanneer `maxmemory` (grootte van Hallo cache bieden u geselecteerd tijdens het maken van de cache Hallo Hallo) is bereikt.</span><span class="sxs-lookup"><span data-stu-id="b869e-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="b869e-357">Met Azure Redis-Cache Hallo standaard instelling is `volatile-lru`, waarbij Hallo sleutels worden verwijderd met een vervaldatum instellen met behulp van een LRU-algoritme.</span><span class="sxs-lookup"><span data-stu-id="b869e-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="b869e-358">Deze instelling kan worden geconfigureerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b869e-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="b869e-359">Zie voor meer informatie [geheugen beleid](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="b869e-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="b869e-360">3</span><span class="sxs-lookup"><span data-stu-id="b869e-360">3</span></span> |<span data-ttu-id="b869e-361">toosave geheugen, LRU en minimale TTL-algoritmes zijn redelijk algoritmen in plaats van nauwkeurige algoritmen.</span><span class="sxs-lookup"><span data-stu-id="b869e-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="b869e-362">Standaard Redis controles drie sleutels en uitgelicht Hallo een die minder recent is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b869e-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="b869e-363">5,000</span><span class="sxs-lookup"><span data-stu-id="b869e-363">5,000</span></span> |<span data-ttu-id="b869e-364">Maximale uitvoeringstijd van een script Lua in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="b869e-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="b869e-365">Als de maximale uitvoeringstijd Hallo is bereikt, registreert Redis dat een script nog steeds uitgevoerd na Hallo maximale toegestane tijd wordt en tooreply tooqueries met een fout opgetreden begint.</span><span class="sxs-lookup"><span data-stu-id="b869e-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="b869e-366">500</span><span class="sxs-lookup"><span data-stu-id="b869e-366">500</span></span> |<span data-ttu-id="b869e-367">Maximale grootte van de wachtrij script.</span><span class="sxs-lookup"><span data-stu-id="b869e-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="b869e-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="b869e-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="b869e-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="b869e-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="b869e-370">Hallo client uitvoer buffer kan worden beperkt tooforce verbreken van clients die niet van gegevens van Hallo server snel genoeg voor een bepaalde reden lezen zijn (een veelvoorkomende reden is dat een client Pub subitems snel Hallo publisher kan ze produceren berichten kan niet gebruiken) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b869e-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="b869e-371">Zie voor meer informatie [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="b869e-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="b869e-372"><a name="databases"></a>
<sup>1</sup>Hallo limiet voor `databases` verschilt voor elk Azure Redis-Cache prijscategorie en kan worden ingesteld bij het maken van de cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="b869e-373">Als er geen `databases` instelling is opgegeven tijdens het maken van de cache Hallo standaardwaarde is 16.</span><span class="sxs-lookup"><span data-stu-id="b869e-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="b869e-374">Basic en Standard caches</span><span class="sxs-lookup"><span data-stu-id="b869e-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="b869e-375">C0 (250 MB)-cache - up van databases too16</span><span class="sxs-lookup"><span data-stu-id="b869e-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="b869e-376">C1 (1 GB)-cache - up van databases too16</span><span class="sxs-lookup"><span data-stu-id="b869e-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="b869e-377">C2 (2,5 GB)-cache - up van databases too16</span><span class="sxs-lookup"><span data-stu-id="b869e-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="b869e-378">C3 (6 GB)-cache - up van databases too16</span><span class="sxs-lookup"><span data-stu-id="b869e-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="b869e-379">C4 (13 GB)-cache - up van databases too32</span><span class="sxs-lookup"><span data-stu-id="b869e-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="b869e-380">C5 (26 GB)-cache - up van databases too48</span><span class="sxs-lookup"><span data-stu-id="b869e-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="b869e-381">C6 (53 GB)-cache - up van databases too64</span><span class="sxs-lookup"><span data-stu-id="b869e-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="b869e-382">Premium-caches</span><span class="sxs-lookup"><span data-stu-id="b869e-382">Premium caches</span></span>
  * <span data-ttu-id="b869e-383">P1 (6 GB - 60 GB) van de too16-databases</span><span class="sxs-lookup"><span data-stu-id="b869e-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="b869e-384">P2 (13 GB - 130 GB) van de too32-databases</span><span class="sxs-lookup"><span data-stu-id="b869e-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="b869e-385">P3 (26 GB - 260 GB) van de too48-databases</span><span class="sxs-lookup"><span data-stu-id="b869e-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="b869e-386">P4 (53 GB - 530 GB) van de too64-databases</span><span class="sxs-lookup"><span data-stu-id="b869e-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="b869e-387">Alle premium caches met Redis-cluster ingeschakeld - Redis-cluster ondersteunt alleen gebruik van database 0 dus Hallo `databases` limiet voor elke premium-cache met Redis-cluster ingeschakeld is in feite 1 en Hallo [Selecteer](http://redis.io/commands/select) opdracht is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="b869e-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="b869e-388">Zie voor meer informatie [heb ik nodig toomake eventuele wijzigingen toomy client toepassing toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="b869e-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="b869e-389">Zie voor meer informatie over databases [wat Redis-databases zijn?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="b869e-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="b869e-390">Hallo `databases` instelling kan worden geconfigureerd tijdens de cache maken en alleen met behulp van PowerShell, CLI of andere clients management.</span><span class="sxs-lookup"><span data-stu-id="b869e-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="b869e-391">Voor een voorbeeld van de configuratie van `databases` tijdens het maken van de cache met behulp van PowerShell, Zie [nieuw AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="b869e-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="b869e-392"><a name="maxclients"></a>
<sup>2</sup> `maxclients` verschilt voor elk Azure Redis-Cache prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="b869e-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="b869e-393">Basic en Standard caches</span><span class="sxs-lookup"><span data-stu-id="b869e-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="b869e-394">C0 (250 MB)-cache - too256 verbindingen configureren</span><span class="sxs-lookup"><span data-stu-id="b869e-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="b869e-395">C1 (1 GB)-cache - up too1, 000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="b869e-396">C2 (2,5 GB)-cache - up too2, 000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="b869e-397">C3 (6 GB)-cache - up too5, 000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="b869e-398">C4 (13 GB)-cache - up too10, 000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="b869e-399">C5 (26 GB)-cache - up too15, 000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="b869e-400">C6 (53 GB)-cache - up too20, 000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="b869e-401">Premium-caches</span><span class="sxs-lookup"><span data-stu-id="b869e-401">Premium caches</span></span>
  * <span data-ttu-id="b869e-402">P1 (6 GB - 60 GB) - up too7, 500-verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="b869e-403">P2 (13 GB - 130 GB) - up too15, 000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="b869e-404">P3 (26 GB - 260 GB) - up too30, 000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="b869e-405">P4 (53 GB - 530 GB) - up too40, 000 verbindingen</span><span class="sxs-lookup"><span data-stu-id="b869e-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="b869e-406">Kunt u elke grootte van cache *tot* een bepaald aantal verbindingen, elke tooRedis verbinding heeft de overhead gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="b869e-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="b869e-407">Een voorbeeld van een dergelijke overhead zou zijn CPU- en geheugengebruik als gevolg van TLS/SSL-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="b869e-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="b869e-408">Hallo maximale verbindingslimiet voor een opgegeven cachegrootte wordt ervan uitgegaan dat een licht geladen cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="b869e-409">Als uit verbinding overhead laden *plus* laden vanaf de clientbewerkingen dan er capaciteit voor Hallo systeem, Hallo cache kunt capaciteitsproblemen moeten ondervinden zelfs als u hebt niet de verbindingslimiet Hallo voor de huidige cachegrootte Hallo overschreden.</span><span class="sxs-lookup"><span data-stu-id="b869e-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="b869e-410">Redis opdrachten niet ondersteund in Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="b869e-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b869e-411">Omdat de configuratie en beheer van exemplaren van Azure Redis-Cache wordt beheerd door Microsoft, zijn hello volgende opdrachten uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b869e-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="b869e-412">Als u tooinvoke probeert ze, verschijnt een foutbericht te`"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="b869e-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="b869e-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="b869e-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="b869e-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="b869e-414">BGSAVE</span></span>
> * <span data-ttu-id="b869e-415">CONFIGURATIE</span><span class="sxs-lookup"><span data-stu-id="b869e-415">CONFIG</span></span>
> * <span data-ttu-id="b869e-416">FOUTEN OPSPOREN</span><span class="sxs-lookup"><span data-stu-id="b869e-416">DEBUG</span></span>
> * <span data-ttu-id="b869e-417">MIGREREN</span><span class="sxs-lookup"><span data-stu-id="b869e-417">MIGRATE</span></span>
> * <span data-ttu-id="b869e-418">OPSLAAN</span><span class="sxs-lookup"><span data-stu-id="b869e-418">SAVE</span></span>
> * <span data-ttu-id="b869e-419">AFSLUITEN</span><span class="sxs-lookup"><span data-stu-id="b869e-419">SHUTDOWN</span></span>
> * <span data-ttu-id="b869e-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="b869e-420">SLAVEOF</span></span>
> * <span data-ttu-id="b869e-421">CLUSTER - schrijven zijn uitgeschakeld, maar alleen-lezen Cluster opdrachten zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="b869e-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="b869e-422">Zie voor meer informatie over Redis opdrachten [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="b869e-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="b869e-423">Redis-console</span><span class="sxs-lookup"><span data-stu-id="b869e-423">Redis console</span></span>
<span data-ttu-id="b869e-424">Kunt u veilig uitgeven opdrachten tooyour Azure Redis-Cache-exemplaren die gebruikmaken van Hallo **Redis-Console**, die beschikbaar is in hello Azure-portal voor alle cachelagen.</span><span class="sxs-lookup"><span data-stu-id="b869e-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="b869e-425">Hallo Redis-Console werkt niet met [VNET](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="b869e-426">Als uw cache deel van een VNET uitmaakt, toegang alleen clients in VNET Hallo Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="b869e-427">Omdat Redis-Console wordt uitgevoerd in uw lokale browser, die zich buiten de Hallo VNET, kunt deze cache tooyour kan geen verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="b869e-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="b869e-428">Niet alle Redis-opdrachten worden ondersteund in Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="b869e-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="b869e-429">Zie voor een lijst met Redis-opdrachten die zijn uitgeschakeld voor Azure Redis-Cache, Hallo vorige [Redis opdrachten niet ondersteund in Azure Redis-Cache](#redis-commands-not-supported-in-azure-redis-cache) sectie.</span><span class="sxs-lookup"><span data-stu-id="b869e-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="b869e-430">Zie voor meer informatie over Redis opdrachten [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="b869e-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="b869e-431">tooaccess hello Redis-Console klikt u op **Console** van Hallo **Redis-Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="b869e-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Redis-console](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="b869e-433">tooissue opdrachten op basis van uw cache-exemplaar, gewoon type Hallo gewenste opdracht in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="b869e-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Redis-console](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="b869e-435">Hallo met Redis-Console met een premium cache voor geclusterde</span><span class="sxs-lookup"><span data-stu-id="b869e-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="b869e-436">Wanneer met behulp van Hallo Redis-Console met een premium cache voor geclusterde, kunt u opdrachten tooa één shard van Hallo cache uitgeven.</span><span class="sxs-lookup"><span data-stu-id="b869e-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="b869e-437">een opdracht tooa specifieke shard, tooissue toohello gewenste shard wordt door erop te klikken op Hallo shard objectkiezer eerst verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="b869e-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Redis-console](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="b869e-439">Als u een sleutel die is opgeslagen in een andere shard probeert dan Hallo verbonden shard tooaccess, ontvangt u een fout bericht vergelijkbaar toohello volgende bericht.</span><span class="sxs-lookup"><span data-stu-id="b869e-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="b869e-440">In het vorige voorbeeld hello, is 1 shard Hallo geselecteerde shard, maar `myKey` bevindt zich in de shard 0, zoals aangegeven door Hallo `(shard 0)` gedeelte van het foutbericht Hallo.</span><span class="sxs-lookup"><span data-stu-id="b869e-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="b869e-441">In dit voorbeeld tooaccess `myKey`, selecteer met behulp van shard 0 Hallo shard objectkiezer en probleem Hallo gewenst opdracht.</span><span class="sxs-lookup"><span data-stu-id="b869e-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="b869e-442">Uw cache tooa nieuw abonnement verplaatsen</span><span class="sxs-lookup"><span data-stu-id="b869e-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="b869e-443">U kunt uw cache tooa nieuw abonnement verplaatsen door te klikken op **verplaatsen**.</span><span class="sxs-lookup"><span data-stu-id="b869e-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![Verplaatsen van Redis-Cache](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="b869e-445">Zie voor meer informatie over het verplaatsen van resources van één resource groep tooanother en van één abonnement tooanother [verplaatsen van resources toonew resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b869e-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b869e-446">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b869e-446">Next steps</span></span>
* <span data-ttu-id="b869e-447">Zie voor meer informatie over het werken met Redis-opdrachten [hoe kan ik Redis-opdrachten uitvoeren?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="b869e-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

