een cache toocreate toohello zich eerst aanmelden [Azure-portal](https://portal.azure.com), en klik op **nieuw** > **Databases** > **Redis-Cache**.

> [!NOTE]
> Als u geen Azure-account hebt, kunt u binnen een paar minuten [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).
> 
> 

![Nieuwe cache](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> Bovendien toocreating-caches in hello Azure-portal, u kunt ook deze met Resource Manager-sjablonen, PowerShell of Azure CLI.
> 
> * toocreate een cache met behulp van Resource Manager-sjablonen, Zie [een Redis-cache met behulp van een sjabloon maken](../articles/redis-cache/cache-redis-cache-arm-provision.md).
> * een cache met Azure PowerShell toocreate Zie [beheren van Azure Redis-Cache met Azure PowerShell](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md).
> * een cache met Azure CLI toocreate Zie [hoe toocreate en beheren van Azure Redis-Cache met behulp van Azure-opdrachtregelinterface (Azure CLI) Hallo](../articles/redis-cache/cache-manage-cli.md).
> 
> 

In Hallo **nieuwe Redis-Cache** blade Hallo gewenste configuratie voor Hallo cache opgeven.

![Cache maken](media/redis-cache-create/redis-cache-cache-create.png) 

* In **DNS-naam**, voer een unieke cache naam toouse voor Hallo cache-eindpunt. Hallo Cachenaam moet een waarde in tussen 1 en 63 tekens lang zijn en mag alleen cijfers, letters en Hallo `-` teken. Hallo Cachenaam mag niet beginnen of eindigen met Hallo `-` teken en opeenvolgende `-` tekens zijn niet geldig.
* Voor **abonnement**, selecteer hello Azure-abonnement dat u toouse Hallo-cache wenst. Als uw account slechts één abonnement heeft, deze wordt automatisch geselecteerd en Hallo **abonnement** vervolgkeuzelijst worden niet weergegeven.
* In **Resourcegroep** selecteert of maakt u een resourcegroep voor uw cache. Zie voor meer informatie [met behulp van resourcegroepen toomanage uw Azure-resources](../articles/azure-resource-manager/resource-group-overview.md). 
* Gebruik **locatie** toospecify Hallo geografische locatie waar uw cache wordt gehost. Voor de beste prestaties Hallo Microsoft raadt u Hallo cache maken in Hallo dezelfde regio bevinden als de cacheclienttoepassing Hallo.
* Gebruik **prijscategorie** tooselect Hallo gewenste cachegrootte en -functies.
* **Redis-cluster** kunt u caches toocreate groter zijn dan 53 GB en tooshard gegevens over meerdere Redis-knooppunten. Zie voor meer informatie [hoe tooconfigure clustering voor een Premium Azure Redis-Cache](../articles/redis-cache/cache-how-to-premium-clustering.md).
* **Redis-persistentie** Hallo mogelijkheid toopersist biedt uw cache tooan Azure Storage-account. Zie voor instructies over het configureren van persistentie [hoe tooconfigure persistentie voor een Premium Azure Redis-Cache](../articles/redis-cache/cache-how-to-premium-persistence.md).
* **Virtueel netwerk** biedt verbeterde beveiliging en isolatie door het beperken van toegang tooyour cache tooonly de clients binnen de opgegeven hello Azure Virtual Network. U kunt alle Hallo functies van VNet, zoals subnetten, toegangscontrolebeleid en andere functies toofurther tooRedis toegang beperken. Zie voor meer informatie [hoe tooconfigure Virtual Network-ondersteuning voor een Premium Azure Redis-Cache](../articles/redis-cache/cache-how-to-premium-vnet.md).
* Voor nieuwe caches is niet-SSL-toegang standaard uitgeschakeld. tooenable hello niet-SSL-poort, selectievakje **deblokkeren poort 6379 (niet SSL versleuteld)**.

Zodra het Hallo-opties voor nieuwe cache zijn geconfigureerd, klikt u op **maken**. Het kan enkele minuten duren voordat Hallo cache toobe gemaakt. toocheck hello status, kunt u voortgang Hallo op Hallo startboard. Nadat het Hallo-cache is gemaakt, heeft de nieuwe cache een **met** status en is gereed voor gebruik met [standaardinstellingen](../articles/redis-cache/cache-configure.md#default-redis-server-configuration).

![Cache gemaakt](media/redis-cache-create/redis-cache-cache-created.png)

