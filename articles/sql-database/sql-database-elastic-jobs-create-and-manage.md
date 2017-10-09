---
title: groepen van Azure SQL-databases aaaManage | Microsoft Docs
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
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="a643c-103">Maken en beheren van geschaalde uit Azure SQL-Databases met elastische taken (preview)</span><span class="sxs-lookup"><span data-stu-id="a643c-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="a643c-104">**Elastische Database taken** vereenvoudigd beheer van groepen van databases door het uitvoeren van administratieve bewerkingen, zoals wijzigingen in het schema, Referentiebeheer, verwijzing Gegevensupdates, prestatiegegevens verzamelen of telemetrie van de tenant (klant) verzameling.</span><span class="sxs-lookup"><span data-stu-id="a643c-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="a643c-105">Elastische taken van de Database is momenteel beschikbaar is via hello Azure-portal en PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a643c-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="a643c-106">Echter wel hello Azure portal verwerkingsinformatie gereduceerde tooexecution beperkt voor alle databases in een [elastische pool (preview)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="a643c-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="a643c-107">aanvullende functies tooaccess en uitvoering van scripts in een groep van databases met inbegrip van een aangepaste verzameling of een shard ingesteld (gemaakt met behulp van [clientbibliotheek voor elastische Database](sql-database-elastic-scale-introduction.md)), Zie [maken en beheren taken met behulp van PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a643c-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="a643c-108">Zie voor meer informatie over taken [elastische Database taken overzicht](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a643c-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a643c-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a643c-109">Prerequisites</span></span>
* <span data-ttu-id="a643c-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a643c-110">An Azure subscription.</span></span> <span data-ttu-id="a643c-111">Zie voor een gratis proefversie [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a643c-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a643c-112">Een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="a643c-112">An elastic pool.</span></span> <span data-ttu-id="a643c-113">Zie [over elastische pools](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="a643c-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="a643c-114">Installatie van de onderdelen van de service taak elastische database.</span><span class="sxs-lookup"><span data-stu-id="a643c-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="a643c-115">Zie [installeren Hallo elastische database taak service](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="a643c-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="a643c-116">Taken maken</span><span class="sxs-lookup"><span data-stu-id="a643c-116">Creating jobs</span></span>
1. <span data-ttu-id="a643c-117">Met behulp van Hallo [Azure-portal](https://portal.azure.com), van een bestaande taak pool voor elastische database, klikt u op **maken taak**.</span><span class="sxs-lookup"><span data-stu-id="a643c-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="a643c-118">Typ in het Hallo-gebruikersnaam en wachtwoord van de beheerder van de database hello (gemaakt tijdens de installatie van taken) voor Hallo taken beheer database (metagegevensopslag voor taken).</span><span class="sxs-lookup"><span data-stu-id="a643c-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![Naam Hallo taak Typ of plak in de code en klik op uitvoeren][1]
3. <span data-ttu-id="a643c-120">In Hallo **taak maken** blade, typ een naam voor het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="a643c-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="a643c-121">Typ Hallo gebruiker naam en het wachtwoord tooconnect toohello doeldatabases op met voldoende machtigingen voor het script uitvoeren toosucceed.</span><span class="sxs-lookup"><span data-stu-id="a643c-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="a643c-122">Plakken of typ in het Hallo T-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="a643c-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="a643c-123">Klik op **opslaan** en klik vervolgens op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="a643c-123">Click **Save** and then click **Run**.</span></span>
   
    ![Taken maken en uitvoeren][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="a643c-125">De idempotent-taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a643c-125">Run idempotent jobs</span></span>
<span data-ttu-id="a643c-126">Wanneer u een script op een set databases uitvoeren, moet u ervoor dat Hallo script idempotent zijn.</span><span class="sxs-lookup"><span data-stu-id="a643c-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="a643c-127">Dat wil zeggen, Hallo script moet kunnen toorun meerdere keren, zelfs als deze is mislukt voordat een onvoltooide status.</span><span class="sxs-lookup"><span data-stu-id="a643c-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="a643c-128">Bijvoorbeeld, een script is mislukt, Hallo-taak wordt automatisch herhaald totdat dit is gelukt (binnen de limieten, als Hallo opnieuw logica uiteindelijk stopt Hallo opnieuw uit te voeren).</span><span class="sxs-lookup"><span data-stu-id="a643c-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="a643c-129">Hallo manier toodo toouse Hallo is een component 'IF bestaat' en een willekeurig exemplaar gevonden verwijderen voordat u een nieuw object maakt.</span><span class="sxs-lookup"><span data-stu-id="a643c-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="a643c-130">Hier ziet u een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a643c-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="a643c-131">Voordat u een nieuw exemplaar in plaats daarvan een 'Bestaat niet als'-component gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a643c-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

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

<span data-ttu-id="a643c-132">Dit script werkt vervolgens Hallo tabel eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a643c-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="a643c-133">Taakstatus controleren</span><span class="sxs-lookup"><span data-stu-id="a643c-133">Checking job status</span></span>
<span data-ttu-id="a643c-134">Nadat een taak is gestart, kunt u de voortgang controleren.</span><span class="sxs-lookup"><span data-stu-id="a643c-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="a643c-135">Klik op de pagina Hallo elastische pool **beheren van taken**.</span><span class="sxs-lookup"><span data-stu-id="a643c-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    ![Klik op 'Taken beheren'][2]
2. <span data-ttu-id="a643c-137">Klik op Hallo naam, (a) van een taak.</span><span class="sxs-lookup"><span data-stu-id="a643c-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="a643c-138">Hallo **STATUS** mag 'Voltooid' of 'Mislukt'.</span><span class="sxs-lookup"><span data-stu-id="a643c-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="a643c-139">Hallo taakdetails weergegeven (b) met de datum en tijd van het maken en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a643c-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="a643c-140">Hallo lijst (c) onder Hallo waarin Hallo voortgang van Hallo-script op elke database in de groep hello, geeft de details van de datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="a643c-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![Een voltooide taak controleren][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="a643c-142">Controleren van de mislukte taken</span><span class="sxs-lookup"><span data-stu-id="a643c-142">Checking failed jobs</span></span>
<span data-ttu-id="a643c-143">Als een taak mislukt, kan een logboek van de uitvoering ervan kan worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="a643c-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="a643c-144">Klik op Hallo-naam van Hallo mislukt taak toosee de details ervan.</span><span class="sxs-lookup"><span data-stu-id="a643c-144">Click hello name of hello failed job toosee its details.</span></span>

![Een mislukte taak controleren][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


