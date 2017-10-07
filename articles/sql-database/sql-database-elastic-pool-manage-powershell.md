---
title: 'PowerShell: Maken en beheren van een Azure SQL elastische pool | Microsoft Docs'
description: Meer informatie over hoe toouse PowerShell toomanage een elastische pool.
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="7c8da-103">Maken en beheren van een elastische pool met PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c8da-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="7c8da-104">Dit onderwerp leest u hoe toocreate en beheren van schaalbare [elastische pools](sql-database-elastic-pool.md) met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c8da-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="7c8da-105">U kunt ook maken en beheren van een Azure elastische pool met Hallo [Azure-portal](https://portal.azure.com/), REST-API of [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="7c8da-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="7c8da-106">U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="7c8da-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="7c8da-107">Elastische pool maken</span><span class="sxs-lookup"><span data-stu-id="7c8da-107">Create an elastic pool</span></span>
<span data-ttu-id="7c8da-108">Hallo [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet maakt een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="7c8da-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="7c8da-109">Hallo-waarden voor eDTU per pool, min. en max. dtu's worden beperkt door Hallo service tier waarde (Basic, Standard, Premium of Premium RS).</span><span class="sxs-lookup"><span data-stu-id="7c8da-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="7c8da-110">Zie [eDTU en opslaglimieten voor elastische pools en gegroepeerde databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="7c8da-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="7c8da-111">Maak een gegroepeerde database in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="7c8da-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="7c8da-112">Gebruik Hallo [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet en set Hallo **ElasticPoolName** parameter toohello doelgroep.</span><span class="sxs-lookup"><span data-stu-id="7c8da-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="7c8da-113">Zie voor een bestaande database in een elastische pool toomove [verplaatsen van een database in een elastische pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="7c8da-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="7c8da-114">Script voltooien</span><span class="sxs-lookup"><span data-stu-id="7c8da-114">Complete script</span></span>
<span data-ttu-id="7c8da-115">Dit script maakt een Azure-resourcegroep en een server.</span><span class="sxs-lookup"><span data-stu-id="7c8da-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="7c8da-116">Als u wordt gevraagd, geeft u een gebruikersnaam voor de beheerder en het wachtwoord voor Hallo nieuwe server (niet uw Azure-referenties).</span><span class="sxs-lookup"><span data-stu-id="7c8da-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="7c8da-117">Een elastische pool maken en toevoegen van meerdere gegroepeerde databases</span><span class="sxs-lookup"><span data-stu-id="7c8da-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="7c8da-118">Maken van veel databases in een elastische pool kan duren wanneer klaar met Hallo portal of PowerShell-cmdlets die slechts één database tegelijkertijd maken.</span><span class="sxs-lookup"><span data-stu-id="7c8da-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="7c8da-119">Zie tooautomate maken voor een elastische pool [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="7c8da-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="7c8da-120">Een database verplaatsen naar een elastische pool</span><span class="sxs-lookup"><span data-stu-id="7c8da-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="7c8da-121">U kunt een database verplaatsen van of naar een elastische groep met Hallo [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="7c8da-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="7c8da-122">Instellingen van de prestaties van een elastische groep wijzigen</span><span class="sxs-lookup"><span data-stu-id="7c8da-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="7c8da-123">Wanneer de prestaties te lijden heeft onder, kunt u instellingen Hallo Hallo groep tooaccommodate groei kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="7c8da-124">Gebruik Hallo [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7c8da-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="7c8da-125">Hallo - Dtu parameter toohello edtu's per groep ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7c8da-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="7c8da-126">Zie [eDTU en opslaglimieten](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor mogelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="7c8da-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="7c8da-127">De opslaglimiet Hallo voor een elastische groep wijzigen</span><span class="sxs-lookup"><span data-stu-id="7c8da-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="7c8da-128">Gebruik Hallo [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _- StorageMB_ parameter.</span><span class="sxs-lookup"><span data-stu-id="7c8da-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="7c8da-129">Geef de opslaglimiet Hallo in MB (bijvoorbeeld 2097152 sets Hallo opslag limiet too2 TB).</span><span class="sxs-lookup"><span data-stu-id="7c8da-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="7c8da-130">Zie [eDTU en opslaglimieten](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor mogelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="7c8da-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c8da-131">Hallo standaard maximale gegevensopslag per groep voor Premium-groepen met edtu's 1500 of meer is dan 750 GB.</span><span class="sxs-lookup"><span data-stu-id="7c8da-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="7c8da-132">tooobtain hello hoger _maximale opslaggrootte van de gegevens per groep_, Hallo opslaglimiet moet expliciet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7c8da-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="7c8da-133">Premium-adresgroepen met meer dan 750 GB aan opslagruimte bevindt zich momenteel in de openbare preview in Hallo gebieden te volgen: VS-Oost 2, VS-West, Gov ons Virginia, West-Europa, Duitsland centraal, Zuidoost-Azië, Japan-Oost, Australië-Oost, Canada centraal en Canada-Oost.</span><span class="sxs-lookup"><span data-stu-id="7c8da-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="7c8da-134">Hallo-status van de groep operations ophalen</span><span class="sxs-lookup"><span data-stu-id="7c8da-134">Get hello status of pool operations</span></span>
<span data-ttu-id="7c8da-135">Maken van een elastische pool kan tijd duren.</span><span class="sxs-lookup"><span data-stu-id="7c8da-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="7c8da-136">tootrack hello status van de groep operations waaronder het maken en updates, gebruik Hallo [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7c8da-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="7c8da-137">Hallo-status van een database verplaatsen naar en van een elastische pool ophalen</span><span class="sxs-lookup"><span data-stu-id="7c8da-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="7c8da-138">Verplaatsen van een database kan duren.</span><span class="sxs-lookup"><span data-stu-id="7c8da-138">Moving a database can take time.</span></span> <span data-ttu-id="7c8da-139">De status van een verplaatsing met Hallo volgen [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7c8da-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="7c8da-140">Gegevens over brongebruik ophalen voor een elastische pool</span><span class="sxs-lookup"><span data-stu-id="7c8da-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="7c8da-141">Metrische gegevens die kunnen worden opgehaald als een percentage van de limiet van Hallo resource:</span><span class="sxs-lookup"><span data-stu-id="7c8da-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="7c8da-142">Metrische naam</span><span class="sxs-lookup"><span data-stu-id="7c8da-142">Metric name</span></span> | <span data-ttu-id="7c8da-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7c8da-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7c8da-144">CPU\_procent</span><span class="sxs-lookup"><span data-stu-id="7c8da-144">cpu\_percent</span></span> |<span data-ttu-id="7c8da-145">Gemiddelde compute-gebruik in een percentage van het Hallo-limiet van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="7c8da-146">fysieke\_gegevens\_lezen\_procent</span><span class="sxs-lookup"><span data-stu-id="7c8da-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="7c8da-147">Gemiddelde i/o-gebruik in een percentage op basis van het Hallo-limiet van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="7c8da-148">logboek\_schrijven\_procent</span><span class="sxs-lookup"><span data-stu-id="7c8da-148">log\_write\_percent</span></span> |<span data-ttu-id="7c8da-149">Gemiddelde schrijven Resourcegebruik percentage van het Hallo-limiet van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="7c8da-150">DTU\_verbruik\_procent</span><span class="sxs-lookup"><span data-stu-id="7c8da-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="7c8da-151">Gemiddelde eDTU-gebruik in een percentage van de eDTU-limiet voor het Hallo-groep</span><span class="sxs-lookup"><span data-stu-id="7c8da-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="7c8da-152">opslag\_procent</span><span class="sxs-lookup"><span data-stu-id="7c8da-152">storage\_percent</span></span> |<span data-ttu-id="7c8da-153">Gemiddelde gebruik van de opslag in een percentage van de opslaglimiet Hallo van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="7c8da-154">werknemers\_procent</span><span class="sxs-lookup"><span data-stu-id="7c8da-154">workers\_percent</span></span> |<span data-ttu-id="7c8da-155">Maximum aantal gelijktijdige werknemers (aanvragen) in een percentage op basis van het Hallo-limiet van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="7c8da-156">sessies\_procent</span><span class="sxs-lookup"><span data-stu-id="7c8da-156">sessions\_percent</span></span> |<span data-ttu-id="7c8da-157">Maximum aantal gelijktijdige sessies in een percentage op basis van het Hallo-limiet van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="7c8da-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="7c8da-158">eDTU_limit</span></span> |<span data-ttu-id="7c8da-159">Huidige elastische pool max. DTU-instelling voor deze elastische groep gedurende deze periode.</span><span class="sxs-lookup"><span data-stu-id="7c8da-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="7c8da-160">opslag\_limiet</span><span class="sxs-lookup"><span data-stu-id="7c8da-160">storage\_limit</span></span> |<span data-ttu-id="7c8da-161">Huidige max opslaglimiet elastische pool instellen voor deze elastische groep in megabytes gedurende deze periode.</span><span class="sxs-lookup"><span data-stu-id="7c8da-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="7c8da-162">eDTU\_gebruikt</span><span class="sxs-lookup"><span data-stu-id="7c8da-162">eDTU\_used</span></span> |<span data-ttu-id="7c8da-163">Gemiddelde edtu's worden gebruikt door toepassingen Hallo in dit interval.</span><span class="sxs-lookup"><span data-stu-id="7c8da-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="7c8da-164">opslag\_gebruikt</span><span class="sxs-lookup"><span data-stu-id="7c8da-164">storage\_used</span></span> |<span data-ttu-id="7c8da-165">Gemiddelde opslag gebruikt door toepassingen Hallo in dit interval in bytes</span><span class="sxs-lookup"><span data-stu-id="7c8da-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="7c8da-166">**Metrische gegevens granulatie/bewaartermijnen:**</span><span class="sxs-lookup"><span data-stu-id="7c8da-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="7c8da-167">Gegevens worden geretourneerd in samenvattingen van 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="7c8da-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="7c8da-168">Bewaren van gegevens is 35 dagen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="7c8da-169">Deze cmdlet en API beperkt Hallo aantal rijen dat in één aanroep too1000 rijen (ongeveer 3 dagen aan gegevens samenvattingen van 5 minuten) kan worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="7c8da-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="7c8da-170">Maar deze opdracht kan worden meermaals aangeroepen met verschillende beginnen of eindigen tijd intervallen tooretrieve meer gegevens</span><span class="sxs-lookup"><span data-stu-id="7c8da-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="7c8da-171">tooretrieve hello metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="7c8da-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="7c8da-172">Gegevens over brongebruik ophalen voor een database in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="7c8da-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="7c8da-173">Deze API's zijn hetzelfde als de API's gebruikt voor het bewaken van Resourcegebruik Hallo van één database, met uitzondering van de volgende semantische verschil Hallo HALLO hallo: metrische gegevens opgehaald worden uitgedrukt als percentage van Hallo per database max edtu's (of gelijkwaardige cap voor Hallo onderliggende metrische gegevens zoals CPU of i/o) ingesteld voor die groep.</span><span class="sxs-lookup"><span data-stu-id="7c8da-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="7c8da-174">Bijvoorbeeld, 50% gebruik van een van deze metrische gegevens geeft aan dat specifieke Hallo-brongebruik op 50% van Hallo per database cap limiet voor die bron in Hallo bovenliggende groep.</span><span class="sxs-lookup"><span data-stu-id="7c8da-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="7c8da-175">tooretrieve hello metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="7c8da-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="7c8da-176">Een elastische pool waarschuwing tooan resource toevoegen</span><span class="sxs-lookup"><span data-stu-id="7c8da-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="7c8da-177">U kunt regels voor waarschuwingen tooan elastische pool toosend e-mailmeldingen of tekenreeksen te waarschuwen toevoegen[URL eindpunten](https://msdn.microsoft.com/library/mt718036.aspx) wanneer de elastische groep Hallo treffers in een drempelwaarde voor overbenutting die u hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7c8da-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="7c8da-178">Hallo toevoegen AzureRmMetricAlertRule cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c8da-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c8da-179">Bewaking voor elastische pools Resourcegebruik heeft een vertraging van minstens 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="7c8da-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="7c8da-180">Instellen van waarschuwingen van minder dan 10 minuten voor elastische pools is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7c8da-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="7c8da-181">Geen waarschuwingen instellen voor elastische pools met een punt (parameter met de naam '-venstergrootte ' in PowerShell API) van minder dan 10 minuten kunnen niet worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="7c8da-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="7c8da-182">Zorg ervoor dat er waarschuwingen te definiëren voor een periode (venstergrootte) van 10 minuten of meer elastische pools niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c8da-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="7c8da-183">Dit voorbeeld wordt een waarschuwing voor het ophalen van een melding wanneer een elastische pool-eDTU-gebruik hoger dan bepaalde drempelwaarde komt is.</span><span class="sxs-lookup"><span data-stu-id="7c8da-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="7c8da-184">Zie voor meer informatie [waarschuwingen van de SQL-Database maken in Azure portal](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7c8da-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="7c8da-185">Waarschuwingen tooall databases in een elastische groep toevoegen</span><span class="sxs-lookup"><span data-stu-id="7c8da-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="7c8da-186">U kunt regels voor waarschuwingen tooall database in een elastische pool toosend e-mailmeldingen of tekenreeksen te waarschuwen toevoegen[URL eindpunten](https://msdn.microsoft.com/library/mt718036.aspx) wanneer een resource komt binnen via een drempelwaarde voor overbenutting Hallo waarschuwing instellen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c8da-187">Bewaking voor elastische pools Resourcegebruik heeft een vertraging van minstens 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="7c8da-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="7c8da-188">Instellen van waarschuwingen van minder dan 10 minuten voor elastische pools is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7c8da-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="7c8da-189">Geen waarschuwingen instellen voor elastische pools met een punt (parameter met de naam '-venstergrootte ' in PowerShell API) van minder dan 10 minuten kunnen niet worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="7c8da-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="7c8da-190">Zorg ervoor dat er waarschuwingen te definiëren voor een periode (venstergrootte) van 10 minuten of meer elastische pools niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c8da-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="7c8da-191">Dit voorbeeld wordt een waarschuwing tooeach van Hallo databases in een elastische groep voor het ophalen van een melding krijgen wanneer die database DTU-verbruik hoger dan een bepaalde drempelwaarde komt is.</span><span class="sxs-lookup"><span data-stu-id="7c8da-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="7c8da-192">Verzamelen en bewaken van gegevens over brongebruik voor meerdere toepassingen in een abonnement</span><span class="sxs-lookup"><span data-stu-id="7c8da-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="7c8da-193">Wanneer u veel databases in een abonnement hebt, is het lastig toomonitor elke elastische pool afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="7c8da-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="7c8da-194">In plaats daarvan kunnen SQL database PowerShell-cmdlets en T-SQL-query's gecombineerde toocollect gegevens over brongebruik van meerdere groepen en hun databases voor controle en analyse van Resourcegebruik zijn.</span><span class="sxs-lookup"><span data-stu-id="7c8da-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="7c8da-195">Een [Voorbeeldimplementatie](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) van dergelijke een reeks powershell-scripts vindt u in Hallo GitHub SQL Server-voorbeelden opslagplaats samen met documentatie over wat het doet en hoe toouse deze.</span><span class="sxs-lookup"><span data-stu-id="7c8da-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="7c8da-196">toouse deze voorbeeldimplementatie als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="7c8da-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="7c8da-197">Hallo downloaden [scripts en documentatie](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="7c8da-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="7c8da-198">Hallo-scripts voor uw omgeving aanpassen.</span><span class="sxs-lookup"><span data-stu-id="7c8da-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="7c8da-199">Geef een of meer servers waarop elastische pools worden gehost.</span><span class="sxs-lookup"><span data-stu-id="7c8da-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="7c8da-200">Geef een telemetrie-database waar hello verzamelde metrische gegevens toobe opgeslagen zijn.</span><span class="sxs-lookup"><span data-stu-id="7c8da-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="7c8da-201">Aanpassen Hallo script toospecify Hallo duur van Hallo-scripts worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7c8da-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="7c8da-202">Op een hoog niveau Hallo scripts Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c8da-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="7c8da-203">Alle servers in een bepaald Azure-abonnement (of een opgegeven lijst met servers) inventariseren.</span><span class="sxs-lookup"><span data-stu-id="7c8da-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="7c8da-204">Kan een achtergrondtaak voor elke server worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7c8da-204">Runs a background job for each server.</span></span> <span data-ttu-id="7c8da-205">Hallo-taak wordt uitgevoerd in een lus met regelmatige tussenpozen en worden telemetriegegevens verzameld voor alle Hallo opslaggroepen in Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="7c8da-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="7c8da-206">Hallo verzamelde gegevens worden vervolgens geladen in Hallo opgegeven telemetrie-database.</span><span class="sxs-lookup"><span data-stu-id="7c8da-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="7c8da-207">Een lijst met databases in elke groep toocollect Hallo databasegegevens over brongebruik inventariseren.</span><span class="sxs-lookup"><span data-stu-id="7c8da-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="7c8da-208">Hallo verzamelde gegevens worden vervolgens geladen in Hallo telemetrie-database.</span><span class="sxs-lookup"><span data-stu-id="7c8da-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="7c8da-209">Hallo kan verzamelde metrische gegevens in Hallo telemetrie database worden geanalyseerd toomonitor Hallo gezondheid van elastische pools en Hallo-databases in deze.</span><span class="sxs-lookup"><span data-stu-id="7c8da-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="7c8da-210">Hallo script installeert ook een vooraf gedefinieerde tabelwaarde functie (TVF) in Hallo telemetrie database toohelp cumulatieve Hallo metrische gegevens voor een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="7c8da-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="7c8da-211">Bijvoorbeeld: resultaten van Hallo TVF kunnen worden gebruikt tooshow 'top N elastische groepen met gebruik van Hallo maximale aantal edtu's in het venster van een bepaald moment.'</span><span class="sxs-lookup"><span data-stu-id="7c8da-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="7c8da-212">Eventueel analytische hulpprogramma's zoals Excel of Power BI tooquery gebruiken en analyseren van Hallo verzamelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="7c8da-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="7c8da-213">Voorbeeld: resource verbruik metrische gegevens voor een elastische groep en de databases ophalen</span><span class="sxs-lookup"><span data-stu-id="7c8da-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="7c8da-214">In dit voorbeeld haalt Hallo verbruik metrische gegevens voor een bepaalde elastische groep en alle bijbehorende databases.</span><span class="sxs-lookup"><span data-stu-id="7c8da-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="7c8da-215">Verzamelde gegevens is ingedeeld en geformatteerd tooa CSV-bestand geschreven.</span><span class="sxs-lookup"><span data-stu-id="7c8da-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="7c8da-216">Hallo-bestand kan worden gebladerd in Excel.</span><span class="sxs-lookup"><span data-stu-id="7c8da-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="7c8da-217">Latentie van bewerkingen van de elastische groep</span><span class="sxs-lookup"><span data-stu-id="7c8da-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="7c8da-218">Hallo min edtu's per database of max edtu's per database doorgaans wijzigen is voltooid in de 5 minuten of minder.</span><span class="sxs-lookup"><span data-stu-id="7c8da-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="7c8da-219">Hallo edtu's per groep wijzigen hangt af van de totale hoeveelheid ruimte die wordt gebruikt door alle databases in de groep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7c8da-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="7c8da-220">Wijzigingen duren gemiddeld 90 minuten of minder per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="7c8da-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="7c8da-221">Bijvoorbeeld, als de totale ruimte hello worden gebruikt door alle databases in de groep Hallo is 200 GB en vervolgens Hallo verwachte latentie voor het wijzigen van Hallo groeps-eDTU per pool is drie uur of minder.</span><span class="sxs-lookup"><span data-stu-id="7c8da-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="7c8da-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7c8da-222">Next steps</span></span>
* <span data-ttu-id="7c8da-223">[Elastische taken maken](sql-database-elastic-jobs-overview.md) elastische taken kunt u de T-SQL-scripts uitvoeren op een willekeurig aantal databases in Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="7c8da-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="7c8da-224">Zie [uitbreiden met Azure SQL Database](sql-database-elastic-scale-introduction.md): tooscale uit elastische hulpprogramma's gebruiken, gegevens, opvragen of transacties maken.</span><span class="sxs-lookup"><span data-stu-id="7c8da-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
