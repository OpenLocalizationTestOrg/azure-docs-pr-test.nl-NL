---
title: Azure Redis-Cache met Azure PowerShell aaaManage | Microsoft Docs
description: Meer informatie over hoe tooperform beheertaken voor Azure Redis-Cache met Azure PowerShell.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a>Azure Redis-Cache met Azure PowerShell beheren
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Azure-CLI](cache-manage-cli.md)
> 
> 

Dit onderwerp leest u hoe tooperform algemene taken, zoals het maken, bijwerken en schalen van uw Azure Redis-Cache-exemplaren hoe tooregenerate toegangstoetsen, en hoe tooview informatie over uw caches. Zie voor een volledige lijst met Azure Redis-Cache PowerShell-cmdlets, [cmdlets van Azure Redis-Cache](https://msdn.microsoft.com/library/azure/mt634513.aspx).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

Zie voor meer informatie over het klassieke implementatiemodel Hallo [Azure Resource Manager versus klassieke implementatie: implementatiemodellen begrijpen en de status van uw resources Hallo](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).

## <a name="prerequisites"></a>Vereisten
Als u Azure PowerShell al hebt geïnstalleerd, moet u Azure PowerShell versie 1.0.0 hebben of hoger. U kunt controleren Hallo-versie van Azure PowerShell die u hebt geïnstalleerd met deze opdracht op Hallo Azure PowerShell-opdrachtregel.

    Get-Module azure | format-table version


U moet eerst tooAzure met deze opdracht aanmelden.

    Login-AzureRmAccount

Hallo e-mailadres van uw Azure-account en het bijbehorende wachtwoord in het dialoogvenster Hallo Microsoft Azure-aanmeldingspagina opgeven.

Vervolgens als u meerdere Azure-abonnementen hebt, moet u tooset uw Azure-abonnement. een lijst met uw huidige abonnementen toosee deze opdracht uitvoeren.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello abonnement, Hallo volgende opdracht uitvoeren. In de Hallo voorbeeld te volgen, is de naam van Hallo abonnement `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

Voordat u Windows PowerShell met Azure Resource Manager gebruiken kunt, moet u de volgende Hallo:

* Windows PowerShell versie 3.0 of 4.0. toofind hello versie van Windows PowerShell, typ:`$PSVersionTable` en controleer of de waarde van Hallo `PSVersion` 3.0 of 4.0. Zie een compatibele versie tooinstall [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) of [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

tooget gedetailleerde help voor een cmdlet die u in deze zelfstudie Hallo gebruik de cmdlet Get-Help ziet.

    Get-Help <cmdlet-name> -Detailed

Bijvoorbeeld, tooget help voor Hallo `New-AzureRmRedisCache` cmdlet, type:

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a>Hoe tooconnect tooother clouds
Door standaard hello Azure-omgeving is `AzureCloud`, welke vertegenwoordigt Hallo globale Azure cloud-exemplaar. tooconnect tooa ander exemplaar, gebruik Hallo `Add-AzureRmAccount` opdracht Hello `-Environment` of -`EnvironmentName` opdrachtregelparameter met de gewenste omgeving Hallo of de omgevingsnaam van de.

toosee hello lijst met beschikbare omgevingen, Voer Hallo `Get-AzureRmEnvironment` cmdlet.

### <a name="tooconnect-toohello-azure-government-cloud"></a>tooconnect toohello Azure Government Cloud
tooconnect toohello Azure Government Cloud, gebruik een van de volgende opdrachten Hallo.

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

of

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

toocreate een cache in hello Azure Government Cloud, gebruik een van de volgende locaties Hallo.

* Amerikaanse overheid Virginia
* Amerikaanse overheid Iowa

Zie voor meer informatie over hello Azure Government Cloud [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) en [Ontwikkelaarshandleiding voor Microsoft Azure Government](../azure-government-developer-guide.md).

### <a name="tooconnect-toohello-azure-china-cloud"></a>tooconnect toohello Azure China Cloud
tooconnect toohello Azure China Cloud, gebruik een van de volgende opdrachten Hallo.

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

of

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

toocreate een cache in hello Azure China Cloud, gebruik een van de volgende locaties Hallo.

* China - oost
* China - noord

Zie voor meer informatie over hello Azure China Cloud [AzureChinaCloud voor Azure wordt beheerd door 21Vianet in China](http://www.windowsazure.cn/).

### <a name="tooconnect-toomicrosoft-azure-germany"></a>tooconnect tooMicrosoft Duitse Azure
tooconnect tooMicrosoft Duitse Azure, gebruik een van de volgende opdrachten Hallo.

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


of

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

toocreate een cache in Microsoft Azure Duitsland, gebruik een van de volgende locaties Hallo.

* Duitsland - centraal
* Duitsland - noordoost

Zie voor meer informatie over Microsoft Azure Duitsland [Microsoft Azure Duitsland](https://azure.microsoft.com/overview/clouds/germany/).

### <a name="properties-used-for-azure-redis-cache-powershell"></a>Eigenschappen die worden gebruikt voor Azure Redis-Cache PowerShell
Hallo volgende tabel bevat de eigenschappen en beschrijvingen voor vaak gebruikte parameters bij het maken en beheren van uw Azure Redis-Cache-exemplaren die gebruikmaken van Azure PowerShell.

| Parameter | Beschrijving | Standaard |
| --- | --- | --- |
| Naam |Naam van het Hallo-cache | |
| Locatie |Locatie van het Hallo-cache | |
| resourceGroupName |Naam van resourcegroep in welke toocreate Hallo-cache | |
| Grootte |Hallo-grootte van Hallo-cache. Geldige waarden zijn: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB |1 GB |
| ShardCount |Hallo aantal shards toocreate bij het maken van een premium-cache met clustering is ingeschakeld. Geldige waarden zijn: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | |
| SKU |Hiermee geeft u Hallo SKU van Hallo-cache. Geldige waarden zijn: Basic, Standard, Premium |Standard |
| RedisConfiguration |Hiermee geeft u Redis-configuratie-instellingen. Zie voor meer informatie over elke instelling Hallo volgende [RedisConfiguration eigenschappen](#redisconfiguration-properties) tabel. | |
| EnableNonSslPort |Hiermee wordt aangegeven of het Hallo-niet-SSL-poort is ingeschakeld. |False |
| MaxMemoryPolicy |Deze parameter is afgeschaft - gebruik in plaats daarvan RedisConfiguration. | |
| StaticIP |Bij het hosten van uw cache in een VNET, geeft een uniek IP-adres in Hallo-subnet voor Hallo-cache. Als niet wordt opgegeven, wordt een gekozen voor u van Hallo subnet. | |
| Subnet |Bij het hosten van uw cache in een VNET, geeft Hallo-naam van Hallo subnet in welke toodeploy Hallo-cache. | |
| VirtualNetwork |Bij het hosten van uw cache in een VNET Hallo bron-ID van Hallo dan VNET in welke toodeploy Hallo-cache. | |
| KeyType |Hiermee geeft u op welke toegangssleutel tooregenerate tijdens het vernieuwen van de toegangssleutels. Geldige waarden zijn: primaire, secundaire | |

### <a name="redisconfiguration-properties"></a>RedisConfiguration eigenschappen
| Eigenschap | Beschrijving | Prijscategorieën |
| --- | --- | --- |
| RDB back-up is ingeschakeld |Of [Redis-gegevenspersistentie](cache-how-to-premium-persistence.md) is ingeschakeld |Alleen Premium |
| RDB---verbindingsreeks voor opslag |Hallo tekenreeks toohello storage-account voor verbinding [Redis-gegevenspersistentie](cache-how-to-premium-persistence.md) |Alleen Premium |
| back-up RDB frequentie |back-upfrequentie voor Hallo [Redis-gegevenspersistentie](cache-how-to-premium-persistence.md) |Alleen Premium |
| maxmemory gereserveerd |Hiermee configureert u Hallo [geheugen gereserveerd](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) voor niet-cache-processen |Standard en Premium |
| maxmemory-beleid |Hiermee configureert u Hallo [taakverwijdering beleid](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) voor Hallo-cache |Alle Prijscategorieën |
| melding-keyspace-gebeurtenissen |Hiermee configureert u [keyspace-kennisgevingen](cache-configure.md#keyspace-notifications-advanced-settings) |Standard en Premium |
| hash-max-ziplist-vermeldingen |Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen |Standard en Premium |
| hash-max-ziplist-waarde |Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen |Standard en Premium |
| set-max-intset-vermeldingen |Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen |Standard en Premium |
| zset max-ziplist vermeldingen |Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen |Standard en Premium |
| zset-max-ziplist-waarde |Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen |Standard en Premium |
| databases |Hiermee configureert u het aantal databases Hallo. Deze eigenschap kan alleen bij het maken van de cache worden geconfigureerd. |Standard en Premium |

## <a name="toocreate-a-redis-cache"></a>toocreate een Redis-Cache
Nieuwe exemplaren van Azure Redis-Cache zijn gemaakt met behulp van Hallo [nieuw AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

> [!IMPORTANT]
> Hallo eerste keer dat u een Redis-cache maken in een abonnement met Azure-portal Hallo Hallo portal registreert Hallo `Microsoft.Cache` naamruimte voor dat abonnement. Als u probeert toocreate Hallo eerst Redis-cache in een abonnement met behulp van PowerShell, moet u eerst registreren die naamruimte met behulp van Hallo na de opdracht; anders cmdlets zoals `New-AzureRmRedisCache` en `Get-AzureRmRedisCache` mislukken.
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `New-AzureRmRedisCache`, voert hello na de opdracht.

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

toocreate een cache met standaardparameters Hallo volgende opdracht uitvoeren.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

`ResourceGroupName`, `Name`, en `Location` vereiste parameters zijn, maar Hallo rest zijn optioneel en standaardwaarden. Hallo vorige opdracht uitvoert, maakt een standaard SKU Azure Redis-Cache-exemplaar met de opgegeven naam hello, locatie en resourcegroep die 1 GB aan de grootte van niet-SSL-poort Hallo uitgeschakeld.

toocreate een premium-cache een grootte van P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), geef P3 (26 GB - 260 GB), of P4 (53 GB tot 530 GB). tooenable clustering, een shard aantal opgeven met behulp van Hallo `ShardCount` parameter. Hallo volgende voorbeeld wordt een premium P1 cache met 3 shards. Een cache van de premium P1 6 GB groot is en omdat we drie shards Hallo totale grootte opgegeven is 18 GB (3 x 6 GB).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

toospecify waarden voor Hallo `RedisConfiguration` parameter, moet u waarden binnen Hallo `{}` als sleutel/waarde-paren, zoals `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`. Hallo volgende voorbeeld wordt een standaard 1 GB cache met `allkeys-random` maxmemory-beleid en keyspace meldingen geconfigureerd met `KEA`. Zie voor meer informatie [Keyspace-kennisgevingen (geavanceerde instellingen)](cache-configure.md#keyspace-notifications-advanced-settings) en [geheugen beleid](cache-configure.md#memory-policies).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a>tooconfigure hello databases instellen tijdens het maken van de cache
Hallo `databases` instelling kan alleen tijdens het maken van de cache worden geconfigureerd. Hallo volgende voorbeeld wordt een premium P3 (26 GB)-cache met 48-databases via Hallo [nieuw AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

Voor meer informatie over Hallo `databases` eigenschap, Zie [serverconfiguratie Azure Redis-Cache standaard](cache-configure.md#default-redis-server-configuration). Voor meer informatie over het maken van een cache met behulp van Hallo [nieuw AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, Zie de vorige Hallo [toocreate een Redis-Cache](#to-create-a-redis-cache) sectie.

## <a name="tooupdate-a-redis-cache"></a>tooupdate een Redis-cache
Azure Redis-Cache-exemplaren zijn bijgewerkt met Hallo [Set AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.

een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Set-AzureRmRedisCache`, voert hello na de opdracht.

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Hallo `Set-AzureRmRedisCache` cmdlet kan worden gebruikt tooupdate eigenschappen zoals `Size`, `Sku`, `EnableNonSslPort`, en Hallo `RedisConfiguration` waarden. 

Hallo volgende opdracht updates Hallo maxmemory-beleid voor Hallo Redis-Cache met de naam myCache.

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a>tooscale een Redis-cache
`Set-AzureRmRedisCache`gebruikte tooscale een Azure Redis-cache-exemplaar als hello kan worden `Size`, `Sku`, of `ShardCount` eigenschappen zijn gewijzigd. 

> [!NOTE]
> Schalen van een cache met behulp van PowerShell is onderwerp toohello grenzen en richtlijnen als u een cache van schalen hello Azure-portal. U kunt andere prijscategorie Hello volgen beperkingen tooa schalen.
> 
> * U kan niet uit een hogere prijscategorie laag tooa lagere prijscategorie schalen.
> * U kunt geen schalen van een **Premium** cache omlaag tooa **standaard** of een **Basic** cache.
> * U kunt geen schalen van een **standaard** cache omlaag tooa **Basic** cache.
> * U kunt opschalen van een **Basic** cache tooa **standaard** cache, maar niet wijzigen Hallo grootte op Hallo hetzelfde moment. Als u een ander formaat nodig hebt, kunt u een daaropvolgende vergroten/verkleinen bewerking toohello gewenst grootte kunt doen.
> * U kunt geen schalen van een **Basic** cache rechtstreeks tooa **Premium** cache. U moet de schaal van **Basic** te**standaard** in één bewerking van de schaal en vervolgens van **standaard** te**Premium** bij een volgende schaal de bewerking.
> * Kan niet worden geschaald uit een groter formaat omlaag toohello **C0 (250 MB)** grootte.
> 
> Zie voor meer informatie [hoe tooScale Azure Redis-Cache](cache-how-to-scale.md).
> 
> 

Hallo volgende voorbeeld laat zien hoe tooscale een cache met de naam `myCache` tooa 2,5 GB cache. Houd er rekening mee dat deze opdracht voor zowel een Basislidmaatschap of een standaard-cache werkt.

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Nadat u deze opdracht wordt uitgevoerd, Hallo status van Hallo cache geretourneerd (vergelijkbaar toocalling `Get-AzureRmRedisCache`). Houd er rekening mee dat Hallo `ProvisioningState` is `Scaling`.

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

Wanneer Hallo schalen van de bewerking voltooid is, Hallo `ProvisioningState` wijzigingen te`Succeeded`. Als u nodig hebt toomake volgende vergroten/verkleinen bewerking, zoals het wijzigen van Basic tooStandard en vervolgens wijzigen Hallo grootte, moet u wachten tot Hallo vorige bewerking voltooid is of dat u een foutbericht vergelijkbaar toohello volgende ontvangt.

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a>tooget informatie over een Redis-cache
U kunt informatie ophalen over een cache met behulp van Hallo [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.

een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Get-AzureRmRedisCache`, voert hello na de opdracht.

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooreturn informatie over alle caches in het huidige abonnement hello, voeren `Get-AzureRmRedisCache` zonder parameters.

    Get-AzureRmRedisCache

informatie over alle caches in een specifieke resourcegroep tooreturn uitvoeren `Get-AzureRmRedisCache` Hello `ResourceGroupName` parameter.

    Get-AzureRmRedisCache -ResourceGroupName myGroup

informatie over een specifieke cache tooreturn uitvoeren `Get-AzureRmRedisCache` Hello `Name` parameter met de naam Hallo van Hallo-cache en Hallo `ResourceGroupName` Hallo resourcegroep die cache met de parameter.

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a>tooretrieve hello toegangstoetsen voor Redis-cache
tooretrieve hello toegangssleutels voor uw cache, kunt u Hallo [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.

een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Get-AzureRmRedisCacheKey`, voert hello na de opdracht.

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Hallo tooretrieve sleutels voor uw cache, aanroep Hallo `Get-AzureRmRedisCacheKey` cmdlet en geeft u Hallo-naam van uw cache Hallo naam van resourcegroep Hallo met Hallo-cache.

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a>tooregenerate toegangstoetsen voor Redis-cache
tooregenerate hello toegangssleutels voor uw cache, kunt u Hallo [nieuw AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.

een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `New-AzureRmRedisCacheKey`, voert hello na de opdracht.

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooregenerate hello primaire of secundaire sleutel voor uw cache, aanroep Hallo `New-AzureRmRedisCacheKey` cmdlet Hallo geeft u een naam, resourcegroep, en Geef ofwel `Primary` of `Secondary` voor Hallo `KeyType` parameter. In de Hallo voorbeeld te volgen, wordt Hallo secundaire toegangssleutel voor een cache gegenereerd.

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a>toodelete een Redis-cache
toodelete een Redis-cache gebruiken Hallo [verwijderen AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.

een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Remove-AzureRmRedisCache`, voert hello na de opdracht.

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Hallo in Hallo voorbeeld te volgen, cache met de naam `myCache` wordt verwijderd.

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a>tooimport een Redis-cache
U kunt gegevens importeren in een Azure Redis-Cache-exemplaar met behulp van Hallo `Import-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> Import/Export is alleen beschikbaar voor [premium-laag](cache-premium-tier-intro.md) in de cache opslaat. Zie voor meer informatie over het importeren/exporteren [importeren en exporteren van gegevens in Azure Redis-Cache](cache-how-to-import-export-data.md).
> 
> 

een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Import-AzureRmRedisCache`, voert hello na de opdracht.

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hallo importeert volgende opdracht gegevens van Hallo blob in Azure Redis-Cache door Hallo SAS-uri is opgegeven.

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a>tooexport een Redis-cache
U kunt gegevens exporteren van een Azure Redis-Cache-exemplaar met behulp van Hallo `Export-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> Import/Export is alleen beschikbaar voor [premium-laag](cache-premium-tier-intro.md) in de cache opslaat. Zie voor meer informatie over het importeren/exporteren [importeren en exporteren van gegevens in Azure Redis-Cache](cache-how-to-import-export-data.md).
> 
> 

een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Export-AzureRmRedisCache`, voert hello na de opdracht.

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hallo volgende opdracht exporteert u de gegevens van een Azure Redis-Cache-exemplaar naar Hallo-container door Hallo SAS-uri opgegeven.

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a>tooreboot een Redis-cache
U kunt uw Azure Redis-Cache-exemplaar met behulp van Hallo opstarten `Reset-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> Opnieuw opstarten is alleen beschikbaar voor [premium-laag](cache-premium-tier-intro.md) in de cache opslaat. Zie voor meer informatie over het opnieuw opstarten van uw cache [beheer in de Cache - opnieuw opstarten](cache-administration.md#reboot).
> 
> 

een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Reset-AzureRmRedisCache`, voert hello na de opdracht.

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hallo volgende opdracht wordt opnieuw opgestart beide knooppunten van de opgegeven Hallo cache.

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Windows PowerShell gebruiken met Azure, Zie Hallo resources te volgen:

* [Azure Redis-Cache-cmdlet-documentatie op MSDN](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* [Azure Resource Manager-Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): informatie over toouse Hallo-cmdlets in hello Azure Resource Manager-module.
* [Toomanage uw Azure-resources met behulp van de Resource groepen](../azure-resource-manager/resource-group-template-deploy-portal.md): meer informatie over hoe toocreate en resourcegroepen in hello Azure-portal beheren.
* [Azure-blog](http://blogs.msdn.com/windowsazure): meer informatie over nieuwe functies in Azure.
* [Windows PowerShell-blog](http://blogs.msdn.com/powershell): meer informatie over nieuwe functies in Windows PowerShell.
* ["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): echte tips en trucs ophalen uit Hallo Windows PowerShell-community.

