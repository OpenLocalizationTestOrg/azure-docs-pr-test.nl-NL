---
title: Groepen van Azure SQL-databases beheren | Microsoft Docs
description: Maken en beheren van een taak elastische doorlopen.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d30cc74778e0b36dd632c2f040ce80d1ca8af5a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="ab3b0-103">Maken en beheren van geschaalde uit Azure SQL-Databases met elastische taken (preview)</span><span class="sxs-lookup"><span data-stu-id="ab3b0-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="ab3b0-104">**Elastische Database taken** vereenvoudigd beheer van groepen van databases door het uitvoeren van administratieve bewerkingen, zoals wijzigingen in het schema, Referentiebeheer, verwijzing Gegevensupdates, prestatiegegevens verzamelen of telemetrie van de tenant (klant) verzameling.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="ab3b0-105">Elastische taken van de Database is momenteel beschikbaar is via de Azure-portal en de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="ab3b0-106">Echter, de Azure portal vlakken verminderde functionaliteit beschikken beperkt tot uitvoering voor alle databases in een [elastische pool (preview)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="ab3b0-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="ab3b0-107">Toegang tot extra functies en uitvoering van scripts in een groep van databases met inbegrip van een aangepaste verzameling of een shard ingesteld (gemaakt met behulp van [clientbibliotheek voor elastische Database](sql-database-elastic-scale-introduction.md)), Zie [maken en beheren taken met behulp van PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ab3b0-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="ab3b0-108">Zie voor meer informatie over taken [elastische Database taken overzicht](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab3b0-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ab3b0-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ab3b0-109">Prerequisites</span></span>
* <span data-ttu-id="ab3b0-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-110">An Azure subscription.</span></span> <span data-ttu-id="ab3b0-111">Zie voor een gratis proefversie [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab3b0-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ab3b0-112">Een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-112">An elastic pool.</span></span> <span data-ttu-id="ab3b0-113">Zie [over elastische pools](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="ab3b0-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="ab3b0-114">Installatie van de onderdelen van de service taak elastische database.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="ab3b0-115">Zie [installeren van de service van de taak elastische database](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="ab3b0-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="ab3b0-116">Taken maken</span><span class="sxs-lookup"><span data-stu-id="ab3b0-116">Creating jobs</span></span>
1. <span data-ttu-id="ab3b0-117">Met behulp van de [Azure-portal](https://portal.azure.com), van een bestaande taak pool voor elastische database, klikt u op **maken taak**.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="ab3b0-118">Typ de gebruikersnaam en wachtwoord van de beheerder van de database (gemaakt tijdens de installatie van taken) voor de database taken (metagegevensopslag voor taken).</span><span class="sxs-lookup"><span data-stu-id="ab3b0-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span></span>
   
    ![De taak een naam, typ of plak in de code en klik op uitvoeren][1]
3. <span data-ttu-id="ab3b0-120">In de **taak maken** blade, typ een naam voor de taak.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-120">In the **Create Job** blade, type a name for the job.</span></span>
4. <span data-ttu-id="ab3b0-121">Typ de gebruikersnaam en wachtwoord verbinding maken met de doeldatabases op met voldoende machtigingen voor het uitvoeren van scripts.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span></span>
5. <span data-ttu-id="ab3b0-122">Plakken of typ in het T-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-122">Paste or type in the T-SQL script.</span></span>
6. <span data-ttu-id="ab3b0-123">Klik op **opslaan** en klik vervolgens op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-123">Click **Save** and then click **Run**.</span></span>
   
    ![Taken maken en uitvoeren][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="ab3b0-125">De idempotent-taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ab3b0-125">Run idempotent jobs</span></span>
<span data-ttu-id="ab3b0-126">Wanneer u een script op een set databases uitvoeren, moet u ervoor dat het script idempotent zijn.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span></span> <span data-ttu-id="ab3b0-127">Dat wil zeggen, moet het script mogelijk meerdere keren uitvoeren, zelfs als deze is mislukt voordat een onvoltooide status.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="ab3b0-128">Bijvoorbeeld, een script is mislukt, de taak wordt automatisch herhaald totdat dit is gelukt (binnen de limieten, als de nieuwe poging logica uiteindelijk stopt het opnieuw proberen).</span><span class="sxs-lookup"><span data-stu-id="ab3b0-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span></span> <span data-ttu-id="ab3b0-129">De manier om dit te doen is met het een component 'IF bestaat' en een willekeurig exemplaar gevonden verwijderen voordat u een nieuw object maakt.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="ab3b0-130">Hier ziet u een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ab3b0-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="ab3b0-131">Voordat u een nieuw exemplaar in plaats daarvan een 'Bestaat niet als'-component gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ab3b0-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="ab3b0-132">Dit script werkt vervolgens de tabel die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-132">This script then updates the table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="ab3b0-133">Taakstatus controleren</span><span class="sxs-lookup"><span data-stu-id="ab3b0-133">Checking job status</span></span>
<span data-ttu-id="ab3b0-134">Nadat een taak is gestart, kunt u de voortgang controleren.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="ab3b0-135">Klik op de pagina elastische pool **beheren van taken**.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-135">From the elastic pool page, click **Manage jobs**.</span></span>
   
    ![Klik op 'Taken beheren'][2]
2. <span data-ttu-id="ab3b0-137">Klik op de naam (a) van een taak.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-137">Click on the name (a) of a job.</span></span> <span data-ttu-id="ab3b0-138">De **STATUS** mag 'Voltooid' of 'Mislukt'.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-138">The **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="ab3b0-139">Details van de taak weergegeven (b) met de datum en tijd van het maken en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-139">The job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="ab3b0-140">De onderstaande lijst met (c) dat geeft de voortgang van het script dat op elke database in de groep, geeft de details van de datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span></span>
   
    ![Een voltooide taak controleren][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="ab3b0-142">Controleren van de mislukte taken</span><span class="sxs-lookup"><span data-stu-id="ab3b0-142">Checking failed jobs</span></span>
<span data-ttu-id="ab3b0-143">Als een taak mislukt, kan een logboek van de uitvoering ervan kan worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="ab3b0-144">Klik op de naam van de mislukte taak om de details te bekijken.</span><span class="sxs-lookup"><span data-stu-id="ab3b0-144">Click the name of the failed job to see its details.</span></span>

![Een mislukte taak controleren][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


