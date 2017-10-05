---
title: Aan de slag met elastische database taken | Microsoft Docs
description: het gebruik van taken voor elastische database
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
ms.openlocfilehash: 05c20e880d4eb1eacdecc0c4c7e7491dfe1e6a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="228a6-103">Aan de slag met taken voor elastische Database</span><span class="sxs-lookup"><span data-stu-id="228a6-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="228a6-104">Elastische Database-taken (preview) voor Azure SQL Database kunt u betrouwbaarheid T-SQL-scripts die meerdere databases tijdens het automatisch opnieuw uit te voeren en het geven van de uiteindelijke voltooiing garanties omvatten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="228a6-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="228a6-105">Zie voor meer informatie over de functie van de taak elastische Database, de [overzicht functiepagina](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="228a6-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="228a6-106">In dit onderwerp wordt uitgebreid voor het voorbeeld dat is gevonden in [aan de slag met hulpprogramma's voor elastische Database](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="228a6-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="228a6-107">Wanneer voltooid, wordt u: informatie over het maken en beheren van taken die een groep verwante databases beheren.</span><span class="sxs-lookup"><span data-stu-id="228a6-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="228a6-108">Het is niet vereist voor het gebruik van de elastische Schaalfunctionaliteit van hulpprogramma's om te profiteren van de voordelen van elastische taken.</span><span class="sxs-lookup"><span data-stu-id="228a6-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="228a6-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="228a6-109">Prerequisites</span></span>
<span data-ttu-id="228a6-110">Downloaden en uitvoeren van de [aan de slag met elastische Database extra voorbeeld](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="228a6-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="228a6-111">Een shard-toewijzing manager met behulp van de voorbeeld-app maken</span><span class="sxs-lookup"><span data-stu-id="228a6-111">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="228a6-112">Hier maakt u een shard-toewijzing manager samen met enkele shards, gevolgd door het invoegen van gegevens in de shards.</span><span class="sxs-lookup"><span data-stu-id="228a6-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="228a6-113">Als u al shards instellen met gedeelde gegevens bevat, kunt u de volgende stappen overslaan en verplaatsen naar de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="228a6-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="228a6-114">Bouwen en uitvoeren van de **aan de slag met hulpprogramma's voor elastische Database** voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="228a6-114">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="228a6-115">Volg de stappen totdat stap 7 in de sectie [downloaden en uitvoeren van de voorbeeld-app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="228a6-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="228a6-116">Aan het einde van stap 7 ziet u de volgende opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="228a6-116">At the end of Step 7, you will see the following command prompt:</span></span>

   ![opdrachtprompt](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="228a6-118">Typ in het opdrachtvenster '1' en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="228a6-118">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="228a6-119">Dit maakt de shard kaart manager en voegt twee shards aan de server.</span><span class="sxs-lookup"><span data-stu-id="228a6-119">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="228a6-120">Vervolgens typt u "3" en druk op **Enter**; deze actie vier keer herhalen.</span><span class="sxs-lookup"><span data-stu-id="228a6-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="228a6-121">Dit invoegen voorbeeld gegevensrijen in uw shards.</span><span class="sxs-lookup"><span data-stu-id="228a6-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="228a6-122">De [Azure Portal](https://portal.azure.com) drie nieuwe databases moeten worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="228a6-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio-bevestiging](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="228a6-124">We gaan nu een verzameling aangepaste database die overeenkomt met de databases in de shard-toewijzing maken.</span><span class="sxs-lookup"><span data-stu-id="228a6-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span></span> <span data-ttu-id="228a6-125">Dit kunnen we maken en uitvoeren van een taak die een nieuwe tabel toevoegen via shards.</span><span class="sxs-lookup"><span data-stu-id="228a6-125">This will allow us to create and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="228a6-126">Hier wordt meestal maken we een shard-toewijzing met als doel, met behulp van de **nieuw AzureSqlJobTarget** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="228a6-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="228a6-127">De shard kaart manager-database moet worden ingesteld als het doel van een database en vervolgens de specifieke shard-toewijzing is opgegeven als een doel.</span><span class="sxs-lookup"><span data-stu-id="228a6-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span></span> <span data-ttu-id="228a6-128">We gaan in plaats daarvan inventariseren van alle databases in de server en de databases toevoegen aan de nieuwe aangepaste verzameling met uitzondering van de database master.</span><span class="sxs-lookup"><span data-stu-id="228a6-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-the-server-to-the-custom-collection-target-with-the-exception-of-master"></a><span data-ttu-id="228a6-129">Een aangepaste verzameling maakt en alle databases op de server toevoegen aan het doel van de aangepaste verzameling met uitzondering van de master.</span><span class="sxs-lookup"><span data-stu-id="228a6-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span></span>
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
             Write-Host $currentdb "is already in the custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="228a6-130">Maken van een T-SQL-Script voor uitvoering tussen databases</span><span class="sxs-lookup"><span data-stu-id="228a6-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-the-job-to-execute-a-script-across-the-custom-group-of-databases"></a><span data-ttu-id="228a6-131">De taak voor het uitvoeren van een script via de aangepaste groep van databases maken</span><span class="sxs-lookup"><span data-stu-id="228a6-131">Create the job to execute a script across the custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-the-job"></a><span data-ttu-id="228a6-132">De taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="228a6-132">Execute the job</span></span>
<span data-ttu-id="228a6-133">De volgende PowerShell-script kan worden gebruikt als een bestaande taak wilt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="228a6-133">The following PowerShell script can be used to execute an existing job:</span></span>

<span data-ttu-id="228a6-134">Update de volgende variabele in overeenstemming met de naam van de gewenste taak hebt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="228a6-134">Update the following variable to reflect the desired job name to have executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="228a6-135">De status van het uitvoeren van een enkele taak ophalen</span><span class="sxs-lookup"><span data-stu-id="228a6-135">Retrieve the state of a single job execution</span></span>
<span data-ttu-id="228a6-136">Gebruik van dezelfde **Get-AzureSqlJobExecution** cmdlet uit met de **voor IncludeChildren** -parameter voor de status van onderliggende taak uitvoeringen, namelijk de specifieke status voor elke taak uitgevoerd op elke database weergeven gericht door de taak.</span><span class="sxs-lookup"><span data-stu-id="228a6-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-the-state-across-multiple-job-executions"></a><span data-ttu-id="228a6-137">De status tussen uitvoeringen van meerdere taak weergeven</span><span class="sxs-lookup"><span data-stu-id="228a6-137">View the state across multiple job executions</span></span>
<span data-ttu-id="228a6-138">De **Get-AzureSqlJobExecution** cmdlet heeft meerdere optionele parameters die kunnen worden gebruikt om meerdere taak uitvoeringen, gefilterd via de opgegeven parameters weer te geven.</span><span class="sxs-lookup"><span data-stu-id="228a6-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="228a6-139">Het volgende voorbeeld toont een aantal mogelijke manieren waarop Get-AzureSqlJobExecution gebruiken:</span><span class="sxs-lookup"><span data-stu-id="228a6-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="228a6-140">Alle actieve taken voor de bovenste niveau uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="228a6-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="228a6-141">Alle bovenste niveau taak uitvoeringen, met inbegrip van niet-actieve taak uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="228a6-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="228a6-142">Alle onderliggende taak uitvoeringen van een opgegeven taak uitvoerings-ID, met inbegrip van niet-actieve taak uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="228a6-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="228a6-143">Ophalen van alle taak uitvoeringen gemaakt met behulp van een planning / taak combinatie, met inbegrip van niet-actieve taken:</span><span class="sxs-lookup"><span data-stu-id="228a6-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="228a6-144">Alle taken die gericht is op een opgegeven shard-kaart, inclusief niet-actieve taken worden opgehaald:</span><span class="sxs-lookup"><span data-stu-id="228a6-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="228a6-145">Alle taken die gericht is op een opgegeven aangepaste verzameling, met inbegrip van niet-actieve taken worden opgehaald:</span><span class="sxs-lookup"><span data-stu-id="228a6-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="228a6-146">Ophalen van de lijst van de taak taak uitvoeringen binnen een specifieke taak kan worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="228a6-146">Retrieve the list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="228a6-147">Taak uitvoeren taakdetails ophalen:</span><span class="sxs-lookup"><span data-stu-id="228a6-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="228a6-148">De volgende PowerShell-script kan worden gebruikt om de details van een taak uitvoering van taken, die bijzonder nuttig is bij het opsporen van fouten in uitvoering weer te geven.</span><span class="sxs-lookup"><span data-stu-id="228a6-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="228a6-149">Storingen in uitvoering taak ophalen</span><span class="sxs-lookup"><span data-stu-id="228a6-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="228a6-150">Het object JobTaskExecution bevat een eigenschap voor de levenscyclus van de taak samen met een berichteigenschap.</span><span class="sxs-lookup"><span data-stu-id="228a6-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span></span> <span data-ttu-id="228a6-151">Als de uitvoering van de taak een taak is mislukt, de levenscyclus van de eigenschap wordt ingesteld op *mislukt* en de berichteigenschap zal worden ingesteld op de resulterende uitzonderingsbericht en de stack.</span><span class="sxs-lookup"><span data-stu-id="228a6-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="228a6-152">Als een taak is mislukt, is het belangrijk om de details van taken waarvoor is mislukt voor een bepaalde taak weer te geven.</span><span class="sxs-lookup"><span data-stu-id="228a6-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-to-complete"></a><span data-ttu-id="228a6-153">Wacht op de taakuitvoering van een te voltooien</span><span class="sxs-lookup"><span data-stu-id="228a6-153">Waiting for a job execution to complete</span></span>
<span data-ttu-id="228a6-154">De volgende PowerShell-script kan worden gebruikt om te wachten op een taak te voltooien:</span><span class="sxs-lookup"><span data-stu-id="228a6-154">The following PowerShell script can be used to wait for a job task to complete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="228a6-155">Maken van een aangepaste uitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="228a6-155">Create a custom execution policy</span></span>
<span data-ttu-id="228a6-156">Elastische Database taken ondersteunt het maken van aangepaste uitvoeringsbeleidsregels die kunnen worden toegepast wanneer u taken start.</span><span class="sxs-lookup"><span data-stu-id="228a6-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="228a6-157">Uitvoeringsbeleidsregels toestaan op dit moment voor het definiëren van:</span><span class="sxs-lookup"><span data-stu-id="228a6-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="228a6-158">Naam: Id voor het uitvoeringsbeleid.</span><span class="sxs-lookup"><span data-stu-id="228a6-158">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="228a6-159">De time-out van de taak: Totale tijd voordat een taak met elastische taken van de Database, worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="228a6-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="228a6-160">Eerste Interval voor opnieuw proberen: Interval moet worden gewacht voordat de eerste poging.</span><span class="sxs-lookup"><span data-stu-id="228a6-160">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="228a6-161">Maximale Interval voor opnieuw proberen: Cap intervallen voor opnieuw proberen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="228a6-161">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="228a6-162">Opnieuw proberen Interval Backoff Coefficient: Coefficient die wordt gebruikt voor het berekenen van de volgende interval tussen nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="228a6-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="228a6-163">De volgende formule wordt gebruikt: (eerste Interval voor opnieuw proberen) * Math.pow ((Interval Backoff Coefficient) (nummer van pogingen) - 2).</span><span class="sxs-lookup"><span data-stu-id="228a6-163">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="228a6-164">Maximum aantal pogingen: Het maximum aantal probeer het opnieuw probeert uit te voeren in een job.</span><span class="sxs-lookup"><span data-stu-id="228a6-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="228a6-165">Het standaarduitvoeringsbeleid maakt gebruik van de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="228a6-165">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="228a6-166">Naam: Standaarduitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="228a6-166">Name: Default execution policy</span></span>
* <span data-ttu-id="228a6-167">De time-out van de taak: 1 week</span><span class="sxs-lookup"><span data-stu-id="228a6-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="228a6-168">Eerste Interval voor opnieuw proberen: 100 milliseconden</span><span class="sxs-lookup"><span data-stu-id="228a6-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="228a6-169">Maximale Interval voor opnieuw proberen: 30 minuten</span><span class="sxs-lookup"><span data-stu-id="228a6-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="228a6-170">Coefficient Interval opnieuw proberen: 2</span><span class="sxs-lookup"><span data-stu-id="228a6-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="228a6-171">Maximum aantal pogingen: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="228a6-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="228a6-172">Maak de gewenste uitvoeringsbeleid:</span><span class="sxs-lookup"><span data-stu-id="228a6-172">Create the desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="228a6-173">Een aangepaste uitvoeringsbeleid bijwerken</span><span class="sxs-lookup"><span data-stu-id="228a6-173">Update a custom execution policy</span></span>
<span data-ttu-id="228a6-174">Werk het gewenste uitvoeringsbeleid om bij te werken:</span><span class="sxs-lookup"><span data-stu-id="228a6-174">Update the desired execution policy to update:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="228a6-175">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="228a6-175">Cancel a job</span></span>
<span data-ttu-id="228a6-176">Elastische Database taken ondersteunt taken annulering aanvragen.</span><span class="sxs-lookup"><span data-stu-id="228a6-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="228a6-177">Als taken voor elastische Database een annuleringsverzoek voor een taak die momenteel wordt uitgevoerd detecteert, wordt geprobeerd de taak te stoppen.</span><span class="sxs-lookup"><span data-stu-id="228a6-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="228a6-178">Er zijn twee verschillende manieren dat elastische Database taken een annulering kan uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="228a6-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="228a6-179">Momenteel worden uitgevoerd annuleren taken: als een annulering wordt gedetecteerd, terwijl een taak die momenteel wordt uitgevoerd, een annulering wordt geprobeerd binnen het momenteel wordt uitgevoerd aspect van de taak.</span><span class="sxs-lookup"><span data-stu-id="228a6-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="228a6-180">Bijvoorbeeld: als er een langdurige query die momenteel wordt uitgevoerd wanneer een annulering wordt uitgevoerd, zal er een poging om de query te annuleren.</span><span class="sxs-lookup"><span data-stu-id="228a6-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="228a6-181">Annuleren pogingen: Als een annulering wordt gedetecteerd door de besturingselement-thread voordat een taak voor uitvoering wordt gestart, de besturingselement-thread wordt voorkomen dat de taak starten en declareren van de aanvraag als geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="228a6-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="228a6-182">Als een taak annulering is aangevraagd voor een bovenliggende taak, wordt de annuleringsaanvraag gehonoreerd voor de bovenliggende taak en alle bijbehorende onderliggende taken.</span><span class="sxs-lookup"><span data-stu-id="228a6-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="228a6-183">Gebruik hiervoor een annuleringsaanvraag indienen, de **Stop AzureSqlJobExecution** cmdlet en stel de **JobExecutionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="228a6-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-the-jobs-history"></a><span data-ttu-id="228a6-184">Een taak door de naam van de taakgeschiedenis verwijderen</span><span class="sxs-lookup"><span data-stu-id="228a6-184">Delete a job by name and the job's history</span></span>
<span data-ttu-id="228a6-185">Elastische taken van de Database biedt ondersteuning voor asynchrone verwijderen van jobs.</span><span class="sxs-lookup"><span data-stu-id="228a6-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="228a6-186">Een taak kan worden gemarkeerd voor verwijdering en het systeem de taak en de taakgeschiedenis wordt verwijderd nadat alle uitvoeringen van de taak voor de taak hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="228a6-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="228a6-187">Het systeem wordt niet automatisch uitvoeringen van de actieve taak geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="228a6-187">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="228a6-188">Stop AzureSqlJobExecution moet in plaats daarvan worden aangeroepen om te annuleren uitvoeringen van actieve taken.</span><span class="sxs-lookup"><span data-stu-id="228a6-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span></span>

<span data-ttu-id="228a6-189">Gebruiken om te verwijderen van een taak activeren, de **verwijderen AzureSqlJob** cmdlet en stel de **JobName** parameter.</span><span class="sxs-lookup"><span data-stu-id="228a6-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="228a6-190">Het doel van een aangepaste database maken</span><span class="sxs-lookup"><span data-stu-id="228a6-190">Create a custom database target</span></span>
<span data-ttu-id="228a6-191">Aangepaste database doelen kunnen worden gedefinieerd in elastische Database-taken die kunnen worden gebruikt voor uitvoering rechtstreeks of voor insluiting in de groep van een aangepaste database.</span><span class="sxs-lookup"><span data-stu-id="228a6-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="228a6-192">Aangezien **elastische pools** niet nog rechtstreeks worden ondersteund via de APIs PowerShell u gewoon maakt een aangepaste database doel en de aangepaste database verzameling target dit alle databases in de pool omvat.</span><span class="sxs-lookup"><span data-stu-id="228a6-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="228a6-193">De volgende variabelen in overeenstemming met de gewenste databasegegevens instellen:</span><span class="sxs-lookup"><span data-stu-id="228a6-193">Set the following variables to reflect the desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="228a6-194">Een doel van de verzameling aangepaste database maken</span><span class="sxs-lookup"><span data-stu-id="228a6-194">Create a custom database collection target</span></span>
<span data-ttu-id="228a6-195">Een verzameling aangepaste database doel kan worden gedefinieerd als de uitvoering inschakelen tussen meerdere gedefinieerde database doelen.</span><span class="sxs-lookup"><span data-stu-id="228a6-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="228a6-196">Nadat de groep van een database is gemaakt, is databases kunnen worden gekoppeld aan het doel van de aangepaste verzameling.</span><span class="sxs-lookup"><span data-stu-id="228a6-196">After a database group is created, databases can be associated to the custom collection target.</span></span>

<span data-ttu-id="228a6-197">Stel de volgende variabelen in overeenstemming met de configuratie van de gewenste aangepaste verzameling doel:</span><span class="sxs-lookup"><span data-stu-id="228a6-197">Set the following variables to reflect the desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="228a6-198">Databases toevoegen aan een doel van de verzameling aangepaste database</span><span class="sxs-lookup"><span data-stu-id="228a6-198">Add databases to a custom database collection target</span></span>
<span data-ttu-id="228a6-199">Database-doelen kunnen worden gekoppeld aan de aangepaste database verzameling doelen voor het maken van een groep met databases.</span><span class="sxs-lookup"><span data-stu-id="228a6-199">Database targets can be associated with custom database collection targets to create a group of databases.</span></span> <span data-ttu-id="228a6-200">Wanneer een taak is gemaakt die een aangepaste database verzameling doel, zal het worden uitgebreid om het doel van de databases die zijn gekoppeld aan de groep op het moment van de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="228a6-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span></span>

<span data-ttu-id="228a6-201">De gewenste database toevoegen aan een specifieke aangepaste verzameling:</span><span class="sxs-lookup"><span data-stu-id="228a6-201">Add the desired database to a specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="228a6-202">Bekijk de databases binnen een verzameling aangepaste database doel</span><span class="sxs-lookup"><span data-stu-id="228a6-202">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="228a6-203">Gebruik de **Get-AzureSqlJobTarget** cmdlet voor het ophalen van de onderliggende databases binnen een doel van de verzameling aangepaste database.</span><span class="sxs-lookup"><span data-stu-id="228a6-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="228a6-204">Een taak voor het uitvoeren van een script voor een doel van de verzameling aangepaste database maken</span><span class="sxs-lookup"><span data-stu-id="228a6-204">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="228a6-205">Gebruik de **nieuw AzureSqlJob** cmdlet een taak op basis van een groep met databases die zijn gedefinieerd door een doel van de verzameling aangepaste database te maken.</span><span class="sxs-lookup"><span data-stu-id="228a6-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="228a6-206">Elastische taken van de Database wordt de taak uitbreiden naar meerdere onderliggende taken elke overeenkomt met een database die is gekoppeld aan het doel van de verzameling aangepaste database en zorg ervoor dat het script wordt uitgevoerd tegen elke database.</span><span class="sxs-lookup"><span data-stu-id="228a6-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="228a6-207">Ook is het belangrijk dat scripts idempotent zijn flexibel omgaan met nieuwe pogingen worden.</span><span class="sxs-lookup"><span data-stu-id="228a6-207">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="228a6-208">Gegevens verzamelen over databases</span><span class="sxs-lookup"><span data-stu-id="228a6-208">Data collection across databases</span></span>
<span data-ttu-id="228a6-209">**Elastische Database taken** ondersteunt een query uit te voeren in een groep van databases en verzendt de resultaten in een opgegeven databasetabel.</span><span class="sxs-lookup"><span data-stu-id="228a6-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span></span> <span data-ttu-id="228a6-210">De tabel kan worden opgevraagd achteraf om te zien van het queryresultaat van elke database.</span><span class="sxs-lookup"><span data-stu-id="228a6-210">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="228a6-211">Dit is een asynchrone mechanisme voor het uitvoeren van een query tussen meerdere databases.</span><span class="sxs-lookup"><span data-stu-id="228a6-211">This provides an asynchronous mechanism to execute a query across many databases.</span></span> <span data-ttu-id="228a6-212">Fout gevallen, zoals een van de databases die tijdelijk niet beschikbaar worden automatisch verwerkt via de nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="228a6-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="228a6-213">De opgegeven doeltabel wordt automatisch gemaakt als deze nog niet bestaat, die overeenkomt met het schema van de geretourneerde resultatenset.</span><span class="sxs-lookup"><span data-stu-id="228a6-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span></span> <span data-ttu-id="228a6-214">Als de uitvoering van een script meerdere resultatensets worden geretourneerd, verzendt elastische Database taken alleen de eerste die aan de tabel van de opgegeven bestemming.</span><span class="sxs-lookup"><span data-stu-id="228a6-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span></span>

<span data-ttu-id="228a6-215">Het volgende PowerShell-script kan worden gebruikt voor het uitvoeren van een script voor het verzamelen van de resultaten in een opgegeven tabel.</span><span class="sxs-lookup"><span data-stu-id="228a6-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span></span> <span data-ttu-id="228a6-216">Dit script wordt ervan uitgegaan dat een T-SQL-script is gemaakt waarmee een enkelvoudig resultaat wordt verkregen set levert en een doel van de verzameling aangepaste database is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="228a6-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="228a6-217">Stel het volgende in overeenstemming met de gewenste script, referenties en uitvoering van doel:</span><span class="sxs-lookup"><span data-stu-id="228a6-217">Set the following to reflect the desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="228a6-218">Maak en start een taak voor scenario's voor het verzamelen van gegevens</span><span class="sxs-lookup"><span data-stu-id="228a6-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="228a6-219">Een planning voor het uitvoeren van de taak met behulp van een trigger taak maken</span><span class="sxs-lookup"><span data-stu-id="228a6-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="228a6-220">De volgende PowerShell-script kan worden gebruikt om een terugkerende planning te maken.</span><span class="sxs-lookup"><span data-stu-id="228a6-220">The following PowerShell script can be used to create a reoccurring schedule.</span></span> <span data-ttu-id="228a6-221">Dit script maakt gebruik van een interval van één minuut, maar nieuwe AzureSqlJobSchedule biedt ook ondersteuning voor parameters - DayInterval, - HourInterval, - MonthInterval, en -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="228a6-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="228a6-222">Schema's die slechts één keer worden uitgevoerd, kunnen worden gemaakt door doorgeven - eenmalige.</span><span class="sxs-lookup"><span data-stu-id="228a6-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="228a6-223">Maak een nieuwe planning:</span><span class="sxs-lookup"><span data-stu-id="228a6-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-to-have-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="228a6-224">Als u wilt dat een taak uitgevoerd op een tijdschema trigger taak maken</span><span class="sxs-lookup"><span data-stu-id="228a6-224">Create a job trigger to have a job executed on a time schedule</span></span>
<span data-ttu-id="228a6-225">Een trigger voor de taak kan worden gedefinieerd als een taak uitgevoerd volgens een tijdschema hebben.</span><span class="sxs-lookup"><span data-stu-id="228a6-225">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="228a6-226">De volgende PowerShell-script kan worden gebruikt voor het maken van een trigger taak.</span><span class="sxs-lookup"><span data-stu-id="228a6-226">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="228a6-227">Stel de volgende variabelen in overeenstemming met de gewenste taak en planning:</span><span class="sxs-lookup"><span data-stu-id="228a6-227">Set the following variables to correspond to the desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="228a6-228">Verwijderen van een associatie met geplande taak wordt uitgevoerd volgens schema stoppen</span><span class="sxs-lookup"><span data-stu-id="228a6-228">Remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="228a6-229">Als u wilt stoppen met het uitvoeren van terugkerende taak via een trigger taak, kan de trigger taak worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="228a6-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span>
<span data-ttu-id="228a6-230">Verwijderen van een trigger taak om te stoppen van een taak uit te voeren volgens een schema met de **verwijderen AzureSqlJobTrigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="228a6-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="228a6-231">De queryresultaten elastische database importeren in Excel</span><span class="sxs-lookup"><span data-stu-id="228a6-231">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="228a6-232">U kunt de resultaten van van een query met een Excel-bestand importeren.</span><span class="sxs-lookup"><span data-stu-id="228a6-232">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="228a6-233">Start Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="228a6-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="228a6-234">Navigeer naar de **gegevens** lint.</span><span class="sxs-lookup"><span data-stu-id="228a6-234">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="228a6-235">Klik op **van andere bronnen** en klik op **van SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="228a6-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Excel importeren uit andere bronnen](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="228a6-237">In de **Wizard Gegevensverbinding** Typ de servernaam en aanmeldingsreferenties van de server.</span><span class="sxs-lookup"><span data-stu-id="228a6-237">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="228a6-238">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="228a6-238">Then click **Next**.</span></span>
5. <span data-ttu-id="228a6-239">In het dialoogvenster **selecteert u de database met de gegevens die u wilt dat**, selecteer de **ElasticDBQuery** database.</span><span class="sxs-lookup"><span data-stu-id="228a6-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="228a6-240">Selecteer de **klanten** tabel in de lijstweergave en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="228a6-240">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="228a6-241">Klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="228a6-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="228a6-242">In de **importgegevens** formulier onder **selecteren hoe u wilt weergeven van deze gegevens in uw werkmap**, selecteer **tabel** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="228a6-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="228a6-243">Alle rijen uit **klanten** tabel, opgeslagen in verschillende shards vullen de Excel-werkblad.</span><span class="sxs-lookup"><span data-stu-id="228a6-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="228a6-244">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="228a6-244">Next steps</span></span>
<span data-ttu-id="228a6-245">Nu kunt u functies van de gegevens van Excel.</span><span class="sxs-lookup"><span data-stu-id="228a6-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="228a6-246">De verbindingsreeks gebruiken met de servernaam, databasenaam en referenties verbinding maken met uw integratiefuncties BI en gegevens van de elastische database.</span><span class="sxs-lookup"><span data-stu-id="228a6-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="228a6-247">Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="228a6-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="228a6-248">Raadpleeg de elastische query uitvoeren op database en de externe tabellen net als elke andere SQL Server-database en SQL Server-tabellen die u met het hulpprogramma verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="228a6-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="228a6-249">Kosten</span><span class="sxs-lookup"><span data-stu-id="228a6-249">Cost</span></span>
<span data-ttu-id="228a6-250">Er zijn geen extra kosten voor het gebruik van de functie van de query elastische Database.</span><span class="sxs-lookup"><span data-stu-id="228a6-250">There is no additional charge for using the Elastic Database query feature.</span></span> <span data-ttu-id="228a6-251">Echter op dit moment deze functie is alleen beschikbaar op premium-databases als een eindpunt, maar de shards kunnen zijn van een servicelaag.</span><span class="sxs-lookup"><span data-stu-id="228a6-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span></span>

<span data-ttu-id="228a6-252">Zie voor informatie over prijzen [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="228a6-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
