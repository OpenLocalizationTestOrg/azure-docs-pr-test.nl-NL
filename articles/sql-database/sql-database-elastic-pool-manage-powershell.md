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
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Maken en beheren van een elastische pool met PowerShell
Dit onderwerp leest u hoe toocreate en beheren van schaalbare [elastische pools](sql-database-elastic-pool.md) met PowerShell.  U kunt ook maken en beheren van een Azure elastische pool met Hallo [Azure-portal](https://portal.azure.com/), REST-API of [C#](sql-database-elastic-pool-manage-csharp.md). U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Elastische pool maken
Hallo [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet maakt een elastische pool. Hallo-waarden voor eDTU per pool, min. en max. dtu's worden beperkt door Hallo service tier waarde (Basic, Standard, Premium of Premium RS). Zie [eDTU en opslaglimieten voor elastische pools en gegroepeerde databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Maak een gegroepeerde database in een elastische pool
Gebruik Hallo [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet en set Hallo **ElasticPoolName** parameter toohello doelgroep. Zie voor een bestaande database in een elastische pool toomove [verplaatsen van een database in een elastische pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Script voltooien
Dit script maakt een Azure-resourcegroep en een server. Als u wordt gevraagd, geeft u een gebruikersnaam voor de beheerder en het wachtwoord voor Hallo nieuwe server (niet uw Azure-referenties).

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Een elastische pool maken en toevoegen van meerdere gegroepeerde databases
Maken van veel databases in een elastische pool kan duren wanneer klaar met Hallo portal of PowerShell-cmdlets die slechts één database tegelijkertijd maken. Zie tooautomate maken voor een elastische pool [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Een database verplaatsen naar een elastische pool
U kunt een database verplaatsen van of naar een elastische groep met Hallo [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Instellingen van de prestaties van een elastische groep wijzigen
Wanneer de prestaties te lijden heeft onder, kunt u instellingen Hallo Hallo groep tooaccommodate groei kunt wijzigen. Gebruik Hallo [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet. Hallo - Dtu parameter toohello edtu's per groep ingesteld. Zie [eDTU en opslaglimieten](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor mogelijke waarden.

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>De opslaglimiet Hallo voor een elastische groep wijzigen

Gebruik Hallo [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _- StorageMB_ parameter. Geef de opslaglimiet Hallo in MB (bijvoorbeeld 2097152 sets Hallo opslag limiet too2 TB). Zie [eDTU en opslaglimieten](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor mogelijke waarden.

> [!IMPORTANT]
> Hallo standaard maximale gegevensopslag per groep voor Premium-groepen met edtu's 1500 of meer is dan 750 GB. tooobtain hello hoger _maximale opslaggrootte van de gegevens per groep_, Hallo opslaglimiet moet expliciet worden ingesteld. Premium-adresgroepen met meer dan 750 GB aan opslagruimte bevindt zich momenteel in de openbare preview in Hallo gebieden te volgen: VS-Oost 2, VS-West, Gov ons Virginia, West-Europa, Duitsland centraal, Zuidoost-Azië, Japan-Oost, Australië-Oost, Canada centraal en Canada-Oost.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>Hallo-status van de groep operations ophalen
Maken van een elastische pool kan tijd duren. tootrack hello status van de groep operations waaronder het maken en updates, gebruik Hallo [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Hallo-status van een database verplaatsen naar en van een elastische pool ophalen
Verplaatsen van een database kan duren. De status van een verplaatsing met Hallo volgen [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Gegevens over brongebruik ophalen voor een elastische pool
Metrische gegevens die kunnen worden opgehaald als een percentage van de limiet van Hallo resource:

| Metrische naam | Beschrijving |
|:--- |:--- |
| CPU\_procent |Gemiddelde compute-gebruik in een percentage van het Hallo-limiet van Hallo van toepassingen. |
| fysieke\_gegevens\_lezen\_procent |Gemiddelde i/o-gebruik in een percentage op basis van het Hallo-limiet van Hallo van toepassingen. |
| logboek\_schrijven\_procent |Gemiddelde schrijven Resourcegebruik percentage van het Hallo-limiet van Hallo van toepassingen. |
| DTU\_verbruik\_procent |Gemiddelde eDTU-gebruik in een percentage van de eDTU-limiet voor het Hallo-groep |
| opslag\_procent |Gemiddelde gebruik van de opslag in een percentage van de opslaglimiet Hallo van Hallo van toepassingen. |
| werknemers\_procent |Maximum aantal gelijktijdige werknemers (aanvragen) in een percentage op basis van het Hallo-limiet van Hallo van toepassingen. |
| sessies\_procent |Maximum aantal gelijktijdige sessies in een percentage op basis van het Hallo-limiet van Hallo van toepassingen. |
| eDTU_limit |Huidige elastische pool max. DTU-instelling voor deze elastische groep gedurende deze periode. |
| opslag\_limiet |Huidige max opslaglimiet elastische pool instellen voor deze elastische groep in megabytes gedurende deze periode. |
| eDTU\_gebruikt |Gemiddelde edtu's worden gebruikt door toepassingen Hallo in dit interval. |
| opslag\_gebruikt |Gemiddelde opslag gebruikt door toepassingen Hallo in dit interval in bytes |

**Metrische gegevens granulatie/bewaartermijnen:**

* Gegevens worden geretourneerd in samenvattingen van 5 minuten.  
* Bewaren van gegevens is 35 dagen.  

Deze cmdlet en API beperkt Hallo aantal rijen dat in één aanroep too1000 rijen (ongeveer 3 dagen aan gegevens samenvattingen van 5 minuten) kan worden opgehaald. Maar deze opdracht kan worden meermaals aangeroepen met verschillende beginnen of eindigen tijd intervallen tooretrieve meer gegevens

tooretrieve hello metrische gegevens:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Gegevens over brongebruik ophalen voor een database in een elastische pool
Deze API's zijn hetzelfde als de API's gebruikt voor het bewaken van Resourcegebruik Hallo van één database, met uitzondering van de volgende semantische verschil Hallo HALLO hallo: metrische gegevens opgehaald worden uitgedrukt als percentage van Hallo per database max edtu's (of gelijkwaardige cap voor Hallo onderliggende metrische gegevens zoals CPU of i/o) ingesteld voor die groep. Bijvoorbeeld, 50% gebruik van een van deze metrische gegevens geeft aan dat specifieke Hallo-brongebruik op 50% van Hallo per database cap limiet voor die bron in Hallo bovenliggende groep.

tooretrieve hello metrische gegevens:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Een elastische pool waarschuwing tooan resource toevoegen
U kunt regels voor waarschuwingen tooan elastische pool toosend e-mailmeldingen of tekenreeksen te waarschuwen toevoegen[URL eindpunten](https://msdn.microsoft.com/library/mt718036.aspx) wanneer de elastische groep Hallo treffers in een drempelwaarde voor overbenutting die u hebt ingesteld. Hallo toevoegen AzureRmMetricAlertRule cmdlet gebruiken.

> [!IMPORTANT]
> Bewaking voor elastische pools Resourcegebruik heeft een vertraging van minstens 5 minuten. Instellen van waarschuwingen van minder dan 10 minuten voor elastische pools is momenteel niet ondersteund. Geen waarschuwingen instellen voor elastische pools met een punt (parameter met de naam '-venstergrootte ' in PowerShell API) van minder dan 10 minuten kunnen niet worden geactiveerd. Zorg ervoor dat er waarschuwingen te definiëren voor een periode (venstergrootte) van 10 minuten of meer elastische pools niet gebruiken.
>
>

Dit voorbeeld wordt een waarschuwing voor het ophalen van een melding wanneer een elastische pool-eDTU-gebruik hoger dan bepaalde drempelwaarde komt is.

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

Zie voor meer informatie [waarschuwingen van de SQL-Database maken in Azure portal](sql-database-insights-alerts-portal.md).

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>Waarschuwingen tooall databases in een elastische groep toevoegen
U kunt regels voor waarschuwingen tooall database in een elastische pool toosend e-mailmeldingen of tekenreeksen te waarschuwen toevoegen[URL eindpunten](https://msdn.microsoft.com/library/mt718036.aspx) wanneer een resource komt binnen via een drempelwaarde voor overbenutting Hallo waarschuwing instellen.

> [!IMPORTANT]
> Bewaking voor elastische pools Resourcegebruik heeft een vertraging van minstens 5 minuten. Instellen van waarschuwingen van minder dan 10 minuten voor elastische pools is momenteel niet ondersteund. Geen waarschuwingen instellen voor elastische pools met een punt (parameter met de naam '-venstergrootte ' in PowerShell API) van minder dan 10 minuten kunnen niet worden geactiveerd. Zorg ervoor dat er waarschuwingen te definiëren voor een periode (venstergrootte) van 10 minuten of meer elastische pools niet gebruiken.
>

Dit voorbeeld wordt een waarschuwing tooeach van Hallo databases in een elastische groep voor het ophalen van een melding krijgen wanneer die database DTU-verbruik hoger dan een bepaalde drempelwaarde komt is.

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

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Verzamelen en bewaken van gegevens over brongebruik voor meerdere toepassingen in een abonnement
Wanneer u veel databases in een abonnement hebt, is het lastig toomonitor elke elastische pool afzonderlijk. In plaats daarvan kunnen SQL database PowerShell-cmdlets en T-SQL-query's gecombineerde toocollect gegevens over brongebruik van meerdere groepen en hun databases voor controle en analyse van Resourcegebruik zijn. Een [Voorbeeldimplementatie](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) van dergelijke een reeks powershell-scripts vindt u in Hallo GitHub SQL Server-voorbeelden opslagplaats samen met documentatie over wat het doet en hoe toouse deze.

toouse deze voorbeeldimplementatie als volgt te werk.

1. Hallo downloaden [scripts en documentatie](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Hallo-scripts voor uw omgeving aanpassen. Geef een of meer servers waarop elastische pools worden gehost.
3. Geef een telemetrie-database waar hello verzamelde metrische gegevens toobe opgeslagen zijn.
4. Aanpassen Hallo script toospecify Hallo duur van Hallo-scripts worden uitgevoerd.

Op een hoog niveau Hallo scripts Hallo te volgen:

* Alle servers in een bepaald Azure-abonnement (of een opgegeven lijst met servers) inventariseren.
* Kan een achtergrondtaak voor elke server worden uitgevoerd. Hallo-taak wordt uitgevoerd in een lus met regelmatige tussenpozen en worden telemetriegegevens verzameld voor alle Hallo opslaggroepen in Hallo-server. Hallo verzamelde gegevens worden vervolgens geladen in Hallo opgegeven telemetrie-database.
* Een lijst met databases in elke groep toocollect Hallo databasegegevens over brongebruik inventariseren. Hallo verzamelde gegevens worden vervolgens geladen in Hallo telemetrie-database.

Hallo kan verzamelde metrische gegevens in Hallo telemetrie database worden geanalyseerd toomonitor Hallo gezondheid van elastische pools en Hallo-databases in deze. Hallo script installeert ook een vooraf gedefinieerde tabelwaarde functie (TVF) in Hallo telemetrie database toohelp cumulatieve Hallo metrische gegevens voor een opgegeven periode. Bijvoorbeeld: resultaten van Hallo TVF kunnen worden gebruikt tooshow 'top N elastische groepen met gebruik van Hallo maximale aantal edtu's in het venster van een bepaald moment.' Eventueel analytische hulpprogramma's zoals Excel of Power BI tooquery gebruiken en analyseren van Hallo verzamelde gegevens.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Voorbeeld: resource verbruik metrische gegevens voor een elastische groep en de databases ophalen
In dit voorbeeld haalt Hallo verbruik metrische gegevens voor een bepaalde elastische groep en alle bijbehorende databases. Verzamelde gegevens is ingedeeld en geformatteerd tooa CSV-bestand geschreven. Hallo-bestand kan worden gebladerd in Excel.

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

## <a name="latency-of-elastic-pool-operations"></a>Latentie van bewerkingen van de elastische groep
* Hallo min edtu's per database of max edtu's per database doorgaans wijzigen is voltooid in de 5 minuten of minder.
* Hallo edtu's per groep wijzigen hangt af van de totale hoeveelheid ruimte die wordt gebruikt door alle databases in de groep Hallo Hallo. Wijzigingen duren gemiddeld 90 minuten of minder per 100 GB. Bijvoorbeeld, als de totale ruimte hello worden gebruikt door alle databases in de groep Hallo is 200 GB en vervolgens Hallo verwachte latentie voor het wijzigen van Hallo groeps-eDTU per pool is drie uur of minder.



## <a name="next-steps"></a>Volgende stappen
* [Elastische taken maken](sql-database-elastic-jobs-overview.md) elastische taken kunt u de T-SQL-scripts uitvoeren op een willekeurig aantal databases in Hallo-groep.
* Zie [uitbreiden met Azure SQL Database](sql-database-elastic-scale-introduction.md): tooscale uit elastische hulpprogramma's gebruiken, gegevens, opvragen of transacties maken.
