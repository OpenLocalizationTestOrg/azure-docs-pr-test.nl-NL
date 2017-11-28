---
title: een BACPAC aaaImport bestand toocreate een Azure SQL database | Microsoft Docs
description: Maak een newAzure SQL-database door een Bacpac-bestand te importeren.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="9ad55-103">Een Bacpac-bestand tooa importeren nieuwe Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9ad55-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="9ad55-104">Wanneer u een database van een archief tooimport moet of wanneer u migreert vanaf een ander platform, u kunt databaseschema Hallo en gegevens van importeren een [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) bestand.</span><span class="sxs-lookup"><span data-stu-id="9ad55-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="9ad55-105">Een Bacpac-bestand is een ZIP-bestand met de extensie BACPAC met Hallo metagegevens en gegevens uit een SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="9ad55-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="9ad55-106">Een Bacpac-bestand kan worden geïmporteerd uit Azure blob storage (standard-opslag alleen) of van lokale opslag in een on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="9ad55-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="9ad55-107">toomaximize hello importeren snelheid, wordt aangeraden dat u een hogere prijscategorie en prestatieniveau serviceniveau, zoals een P6 opgeven en daarna geschaald toodown naar gelang van toepassing nadat Hallo importeren voltooid is.</span><span class="sxs-lookup"><span data-stu-id="9ad55-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="9ad55-108">Bovendien Hallo databasecompatibiliteitsniveau na het importeren van Hallo is gebaseerd op Hallo compatibiliteitsniveau van de brondatabase Hallo.</span><span class="sxs-lookup"><span data-stu-id="9ad55-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="9ad55-109">Nadat u uw database tooAzure SQL-Database migreert, kunt u toooperate Hallo database op het huidige compatibiliteitsniveau (level 100 voor Hallo AdventureWorks2008R2 database) of op een hoger niveau.</span><span class="sxs-lookup"><span data-stu-id="9ad55-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="9ad55-110">Zie voor meer informatie over Hallo gevolgen en opties voor de werking van een database op een specifieke compatibiliteitsniveau [databasecompatibiliteitsniveau ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="9ad55-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="9ad55-111">Zie ook [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) voor meer informatie over overige instellingen op databaseniveau gerelateerde toocompatibility niveaus.</span><span class="sxs-lookup"><span data-stu-id="9ad55-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="9ad55-112">tooimport een Bacpac-tooa nieuwe database, moet u eerst een logische Azure SQL Database-server maken.</span><span class="sxs-lookup"><span data-stu-id="9ad55-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="9ad55-113">Zie voor een zelfstudie die laat zien hoe toomigrate een SQL Server-database tooAzure SQL-Database met behulp van SQLPackage, [migreren van een SQL Server-Database](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="9ad55-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="9ad55-114">Importeren uit een Bacpac-bestand met Azure portal</span><span class="sxs-lookup"><span data-stu-id="9ad55-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="9ad55-115">Dit artikel bevat instructies voor het maken van een Azure SQL database van een Bacpac-bestand dat is opgeslagen in Azure blob storage met Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9ad55-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9ad55-116">Importeren met behulp van Hallo alleen Azure portal ondersteunt een BACPAC-bestand te importeren uit Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="9ad55-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="9ad55-117">een database met tooimport hello Azure-portal, open Hallo-pagina voor uw database en klik op **importeren** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="9ad55-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="9ad55-118">Geef Hallo-opslagaccount en container en Hallo Bacpac-bestand dat u tooimport wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="9ad55-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="9ad55-119">Selecteer Hallo grootte van de nieuwe database hello (meestal Hallo dezelfde als de oorsprong) en geef aanmeldgegevens op Hallo bestemming SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9ad55-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![De database wordt geïmporteerd](./media/sql-database-import/import.png)

<span data-ttu-id="9ad55-121">toomonitor hello voortgang van Hallo importbewerking, open de pagina Hallo voor Hallo logische server met Hallo-database wordt geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="9ad55-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="9ad55-122">Schuif naar beneden te**Operations** en klik vervolgens op **voor importeren/exporteren** geschiedenis.</span><span class="sxs-lookup"><span data-stu-id="9ad55-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="9ad55-123">Hallo-voortgang van een importbewerking</span><span class="sxs-lookup"><span data-stu-id="9ad55-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="9ad55-124">toomonitor Hallo voortgang van Hallo importbewerking, open de pagina Hallo voor Hallo logische server in welke Hallo database wordt geïmporteerd geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="9ad55-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="9ad55-125">Schuif naar beneden te**Operations** en klik vervolgens op **voor importeren/exporteren** geschiedenis.</span><span class="sxs-lookup"><span data-stu-id="9ad55-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="9ad55-126">![importeren](./media/sql-database-import/import-history.png) ![status importeren](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="9ad55-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="9ad55-127">tooverify hello database live op Hallo-server, klikt u op **SQL-databases** en controleer of de nieuwe database Hallo **Online**.</span><span class="sxs-lookup"><span data-stu-id="9ad55-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="9ad55-128">Importeren uit een Bacpac-bestand met SQLPackage</span><span class="sxs-lookup"><span data-stu-id="9ad55-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="9ad55-129">tooimport een SQL database met Hallo [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) opdrachtregelhulpprogramma Zie [importeren parameters en eigenschappen](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="9ad55-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="9ad55-130">Hallo SQLPackage hulpprogramma wordt geleverd met de nieuwste versies van Hallo [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) en [SQL Server Data Tools voor Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), of u kunt de meest recente versie van Hallo downloaden [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) rechtstreeks vanuit Hallo Microsoft download center.</span><span class="sxs-lookup"><span data-stu-id="9ad55-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="9ad55-131">Het wordt aangeraden de Hallo gebruik van Hallo SQLPackage hulpprogramma voor schaal en prestaties in de meeste productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="9ad55-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="9ad55-132">Voor een SQL Server Customer Advisory Team blog over het migreren met behulp van Bacpac-bestanden, Zie [migreren van SQL Server-tooAzure SQL-Database Bacpac-bestanden met](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="9ad55-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="9ad55-133">Zie Hallo SQLPackage opdracht voor een scriptvoorbeeld van een voor het volgende tooimport hello **AdventureWorks2008R2** -database van lokale opslag tooan Azure SQL Database logische server, aangeroepen **mynewserver20170403** in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9ad55-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="9ad55-134">Dit script toont Hallo maken van een nieuwe database aangeroepen **myMigratedDatabase**, met een servicelaag van **Premium**, en een Servicedoelstelling van **P6**.</span><span class="sxs-lookup"><span data-stu-id="9ad55-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="9ad55-135">Deze waarden te wijzigen als de juiste tooyour omgeving.</span><span class="sxs-lookup"><span data-stu-id="9ad55-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage importeren](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="9ad55-137">Een logische Azure SQL Database-server luistert naar poort 1433.</span><span class="sxs-lookup"><span data-stu-id="9ad55-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="9ad55-138">Als u tooconnect tooan Azure SQL Database logische server vanuit een bedrijfsfirewall probeert, moet deze poort openen in de bedrijfsfirewall Hallo voor u toosuccessfully verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="9ad55-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="9ad55-139">Dit voorbeeld ziet u hoe tooimport een database met behulp van SqlPackage.exe met Universal verificatie van Active Directory:</span><span class="sxs-lookup"><span data-stu-id="9ad55-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="9ad55-140">Importeren uit een Bacpac-bestand met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ad55-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="9ad55-141">Gebruik Hallo [nieuw AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit een import database aanvraag toohello Azure SQL Database-service.</span><span class="sxs-lookup"><span data-stu-id="9ad55-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="9ad55-142">Afhankelijk van de grootte van de Hallo van uw database, kan de importbewerking Hallo sommige toocomplete tijd duren.</span><span class="sxs-lookup"><span data-stu-id="9ad55-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="9ad55-143">toocheck hello status Hallo aanvraag importeren, gebruikt u Hallo [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9ad55-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="9ad55-144">Dit uitgevoerd onmiddellijk na Hallo aanvragen meestal retourneert **Status: InProgress**.</span><span class="sxs-lookup"><span data-stu-id="9ad55-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="9ad55-145">Wanneer er **Status: geslaagd** Hallo importeren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9ad55-145">When you see **Status: Succeeded** hello import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
<span data-ttu-id="9ad55-146">Zie voor een ander scriptvoorbeeld [een database uit een Bacpac-bestand importeren](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9ad55-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ad55-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ad55-147">Next steps</span></span>
* <span data-ttu-id="9ad55-148">toolearn hoe tooconnect tooand query uitvoeren op een geïmporteerde SQL-Database raadpleegt [tooSQL Database verbinding met SQL Server Management Studio en een voorbeeld T-SQL-query uitvoert](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="9ad55-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="9ad55-149">Voor een SQL Server Customer Advisory Team blog over het migreren met behulp van Bacpac-bestanden, Zie [migreren van SQL Server-tooAzure SQL-Database Bacpac-bestanden met](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="9ad55-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="9ad55-150">Zie voor een beschrijving van Hallo volledige SQL Server-databasemigratieproces, inclusief aanbevelingen voor prestaties [migreren van een SQL Server-database tooAzure SQL-Database](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="9ad55-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



