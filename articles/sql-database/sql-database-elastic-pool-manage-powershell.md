---
title: 'PowerShell: Maken en beheren van een Azure SQL elastische pool | Microsoft Docs'
description: Informatie over het gebruiken van PowerShell voor het beheren van een elastische pool.
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
ms.openlocfilehash: 5e76397c62e5a6ff7fb356bd81218c307f3fda31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="cc64d-103">Maken en beheren van een elastische pool met PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc64d-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="cc64d-104">In dit onderwerp wordt beschreven hoe u maken en beheren van schaalbare [elastische pools](sql-database-elastic-pool.md) met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc64d-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="cc64d-105">Ook kunt maken en beheren van een Azure elastische groep met de [Azure-portal](https://portal.azure.com/), REST-API of [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="cc64d-105">You can also create and manage an Azure elastic pool using the [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="cc64d-106">U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="cc64d-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="cc64d-107">Elastische pool maken</span><span class="sxs-lookup"><span data-stu-id="cc64d-107">Create an elastic pool</span></span>
<span data-ttu-id="cc64d-108">De [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet maakt een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="cc64d-108">The [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="cc64d-109">De waarden voor eDTU per pool, min. en max. dtu's worden beperkt door de waarde van de servicecategorie (Basic, Standard, Premium of Premium RS).</span><span class="sxs-lookup"><span data-stu-id="cc64d-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="cc64d-110">Zie [eDTU en opslaglimieten voor elastische pools en gegroepeerde databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="cc64d-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="cc64d-111">Maak een gegroepeerde database in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="cc64d-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="cc64d-112">Gebruik de [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)-cmdlet en stel de **ElasticPoolName**-parameter in voor de doelpool.</span><span class="sxs-lookup"><span data-stu-id="cc64d-112">Use the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="cc64d-113">Zie voor het verplaatsen van een bestaande database in een elastische pool, [verplaatsen van een database in een elastische pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="cc64d-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="cc64d-114">Script voltooien</span><span class="sxs-lookup"><span data-stu-id="cc64d-114">Complete script</span></span>
<span data-ttu-id="cc64d-115">Dit script maakt een Azure-resourcegroep en een server.</span><span class="sxs-lookup"><span data-stu-id="cc64d-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="cc64d-116">Als dit wordt gevraagd, geeft u een gebruikersnaam voor de beheerder op en een wachtwoord voor de nieuwe server (niet uw Azure-referenties).</span><span class="sxs-lookup"><span data-stu-id="cc64d-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="cc64d-117">Een elastische pool maken en toevoegen van meerdere gegroepeerde databases</span><span class="sxs-lookup"><span data-stu-id="cc64d-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="cc64d-118">Maken van veel databases in een elastische pool kan duren wanneer het wordt gedaan via de portal of PowerShell-cmdlets die slechts één database tegelijkertijd maken.</span><span class="sxs-lookup"><span data-stu-id="cc64d-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="cc64d-119">Als u wilt maken voor een elastische pool automatiseren, Zie [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="cc64d-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="cc64d-120">Een database verplaatsen naar een elastische pool</span><span class="sxs-lookup"><span data-stu-id="cc64d-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="cc64d-121">U kunt een database verplaatsen van of naar een elastische groep met de [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="cc64d-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="cc64d-122">Instellingen van de prestaties van een elastische groep wijzigen</span><span class="sxs-lookup"><span data-stu-id="cc64d-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="cc64d-123">Wanneer de prestaties te lijden heeft onder, kunt u de instellingen van de groep van toepassingen voor groei.</span><span class="sxs-lookup"><span data-stu-id="cc64d-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="cc64d-124">Gebruik de [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cc64d-124">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="cc64d-125">Stel de parameter - Dtu op de edtu's per groep.</span><span class="sxs-lookup"><span data-stu-id="cc64d-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="cc64d-126">Zie [eDTU en opslaglimieten](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor mogelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="cc64d-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="cc64d-127">De opslaglimiet voor een elastische groep wijzigen</span><span class="sxs-lookup"><span data-stu-id="cc64d-127">Change the storage limit for an elastic pool</span></span>

<span data-ttu-id="cc64d-128">Gebruik de [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet om in te stellen de _- StorageMB_ parameter.</span><span class="sxs-lookup"><span data-stu-id="cc64d-128">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet to set the _-StorageMB_ parameter.</span></span> <span data-ttu-id="cc64d-129">Geef de opslaglimiet in MB (bijvoorbeeld 2097152 sets de opslag beperken tot 2 TB).</span><span class="sxs-lookup"><span data-stu-id="cc64d-129">Provide the storage limit in MB (for example, 2097152 sets the storage limit to 2 TB).</span></span> <span data-ttu-id="cc64d-130">Zie [eDTU en opslaglimieten](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor mogelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="cc64d-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc64d-131">De standaard maximale gegevensopslag per groep voor Premium-groepen met edtu's 1500 of meer is dan 750 GB.</span><span class="sxs-lookup"><span data-stu-id="cc64d-131">The default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="cc64d-132">Verkrijgen van de hogere _maximale opslaggrootte van de gegevens per groep_, de opslaglimiet moet expliciet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cc64d-132">To obtain the higher _max data storage size per pool_, the storage limit must be explicitly set.</span></span> <span data-ttu-id="cc64d-133">Premium-adresgroepen met meer dan 750 GB aan opslagruimte bevindt zich momenteel in de openbare preview in de volgende gebieden: VS-Oost 2, VS-West, Gov ons Virginia, West-Europa, Duitsland centraal, Zuidoost-Azië, Japan-Oost, Australië-Oost, Canada centraal en Canada-Oost.</span><span class="sxs-lookup"><span data-stu-id="cc64d-133">Premium pools with more than 750 GB of storage is currently in public preview in the following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="cc64d-134">De status van de bewerkingen van toepassingen niet ophalen</span><span class="sxs-lookup"><span data-stu-id="cc64d-134">Get the status of pool operations</span></span>
<span data-ttu-id="cc64d-135">Maken van een elastische pool kan tijd duren.</span><span class="sxs-lookup"><span data-stu-id="cc64d-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="cc64d-136">Om bij te houden de status van toepassingen bewerkingen, inclusief het maken en -updates, gebruiken de [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cc64d-136">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="cc64d-137">De status van een database verplaatsen naar en van een elastische pool ophalen</span><span class="sxs-lookup"><span data-stu-id="cc64d-137">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="cc64d-138">Verplaatsen van een database kan duren.</span><span class="sxs-lookup"><span data-stu-id="cc64d-138">Moving a database can take time.</span></span> <span data-ttu-id="cc64d-139">Bijhouden van een verplaatsing status met het [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cc64d-139">Track a move status using the [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="cc64d-140">Gegevens over brongebruik ophalen voor een elastische pool</span><span class="sxs-lookup"><span data-stu-id="cc64d-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="cc64d-141">Metrische gegevens die kunnen worden opgehaald als een percentage van de limiet van de resource:</span><span class="sxs-lookup"><span data-stu-id="cc64d-141">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>

| <span data-ttu-id="cc64d-142">Metrische naam</span><span class="sxs-lookup"><span data-stu-id="cc64d-142">Metric name</span></span> | <span data-ttu-id="cc64d-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cc64d-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cc64d-144">CPU\_procent</span><span class="sxs-lookup"><span data-stu-id="cc64d-144">cpu\_percent</span></span> |<span data-ttu-id="cc64d-145">Gemiddelde compute-gebruik in een percentage van de limiet van de groep.</span><span class="sxs-lookup"><span data-stu-id="cc64d-145">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="cc64d-146">fysieke\_gegevens\_lezen\_procent</span><span class="sxs-lookup"><span data-stu-id="cc64d-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="cc64d-147">Gemiddelde i/o-gebruik in een percentage op basis van de limiet van de groep.</span><span class="sxs-lookup"><span data-stu-id="cc64d-147">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="cc64d-148">logboek\_schrijven\_procent</span><span class="sxs-lookup"><span data-stu-id="cc64d-148">log\_write\_percent</span></span> |<span data-ttu-id="cc64d-149">Gemiddelde schrijven bronnen beter worden benut als percentage van de limiet van de groep.</span><span class="sxs-lookup"><span data-stu-id="cc64d-149">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="cc64d-150">DTU\_verbruik\_procent</span><span class="sxs-lookup"><span data-stu-id="cc64d-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="cc64d-151">Gemiddelde eDTU-gebruik in een percentage van de eDTU-limiet voor de pool</span><span class="sxs-lookup"><span data-stu-id="cc64d-151">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="cc64d-152">opslag\_procent</span><span class="sxs-lookup"><span data-stu-id="cc64d-152">storage\_percent</span></span> |<span data-ttu-id="cc64d-153">Gemiddelde gebruik van de opslag in een percentage van de opslaglimiet van de groep.</span><span class="sxs-lookup"><span data-stu-id="cc64d-153">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="cc64d-154">werknemers\_procent</span><span class="sxs-lookup"><span data-stu-id="cc64d-154">workers\_percent</span></span> |<span data-ttu-id="cc64d-155">Maximum aantal gelijktijdige werknemers (aanvragen) in een percentage op basis van de limiet van de groep.</span><span class="sxs-lookup"><span data-stu-id="cc64d-155">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="cc64d-156">sessies\_procent</span><span class="sxs-lookup"><span data-stu-id="cc64d-156">sessions\_percent</span></span> |<span data-ttu-id="cc64d-157">Maximum aantal gelijktijdige sessies in een percentage op basis van de limiet van de groep.</span><span class="sxs-lookup"><span data-stu-id="cc64d-157">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="cc64d-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="cc64d-158">eDTU_limit</span></span> |<span data-ttu-id="cc64d-159">Huidige elastische pool max. DTU-instelling voor deze elastische groep gedurende deze periode.</span><span class="sxs-lookup"><span data-stu-id="cc64d-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="cc64d-160">opslag\_limiet</span><span class="sxs-lookup"><span data-stu-id="cc64d-160">storage\_limit</span></span> |<span data-ttu-id="cc64d-161">Huidige max opslaglimiet elastische pool instellen voor deze elastische groep in megabytes gedurende deze periode.</span><span class="sxs-lookup"><span data-stu-id="cc64d-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="cc64d-162">eDTU\_gebruikt</span><span class="sxs-lookup"><span data-stu-id="cc64d-162">eDTU\_used</span></span> |<span data-ttu-id="cc64d-163">Gemiddelde edtu's worden gebruikt door de toepassingen in dit interval.</span><span class="sxs-lookup"><span data-stu-id="cc64d-163">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="cc64d-164">opslag\_gebruikt</span><span class="sxs-lookup"><span data-stu-id="cc64d-164">storage\_used</span></span> |<span data-ttu-id="cc64d-165">Gemiddelde opslag gebruikt door de toepassingen in dit interval in bytes</span><span class="sxs-lookup"><span data-stu-id="cc64d-165">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="cc64d-166">**Metrische gegevens granulatie/bewaartermijnen:**</span><span class="sxs-lookup"><span data-stu-id="cc64d-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="cc64d-167">Gegevens worden geretourneerd in samenvattingen van 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="cc64d-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="cc64d-168">Bewaren van gegevens is 35 dagen.</span><span class="sxs-lookup"><span data-stu-id="cc64d-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="cc64d-169">Deze cmdlet en API beperkt het aantal rijen dat in één aanroep van 1000 rijen (ongeveer 3 dagen aan gegevens samenvattingen van 5 minuten) kan worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="cc64d-169">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="cc64d-170">Maar deze opdracht kan worden aangeroepen meerdere keren met verschillende beginnen of eindigen tijdsintervallen meer gegevens op te halen</span><span class="sxs-lookup"><span data-stu-id="cc64d-170">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="cc64d-171">Voor het ophalen van de metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="cc64d-171">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="cc64d-172">Gegevens over brongebruik ophalen voor een database in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="cc64d-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="cc64d-173">Deze API's zijn hetzelfde als de API's gebruikt voor het bewaken van het Resourcegebruik van één database, met uitzondering van de volgende semantische verschil: metrische gegevens opgehaald worden uitgedrukt als percentage van de per database max edtu's (of gelijkwaardige cap voor de onderliggende metrische gegevens zoals CPU of i/o) ingesteld voor die groep.</span><span class="sxs-lookup"><span data-stu-id="cc64d-173">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="cc64d-174">Bijvoorbeeld: 50% gebruik van een van deze metrische gegevens geeft aan dat het specifieke brongebruik op 50% van de database cap limiet voor die bron in de bovenliggende groep per.</span><span class="sxs-lookup"><span data-stu-id="cc64d-174">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="cc64d-175">Voor het ophalen van de metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="cc64d-175">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="cc64d-176">Een waarschuwing toevoegen aan een resource voor de elastische groep</span><span class="sxs-lookup"><span data-stu-id="cc64d-176">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="cc64d-177">U kunt regels voor waarschuwingen toevoegen aan een elastische pool verzenden van e-mailmeldingen of waarschuwing tekenreeksen die moeten [URL eindpunten](https://msdn.microsoft.com/library/mt718036.aspx) wanneer de elastische groep treffers in een drempelwaarde voor overbenutting die u hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cc64d-177">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="cc64d-178">Gebruik de cmdlet Add-AzureRmMetricAlertRule.</span><span class="sxs-lookup"><span data-stu-id="cc64d-178">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc64d-179">Bewaking voor elastische pools Resourcegebruik heeft een vertraging van minstens 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="cc64d-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="cc64d-180">Instellen van waarschuwingen van minder dan 10 minuten voor elastische pools is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cc64d-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="cc64d-181">Geen waarschuwingen instellen voor elastische pools met een punt (parameter met de naam '-venstergrootte ' in PowerShell API) van minder dan 10 minuten kunnen niet worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="cc64d-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="cc64d-182">Zorg ervoor dat er waarschuwingen te definiëren voor een periode (venstergrootte) van 10 minuten of meer elastische pools niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cc64d-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="cc64d-183">Dit voorbeeld wordt een waarschuwing voor het ophalen van een melding wanneer een elastische pool-eDTU-gebruik hoger dan bepaalde drempelwaarde komt is.</span><span class="sxs-lookup"><span data-stu-id="cc64d-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

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

<span data-ttu-id="cc64d-184">Zie voor meer informatie [waarschuwingen van de SQL-Database maken in Azure portal](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cc64d-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="cc64d-185">Meldingen op alle databases in een elastische groep toevoegen</span><span class="sxs-lookup"><span data-stu-id="cc64d-185">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="cc64d-186">U kunt regels voor waarschuwingen toevoegen aan alle database in een elastische pool verzenden van e-mailmeldingen of waarschuwing tekenreeksen die moeten [URL eindpunten](https://msdn.microsoft.com/library/mt718036.aspx) wanneer een resource komt binnen via een drempelwaarde voor overbenutting instellen door de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="cc64d-186">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc64d-187">Bewaking voor elastische pools Resourcegebruik heeft een vertraging van minstens 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="cc64d-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="cc64d-188">Instellen van waarschuwingen van minder dan 10 minuten voor elastische pools is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cc64d-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="cc64d-189">Geen waarschuwingen instellen voor elastische pools met een punt (parameter met de naam '-venstergrootte ' in PowerShell API) van minder dan 10 minuten kunnen niet worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="cc64d-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="cc64d-190">Zorg ervoor dat er waarschuwingen te definiëren voor een periode (venstergrootte) van 10 minuten of meer elastische pools niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cc64d-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="cc64d-191">In dit voorbeeld wordt een waarschuwing toegevoegd aan elk van de databases in een elastische groep voor het ophalen van een melding krijgen wanneer die database DTU-verbruik hoger dan een bepaalde drempelwaarde komt is.</span><span class="sxs-lookup"><span data-stu-id="cc64d-191">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="cc64d-192">Verzamelen en bewaken van gegevens over brongebruik voor meerdere toepassingen in een abonnement</span><span class="sxs-lookup"><span data-stu-id="cc64d-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="cc64d-193">Wanneer u veel databases in een abonnement hebt, is het lastig voor het bewaken van elke elastische pool afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="cc64d-193">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="cc64d-194">In plaats daarvan kunnen SQL database PowerShell-cmdlets en T-SQL-query's worden gecombineerd voor het verzamelen van gegevens over brongebruik van meerdere groepen en hun databases voor controle en analyse van Resourcegebruik.</span><span class="sxs-lookup"><span data-stu-id="cc64d-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="cc64d-195">Een [Voorbeeldimplementatie](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) van dergelijke een reeks powershell-scripts vindt u in de opslagplaats GitHub SQL Server-voorbeelden samen met de documentatie op hoe het werkt en het gebruik ervan.</span><span class="sxs-lookup"><span data-stu-id="cc64d-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="cc64d-196">Volg deze stappen voor het gebruik van deze voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="cc64d-196">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="cc64d-197">Download de [scripts en documentatie](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="cc64d-197">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="cc64d-198">Wijzig de scripts voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="cc64d-198">Modify the scripts for your environment.</span></span> <span data-ttu-id="cc64d-199">Geef een of meer servers waarop elastische pools worden gehost.</span><span class="sxs-lookup"><span data-stu-id="cc64d-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="cc64d-200">Geef een telemetrie-database waar de verzamelde metrische gegevens zullen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cc64d-200">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="cc64d-201">Pas het script voor het opgeven van de duur van de de scripts worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc64d-201">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="cc64d-202">Op een hoog niveau doen de scripts het volgende:</span><span class="sxs-lookup"><span data-stu-id="cc64d-202">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="cc64d-203">Alle servers in een bepaald Azure-abonnement (of een opgegeven lijst met servers) inventariseren.</span><span class="sxs-lookup"><span data-stu-id="cc64d-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="cc64d-204">Kan een achtergrondtaak voor elke server worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc64d-204">Runs a background job for each server.</span></span> <span data-ttu-id="cc64d-205">De taak wordt uitgevoerd in een lus met regelmatige tussenpozen en verzamelt telemetriegegevens voor alle toepassingen op de server.</span><span class="sxs-lookup"><span data-stu-id="cc64d-205">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="cc64d-206">Vervolgens worden de verzamelde gegevens geladen in de opgegeven telemetrie-database.</span><span class="sxs-lookup"><span data-stu-id="cc64d-206">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="cc64d-207">Een lijst met databases in elke groep voor het verzamelen van de gegevens over brongebruik database inventariseren.</span><span class="sxs-lookup"><span data-stu-id="cc64d-207">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="cc64d-208">Vervolgens worden de verzamelde gegevens geladen in de telemetrie-database.</span><span class="sxs-lookup"><span data-stu-id="cc64d-208">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="cc64d-209">De verzamelde metrische gegevens in de telemetrie-database kunnen worden geanalyseerd om te controleren van de status van elastische pools en de databases in deze.</span><span class="sxs-lookup"><span data-stu-id="cc64d-209">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="cc64d-210">Het script installeert ook een vooraf gedefinieerde tabelwaarde functie (TVF) in de database telemetrie om u te helpen aggregatie de metrische gegevens voor een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="cc64d-210">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="cc64d-211">Resultaten van de TVF kunnen bijvoorbeeld worden gebruikt om weer te geven 'top N elastische groepen met het gebruik van het maximale aantal edtu's in het venster van een bepaald moment.'</span><span class="sxs-lookup"><span data-stu-id="cc64d-211">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="cc64d-212">Gebruik eventueel analytische hulpprogramma's zoals Excel of Power BI een query en analyseren van de verzamelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="cc64d-212">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="cc64d-213">Voorbeeld: resource verbruik metrische gegevens voor een elastische groep en de databases ophalen</span><span class="sxs-lookup"><span data-stu-id="cc64d-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="cc64d-214">In dit voorbeeld wordt de verbruik metrische gegevens voor een bepaalde elastische groep en alle bijbehorende databases opgehaald.</span><span class="sxs-lookup"><span data-stu-id="cc64d-214">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="cc64d-215">Verzamelde gegevens is ingedeeld en geschreven naar een geformatteerde CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="cc64d-215">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="cc64d-216">Het bestand kan worden gebladerd in Excel.</span><span class="sxs-lookup"><span data-stu-id="cc64d-216">The file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login to Azure account and select the subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for the specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format the metrics and output as .csv file using the following script block.
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

# Output the metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="cc64d-217">Latentie van bewerkingen van de elastische groep</span><span class="sxs-lookup"><span data-stu-id="cc64d-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="cc64d-218">Doorgaans wijzigen van de edtu min's per database of max edtu's per database is voltooid in de 5 minuten of minder.</span><span class="sxs-lookup"><span data-stu-id="cc64d-218">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="cc64d-219">Het wijzigen van de edtu's per groep, is afhankelijk van de totale hoeveelheid ruimte die wordt gebruikt door alle databases in de groep.</span><span class="sxs-lookup"><span data-stu-id="cc64d-219">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="cc64d-220">Wijzigingen duren gemiddeld 90 minuten of minder per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="cc64d-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="cc64d-221">Bijvoorbeeld, als de totale ruimte gebruikt door alle databases in de pool is 200 GB, dan is de verwachte latentie voor het wijzigen van de groeps-eDTU per pool drie uur of minder.</span><span class="sxs-lookup"><span data-stu-id="cc64d-221">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="cc64d-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc64d-222">Next steps</span></span>
* <span data-ttu-id="cc64d-223">[Elastische taken maken](sql-database-elastic-jobs-overview.md) Met elastische taken kunt u de T-SQL-scripts uitvoeren op een willekeurig aantal databases in de pool.</span><span class="sxs-lookup"><span data-stu-id="cc64d-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="cc64d-224">Zie [uitbreiden met Azure SQL Database](sql-database-elastic-scale-introduction.md): gebruik elastische hulpprogramma's om te worden uitgebreid, gegevens, opvragen of transacties maken.</span><span class="sxs-lookup"><span data-stu-id="cc64d-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
