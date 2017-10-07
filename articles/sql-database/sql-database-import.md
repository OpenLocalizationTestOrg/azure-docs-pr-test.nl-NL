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
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>Een Bacpac-bestand tooa importeren nieuwe Azure SQL Database

Wanneer u een database van een archief tooimport moet of wanneer u migreert vanaf een ander platform, u kunt databaseschema Hallo en gegevens van importeren een [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) bestand. Een Bacpac-bestand is een ZIP-bestand met de extensie BACPAC met Hallo metagegevens en gegevens uit een SQL Server-database. Een Bacpac-bestand kan worden geïmporteerd uit Azure blob storage (standard-opslag alleen) of van lokale opslag in een on-premises locatie. toomaximize hello importeren snelheid, wordt aangeraden dat u een hogere prijscategorie en prestatieniveau serviceniveau, zoals een P6 opgeven en daarna geschaald toodown naar gelang van toepassing nadat Hallo importeren voltooid is. Bovendien Hallo databasecompatibiliteitsniveau na het importeren van Hallo is gebaseerd op Hallo compatibiliteitsniveau van de brondatabase Hallo. 

> [!IMPORTANT] 
> Nadat u uw database tooAzure SQL-Database migreert, kunt u toooperate Hallo database op het huidige compatibiliteitsniveau (level 100 voor Hallo AdventureWorks2008R2 database) of op een hoger niveau. Zie voor meer informatie over Hallo gevolgen en opties voor de werking van een database op een specifieke compatibiliteitsniveau [databasecompatibiliteitsniveau ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Zie ook [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) voor meer informatie over overige instellingen op databaseniveau gerelateerde toocompatibility niveaus.   >

> [!NOTE]
> tooimport een Bacpac-tooa nieuwe database, moet u eerst een logische Azure SQL Database-server maken. Zie voor een zelfstudie die laat zien hoe toomigrate een SQL Server-database tooAzure SQL-Database met behulp van SQLPackage, [migreren van een SQL Server-Database](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Importeren uit een Bacpac-bestand met Azure portal

Dit artikel bevat instructies voor het maken van een Azure SQL database van een Bacpac-bestand dat is opgeslagen in Azure blob storage met Hallo [Azure-portal](https://portal.azure.com). Importeren met behulp van Hallo alleen Azure portal ondersteunt een BACPAC-bestand te importeren uit Azure blob-opslag.

een database met tooimport hello Azure-portal, open Hallo-pagina voor uw database en klik op **importeren** op Hallo-werkbalk. Geef Hallo-opslagaccount en container en Hallo Bacpac-bestand dat u tooimport wilt selecteren. Selecteer Hallo grootte van de nieuwe database hello (meestal Hallo dezelfde als de oorsprong) en geef aanmeldgegevens op Hallo bestemming SQL Server.  

   ![De database wordt geïmporteerd](./media/sql-database-import/import.png)

toomonitor hello voortgang van Hallo importbewerking, open de pagina Hallo voor Hallo logische server met Hallo-database wordt geïmporteerd. Schuif naar beneden te**Operations** en klik vervolgens op **voor importeren/exporteren** geschiedenis.

### <a name="monitor-hello-progress-of-an-import-operation"></a>Hallo-voortgang van een importbewerking

toomonitor Hallo voortgang van Hallo importbewerking, open de pagina Hallo voor Hallo logische server in welke Hallo database wordt geïmporteerd geïmporteerd. Schuif naar beneden te**Operations** en klik vervolgens op **voor importeren/exporteren** geschiedenis.
   
   ![importeren](./media/sql-database-import/import-history.png) ![status importeren](./media/sql-database-import/import-status.png)

tooverify hello database live op Hallo-server, klikt u op **SQL-databases** en controleer of de nieuwe database Hallo **Online**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>Importeren uit een Bacpac-bestand met SQLPackage

tooimport een SQL database met Hallo [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) opdrachtregelhulpprogramma Zie [importeren parameters en eigenschappen](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). Hallo SQLPackage hulpprogramma wordt geleverd met de nieuwste versies van Hallo [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) en [SQL Server Data Tools voor Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), of u kunt de meest recente versie van Hallo downloaden [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) rechtstreeks vanuit Hallo Microsoft download center.

Het wordt aangeraden de Hallo gebruik van Hallo SQLPackage hulpprogramma voor schaal en prestaties in de meeste productieomgevingen. Voor een SQL Server Customer Advisory Team blog over het migreren met behulp van Bacpac-bestanden, Zie [migreren van SQL Server-tooAzure SQL-Database Bacpac-bestanden met](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Zie Hallo SQLPackage opdracht voor een scriptvoorbeeld van een voor het volgende tooimport hello **AdventureWorks2008R2** -database van lokale opslag tooan Azure SQL Database logische server, aangeroepen **mynewserver20170403** in dit voorbeeld. Dit script toont Hallo maken van een nieuwe database aangeroepen **myMigratedDatabase**, met een servicelaag van **Premium**, en een Servicedoelstelling van **P6**. Deze waarden te wijzigen als de juiste tooyour omgeving.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage importeren](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Een logische Azure SQL Database-server luistert naar poort 1433. Als u tooconnect tooan Azure SQL Database logische server vanuit een bedrijfsfirewall probeert, moet deze poort openen in de bedrijfsfirewall Hallo voor u toosuccessfully verbinding maken.
>

Dit voorbeeld ziet u hoe tooimport een database met behulp van SqlPackage.exe met Universal verificatie van Active Directory:

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>Importeren uit een Bacpac-bestand met behulp van PowerShell

Gebruik Hallo [nieuw AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit een import database aanvraag toohello Azure SQL Database-service. Afhankelijk van de grootte van de Hallo van uw database, kan de importbewerking Hallo sommige toocomplete tijd duren.

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

toocheck hello status Hallo aanvraag importeren, gebruikt u Hallo [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. Dit uitgevoerd onmiddellijk na Hallo aanvragen meestal retourneert **Status: InProgress**. Wanneer er **Status: geslaagd** Hallo importeren is voltooid.

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
Zie voor een ander scriptvoorbeeld [een database uit een Bacpac-bestand importeren](scripts/sql-database-import-from-bacpac-powershell.md).

## <a name="next-steps"></a>Volgende stappen
* toolearn hoe tooconnect tooand query uitvoeren op een geïmporteerde SQL-Database raadpleegt [tooSQL Database verbinding met SQL Server Management Studio en een voorbeeld T-SQL-query uitvoert](sql-database-connect-query-ssms.md).
* Voor een SQL Server Customer Advisory Team blog over het migreren met behulp van Bacpac-bestanden, Zie [migreren van SQL Server-tooAzure SQL-Database Bacpac-bestanden met](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Zie voor een beschrijving van Hallo volledige SQL Server-databasemigratieproces, inclusief aanbevelingen voor prestaties [migreren van een SQL Server-database tooAzure SQL-Database](sql-database-cloud-migrate.md).



