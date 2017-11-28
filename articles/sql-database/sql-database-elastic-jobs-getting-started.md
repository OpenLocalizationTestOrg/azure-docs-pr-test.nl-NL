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
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="5742c-103">Aan de slag met taken voor elastische Database</span><span class="sxs-lookup"><span data-stu-id="5742c-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="5742c-104">Elastische Database-taken (preview) voor Azure SQL Database, u tooreliability kunt T-SQL-scripts die meerdere databases omvatten tijdens het automatisch opnieuw uitvoeren en geven de uiteindelijke voltooiing wordt gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="5742c-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="5742c-105">Zie voor meer informatie over Hallo elastische Database taak functie Hallo [overzicht functiepagina](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5742c-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="5742c-106">In dit onderwerp breidt Hallo voorbeeld gevonden in [aan de slag met hulpprogramma's voor elastische Database](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5742c-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="5742c-107">Wanneer voltooid, wordt u: meer informatie over hoe toocreate en beheren van taken die een groep verwante databases beheren.</span><span class="sxs-lookup"><span data-stu-id="5742c-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="5742c-108">Het is niet vereist toouse Hallo elastische Schaalfunctionaliteit van hulpprogramma's in volgorde tootake profiteren van Hallo voordelen van elastische taken.</span><span class="sxs-lookup"><span data-stu-id="5742c-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5742c-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5742c-109">Prerequisites</span></span>
<span data-ttu-id="5742c-110">Downloaden en uitvoeren van Hallo [aan de slag met elastische Database extra voorbeeld](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5742c-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="5742c-111">Een shard-toewijzing manager met Hallo voorbeeld-app maken</span><span class="sxs-lookup"><span data-stu-id="5742c-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="5742c-112">Hier maakt u een shard-toewijzing manager samen met enkele shards, gevolgd door het invoegen van gegevens in Hallo shards.</span><span class="sxs-lookup"><span data-stu-id="5742c-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="5742c-113">Als u al shards instellen met gedeelde gegevens bevat, kunt u overslaan Hallo stappen te volgen en verplaatsen van de volgende sectie toohello.</span><span class="sxs-lookup"><span data-stu-id="5742c-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="5742c-114">Bouwen en uitvoeren van Hallo **aan de slag met hulpprogramma's voor elastische Database** voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="5742c-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="5742c-115">Hallo stappen tot stap 7 in de sectie Hallo [Hallo voorbeeld-app downloaden en uitvoeren](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="5742c-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="5742c-116">Aan het einde van de Hallo van stap 7 ziet u Hallo na de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="5742c-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![opdrachtprompt](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="5742c-118">In het opdrachtvenster hello, typ '1' en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="5742c-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="5742c-119">Dit maakt Hallo shard-toewijzing manager en voegt u twee shards toohello-server.</span><span class="sxs-lookup"><span data-stu-id="5742c-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="5742c-120">Vervolgens typt u "3" en druk op **Enter**; deze actie vier keer herhalen.</span><span class="sxs-lookup"><span data-stu-id="5742c-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="5742c-121">Dit invoegen voorbeeld gegevensrijen in uw shards.</span><span class="sxs-lookup"><span data-stu-id="5742c-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="5742c-122">Hallo [Azure Portal](https://portal.azure.com) drie nieuwe databases moeten worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5742c-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio-bevestiging](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="5742c-124">We gaan nu een verzameling aangepaste database die overeenkomt met alle Hallo-databases in de shard-toewijzing Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="5742c-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="5742c-125">Hiermee kunnen we toocreate en uitvoeren van een taak die een nieuwe tabel toevoegen via shards.</span><span class="sxs-lookup"><span data-stu-id="5742c-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="5742c-126">Hier zou meestal maken we een doel shard-toewijzing met Hallo **nieuw AzureSqlJobTarget** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5742c-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="5742c-127">Hallo shard kaart manager-database moet worden ingesteld als het doel van een database en vervolgens Hallo specifieke shard-toewijzing is opgegeven als een doel.</span><span class="sxs-lookup"><span data-stu-id="5742c-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="5742c-128">We gaan tooenumerate alle Hallo-databases in Hallo-server zijn en Hallo databases toohello nieuwe aangepaste verzameling met uitzondering van de database master Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5742c-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="5742c-129">Hiermee maakt u een aangepaste verzameling en voegt u alle databases in Hallo server toohello aangepaste verzameling doel met uitzondering van master Hallo.</span><span class="sxs-lookup"><span data-stu-id="5742c-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
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
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="5742c-130">Maken van een T-SQL-Script voor uitvoering tussen databases</span><span class="sxs-lookup"><span data-stu-id="5742c-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="5742c-131">Hallo taak tooexecute een script maken via de aangepaste groep Hallo van databases</span><span class="sxs-lookup"><span data-stu-id="5742c-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="5742c-132">Hallo-taak uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="5742c-132">Execute hello job</span></span>
<span data-ttu-id="5742c-133">Hallo volgende PowerShell-script kan gebruikte tooexecute een bestaande taak zijn:</span><span class="sxs-lookup"><span data-stu-id="5742c-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="5742c-134">Hallo variabele tooreflect Hallo gewenst taak naam toohave uitgevoerd na bijwerken:</span><span class="sxs-lookup"><span data-stu-id="5742c-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="5742c-135">Hallo-status van het uitvoeren van een enkele taak ophalen</span><span class="sxs-lookup"><span data-stu-id="5742c-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="5742c-136">Gebruik dezelfde Hallo **Get-AzureSqlJobExecution** cmdlet Hello **voor IncludeChildren** namelijk Hallo specifieke status voor elke taak uitvoeren voor elke parameter tooview Hallo status van onderliggende taak uitvoeringen, de database is gericht door Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="5742c-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="5742c-137">Hallo weergavestatus over meerdere taak uitvoeringen</span><span class="sxs-lookup"><span data-stu-id="5742c-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="5742c-138">Hallo **Get-AzureSqlJobExecution** cmdlet heeft meerdere optionele parameters die gebruikt toodisplay worden kunnen meerdere taak uitvoeringen, gefilterd via Hallo opgegeven parameters.</span><span class="sxs-lookup"><span data-stu-id="5742c-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="5742c-139">Hallo hieronder toont een aantal Hallo mogelijke manieren toouse Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="5742c-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="5742c-140">Alle actieve taken voor de bovenste niveau uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="5742c-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="5742c-141">Alle bovenste niveau taak uitvoeringen, met inbegrip van niet-actieve taak uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="5742c-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="5742c-142">Alle onderliggende taak uitvoeringen van een opgegeven taak uitvoerings-ID, met inbegrip van niet-actieve taak uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="5742c-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="5742c-143">Ophalen van alle taak uitvoeringen gemaakt met behulp van een planning / taak combinatie, met inbegrip van niet-actieve taken:</span><span class="sxs-lookup"><span data-stu-id="5742c-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="5742c-144">Alle taken die gericht is op een opgegeven shard-kaart, inclusief niet-actieve taken worden opgehaald:</span><span class="sxs-lookup"><span data-stu-id="5742c-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="5742c-145">Alle taken die gericht is op een opgegeven aangepaste verzameling, met inbegrip van niet-actieve taken worden opgehaald:</span><span class="sxs-lookup"><span data-stu-id="5742c-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="5742c-146">Hallo-lijst met taak taak uitvoeringen binnen het uitvoeren van een specifieke taak ophalen:</span><span class="sxs-lookup"><span data-stu-id="5742c-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="5742c-147">Taak uitvoeren taakdetails ophalen:</span><span class="sxs-lookup"><span data-stu-id="5742c-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="5742c-148">Hallo volgende PowerShell-script kan gebruikte tooview Hallo details van een taak uitvoering van taken, die bijzonder nuttig is bij het opsporen van fouten in uitvoering zijn.</span><span class="sxs-lookup"><span data-stu-id="5742c-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="5742c-149">Storingen in uitvoering taak ophalen</span><span class="sxs-lookup"><span data-stu-id="5742c-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="5742c-150">Hallo JobTaskExecution object bevat een eigenschap voor de levenscyclus van taak samen met een berichteigenschap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5742c-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="5742c-151">Als de uitvoering van de taak een taak is mislukt, Hallo Lifecycle eigenschap te worden ingesteld*mislukt* en de resulterende uitzonderingsbericht toohello en de stack Hallo berichteigenschap wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5742c-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="5742c-152">Als een taak is mislukt, is het belangrijk tooview Hallo details van de taken die voor een bepaalde taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="5742c-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="5742c-153">Wachten op een taak uitvoeren toocomplete</span><span class="sxs-lookup"><span data-stu-id="5742c-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="5742c-154">Hallo volgende PowerShell-script kan gebruikte toowait voor een taak taak toocomplete zijn:</span><span class="sxs-lookup"><span data-stu-id="5742c-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="5742c-155">Maken van een aangepaste uitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="5742c-155">Create a custom execution policy</span></span>
<span data-ttu-id="5742c-156">Elastische Database taken ondersteunt het maken van aangepaste uitvoeringsbeleidsregels die kunnen worden toegepast wanneer u taken start.</span><span class="sxs-lookup"><span data-stu-id="5742c-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="5742c-157">Uitvoeringsbeleidsregels toestaan op dit moment voor het definiëren van:</span><span class="sxs-lookup"><span data-stu-id="5742c-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="5742c-158">Naam: Id voor het uitvoeringsbeleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="5742c-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="5742c-159">De time-out van de taak: Totale tijd voordat een taak met elastische taken van de Database, worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="5742c-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="5742c-160">Eerste Interval voor opnieuw proberen: Interval toowait voordat de eerste poging.</span><span class="sxs-lookup"><span data-stu-id="5742c-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="5742c-161">Maximale Interval voor opnieuw proberen: Cap van opnieuw intervallen toouse.</span><span class="sxs-lookup"><span data-stu-id="5742c-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="5742c-162">Probeer het opnieuw Interval Backoff Coefficient: Coefficient gebruikt toocalculate Hallo volgende interval tussen nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="5742c-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="5742c-163">Hallo volgende formule gebruikt: (eerste Interval voor opnieuw proberen) * Math.pow ((Interval Backoff Coefficient) (nummer van pogingen) - 2).</span><span class="sxs-lookup"><span data-stu-id="5742c-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="5742c-164">Maximum aantal pogingen: Hallo maximum aantal nieuwe pogingen pogingen tooperform in een job.</span><span class="sxs-lookup"><span data-stu-id="5742c-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="5742c-165">Hallo standaarduitvoeringsbeleid Hallo volgende waarden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="5742c-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="5742c-166">Naam: Standaarduitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="5742c-166">Name: Default execution policy</span></span>
* <span data-ttu-id="5742c-167">De time-out van de taak: 1 week</span><span class="sxs-lookup"><span data-stu-id="5742c-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="5742c-168">Eerste Interval voor opnieuw proberen: 100 milliseconden</span><span class="sxs-lookup"><span data-stu-id="5742c-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="5742c-169">Maximale Interval voor opnieuw proberen: 30 minuten</span><span class="sxs-lookup"><span data-stu-id="5742c-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="5742c-170">Coefficient Interval opnieuw proberen: 2</span><span class="sxs-lookup"><span data-stu-id="5742c-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="5742c-171">Maximum aantal pogingen: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="5742c-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="5742c-172">Hallo gewenst uitvoeringsbeleid maken:</span><span class="sxs-lookup"><span data-stu-id="5742c-172">Create hello desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="5742c-173">Een aangepaste uitvoeringsbeleid bijwerken</span><span class="sxs-lookup"><span data-stu-id="5742c-173">Update a custom execution policy</span></span>
<span data-ttu-id="5742c-174">Hallo gewenst uitvoering beleid tooupdate bijwerken:</span><span class="sxs-lookup"><span data-stu-id="5742c-174">Update hello desired execution policy tooupdate:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="5742c-175">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="5742c-175">Cancel a job</span></span>
<span data-ttu-id="5742c-176">Elastische Database taken ondersteunt taken annulering aanvragen.</span><span class="sxs-lookup"><span data-stu-id="5742c-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="5742c-177">Als taken voor elastische Database een annuleringsverzoek voor een taak die momenteel wordt uitgevoerd detecteert, wordt geprobeerd toostop Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="5742c-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="5742c-178">Er zijn twee verschillende manieren dat elastische Database taken een annulering kan uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5742c-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="5742c-179">Momenteel worden uitgevoerd annuleren taken: als een annulering wordt gedetecteerd, terwijl een taak die momenteel wordt uitgevoerd, een annulering wordt geprobeerd binnen Hallo aspect van Hallo taak momenteel wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5742c-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="5742c-180">Bijvoorbeeld: als er een langdurige query die momenteel wordt uitgevoerd wanneer een annulering wordt uitgevoerd, zal er een poging toocancel Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="5742c-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="5742c-181">Annuleren pogingen: Als een annulering wordt gedetecteerd door Hallo besturingselement thread voordat een taak voor uitvoering wordt gestart, Hallo besturingselement thread wordt voorkomen Hallo taak starten en Hallo aanvraag declareren als geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="5742c-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="5742c-182">Als een taak annulering is aangevraagd voor een bovenliggende taak, wordt Hallo annuleringsverzoek ingewilligd voor Hallo bovenliggende taak en alle bijbehorende onderliggende taken.</span><span class="sxs-lookup"><span data-stu-id="5742c-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="5742c-183">toosubmit een annuleringsverzoek gebruiken Hallo **Stop AzureSqlJobExecution** cmdlet en set Hallo **JobExecutionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="5742c-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="5742c-184">Een taak op naam en Hallo Taakgeschiedenis verwijderen</span><span class="sxs-lookup"><span data-stu-id="5742c-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="5742c-185">Elastische taken van de Database biedt ondersteuning voor asynchrone verwijderen van jobs.</span><span class="sxs-lookup"><span data-stu-id="5742c-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="5742c-186">Een taak kan worden gemarkeerd voor verwijdering en Hallo system Hallo taak en de taakgeschiedenis wordt verwijderd nadat alle taak uitvoeringen voor Hallo taak hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="5742c-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="5742c-187">Hallo-systeem wordt niet automatisch uitvoeringen van de actieve taak geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="5742c-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="5742c-188">In plaats daarvan moet stoppen AzureSqlJobExecution aangeroepen toocancel actieve taak uitvoeringen.</span><span class="sxs-lookup"><span data-stu-id="5742c-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="5742c-189">tootrigger taak verwijderen, gebruik Hallo **verwijderen AzureSqlJob** cmdlet en set Hallo **JobName** parameter.</span><span class="sxs-lookup"><span data-stu-id="5742c-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="5742c-190">Het doel van een aangepaste database maken</span><span class="sxs-lookup"><span data-stu-id="5742c-190">Create a custom database target</span></span>
<span data-ttu-id="5742c-191">Aangepaste database doelen kunnen worden gedefinieerd in elastische Database-taken die kunnen worden gebruikt voor uitvoering rechtstreeks of voor insluiting in de groep van een aangepaste database.</span><span class="sxs-lookup"><span data-stu-id="5742c-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="5742c-192">Aangezien **elastische pools** niet nog rechtstreeks worden ondersteund via PowerShell APIs Hallo, u gewoon maakt een aangepaste database doel en de aangepaste database verzameling doel op die alle Hallo-databases in de groep Hallo omvat.</span><span class="sxs-lookup"><span data-stu-id="5742c-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="5742c-193">Hallo variabelen tooreflect Hallo gewenst databasegegevens volgende instellen:</span><span class="sxs-lookup"><span data-stu-id="5742c-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="5742c-194">Een doel van de verzameling aangepaste database maken</span><span class="sxs-lookup"><span data-stu-id="5742c-194">Create a custom database collection target</span></span>
<span data-ttu-id="5742c-195">Een doel van de verzameling aangepaste database mag gedefinieerde tooenable worden uitgevoerd op meerdere gedefinieerde database doelen.</span><span class="sxs-lookup"><span data-stu-id="5742c-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="5742c-196">Nadat de groep van een database is gemaakt, kunnen de databases gekoppeld toohello aangepaste verzameling doel kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="5742c-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="5742c-197">Stel Hallo variabelen tooreflect Hallo gewenste aangepaste verzameling doelconfiguratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="5742c-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="5742c-198">Databases tooa aangepaste database verzameling doel toevoegen</span><span class="sxs-lookup"><span data-stu-id="5742c-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="5742c-199">Database-doelen kunnen worden gekoppeld aan de aangepaste database verzameling doelen toocreate een groep met databases.</span><span class="sxs-lookup"><span data-stu-id="5742c-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="5742c-200">Wanneer een taak is gemaakt die een aangepaste database verzameling doel, worden uitgevouwen tootarget hello databasesgroep gekoppeld toohello op Hallo tijdstip van de uitvoering van.</span><span class="sxs-lookup"><span data-stu-id="5742c-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="5742c-201">Hallo gewenst database tooa specifieke aangepaste verzameling toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5742c-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="5742c-202">Hallo-databases binnen een doel van de verzameling aangepaste database controleren</span><span class="sxs-lookup"><span data-stu-id="5742c-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="5742c-203">Gebruik Hallo **Get-AzureSqlJobTarget** cmdlet tooretrieve Hallo onderliggende databases binnen een doel van de verzameling aangepaste database.</span><span class="sxs-lookup"><span data-stu-id="5742c-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="5742c-204">Een taak tooexecute van een script voor een doel van de verzameling aangepaste database maken</span><span class="sxs-lookup"><span data-stu-id="5742c-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="5742c-205">Gebruik Hallo **nieuw AzureSqlJob** cmdlet toocreate een taak op basis van een groep met databases die zijn gedefinieerd door een doel van de verzameling aangepaste database.</span><span class="sxs-lookup"><span data-stu-id="5742c-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="5742c-206">Elastische taken van de Database wordt Hallo taak uitbreiden naar meerdere onderliggende taken elke overeenkomstige tooa-database die is gekoppeld aan Hallo aangepaste database verzameling doel en zorg ervoor dat Hallo script wordt uitgevoerd tegen elke database.</span><span class="sxs-lookup"><span data-stu-id="5742c-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="5742c-207">Ook is het belangrijk dat scripts idempotent toobe robuuste tooretries zijn.</span><span class="sxs-lookup"><span data-stu-id="5742c-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="5742c-208">Gegevens verzamelen over databases</span><span class="sxs-lookup"><span data-stu-id="5742c-208">Data collection across databases</span></span>
<span data-ttu-id="5742c-209">**Elastische Database taken** ondersteunt een query uit te voeren in een groep van databases en verzendt Hallo resultaten tooa opgegeven van de database-tabel.</span><span class="sxs-lookup"><span data-stu-id="5742c-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="5742c-210">Hallo tabel kan worden opgevraagd na Hallo feit toosee Hallo queryresultaat van elke database.</span><span class="sxs-lookup"><span data-stu-id="5742c-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="5742c-211">Dit biedt een mechanisme voor asynchrone tooexecute een query tussen meerdere databases.</span><span class="sxs-lookup"><span data-stu-id="5742c-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="5742c-212">Fout gevallen, zoals een Hallo databases tijdelijk niet beschikbaar worden automatisch verwerkt via de nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="5742c-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="5742c-213">de opgegeven doeltabel Hello wordt automatisch worden gemaakt als deze nog niet bestaat, overeenkomende hello schema Hallo heeft een resultatenset geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5742c-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="5742c-214">Als de uitvoering van een script meerdere resultatensets worden geretourneerd, verzendt elastische Database taken alleen Hallo eerste één toohello opgegeven doeltabel.</span><span class="sxs-lookup"><span data-stu-id="5742c-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="5742c-215">Hallo volgende PowerShell-script kan worden gebruikt tooexecute een script voor het verzamelen van de resultaten in een opgegeven tabel.</span><span class="sxs-lookup"><span data-stu-id="5742c-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="5742c-216">Dit script wordt ervan uitgegaan dat een T-SQL-script is gemaakt waarmee een enkelvoudig resultaat wordt verkregen set levert en een doel van de verzameling aangepaste database is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5742c-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="5742c-217">Stel Hallo tooreflect Hallo gewenst script, referenties en doel van de uitvoering te volgen:</span><span class="sxs-lookup"><span data-stu-id="5742c-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="5742c-218">Maak en start een taak voor scenario's voor het verzamelen van gegevens</span><span class="sxs-lookup"><span data-stu-id="5742c-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="5742c-219">Een planning voor het uitvoeren van de taak met behulp van een trigger taak maken</span><span class="sxs-lookup"><span data-stu-id="5742c-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="5742c-220">Hallo volgende PowerShell-script kan worden gebruikt toocreate een terugkerende planning.</span><span class="sxs-lookup"><span data-stu-id="5742c-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="5742c-221">Dit script maakt gebruik van een interval van één minuut, maar nieuwe AzureSqlJobSchedule biedt ook ondersteuning voor parameters - DayInterval, - HourInterval, - MonthInterval, en -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="5742c-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="5742c-222">Schema's die slechts één keer worden uitgevoerd, kunnen worden gemaakt door doorgeven - eenmalige.</span><span class="sxs-lookup"><span data-stu-id="5742c-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="5742c-223">Maak een nieuwe planning:</span><span class="sxs-lookup"><span data-stu-id="5742c-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="5742c-224">Een taak trigger toohave taak uitgevoerd op een tijdschema maken</span><span class="sxs-lookup"><span data-stu-id="5742c-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="5742c-225">Een trigger voor de taak kan worden gedefinieerd toohave uitgevoerd volgens tooa tijdschema van een taak.</span><span class="sxs-lookup"><span data-stu-id="5742c-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="5742c-226">Hallo volgende PowerShell-script kan worden gebruikt toocreate een trigger taak.</span><span class="sxs-lookup"><span data-stu-id="5742c-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="5742c-227">Stel Hallo variabelen toocorrespond toohello gewenste taak te volgen en plannen:</span><span class="sxs-lookup"><span data-stu-id="5742c-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="5742c-228">Een geplande koppeling toostop-taak wordt uitgevoerd op de planning verwijderen</span><span class="sxs-lookup"><span data-stu-id="5742c-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="5742c-229">toodiscontinue taakuitvoering via een taak worden geactiveerd, Hallo taak trigger opnieuw optreedt, kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5742c-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="5742c-230">Verwijderen van een taak trigger toostop een taak uit te voeren volgens tooa schema met behulp van Hallo **verwijderen AzureSqlJobTrigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5742c-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="5742c-231">Elastische database query resultaten tooExcel importeren</span><span class="sxs-lookup"><span data-stu-id="5742c-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="5742c-232">U kunt Hallo resultaten uit van een query tooan Excel-bestand importeren.</span><span class="sxs-lookup"><span data-stu-id="5742c-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="5742c-233">Start Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="5742c-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="5742c-234">Navigeer toohello **gegevens** lint.</span><span class="sxs-lookup"><span data-stu-id="5742c-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="5742c-235">Klik op **van andere bronnen** en klik op **van SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="5742c-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Excel importeren uit andere bronnen](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="5742c-237">In Hallo **Wizard Gegevensverbinding** Typ Hallo server servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="5742c-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="5742c-238">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="5742c-238">Then click **Next**.</span></span>
5. <span data-ttu-id="5742c-239">In het dialoogvenster Hallo **Selecteer Hallo-database met Hallo gegevens die u wilt**, selecteer Hallo **ElasticDBQuery** database.</span><span class="sxs-lookup"><span data-stu-id="5742c-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="5742c-240">Selecteer Hallo **klanten** tabel in de lijstweergave Hallo en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="5742c-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="5742c-241">Klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="5742c-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="5742c-242">In Hallo **importgegevens** formulier onder **Selecteer hoe u tooview deze gegevens in uw werkmap**, selecteer **tabel** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5742c-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="5742c-243">Alle rijen uit Hallo **klanten** tabel, opgeslagen in verschillende shards vullen Hallo Excel-werkblad.</span><span class="sxs-lookup"><span data-stu-id="5742c-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5742c-244">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5742c-244">Next steps</span></span>
<span data-ttu-id="5742c-245">Nu kunt u functies van de gegevens van Excel.</span><span class="sxs-lookup"><span data-stu-id="5742c-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="5742c-246">Hallo-verbindingsreeks gebruiken met de naam van uw server, databasenaam en referenties tooconnect uw BI en gegevens integratie extra toohello elastische query uitvoeren op database.</span><span class="sxs-lookup"><span data-stu-id="5742c-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="5742c-247">Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="5742c-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="5742c-248">Raadpleeg toohello elastische query uitvoeren op database en de externe tabellen net als elke andere SQL Server-database en SQL Server-tabellen die u wilt verbinding maken toowith uw hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="5742c-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="5742c-249">Kosten</span><span class="sxs-lookup"><span data-stu-id="5742c-249">Cost</span></span>
<span data-ttu-id="5742c-250">Er zijn geen extra kosten voor het gebruik van de functie Hallo elastische Database-query.</span><span class="sxs-lookup"><span data-stu-id="5742c-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="5742c-251">Hoewel op dit moment deze functie is alleen beschikbaar op premium-databases als een eindpunt, Hallo shards kunnen zijn van een servicelaag.</span><span class="sxs-lookup"><span data-stu-id="5742c-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="5742c-252">Zie voor informatie over prijzen [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="5742c-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
