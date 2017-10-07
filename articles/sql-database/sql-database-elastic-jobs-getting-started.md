---
title: aaaGetting gestart met elastische database taken | Microsoft Docs
description: hoe toouse elastische database taken
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a>Aan de slag met taken voor elastische Database
Elastische Database-taken (preview) voor Azure SQL Database, u tooreliability kunt T-SQL-scripts die meerdere databases omvatten tijdens het automatisch opnieuw uitvoeren en geven de uiteindelijke voltooiing wordt gegarandeerd. Zie voor meer informatie over Hallo elastische Database taak functie Hallo [overzicht functiepagina](sql-database-elastic-jobs-overview.md).

In dit onderwerp breidt Hallo voorbeeld gevonden in [aan de slag met hulpprogramma's voor elastische Database](sql-database-elastic-scale-get-started.md). Wanneer voltooid, wordt u: meer informatie over hoe toocreate en beheren van taken die een groep verwante databases beheren. Het is niet vereist toouse Hallo elastische Schaalfunctionaliteit van hulpprogramma's in volgorde tootake profiteren van Hallo voordelen van elastische taken.

## <a name="prerequisites"></a>Vereisten
Downloaden en uitvoeren van Hallo [aan de slag met elastische Database extra voorbeeld](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Een shard-toewijzing manager met Hallo voorbeeld-app maken
Hier maakt u een shard-toewijzing manager samen met enkele shards, gevolgd door het invoegen van gegevens in Hallo shards. Als u al shards instellen met gedeelde gegevens bevat, kunt u overslaan Hallo stappen te volgen en verplaatsen van de volgende sectie toohello.

1. Bouwen en uitvoeren van Hallo **aan de slag met hulpprogramma's voor elastische Database** voorbeeldtoepassing. Hallo stappen tot stap 7 in de sectie Hallo [Hallo voorbeeld-app downloaden en uitvoeren](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Aan het einde van de Hallo van stap 7 ziet u Hallo na de opdrachtprompt:

   ![opdrachtprompt](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. In het opdrachtvenster hello, typ '1' en druk op **Enter**. Dit maakt Hallo shard-toewijzing manager en voegt u twee shards toohello-server. Vervolgens typt u "3" en druk op **Enter**; deze actie vier keer herhalen. Dit invoegen voorbeeld gegevensrijen in uw shards.
3. Hallo [Azure Portal](https://portal.azure.com) drie nieuwe databases moeten worden weergegeven:

   ![Visual Studio-bevestiging](./media/sql-database-elastic-query-getting-started/portal.png)

   We gaan nu een verzameling aangepaste database die overeenkomt met alle Hallo-databases in de shard-toewijzing Hallo maken. Hiermee kunnen we toocreate en uitvoeren van een taak die een nieuwe tabel toevoegen via shards.

Hier zou meestal maken we een doel shard-toewijzing met Hallo **nieuw AzureSqlJobTarget** cmdlet. Hallo shard kaart manager-database moet worden ingesteld als het doel van een database en vervolgens Hallo specifieke shard-toewijzing is opgegeven als een doel. We gaan tooenumerate alle Hallo-databases in Hallo-server zijn en Hallo databases toohello nieuwe aangepaste verzameling met uitzondering van de database master Hallo toevoegen.

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a>Hiermee maakt u een aangepaste verzameling en voegt u alle databases in Hallo server toohello aangepaste verzameling doel met uitzondering van master Hallo.
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Maken van een T-SQL-Script voor uitvoering tussen databases
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a>Hallo taak tooexecute een script maken via de aangepaste groep Hallo van databases

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a>Hallo-taak uitgevoerd
Hallo volgende PowerShell-script kan gebruikte tooexecute een bestaande taak zijn:

Hallo variabele tooreflect Hallo gewenst taak naam toohave uitgevoerd na bijwerken:

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a>Hallo-status van het uitvoeren van een enkele taak ophalen
Gebruik dezelfde Hallo **Get-AzureSqlJobExecution** cmdlet Hello **voor IncludeChildren** namelijk Hallo specifieke status voor elke taak uitvoeren voor elke parameter tooview Hallo status van onderliggende taak uitvoeringen, de database is gericht door Hallo-taak.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a>Hallo weergavestatus over meerdere taak uitvoeringen
Hallo **Get-AzureSqlJobExecution** cmdlet heeft meerdere optionele parameters die gebruikt toodisplay worden kunnen meerdere taak uitvoeringen, gefilterd via Hallo opgegeven parameters. Hallo hieronder toont een aantal Hallo mogelijke manieren toouse Get-AzureSqlJobExecution:

Alle actieve taken voor de bovenste niveau uitvoeringen ophalen:

   ```
    Get-AzureSqlJobExecution
   ```

Alle bovenste niveau taak uitvoeringen, met inbegrip van niet-actieve taak uitvoeringen ophalen:

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

Alle onderliggende taak uitvoeringen van een opgegeven taak uitvoerings-ID, met inbegrip van niet-actieve taak uitvoeringen ophalen:

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

Ophalen van alle taak uitvoeringen gemaakt met behulp van een planning / taak combinatie, met inbegrip van niet-actieve taken:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

Alle taken die gericht is op een opgegeven shard-kaart, inclusief niet-actieve taken worden opgehaald:

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Alle taken die gericht is op een opgegeven aangepaste verzameling, met inbegrip van niet-actieve taken worden opgehaald:

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Hallo-lijst met taak taak uitvoeringen binnen het uitvoeren van een specifieke taak ophalen:

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

Taak uitvoeren taakdetails ophalen:

Hallo volgende PowerShell-script kan gebruikte tooview Hallo details van een taak uitvoering van taken, die bijzonder nuttig is bij het opsporen van fouten in uitvoering zijn.
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a>Storingen in uitvoering taak ophalen
Hallo JobTaskExecution object bevat een eigenschap voor de levenscyclus van taak samen met een berichteigenschap Hallo Hallo. Als de uitvoering van de taak een taak is mislukt, Hallo Lifecycle eigenschap te worden ingesteld*mislukt* en de resulterende uitzonderingsbericht toohello en de stack Hallo berichteigenschap wordt ingesteld. Als een taak is mislukt, is het belangrijk tooview Hallo details van de taken die voor een bepaalde taak is mislukt.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-toocomplete"></a>Wachten op een taak uitvoeren toocomplete
Hallo volgende PowerShell-script kan gebruikte toowait voor een taak taak toocomplete zijn:

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a>Maken van een aangepaste uitvoeringsbeleid
Elastische Database taken ondersteunt het maken van aangepaste uitvoeringsbeleidsregels die kunnen worden toegepast wanneer u taken start.

Uitvoeringsbeleidsregels toestaan op dit moment voor het definiëren van:

* Naam: Id voor het uitvoeringsbeleid Hallo.
* De time-out van de taak: Totale tijd voordat een taak met elastische taken van de Database, worden geannuleerd.
* Eerste Interval voor opnieuw proberen: Interval toowait voordat de eerste poging.
* Maximale Interval voor opnieuw proberen: Cap van opnieuw intervallen toouse.
* Probeer het opnieuw Interval Backoff Coefficient: Coefficient gebruikt toocalculate Hallo volgende interval tussen nieuwe pogingen.  Hallo volgende formule gebruikt: (eerste Interval voor opnieuw proberen) * Math.pow ((Interval Backoff Coefficient) (nummer van pogingen) - 2).
* Maximum aantal pogingen: Hallo maximum aantal nieuwe pogingen pogingen tooperform in een job.

Hallo standaarduitvoeringsbeleid Hallo volgende waarden gebruikt:

* Naam: Standaarduitvoeringsbeleid
* De time-out van de taak: 1 week
* Eerste Interval voor opnieuw proberen: 100 milliseconden
* Maximale Interval voor opnieuw proberen: 30 minuten
* Coefficient Interval opnieuw proberen: 2
* Maximum aantal pogingen: 2.147.483.647

Hallo gewenst uitvoeringsbeleid maken:

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a>Een aangepaste uitvoeringsbeleid bijwerken
Hallo gewenst uitvoering beleid tooupdate bijwerken:

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a>Een taak annuleren
Elastische Database taken ondersteunt taken annulering aanvragen.  Als taken voor elastische Database een annuleringsverzoek voor een taak die momenteel wordt uitgevoerd detecteert, wordt geprobeerd toostop Hallo taak.

Er zijn twee verschillende manieren dat elastische Database taken een annulering kan uitvoeren:

1. Momenteel worden uitgevoerd annuleren taken: als een annulering wordt gedetecteerd, terwijl een taak die momenteel wordt uitgevoerd, een annulering wordt geprobeerd binnen Hallo aspect van Hallo taak momenteel wordt uitgevoerd.  Bijvoorbeeld: als er een langdurige query die momenteel wordt uitgevoerd wanneer een annulering wordt uitgevoerd, zal er een poging toocancel Hallo-query.
2. Annuleren pogingen: Als een annulering wordt gedetecteerd door Hallo besturingselement thread voordat een taak voor uitvoering wordt gestart, Hallo besturingselement thread wordt voorkomen Hallo taak starten en Hallo aanvraag declareren als geannuleerd.

Als een taak annulering is aangevraagd voor een bovenliggende taak, wordt Hallo annuleringsverzoek ingewilligd voor Hallo bovenliggende taak en alle bijbehorende onderliggende taken.

toosubmit een annuleringsverzoek gebruiken Hallo **Stop AzureSqlJobExecution** cmdlet en set Hallo **JobExecutionId** parameter.

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a>Een taak op naam en Hallo Taakgeschiedenis verwijderen
Elastische taken van de Database biedt ondersteuning voor asynchrone verwijderen van jobs. Een taak kan worden gemarkeerd voor verwijdering en Hallo system Hallo taak en de taakgeschiedenis wordt verwijderd nadat alle taak uitvoeringen voor Hallo taak hebt voltooid. Hallo-systeem wordt niet automatisch uitvoeringen van de actieve taak geannuleerd.  

In plaats daarvan moet stoppen AzureSqlJobExecution aangeroepen toocancel actieve taak uitvoeringen.

tootrigger taak verwijderen, gebruik Hallo **verwijderen AzureSqlJob** cmdlet en set Hallo **JobName** parameter.

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a>Het doel van een aangepaste database maken
Aangepaste database doelen kunnen worden gedefinieerd in elastische Database-taken die kunnen worden gebruikt voor uitvoering rechtstreeks of voor insluiting in de groep van een aangepaste database. Aangezien **elastische pools** niet nog rechtstreeks worden ondersteund via PowerShell APIs Hallo, u gewoon maakt een aangepaste database doel en de aangepaste database verzameling doel op die alle Hallo-databases in de groep Hallo omvat.

Hallo variabelen tooreflect Hallo gewenst databasegegevens volgende instellen:

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a>Een doel van de verzameling aangepaste database maken
Een doel van de verzameling aangepaste database mag gedefinieerde tooenable worden uitgevoerd op meerdere gedefinieerde database doelen. Nadat de groep van een database is gemaakt, kunnen de databases gekoppeld toohello aangepaste verzameling doel kunnen zijn.

Stel Hallo variabelen tooreflect Hallo gewenste aangepaste verzameling doelconfiguratie te volgen:

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a>Databases tooa aangepaste database verzameling doel toevoegen
Database-doelen kunnen worden gekoppeld aan de aangepaste database verzameling doelen toocreate een groep met databases. Wanneer een taak is gemaakt die een aangepaste database verzameling doel, worden uitgevouwen tootarget hello databasesgroep gekoppeld toohello op Hallo tijdstip van de uitvoering van.

Hallo gewenst database tooa specifieke aangepaste verzameling toevoegen:

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Hallo-databases binnen een doel van de verzameling aangepaste database controleren
Gebruik Hallo **Get-AzureSqlJobTarget** cmdlet tooretrieve Hallo onderliggende databases binnen een doel van de verzameling aangepaste database.

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Een taak tooexecute van een script voor een doel van de verzameling aangepaste database maken
Gebruik Hallo **nieuw AzureSqlJob** cmdlet toocreate een taak op basis van een groep met databases die zijn gedefinieerd door een doel van de verzameling aangepaste database. Elastische taken van de Database wordt Hallo taak uitbreiden naar meerdere onderliggende taken elke overeenkomstige tooa-database die is gekoppeld aan Hallo aangepaste database verzameling doel en zorg ervoor dat Hallo script wordt uitgevoerd tegen elke database. Ook is het belangrijk dat scripts idempotent toobe robuuste tooretries zijn.

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a>Gegevens verzamelen over databases
**Elastische Database taken** ondersteunt een query uit te voeren in een groep van databases en verzendt Hallo resultaten tooa opgegeven van de database-tabel. Hallo tabel kan worden opgevraagd na Hallo feit toosee Hallo queryresultaat van elke database. Dit biedt een mechanisme voor asynchrone tooexecute een query tussen meerdere databases. Fout gevallen, zoals een Hallo databases tijdelijk niet beschikbaar worden automatisch verwerkt via de nieuwe pogingen.

de opgegeven doeltabel Hello wordt automatisch worden gemaakt als deze nog niet bestaat, overeenkomende hello schema Hallo heeft een resultatenset geretourneerd. Als de uitvoering van een script meerdere resultatensets worden geretourneerd, verzendt elastische Database taken alleen Hallo eerste één toohello opgegeven doeltabel.

Hallo volgende PowerShell-script kan worden gebruikt tooexecute een script voor het verzamelen van de resultaten in een opgegeven tabel. Dit script wordt ervan uitgegaan dat een T-SQL-script is gemaakt waarmee een enkelvoudig resultaat wordt verkregen set levert en een doel van de verzameling aangepaste database is gemaakt.

Stel Hallo tooreflect Hallo gewenst script, referenties en doel van de uitvoering te volgen:

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a>Maak en start een taak voor scenario's voor het verzamelen van gegevens
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a>Een planning voor het uitvoeren van de taak met behulp van een trigger taak maken
Hallo volgende PowerShell-script kan worden gebruikt toocreate een terugkerende planning. Dit script maakt gebruik van een interval van één minuut, maar nieuwe AzureSqlJobSchedule biedt ook ondersteuning voor parameters - DayInterval, - HourInterval, - MonthInterval, en -WeekInterval. Schema's die slechts één keer worden uitgevoerd, kunnen worden gemaakt door doorgeven - eenmalige.

Maak een nieuwe planning:
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a>Een taak trigger toohave taak uitgevoerd op een tijdschema maken
Een trigger voor de taak kan worden gedefinieerd toohave uitgevoerd volgens tooa tijdschema van een taak. Hallo volgende PowerShell-script kan worden gebruikt toocreate een trigger taak.

Stel Hallo variabelen toocorrespond toohello gewenste taak te volgen en plannen:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>Een geplande koppeling toostop-taak wordt uitgevoerd op de planning verwijderen
toodiscontinue taakuitvoering via een taak worden geactiveerd, Hallo taak trigger opnieuw optreedt, kan worden verwijderd.
Verwijderen van een taak trigger toostop een taak uit te voeren volgens tooa schema met behulp van Hallo **verwijderen AzureSqlJobTrigger** cmdlet.

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a>Elastische database query resultaten tooExcel importeren
 U kunt Hallo resultaten uit van een query tooan Excel-bestand importeren.

1. Start Excel 2013.
2. Navigeer toohello **gegevens** lint.
3. Klik op **van andere bronnen** en klik op **van SQL Server**.

   ![Excel importeren uit andere bronnen](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. In Hallo **Wizard Gegevensverbinding** Typ Hallo server servernaam en aanmeldingsreferenties. Klik op **Volgende**.
5. In het dialoogvenster Hallo **Selecteer Hallo-database met Hallo gegevens die u wilt**, selecteer Hallo **ElasticDBQuery** database.
6. Selecteer Hallo **klanten** tabel in de lijstweergave Hallo en klikt u op **volgende**. Klik vervolgens op **voltooien**.
7. In Hallo **importgegevens** formulier onder **Selecteer hoe u tooview deze gegevens in uw werkmap**, selecteer **tabel** en klik op **OK**.

Alle rijen uit Hallo **klanten** tabel, opgeslagen in verschillende shards vullen Hallo Excel-werkblad.

## <a name="next-steps"></a>Volgende stappen
Nu kunt u functies van de gegevens van Excel. Hallo-verbindingsreeks gebruiken met de naam van uw server, databasenaam en referenties tooconnect uw BI en gegevens integratie extra toohello elastische query uitvoeren op database. Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma. Raadpleeg toohello elastische query uitvoeren op database en de externe tabellen net als elke andere SQL Server-database en SQL Server-tabellen die u wilt verbinding maken toowith uw hulpprogramma.

### <a name="cost"></a>Kosten
Er zijn geen extra kosten voor het gebruik van de functie Hallo elastische Database-query. Hoewel op dit moment deze functie is alleen beschikbaar op premium-databases als een eindpunt, Hallo shards kunnen zijn van een servicelaag.

Zie voor informatie over prijzen [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
