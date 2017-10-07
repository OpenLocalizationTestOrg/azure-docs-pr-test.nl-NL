---
title: een Azure SQL database tooa Bacpac-bestand aaaExport | Microsoft Docs
description: Een Azure SQL database tooa Bacpac-bestand exporteren via hello Azure Portal
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Een Azure SQL database tooa Bacpac-bestand exporteren

Wanneer u een database tooexport voor het archiveren of voor bewegende tooanother platform moet, kunt u Hallo database schema en de gegevens tooa exporteren [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) bestand. Een Bacpac-bestand is een ZIP-bestand met de extensie BACPAC met Hallo metagegevens en gegevens uit een SQL Server-database. Een Bacpac-bestand worden opgeslagen in Azure blob-opslag of in de lokale opslag in een on-premises locatie en later geïmporteerd terug in Azure SQL Database of in een lokale installatie van SQL Server. 

> [!IMPORTANT] 
> Azure SQL Database geautomatiseerde exporteren buiten gebruik werd gesteld op 1 maart 2017. U kunt [lange bewaartermijn van de back-](sql-database-long-term-retention.md
) of [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically archief SQL-databases met behulp van PowerShell volgens planning tooa van uw keuze. Voor een voorbeeld downloaden Hallo [PowerShell-voorbeeldscript](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) vanuit Github.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Overwegingen bij het exporteren van een Azure SQL database

* Voor het exporteren van een transactioneel consistent is, moet u beide geen schrijfactiviteiten plaatsvindt tijdens het Hallo exporteren, of dat u toobe exporteert vanuit een [transactioneel consistent kopiëren](sql-database-copy.md) van uw Azure SQL database.
* Als u tooblob opslag exporteert, is Hallo maximale grootte van een Bacpac-bestand 200 GB. tooarchive een groter Bacpac-bestand exporteren toolocal opslag.
* Exporteren van een Bacpac-bestand tooAzure premium-opslag met behulp van Hallo-methoden die worden beschreven in dit artikel wordt niet ondersteund.
* Als de exportbewerking Hallo van Azure SQL Database groter is dan 20 uur, kan worden geannuleerd. de prestaties van de tooincrease tijdens het exporteren, kunt u:
  * Tijdelijk verhogen uw serviceniveau.
  * Niet langer alle lees- en schrijfbewerkingen tijdens het Hallo exporteren.
  * Gebruik een [geclusterde index](https://msdn.microsoft.com/library/ms190457.aspx) met niet-null-waarden voor alle grote tabellen. Exporteren van een kan zonder geclusterde indexen mislukken als het duurt langer dan 6 tot 12 uur. Dit is omdat Hallo export-service toocomplete een scan tootry tooexport gehele tabel moet. Een goede manier toodetermine als uw tabellen zijn geoptimaliseerd voor het exporteren is toorun **DBCC SHOW_STATISTICS** en zorg ervoor dat Hallo *RANGE_HI_KEY* niet null is en goed verdeling van de waarde heeft. Zie voor meer informatie [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> BACPACs zijn niet bedoeld toobe gebruikt voor back-up en herstelbewerkingen. Azure SQL Database maakt automatisch een back-ups voor de database van elke gebruiker. Zie voor meer informatie [Business Continuity Overview](sql-database-business-continuity.md) en [back-ups van SQL-Database](sql-database-automated-backups.md).  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>Tooa Bacpac-bestand exporteren via hello Azure-portal

een database met tooexport Hallo [Azure-portal](https://portal.azure.com), Hallo openen voor uw database en klik op **exporteren** op Hallo-werkbalk. Hallo Bacpac-bestandsnaam opgeven en hello Azure-opslagaccount en container bieden voor het exporteren van Hallo Hallo referenties tooconnect toohello-brondatabase opgeven.  

![Database wordt geëxporteerd](./media/sql-database-export/database-export.png)

toomonitor hello voortgang van Hallo exportbewerking, open de pagina Hallo voor Hallo logische server met Hallo-database wordt geëxporteerd. Schuif naar beneden te**Operations** en klik vervolgens op **voor importeren/exporteren** geschiedenis.

![Geschiedenis exporteren](./media/sql-database-export/export-history.png)
![geschiedenis status exporteren](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>Tooa Bacpac-bestand exporteren via Hallo SQLPackage hulpprogramma

tooexport een SQL database met Hallo [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) opdrachtregelhulpprogramma Zie [parameters en eigenschappen exporteren](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). Hallo SQLPackage hulpprogramma wordt geleverd met de nieuwste versies van Hallo [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) en [SQL Server Data Tools voor Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), of u kunt de meest recente versie van Hallo downloaden [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) rechtstreeks vanuit Hallo Microsoft download center.

Het wordt aangeraden de Hallo gebruik van Hallo SQLPackage hulpprogramma voor schaal en prestaties in de meeste productieomgevingen. Voor een SQL Server Customer Advisory Team blog over het migreren met behulp van Bacpac-bestanden, Zie [migreren van SQL Server-tooAzure SQL-Database Bacpac-bestanden met](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Dit voorbeeld ziet u hoe tooexport een database met behulp van SqlPackage.exe met Universal verificatie van Active Directory:

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>Tooa Bacpac-bestand exporteren via SQL Server Management Studio (SSMS)

Hallo nieuwste versies van SQL Server Management Studio bieden een tooexport wizard ook een Azure SQL Database tooa Bacpac-bestand. Zie Hallo [exporteren van een Gegevenslaagtoepassing](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="export-tooa-bacpac-file-using-powershell"></a>Met behulp van PowerShell-tooa Bacpac-bestand exporteren

Gebruik Hallo [nieuw AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit een export database aanvraag toohello Azure SQL Database-service. Afhankelijk van de grootte van de Hallo van uw database, kan de exportbewerking Hallo sommige toocomplete tijd duren.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

toocheck hello status Hallo aanvraag exporteren, gebruikt u Hallo [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. Dit uitgevoerd onmiddellijk na Hallo aanvragen meestal retourneert **Status: InProgress**. Wanneer er **Status: geslaagd** Hallo exporteren is voltooid.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>Volgende stappen

* toolearn over langdurig bewaren van back-up van een Azure SQL-databaseback-up als een alternatieve tooexported een database voor archief-doeleinden, Zie [lange bewaartermijn van de back-](sql-database-long-term-retention.md).
- Voor een SQL Server Customer Advisory Team blog over het migreren met behulp van Bacpac-bestanden, Zie [migreren van SQL Server-tooAzure SQL-Database Bacpac-bestanden met](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Zie toolearn over het importeren van een Bacpac-tooa SQL Server-database [BACPCAC tooa SQL Server-database importeren](https://msdn.microsoft.com/library/hh710052.aspx).
* Zie toolearn over het exporteren van een BACPAC van een SQL Server-database [exporteren van een Gegevenslaagtoepassing](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) en [migreren van uw eerste database](sql-database-migrate-your-sql-server-database.md).
* Als u vanuit SQL Server als een prelude toomigration tooAzure SQL-Database exporteert, raadpleegt u [migreren van een SQL Server-database tooAzure SQL-Database](sql-database-cloud-migrate.md).
