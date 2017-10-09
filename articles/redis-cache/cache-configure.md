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
# <a name="how-tooconfigure-azure-redis-cache"></a>Hoe tooconfigure Azure Redis-Cache
Dit onderwerp wordt beschreven hoe tooreview en update Hallo configuratie voor uw Azure Redis-Cache-exemplaren en dekt Hallo Redis server standaardconfiguratie voor Azure Redis-Cache-exemplaren.

> [!NOTE]
> Zie voor meer informatie over het configureren en het gebruik van Premiumfuncties cache [hoe tooconfigure persistentie](cache-how-to-premium-persistence.md), [hoe tooconfigure clustering](cache-how-to-premium-clustering.md), en [hoe tooconfigure virtueel netwerk ondersteunen ](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Redis-cache-instellingen configureren
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Azure Redis-Cache-instellingen worden weergegeven en geconfigureerd op Hallo **Redis-Cache** blade via Hallo **Resource Menu**.

![Redis-Cache-instellingen](./media/cache-configure/redis-cache-settings.png)

U kunt bekijken en configureren van Hallo-instellingen met Hallo na **Resource Menu**.

* [Overzicht](#overview)
* [Activiteitenlogboek](#activity-log)
* [Toegangsbeheer (IAM)](#access-control-iam)
* [Tags](#tags)
* [Problemen vaststellen en oplossen](#diagnose-and-solve-problems)
* [Instellingen](#settings)
    * [Toegangstoetsen](#access-keys)
    * [Geavanceerde instellingen](#advanced-settings)
    * [Redis-Cache Advisor](#redis-cache-advisor)
    * [Schalen](#scale)
    * [Clustergrootte redis](#cluster-size)
    * [Redis-gegevenspersistentie](#redis-data-persistence)
    * [Updates plannen](#schedule-updates)
    * [Geo-replicatie](#geo-replication)
    * [Virtueel netwerk](#virtual-network)
    * [Firewall](#firewall)
    * [Eigenschappen](#properties)
    * [Hiermee vergrendelt u](#locks)
    * [Automatiseringsscript](#automation-script)
* [Beheer](#administration)
    * [Gegevens importeren](#importexport)
    * [Gegevens exporteren](#importexport)
    * [Opnieuw opstarten](#reboot)
* [Bewaking](#monitoring)
    * [Metrische gegevens redis](#redis-metrics)
    * [Regels voor waarschuwingen](#alert-rules)
    * [Diagnostics](#diagnostics)
* [Ondersteuning en probleemoplossing van instellingen](#support-amp-troubleshooting-settings)
    * [Resourcestatus](#resource-health)
    * [Nieuw ondersteuningsverzoek](#new-support-request)


## <a name="overview"></a>Overzicht

**Overzicht** biedt u basisinformatie over uw cache, zoals naam, poort, prijscategorie, en geselecteerde cache metrische gegevens.

### <a name="activity-log"></a>Activiteitenlogboek

Klik op **activiteitenlogboek** tooview acties uitgevoerd op uw cache. U kunt ook filteren tooexpand deze weergave tooinclude andere bronnen. Zie voor meer informatie over het werken met controlelogboeken [bewerkingen met Resource Manager controleren](../azure-resource-manager/resource-group-audit.md). Zie voor meer informatie over het controleren van gebeurtenissen van Azure Redis-Cache [bewerkingen en waarschuwingen](cache-how-to-monitor.md#operations-and-alerts).

### <a name="access-control-iam"></a>Toegangsbeheer (IAM)

Hallo **toegangsbeheer (IAM)** sectie biedt ondersteuning voor op rollen gebaseerde toegangsbeheer (RBAC) in hello Azure portal toohelp organisaties voldoen aan de beheervereisten toegang eenvoudig en nauwkeurig. Zie voor meer informatie [toegangsbeheer op basis van rollen in hello Azure-portal](../active-directory/role-based-access-control-configure.md).

### <a name="tags"></a>Tags

Hallo **labels** sectie helpt u bij uw resources te organiseren. Zie voor meer informatie [Using tags tooorganize uw Azure-resources](../azure-resource-manager/resource-group-using-tags.md).


### <a name="diagnose-and-solve-problems"></a>Problemen vaststellen en oplossen

Klik op **diagnosticeren en oplossen van problemen** toobe veelvoorkomende problemen en strategieën voor het oplossen van deze voorzien.



## <a name="settings"></a>Instellingen
Hallo **instellingen** sectie kunt u tooaccess en configureren van instellingen voor uw cache te volgen Hallo.

* [Toegangstoetsen](#access-keys)
* [Geavanceerde instellingen](#advanced-settings)
* [Redis-Cache Advisor](#redis-cache-advisor)
* [Schalen](#scale)
* [Clustergrootte redis](#cluster-size)
* [Redis-gegevenspersistentie](#redis-data-persistence)
* [Updates plannen](#schedule-updates)
* [Geo-replicatie](#geo-replication)
* [Virtueel netwerk](#virtual-network)
* [Firewall](#firewall)
* [Eigenschappen](#properties)
* [Hiermee vergrendelt u](#locks)
* [Automatiseringsscript](#automation-script)



### <a name="access-keys"></a>Toegangssleutels
Klik op **toegangssleutels** tooview of opnieuw genereren Hallo toegangssleutels voor uw cache. Deze sleutels worden gebruikt door het Hallo-clients verbinding maken met tooyour cache.

![Redis-Cache toegangstoetsen](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>Geavanceerde instellingen
Hallo volgende instellingen zijn geconfigureerd op Hallo **geavanceerde instellingen** blade.

* [-Poorten](#access-ports)
* [Geheugen-beleid](#memory-policies)
* [Met Keyspace-kennisgevingen (geavanceerde instellingen)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>-Poorten
Voor nieuwe caches is niet-SSL-toegang standaard uitgeschakeld. tooenable Hallo niet-SSL-poort, klikt u op **Nee** voor **toestaan alleen toegang met SSL** op Hallo **geavanceerde instellingen** blade en klik vervolgens op **opslaan**.

![Redis-Cache-poorten](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>Geheugen-beleid
Hallo **Maxmemory beleid**, **maxmemory gereserveerd**, en **maxfragmentationmemory gereserveerd** instellingen op Hallo **geavanceerde instellingen**blade Hallo geheugen beleid voor Hallo-cache configureren.

![Redis-Cache Maxmemory beleid](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Beleid voor Maxmemory** hello taakverwijdering beleid voor Hallo cache configureert en kunt u toochoose van Hallo na verwijdering beleid:

* `volatile-lru`-Dit is de standaardinstelling Hallo.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

Voor meer informatie over `maxmemory` beleid, Zie [Taakverwijdering beleid](http://redis.io/topics/lru-cache#eviction-policies).

Hallo **maxmemory gereserveerd** instelling configureert u het Hallo hoeveelheid geheugen in MB die is gereserveerd voor niet-cache-bewerkingen zoals replicatie tijdens failover. Als u deze waarde kunt u toohave een consistente gebruikerservaring voor Redis-server als de belasting van uw varieert. Deze waarde moet worden ingesteld voor de werkbelastingen die zijn geschreven zware hoger. Wanneer het geheugen is gereserveerd voor dergelijke bewerkingen, is het niet beschikbaar voor de opslag van gegevens in de cache.

Hallo **maxfragmentationmemory gereserveerd** instelling Hallo hoeveelheid geheugen in MB die is gereserveerd tooaccommodate voor geheugenfragmentatie configureert. Als u deze waarde kunt u toohave een consistente gebruikerservaring voor Redis-server wanneer Hallo cache vol is of sluiten toofull en Hallo fragmentatie verhouding ook hoog is. Wanneer het geheugen is gereserveerd voor dergelijke bewerkingen, is het niet beschikbaar voor de opslag van gegevens in de cache.

Één ding tooconsider bij het kiezen van een nieuwe waarde voor geheugen reservering (**maxmemory gereserveerd** of **maxfragmentationmemory gereserveerd**) is hoe deze wijziging van invloed kan zijn op een cache die al wordt uitgevoerd met grote hoeveelheden gegevens. Als u een cache 53 GB met 49 GB aan gegevens vervolgens Hallo reservering waarde too8 GB wijzigen, wordt dit voor het exemplaar Hallo maximale geheugen beschikbaar voor Hallo system omlaag too45 GB verwijderen. Als uw huidige `used_memory` of uw `used_memory_rss` waarden hoger zijn dan de nieuwe limiet Hallo van 45 GB en vervolgens system Hallo tooevict gegevens hebben tot beide `used_memory` en `used_memory_rss` hieronder 45 GB zijn. Verwijderen kan de fragmentatie van de belasting en geheugen van de server te verhogen. Voor meer informatie over metrische gegevens cache zoals `used_memory` en `used_memory_rss`, Zie [beschikbare metrische gegevens en de rapportage van intervallen](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).

> [!IMPORTANT]
> Hallo **maxmemory gereserveerd** en **maxfragmentationmemory gereserveerd** instellingen zijn alleen beschikbaar voor Standard en Premium in cache opgeslagen.
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Met Keyspace-kennisgevingen (geavanceerde instellingen)
Meldingen zijn geconfigureerd op Hallo keyspace redis **geavanceerde instellingen** blade. Keyspace-kennisgevingen kunnen clients meldingen tooreceive wanneer bepaalde gebeurtenissen optreden.

![Redis-Cache geavanceerde instellingen](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Met Keyspace meldingen en Hallo **melden keyspace gebeurtenissen** instelling zijn alleen beschikbaar voor Standard en Premium-caches.
> 
> 

Zie voor meer informatie [Keyspace-kennisgevingen Redis](http://redis.io/topics/notifications). Zie voor voorbeeldcode Hallo [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) bestand in Hallo [Hallo wereld](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) voorbeeld.


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Redis-Cache Advisor
Hallo **Redis-Cache Advisor** blade geeft aanbevelingen voor uw cache. Tijdens normale bewerkingen worden geen aanbevelingen weergegeven. 

![Aanbevelingen](./media/cache-configure/redis-cache-no-recommendations.png)

Als alle voorwaarden wordt voldaan tijdens het Hallo-bewerkingen van uw cache zoals hoog geheugengebruik, netwerkbandbreedte of belasting van de server, een waarschuwing wordt weergegeven op Hallo **Redis-Cache** blade.

![Aanbevelingen](./media/cache-configure/redis-cache-recommendations-alert.png)

Meer informatie vindt u op Hallo **aanbevelingen** blade.

![Aanbevelingen](./media/cache-configure/redis-cache-recommendations.png)

Kunt u deze metrische gegevens op Hallo bewaken [grafieken bewaking](cache-how-to-monitor.md#monitoring-charts) en [gebruik grafieken](cache-how-to-monitor.md#usage-charts) secties Hallo **Redis-Cache** blade.

Elke prijscategorie heeft verschillende beperkingen voor clientverbindingen, geheugen en bandbreedte. Als uw cache maximale capaciteit voor deze metrische gegevens gedurende een langere periode tijd nadert, wordt een aanbeveling gemaakt. Voor meer informatie over Hallo metrische gegevens en limieten beoordeeld door Hallo **aanbevelingen** hulpprogramma, raadpleegt u Hallo volgende tabel:

| Redis-Cache metrische gegevens | Meer informatie |
| --- | --- |
| Gebruik van netwerkbandbreedte |[Prestaties van de cache - bandbreedte](cache-faq.md#cache-performance) |
| Verbonden clients |[Standaard Redis-serverconfiguratie - maxclients](#maxclients) |
| Belasting van de server |[Gebruik grafieken - belasting van de Redis-Server](cache-how-to-monitor.md#usage-charts) |
| Geheugengebruik |[Prestaties van de cache - grootte](cache-faq.md#cache-performance) |

tooupgrade uw cache, klikt u op **nu bijwerken** toochange Hallo prijscategorie en [scale](#scale) uw cache. Zie voor meer informatie over het kiezen van een prijscategorie [welke aanbieding Redis-Cache en de grootte moet ik gebruiken?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>Schalen
Klik op **Scale** tooview of wijzig Hallo prijscategorie voor uw cache. Zie voor meer informatie over het schalen [hoe tooScale Azure Redis-Cache](cache-how-to-scale.md).

![Redis-Cache prijscategorie](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Clustergrootte redis
Klik op **(PREVIEW) Redis clustergrootte** toochange Hallo clustergrootte voor een actieve premium in de cache met clustering is ingeschakeld.

> [!NOTE]
> Denk eraan dat bij hello Azure Redis-Cache Premium laag is vrijgegeven tooGeneral beschikbaarheid, Hallo clustergrootte Redis-functie is momenteel in preview.
> 
> 

![Clustergrootte redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

Hallo clustergrootte toochange gebruik Hallo schuifregelaar of typ een getal tussen 1 en 10 in Hallo **Shard aantal** tekstvak en klik op **OK** toosave.

> [!IMPORTANT]
> Redis clustering is alleen beschikbaar voor Premium-caches. Zie voor meer informatie [hoe tooconfigure clustering voor een Premium Azure Redis-Cache](cache-how-to-premium-clustering.md).
> 
> 


### <a name="redis-data-persistence"></a>Redis-gegevenspersistentie
Klik op **Redis-gegevenspersistentie** tooenable, uitschakelen of gegevenspersistentie configureren voor uw cache premium. Azure Redis-Cache met behulp van Redis-persistentie biedt [RDB persistentie](cache-how-to-premium-persistence.md#configure-rdb-persistence) of [AOF persistentie](cache-how-to-premium-persistence.md#configure-aof-persistence).

Zie voor meer informatie [hoe tooconfigure persistentie voor een Premium Azure Redis-Cache](cache-how-to-premium-persistence.md).


> [!IMPORTANT]
> Redis-gegevenspersistentie is alleen beschikbaar voor Premium-caches. 
> 
> 

### <a name="schedule-updates"></a>Updates plannen
Hallo **updates plannen** blade kunt u een onderhoudsvenster voor Redis-serverupdates voor uw cache toodesignate. 

> [!IMPORTANT]
> Hallo-onderhoudsvenster van toepassing is alleen tooRedis serverupdates en niet tooany Azure-updates of updates toohello besturingssysteem Hallo VM's die als host Hallo-cache fungeren.
> 
> 

![Updates plannen](./media/cache-configure/redis-schedule-updates.png)

een onderhoudsvenster toospecify controleren Hallo gewenst dagen Hallo onderhoud-venster Beginuur voor elke dag opgeven, en klik **OK**. Houd er rekening mee dat de duur van het onderhoudsvenster Hallo ingesteld op UTC is. 

> [!IMPORTANT]
> Hallo **updates plannen** functionaliteit is alleen beschikbaar voor Premium-laag caches. Zie voor meer informatie en instructies [beheer van Azure Redis-Cache - updates plannen](cache-administration.md#schedule-updates).
> 
> 

### <a name="geo-replication"></a>Geo-replicatie

Hallo **Geo-replicatie** blade biedt een mechanisme voor het koppelen van twee exemplaren van Premium-laag Azure Redis-Cache. Een cache is aangewezen als Hallo primaire gekoppelde cache en andere als secundaire gekoppelde cache Hallo Hallo. Hallo secundaire gekoppelde cache wordt alleen-lezen en gegevens die zijn geschreven toohello primaire-cache is gerepliceerd toohello secundaire gekoppelde cache. Deze functionaliteit kan gebruikte tooreplicate een cache in Azure-regio's zijn.

> [!IMPORTANT]
> **Geo-replicatie** is alleen beschikbaar voor Premium-laag caches. Zie voor meer informatie en instructies [hoe tooconfigure Geo-replicatie voor Azure Redis-Cache](cache-how-to-geo-replication.md).
> 
> 

### <a name="virtual-network"></a>Virtual Network
Hallo **virtueel netwerk** sectie kunt u tooconfigure Hallo virtuele-netwerkinstellingen voor uw cache. Voor informatie over het maken van een premium-cache met VNET ondersteunen en bijwerken van de instellingen, Zie [hoe tooconfigure Virtual Network-ondersteuning voor een Premium Azure Redis-Cache](cache-how-to-premium-vnet.md).

> [!IMPORTANT]
> Instellingen voor virtuele netwerken zijn alleen beschikbaar voor premium-caches die zijn geconfigureerd met ondersteuning voor VNET tijdens het maken van de cache. 
> 
> 

### <a name="firewall"></a>Firewall

Klik op **Firewall** tooview en firewallregels configureren voor uw Premium Azure Redis-Cache.

![Firewall](./media/cache-configure/redis-firewall-rules.png)

U kunt firewallregels opgeven met een begin- en IP-adresbereik. Wanneer de firewallregels zijn geconfigureerd, wordt alleen clientverbindingen van Hallo opgegeven IP-adresbereiken verbinding kunnen maken van toohello cache. Wanneer een firewallregel wordt opgeslagen is er een korte vertraging optreden voordat het Hallo-regel is van kracht. Dit uitstel is meestal minder dan een minuut.

> [!IMPORTANT]
> Verbindingen van Azure Redis-Cache bewaken altijd toegestaan, zelfs als de firewallregels zijn geconfigureerd.
> 
> Firewallregels zijn alleen beschikbaar voor Premium-laag caches.
> 
> 

### <a name="properties"></a>Eigenschappen
Klik op **eigenschappen** tooview informatie over uw cache, waaronder Hallo cache-eindpunt en poorten.

![Redis-Cache-eigenschappen](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>Vergrendelingen
Hallo **vergrendelt** sectie kunt u toolock een abonnement, resourcegroep of resource tooprevent andere gebruikers in uw organisatie per ongeluk worden kritieke bronnen wijzigen of verwijderen. Zie voor meer informatie [Resources vergrendelen met Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).

### <a name="automation-script"></a>Automatiseringsscript

Klik op **automatiseringsscript** toobuild en exporteren van een sjabloon van uw geïmplementeerde resources voor toekomstige implementaties. Zie voor meer informatie over het werken met sjablonen [implementeren van resources met Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="administration-settings"></a>Instellingen voor beheer
Hallo-instellingen in Hallo **beheer** sectie kunt u tooperform Hallo beheertaken voor uw cache te volgen. 

![Beheer](./media/cache-configure/redis-cache-administration.png)

* [Gegevens importeren](#importexport)
* [Gegevens exporteren](#importexport)
* [Opnieuw opstarten](#reboot)


### <a name="importexport"></a>Import/Export
Import/Export is een Azure Redis-Cache gegevensbewerking voor het beheer, zodat u tooimport en exporteren van gegevens in cache van Hallo door te importeren en exporteren van een momentopname van een Redis-Cache Database (RDB) van een premium cache tooa pagina-blob in Azure Storage-Account. Voor importeren/exporteren kunt u toomigrate tussen verschillende exemplaren van Azure Redis-Cache of vullen Hallo cache met gegevens voor het gebruik.

Importeren kan gebruikte toobring Redis compatibele RDB bestanden vanaf een willekeurige Redis-server uitgevoerd in een cloud of de omgeving, inclusief Redis uitgevoerd op Linux, Windows of elke cloudprovider zoals Amazon Web Services en andere zijn. Het importeren van gegevens is een eenvoudige manier toocreate een cache met vooraf ingestelde gegevens. Tijdens het importproces hello, Azure Redis-Cache Hallo RDB bestanden uit Azure storage in het geheugen geladen en Hallo sleutels wordt ingevoegd in de cache Hallo.

Exporteren kunt u tooexport Hallo opgeslagen gegevens in Azure Redis-Cache tooRedis compatibele RDB bestanden. U kunt deze functie toomove op gegevens uit een Azure Redis-Cache-exemplaar tooanother of tooanother Redis-server gebruiken. Tijdens het exportproces hello, wordt een tijdelijk bestand op Hallo VM dat hosts Hallo server-exemplaar van Azure Redis-Cache en Hallo bestand geüploade toohello aangewezen storage-account is gemaakt. Wanneer de exportbewerking Hallo is voltooid met de status van slagen of mislukken, wordt Hallo tijdelijk bestand verwijderd.

> [!IMPORTANT]
> Import/Export is alleen beschikbaar voor Premium-laag caches. Zie voor meer informatie en instructies [importeren en exporteren van gegevens in Azure Redis-Cache](cache-how-to-import-export-data.md).
> 
> 

### <a name="reboot"></a>Opnieuw opstarten
Hallo **opnieuw opstarten** blade kunt u tooreboot Hallo knooppunten van de cache. Deze mogelijkheid opnieuw opstarten kan tootest u uw toepassing voor tolerantie als er een storing van een cacheknooppunt.

![Opnieuw opstarten](./media/cache-configure/redis-cache-reboot.png)

Als u een premium-cache hebt met clusteren is ingeschakeld, kunt u selecteren welke shards van Hallo cache tooreboot.

![Opnieuw opstarten](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot een of meer knooppunten van de cache Hallo gewenst knooppunten te selecteren en klik op **opnieuw opstarten**. Als u een premium-cache hebt met clustering is ingeschakeld, Hallo shard(s) tooreboot selecteren en klik vervolgens op **opnieuw opstarten**. Hallo geselecteerde knooppunt opnieuw opstarten na een paar minuten en weer online zijn een paar minuten later.

> [!IMPORTANT]
> Opnieuw opstarten is nu beschikbaar voor alle Prijscategorieën. Zie voor meer informatie en instructies [beheer van Azure Redis-Cache - opnieuw opstarten](cache-administration.md#reboot).
> 
> 


## <a name="monitoring"></a>Bewaking

Hallo **bewaking** sectie kunt u tooconfigure diagnostische gegevens en de bewaking van uw Redis-Cache. Zie voor meer informatie over het controleren van Azure Redis-Cache en diagnostische gegevens [hoe toomonitor Azure Redis-Cache](cache-how-to-monitor.md).

![Diagnostiek](./media/cache-configure/redis-cache-diagnostics.png)

* [Metrische gegevens redis](#redis-metrics)
* [Regels voor waarschuwingen](#alert-rules)
* [Diagnostics](#diagnostics)

### <a name="redis-metrics"></a>Metrische gegevens redis
Klik op **Redis metrische gegevens** te[metrische gegevens weergeven](cache-how-to-monitor.md#view-cache-metrics) voor uw cache.

### <a name="alert-rules"></a>Regels voor waarschuwingen

Klik op **waarschuwing regels** tooconfigure waarschuwingen op basis van Redis-Cache metrische gegevens. Zie voor meer informatie [waarschuwingen](cache-how-to-monitor.md#alerts).

### <a name="diagnostics"></a>Diagnostiek

Cache metrische gegevens in de Azure-Monitor zijn standaard [30 dagen bewaard](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) en vervolgens verwijderd. toopersist metrische gegevens van uw cache langer dan 30 dagen, klikt u op **Diagnostics** te[opslagaccount Hallo configureren](cache-how-to-monitor.md#export-cache-metrics) toostore cache diagnostische gegevens gebruikt.

>[!NOTE]
>In aanvulling tooarchiving uw cache metrische gegevens toostorage, kunt u ook [stream ze tooan Event hub of verzend deze tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

## <a name="support--troubleshooting-settings"></a>Ondersteuning en probleemoplossing van instellingen
Hallo-instellingen in Hallo **ondersteuning + probleemoplossing** sectie bieden u opties voor het oplossen van problemen met uw cache.

![Ondersteuning + probleemoplossing](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [Resourcestatus](#resource-health)
* [Nieuw ondersteuningsverzoek](#new-support-request)

### <a name="resource-health"></a>Status van resources
**Resourcestatus** controleert uw resource en geeft u aan als deze wordt uitgevoerd zoals verwacht. Zie voor meer informatie over health-service van Azure Resource Hallo [overzicht van Azure Resource health](../resource-health/resource-health-overview.md).

> [!NOTE]
> De resourcestatus is momenteel niet mogelijk tooreport Hallo gezondheid van Azure Redis-Cache-exemplaren die worden gehost in een virtueel netwerk. Zie voor meer informatie [alle functies van de cache werken bij het hosten van een cache in een VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)
> 
> 

### <a name="new-support-request"></a>Nieuw ondersteuningsverzoek
Klik op **nieuw ondersteuningsverzoek** tooopen ondersteuning aan te vragen voor uw cache.





## <a name="default-redis-server-configuration"></a>Standaardconfiguratie van het Redis-server
Nieuwe exemplaren van Azure Redis-Cache zijn geconfigureerd met Hallo standaardwaarden van het Redis-configuratie te volgen.

> [!NOTE]
> Hallo-instellingen in deze sectie kunnen niet worden gewijzigd met Hallo `StackExchange.Redis.IServer.ConfigSet` methode. Als deze methode is aangeroepen met een van de opdrachten in deze sectie hello, wordt een uitzondering vergelijkbare toohello volgende gegenereerd:  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> Alle waarden die kunnen worden geconfigureerd, zoals **max-geheugen-policy**, kunnen worden geconfigureerd via hello Azure-portal of beheer via de opdrachtregel-hulpprogramma's zoals Azure CLI of PowerShell.
> 
> 

| Instelling | Standaardwaarde | Beschrijving |
| --- | --- | --- |
| `databases` |16 |Hallo standaardaantal databases dat is 16 maar u kunt een ander nummer op basis van Hallo prijscategorie configureren. <sup>1</sup> Hallo standaarddatabase DB 0 is, kunt u een andere naam op een afzonderlijke verbinding basis met `connection.GetDatabase(dbid)` waar `dbid` is een getal tussen `0` en `databases - 1`. |
| `maxclients` |Afhankelijk van Hallo prijscategorie<sup>2</sup> |Dit is Hallo kunt u het maximum aantal verbonden clients toegestaan op Hallo dezelfde tijd. Zodra Hallo limiet is bereikt Redis Hiermee sluit u alle Hallo nieuwe verbindingen, een 'max. aantal clients bereikt'-fout. |
| `maxmemory-policy` |`volatile-lru` |Maxmemory beleid is Hallo-instelling voor hoe Redis welke tooremove geselecteerd wanneer `maxmemory` (grootte van Hallo cache bieden u geselecteerd tijdens het maken van de cache Hallo Hallo) is bereikt. Met Azure Redis-Cache Hallo standaard instelling is `volatile-lru`, waarbij Hallo sleutels worden verwijderd met een vervaldatum instellen met behulp van een LRU-algoritme. Deze instelling kan worden geconfigureerd in hello Azure-portal. Zie voor meer informatie [geheugen beleid](#memory-policies). |
| `maxmemory-samples` |3 |toosave geheugen, LRU en minimale TTL-algoritmes zijn redelijk algoritmen in plaats van nauwkeurige algoritmen. Standaard Redis controles drie sleutels en uitgelicht Hallo een die minder recent is gebruikt. |
| `lua-time-limit` |5,000 |Maximale uitvoeringstijd van een script Lua in milliseconden. Als de maximale uitvoeringstijd Hallo is bereikt, registreert Redis dat een script nog steeds uitgevoerd na Hallo maximale toegestane tijd wordt en tooreply tooqueries met een fout opgetreden begint. |
| `lua-event-limit` |500 |Maximale grootte van de wachtrij script. |
| `client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub` |0 0 032mb 8mb 60 |Hallo client uitvoer buffer kan worden beperkt tooforce verbreken van clients die niet van gegevens van Hallo server snel genoeg voor een bepaalde reden lezen zijn (een veelvoorkomende reden is dat een client Pub subitems snel Hallo publisher kan ze produceren berichten kan niet gebruiken) gebruikt. Zie voor meer informatie [http://redis.io/topics/clients](http://redis.io/topics/clients). |

<a name="databases"></a>
<sup>1</sup>Hallo limiet voor `databases` verschilt voor elk Azure Redis-Cache prijscategorie en kan worden ingesteld bij het maken van de cache. Als er geen `databases` instelling is opgegeven tijdens het maken van de cache Hallo standaardwaarde is 16.

* Basic en Standard caches
  * C0 (250 MB)-cache - up van databases too16
  * C1 (1 GB)-cache - up van databases too16
  * C2 (2,5 GB)-cache - up van databases too16
  * C3 (6 GB)-cache - up van databases too16
  * C4 (13 GB)-cache - up van databases too32
  * C5 (26 GB)-cache - up van databases too48
  * C6 (53 GB)-cache - up van databases too64
* Premium-caches
  * P1 (6 GB - 60 GB) van de too16-databases
  * P2 (13 GB - 130 GB) van de too32-databases
  * P3 (26 GB - 260 GB) van de too48-databases
  * P4 (53 GB - 530 GB) van de too64-databases
  * Alle premium caches met Redis-cluster ingeschakeld - Redis-cluster ondersteunt alleen gebruik van database 0 dus Hallo `databases` limiet voor elke premium-cache met Redis-cluster ingeschakeld is in feite 1 en Hallo [Selecteer](http://redis.io/commands/select) opdracht is niet toegestaan. Zie voor meer informatie [heb ik nodig toomake eventuele wijzigingen toomy client toepassing toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

Zie voor meer informatie over databases [wat Redis-databases zijn?](cache-faq.md#what-are-redis-databases)

> [!NOTE]
> Hallo `databases` instelling kan worden geconfigureerd tijdens de cache maken en alleen met behulp van PowerShell, CLI of andere clients management. Voor een voorbeeld van de configuratie van `databases` tijdens het maken van de cache met behulp van PowerShell, Zie [nieuw AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).
> 
> 

<a name="maxclients"></a>
<sup>2</sup> `maxclients` verschilt voor elk Azure Redis-Cache prijscategorie.

* Basic en Standard caches
  * C0 (250 MB)-cache - too256 verbindingen configureren
  * C1 (1 GB)-cache - up too1, 000 verbindingen
  * C2 (2,5 GB)-cache - up too2, 000 verbindingen
  * C3 (6 GB)-cache - up too5, 000 verbindingen
  * C4 (13 GB)-cache - up too10, 000 verbindingen
  * C5 (26 GB)-cache - up too15, 000 verbindingen
  * C6 (53 GB)-cache - up too20, 000 verbindingen
* Premium-caches
  * P1 (6 GB - 60 GB) - up too7, 500-verbindingen
  * P2 (13 GB - 130 GB) - up too15, 000 verbindingen
  * P3 (26 GB - 260 GB) - up too30, 000 verbindingen
  * P4 (53 GB - 530 GB) - up too40, 000 verbindingen

> [!NOTE]
> Kunt u elke grootte van cache *tot* een bepaald aantal verbindingen, elke tooRedis verbinding heeft de overhead gekoppeld. Een voorbeeld van een dergelijke overhead zou zijn CPU- en geheugengebruik als gevolg van TLS/SSL-versleuteling. Hallo maximale verbindingslimiet voor een opgegeven cachegrootte wordt ervan uitgegaan dat een licht geladen cache. Als uit verbinding overhead laden *plus* laden vanaf de clientbewerkingen dan er capaciteit voor Hallo systeem, Hallo cache kunt capaciteitsproblemen moeten ondervinden zelfs als u hebt niet de verbindingslimiet Hallo voor de huidige cachegrootte Hallo overschreden.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Redis opdrachten niet ondersteund in Azure Redis-Cache
> [!IMPORTANT]
> Omdat de configuratie en beheer van exemplaren van Azure Redis-Cache wordt beheerd door Microsoft, zijn hello volgende opdrachten uitgeschakeld. Als u tooinvoke probeert ze, verschijnt een foutbericht te`"(error) ERR unknown command"`.
> 
> * BGREWRITEAOF
> * BGSAVE
> * CONFIGURATIE
> * FOUTEN OPSPOREN
> * MIGREREN
> * OPSLAAN
> * AFSLUITEN
> * SLAVEOF
> * CLUSTER - schrijven zijn uitgeschakeld, maar alleen-lezen Cluster opdrachten zijn toegestaan.
> 
> 

Zie voor meer informatie over Redis opdrachten [http://redis.io/commands](http://redis.io/commands).

## <a name="redis-console"></a>Redis-console
Kunt u veilig uitgeven opdrachten tooyour Azure Redis-Cache-exemplaren die gebruikmaken van Hallo **Redis-Console**, die beschikbaar is in hello Azure-portal voor alle cachelagen.

> [!IMPORTANT]
> - Hallo Redis-Console werkt niet met [VNET](cache-how-to-premium-vnet.md). Als uw cache deel van een VNET uitmaakt, toegang alleen clients in VNET Hallo Hallo-cache. Omdat Redis-Console wordt uitgevoerd in uw lokale browser, die zich buiten de Hallo VNET, kunt deze cache tooyour kan geen verbinding maken.
> - Niet alle Redis-opdrachten worden ondersteund in Azure Redis-Cache. Zie voor een lijst met Redis-opdrachten die zijn uitgeschakeld voor Azure Redis-Cache, Hallo vorige [Redis opdrachten niet ondersteund in Azure Redis-Cache](#redis-commands-not-supported-in-azure-redis-cache) sectie. Zie voor meer informatie over Redis opdrachten [http://redis.io/commands](http://redis.io/commands).
> 
> 

tooaccess hello Redis-Console klikt u op **Console** van Hallo **Redis-Cache** blade.

![Redis-console](./media/cache-configure/redis-console-menu.png)

tooissue opdrachten op basis van uw cache-exemplaar, gewoon type Hallo gewenste opdracht in Hallo-console.

![Redis-console](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>Hallo met Redis-Console met een premium cache voor geclusterde

Wanneer met behulp van Hallo Redis-Console met een premium cache voor geclusterde, kunt u opdrachten tooa één shard van Hallo cache uitgeven. een opdracht tooa specifieke shard, tooissue toohello gewenste shard wordt door erop te klikken op Hallo shard objectkiezer eerst verbinding maken.

![Redis-console](./media/cache-configure/redis-console-premium-cluster.png)

Als u een sleutel die is opgeslagen in een andere shard probeert dan Hallo verbonden shard tooaccess, ontvangt u een fout bericht vergelijkbaar toohello volgende bericht.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

In het vorige voorbeeld hello, is 1 shard Hallo geselecteerde shard, maar `myKey` bevindt zich in de shard 0, zoals aangegeven door Hallo `(shard 0)` gedeelte van het foutbericht Hallo. In dit voorbeeld tooaccess `myKey`, selecteer met behulp van shard 0 Hallo shard objectkiezer en probleem Hallo gewenst opdracht.


## <a name="move-your-cache-tooa-new-subscription"></a>Uw cache tooa nieuw abonnement verplaatsen
U kunt uw cache tooa nieuw abonnement verplaatsen door te klikken op **verplaatsen**.

![Verplaatsen van Redis-Cache](./media/cache-configure/redis-cache-move.png)

Zie voor meer informatie over het verplaatsen van resources van één resource groep tooanother en van één abonnement tooanother [verplaatsen van resources toonew resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md).

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het werken met Redis-opdrachten [hoe kan ik Redis-opdrachten uitvoeren?](cache-faq.md#how-can-i-run-redis-commands)

